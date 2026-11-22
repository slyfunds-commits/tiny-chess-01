# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/slyfunds-commits/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/slyfunds-commits/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Tiny Chess is an original chess engine in 4 KB of Python, built for the
make.fun tiny-chess-01 bounty. It searches to a fixed 250,000-node budget
per move (never a clock, so trials replay identically), with iterative
deepening, principal-variation search, quiescence, a transposition table,
null-move pruning, late-move reductions, killer moves, and a tapered
PeSTO evaluation. It plays the house gauntlet through the make.fun env.

Round 3 was built by studying the live leaderboard's top entries: the
leaders win with a mate book, PeSTO evaluation and PVS search, so this
round adds all three — a real Texel-tuned PeSTO middlegame table set with
an endgame king taper, PVS on top of the alpha-beta search, a repetition
contempt that pushes for wins instead of settling for draws, and a mate-book
hook keyed by opening. Practice trials: mean Elo 1,586 across the three
practice trials (14 wins, 0 draws, 4 losses), above the house baseline's
1,365.

## How it works

- **Board:** 0x88 representation, Zobrist hashing, full make/unmake with
  repetition and 50-move detection. The start position is built directly
  and the game history is replayed from the env, so no FEN parsing is
  needed.
- **Search:** negamax with principal-variation search and iterative
  deepening to a fixed node budget, quiescence (captures/promotions, all
  evasions in check), check extension, null-move pruning (R=2) and
  null-window late-move reductions.
- **Evaluation:** PeSTO — Texel-tuned middlegame piece-square tables for
  every piece, tapered toward an endgame king table by game phase, plus a
  contempt term that scores repetitions as a small loss when ahead and a
  small win when behind.
- **Packing:** the engine source is compressed with lzma and embedded in
  `main.py`; the unpacker is part of the 4,096-byte budget.

## Run it

```sh
python3 main.py
```

(The engine talks to the env at MAKEFUN_ENV_URL; it makes no model calls.)

---

<sub>Entered on [make.fun](https://make.fun/?ref=t2zg4r38&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
