# Cave Runner

A turn-based terminal game written in pure Python. Collect every coin, dodge hidden traps and roaming enemies, then escape through the exit. Each level gets bigger and harder.

No external libraries are needed to play.

## How it looks

```
P . $ . . $
E . . . $ .
$ . . . . .
. . . . . .
. . . . . .
. . . . . X
Level 1 | Lives 3 | Score 0 | Coins 0/4
Move (w/a/s/d, q to quit):
```

| Symbol | Meaning |
|--------|---------|
| `P` | You |
| `$` | Coin (+10 points) |
| `E` | Enemy (moves randomly each turn) |
| `X` | Exit (sealed until you collect every coin) |
| `^` | Trap (hidden until you step on it, then it is revealed) |
| `.` | Empty floor |

## How to play

1. Move one step per turn with `w` (up), `a` (left), `s` (down) or `d` (right), then press Enter.
2. Collect **all** the coins on the level.
3. Walk onto the exit `X` to finish the level.
4. Stepping on a trap or being caught by an enemy costs **1 life**. You start with 3 lives. At 0 lives the game is over.
5. Type `q` at any time to quit. Your score is saved if it beats your high score.

## Scoring

| Event | Points |
|-------|--------|
| Pick up a coin | +10 |
| Finish a level | +50, plus 10 for every life you have left |

## Levels

Each new level changes the cave:

- The grid grows by one cell on each side, up to 12 x 12.
- Coins increase to `3 + level`.
- Hidden traps increase to `level + 1`.
- Enemies increase to one per level.

Lives and score carry over from level to level.

## Run it

You need Python 3.8 or newer.

```bash
git clone https://github.com/Priyasha1503/cave-runner.git
cd cave-runner
python main.py
```

On Windows, use `python main.py` or `py main.py` in Command Prompt or PowerShell.

## Run the tests

```bash
pip install pytest
pytest
```

The tests cover wall collisions, coin pickup, traps and revealing them, the sealed exit, enemy hits and game over, level difficulty, and saving the high score only when it is beaten.

## Project structure

```
cave-runner/
├── game.py        # Game rules and state (no input or printing)
├── main.py        # Terminal input loop and screen output
├── test_game.py   # Unit tests for the game logic
└── README.md
```

## Design notes

- **Logic is separate from the interface.** `game.py` has no `input()` or `print()` calls, so every rule can be tested directly without simulating a terminal. `main.py` only reads keys and prints the board.
- **Seeded randomness.** The `Game` class takes an optional `seed`, which makes any level reproducible for tests and debugging.
- **Safe high-score storage.** The high score is saved to a small JSON file next to the game. If the file is missing or corrupted, the game starts again from 0 instead of crashing.
- **Levels scale from simple formulas.** Grid size, coin count, trap count and enemy count are all derived from the level number, so the difficulty can be tuned in one place.

## Ideas for next steps

- Add a graphical version using `pygame`.
- Give enemies simple chasing behaviour instead of random moves.
- Add power-ups, such as a shield that blocks one trap.
- Add a timer or a move limit to make levels more tense.

## Author

Priyasha Sabbavarapu

[LinkedIn](https://www.linkedin.com/in/priyasha1503/) | [GitHub](https://github.com/Priyasha1503)
