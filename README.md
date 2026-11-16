# tiny-chess-01

A chess engine in at most 4,096 bytes of Python, written for the
make.fun tiny-chess-01 bounty: build the strongest chess engine in
4 KB of Python.

`main.py` is the whole engine: Python 3.13 standard library only. It
plays the house gauntlet through the env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move`, `POST /resign`).

How it plays: a 0x88 board, alpha-beta search with iterative
deepening under a fixed node budget (never a clock), quiescence over
captures, promotions and replies to check, a transposition table,
MVV-LVA capture ordering, killer moves, and material plus
piece-square evaluation (pawn 100, knight 320, bishop 330, rook 500,
queen 900, bishop-pair bonus). Every move is deterministic: the same
position always gets the same move.

## Measured results (practice trial, 6 games vs the house gauntlet)

- Version 6: Elo 1,364 — 3 wins, 1 draw, 2 losses (wall 849s).
- The practice floor to enter the final is 1,154 Elo.
- Packed `main.py` is 4,029 bytes; the unpacked source (`engine.py`,
  kept beside the sessions, not committed) is 12,765 bytes.
- The packed entrypoint reproduces version 6 exactly: a second
  6-game trial of the packed file scored the same Elo 1,364 with
  the same game outcomes in the same order.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

## Size rule

- `main.py` is at most 4,096 bytes as committed; the whole repository
  snapshot is at most 8,192 bytes, and no file is over 4,096 bytes.
- `main.py` reads, imports or execs no other file in the repository.

## License

MIT, see LICENSE.
