# How Creature Code works (Level 1: The Forgetful Village)

The whole game is one file: `index.html`. This guide walks through it in plain words.

## The story

The Glitch Moth ate Mossbrook's memory. You hatch a creature, walk it around the village, and fix things by writing Python at glowing memory stones:

| Stone | Python idea | What your code does in the world |
|---|---|---|
| The egg | `name = "Pip"` (a variable) | The egg hatches |
| Element Stone | `element = "fire"` (strings) | Burns, washes or vines away the brambles |
| Strength Stone | `hp = 50` (numbers vs text) | Pushes the boulder. `"50"` with quotes fails! |
| Voice Stone | `print(name)` | Your creature says its name and wakes Pebble |
| Mood Stone | changing a variable | `mood` goes from "scared" to "brave", and the cave opens |
| Glitch Moth | fixing broken code | Each fixed line is a hit. Each error costs a heart |

## The three languages in one file

| Part | Language | Its job |
|---|---|---|
| `<style>` | CSS | How it looks: the console shell, buttons, the code sheet |
| The tags (`<canvas>`, `<button>`) | HTML | The frame: screen, D-pad, A/B buttons |
| `<script>` | JavaScript | The game: map, walking, talking, sound, the boss |
| `HARNESS` inside the script | **Python** | Runs *your* code one line at a time |

## The JavaScript, section by section

1. **Pixel art.** Each sprite is a grid of letters, and each letter is a colour. `drawSprite()` paints one square per letter.
2. **The map.** `MAP` is a list of strings. Each letter is a 16 × 16 tile: `T` tree, `~` water, `=` path, `*` brambles. `ENTITIES` places the villagers, stones and the boulder.
3. **Saving.** `localStorage` keeps your progress in the browser.
4. **Helpers.** Small tools, like `fill()`, which swaps `{name}` for your creature's name.
5. **Sound.** Every sound effect and both music loops are made from code with the Web Audio API. There are no sound files.
6. **Drawing tiles.** Trees, water, houses and cliffs are drawn pixel by pixel with `fillRect`.
7. **The player.** `tryMove()` checks whether the next tile is solid (`solidAt()`), then slides the creature over.
8. **Game loop.** `loop()` runs about 60 times a second. It moves things, then draws the world (or the battle).
9. **Talking.** `dialog()` shows text letter by letter with a little beep, like old handheld games.
10. **The A button.** `interact()` looks at the tile in front of the creature and decides what happens.
11. **Python.** `_creature_run` runs your code, pausing before every line to take a snapshot of all the variables. It starts with the variables already in your creature's brain, so they carry over between stones.
12. **Friendly errors.** Python's error messages translated into plain words.
13. **Puzzles.** `PUZZLES` holds each stone: what it says, the task, the hints, a `check()` of your variables, and an `effect()` that changes the world.
14. **The code console.** The sheet that slides up. It replays your code line by line and explains what Python did.
15. **Boss battle.** `ATTACKS` lists the moth's broken lines. `startBoss()` runs the fight.
16. **Menus.** Top bar, brain view, level clear screen and skill card.
17. **Controls.** D-pad, A, B, and keyboard support.
18. **Start.** The intro with Old Moss.

## Try changing it

- Add a berry: add `[x, y]` to `BERRIES`.
- Change what a villager says: edit `talkCap()` or `talkMoss()`.
- Move things around: edit the letters in `MAP`.
