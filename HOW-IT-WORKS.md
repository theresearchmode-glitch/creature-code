# How Creature Code works (Level 1: Mossbrook)

The whole game is one file: `index.html`. This guide walks through it in plain words.

## The big idea

Every creature's brain is a real Python program, for example:

```python
name = "Pip"
element = "fire"
power = 4
guard = 3
speed = 3
```

The game runs that code (with real Python, via Pyodide) and uses the variables as the creature's stats:

- `power`: how hard it hits.
- `guard`: how much damage it blocks.
- `speed`: who moves first.
- `element`: fire beats leaf, leaf beats water, water beats fire.

`power + guard + speed` can only add up to so much (10 at level 1, +2 per level), so every build is a choice.

## Where the Python lessons are

| Moment | Python idea |
|---|---|
| Hatching the egg | Your first variable: `name = "..."` |
| Setting up the brain | Strings (`element = "fire"`) and numbers (`power = 4`) |
| Catching | Strings must match exactly: `jar = "Bubbit"` (capitals count!) |
| CODE in battle | Changing a variable's value mid-fight |
| Voice Stone | `print(name)` vs `print("name")` |
| Glitch Moth | Debugging: text instead of a number, a misspelled label, missing quotes |

## The three languages in one file

| Part | Language | Its job |
|---|---|---|
| `<style>` | CSS | How it looks: the console shell, buttons, battle menus |
| The tags (`<canvas>`, `<button>`) | HTML | The frame: screen, D-pad, A/B buttons |
| `<script>` | JavaScript | The game: map, battles, catching, sound |
| `HARNESS` in the script | **Python** | Runs *your* code one line at a time |

## The JavaScript, section by section

1. **Pixel art.** Each sprite is a grid of letters, and each letter is a colour.
2. **Creatures.** `SPECIES` lists every kind of creature. `makeCreature()` builds one, including its brain code. `stats()` reads the brain, and `checkBrain()` lists the rules a brain must follow.
3. **Map.** Each letter in `MAP` is a tile, and `g` is tall grass. `WILD` says which creatures live where.
4. **Saving.** Progress is kept in your browser.
5. **Helpers.** Small tools used everywhere.
6. **Sound.** Sound effects and three music loops, all made from code.
7. **Tiles.** Trees, grass, water and houses, drawn pixel by pixel.
8. **Player.** Walking, picking up berries, and random encounters in tall grass.
9. **Game loop.** Runs about 60 times a second and draws the world or the battle.
10. **Talking.** Text that types itself out, letter by letter.
11. **The A button.** Decides what happens when you talk to or touch something.
12. **Python.** Runs your code and snapshots every variable after each line.
13. **Friendly errors.** Python's error messages in plain words.
14. **Code console.** The editor that slides up. `editBrain()` edits a creature's brain.
15. **Story start.** Hatching and the first brain with Old Moss.
16. **Battles.** `battle()` runs the turns. `attack()` does the damage maths. `catchFlow()` handles the jar. `SABOTAGE` lists the moth's tricks.
17. **Voice Stone and boss.**
18. **Team view (B).** Your creatures, their brains, and the creature log.
19. **Menus and level clear.**
20. **Controls.**
21. **Start.**

## Try changing it

- Make a creature stronger: change its `base` numbers in `SPECIES`.
- Make wild creatures appear more often: change `0.16` in `arrived()`.
- Add a creature to an area: add it to `WILD`.
