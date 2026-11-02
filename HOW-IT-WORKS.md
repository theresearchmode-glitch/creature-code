# How Creature Code works (Level 1)

The whole game is one file: `index.html`. This guide walks through it piece by piece, in plain words.

## The three languages in one file

| Part | Language | Its job |
|---|---|---|
| `<style> … </style>` | CSS | How things look: colours, sizes, the pixel-style boxes |
| The tags in the middle (`<div>`, `<canvas>`, `<main>`) | HTML | The empty frame: top bar, creature window, panel |
| `<script> … </script>` | JavaScript | Everything that happens: lessons, drawing, running your code |
| Inside the script, `HARNESS` | **Python** | Runs *your* code one line at a time |

A web page speaks HTML, CSS and JavaScript. Pyodide is the bridge: it's the real Python language, packed so a browser can run it.

## The CSS

- **Colour names.** At the top, `:root { --cream: …; --ink: …; --yolk: … }` gives every colour a name, used later as `var(--yolk)`. Change it once, it changes everywhere. Same idea as a Python variable!
- **Pixel boxes.** Real pixel games have square, notched corners. The `.px` and `.btn` rules fake that with four hard shadows (`box-shadow`), one per side.
- **Fonts.** Pixelify Sans for text, VT323 for code. Both come from Google Fonts.

## The JavaScript, section by section

1. **Pixel art.** Each sprite (egg, creature, Old Moss, bugs) is a grid of letters. Each letter is a colour: `o` is the outline, `b` is the body, and so on. `drawSprite()` paints one square per letter.
2. **The lessons (`SCREENS`).** The level is a list of screens. Each has a `type`:
   - `talk`: Old Moss explains something. You tap to go on.
   - `example`: you watch some Python run.
   - `quiz`: you pick an answer, and every answer explains itself.
   - `code`: you type Python. Each has `hints` and a `check()` that looks at your variables and decides "it worked" or "almost".

   To change what the game teaches, edit this list. No other code needs to change.
3. **Saving.** `localStorage` is a little notebook the browser keeps. Your screen, code, creature and bugs are saved there.
4. **Helpers.** `rich()` turns `` `backticks` `` in lesson text into code chips. `fill()` swaps `{name}` for your creature's name.
5. **The creature window.** A tiny 80 × 50 pixel canvas, stretched to fill the screen, so every pixel shows as a chunky square. `drawScene()` redraws it 10 times a second: sky, clouds, hill, then the egg or creature. The creature's colours come from `ELEMENTS`.
6. **Python.** `HARNESS` is a Python function, `_creature_run`. It runs your code with `exec`, and uses `sys.settrace` to pause before every line and take a snapshot of every variable. It sends everything back as JSON, a text format both languages understand.
7. **Friendly errors.** `explainError()` turns Python's error messages into plain words. You see Python's real message too, so you learn to read them.
8. **Showing screens.** `render()` clears the panel and calls the right function for the screen type. `go()` moves between screens.
9. **Code challenges.** `renderCode()` builds the editor, the symbol keys and the HINT and RUN buttons. `run()` sends your code to Python, then replays the snapshots one line at a time. It writes "What Python did" in plain words, draws your variables as boxes, and moves the creature.
10. **Level complete.** The creature evolves, and you get a skill card and a share message.
11. **Menu.** How to play, and restart.
12. **Start.** Shows the title screen.

## Bugs you can catch

| Error | Bug | Usually means |
|---|---|---|
| `NameError` | Namegnat | Forgot quotes around text, or misspelled a label |
| `SyntaxError` | Syntick | A missing quote, bracket or `=` |
| `IndentationError` | Indentipede | Spaces at the start of a line |
| `TypeError` | Typemite | Mixed text and numbers with `+` |
| anything else | Mystery Moth | |

## Try changing it

- Change what Old Moss says: edit the `lines` in any `talk` screen.
- Add a quiz: copy a `quiz` screen in `SCREENS` and change the question and options.
- Recolour the fire creature: change `b` (body) and `d` (dark) in `ELEMENTS.fire`.
