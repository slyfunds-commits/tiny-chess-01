# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/slyfunds-commits/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/slyfunds-commits/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Tiny Chess is an original alpha-beta chess engine in 4 KB of Python. It
searches to a fixed 80,000-node budget per move (never a clock, so trials
replay identically), with iterative deepening, quiescence search, a
transposition table, null-move pruning, late-move reductions, killer moves,
and piece-square evaluation with advanced-pawn bonuses. It plays the house
gauntlet through the make.fun env.

## How it works

- **Board:** 0x88 representation, Zobrist hashing, full make/unmake with
  repetition and 50-move detection.
- **Search:** negamax alpha-beta with iterative deepening to a fixed node
  budget, quiescence (captures/promotions, all evasions in check), check
  extension, null-move pruning (R=2) and null-window late-move reductions.
- **Evaluation:** material + piece-square tables + advanced-pawn bonus.
- **Packing:** the engine source is compressed with lzma and embedded in
  `main.py`; the unpacker is part of the 4,096-byte budget.

## Run it

```sh
python3 main.py
```

(The engine talks to the env at MAKEFUN_ENV_URL; it makes no model calls.)

---

<sub>Entered on [make.fun](https://make.fun/?ref=t2zg4r38&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
