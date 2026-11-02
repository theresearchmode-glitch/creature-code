# How Creature Code works (Level 1)

The whole game is one file: `index.html`. Open it in a browser and it runs. This guide walks through it piece by piece, in plain words.

## The three languages in one file

| Part | Language | Its job |
|---|---|---|
| `<style> … </style>` | CSS | How things look: colours, sizes, layout, animations |
| The tags in the middle (`<div>`, `<svg>`, `<textarea>`) | HTML | What's on the page: the habitat, the editor, the buttons |
| `<script> … </script>` | JavaScript | What happens: running code, moving the creature, checking answers |
| Inside the script, `HARNESS` | **Python** | Runs *your* code one line at a time |

You're learning Python, but a web page speaks HTML, CSS and JavaScript. Pyodide is the bridge: it's the real Python language, packed so a browser can run it. No install needed.

## The CSS (look and feel)

- **Colour tokens.** At the top, `:root { --bg: …; --ink: …; --yolk: … }` gives every colour a name. The rest of the page uses the names, like `var(--yolk)`. Change a colour in one place and it updates everywhere. It's the same idea as a Python variable!
- **Dark mode.** The `@media (prefers-color-scheme: dark)` block swaps the colour values when your device is in dark mode.
- **Layout.** `.grid` puts the creature on the left and the code on the right. On a phone (`max-width: 880px`) everything stacks in one column.
- **Animations.** `@keyframes wobble`, `bounce`, `hatch` and `evolve` describe movements. Adding a class like `bounce` to the creature plays one.

## The HTML (what's on the page)

- **The stage** (`id="stage"`) holds the creature, drawn as an SVG. SVG draws shapes with code: `<ellipse>` for eyes, `<path>` for the body. The egg, the flame, the water fin and the leaves are all in there. CSS shows or hides the right parts.
- **The memory shelf** (`id="shelf"`) is where your variables appear as labelled boxes.
- **The bug jar** (`id="jar"`) counts the errors you've fixed.
- **The mission card** (`id="mission"`) is filled in by JavaScript for each step.
- **The editor** is a `<textarea>` (a big text box) with line numbers beside it.

## The JavaScript, section by section

The script has numbered sections. Here's what each one does.

1. **The five missions (`STEPS`).** A list of missions. Each one has a title, the idea it teaches, the code to add, and a `check()` that looks at your variables after a run and says "it worked" or gives a hint. For example, mission 3 checks that `hp` is a number and not the string `"20"`.
2. **Saving progress.** `localStorage` is a small notebook the browser keeps for this page. Your step, code and bugs are saved there, so a reload doesn't lose your place.
3. **Grabbing page parts.** `document.getElementById("code")` finds the editor so the script can read your code.
4. **The Python side (`HARNESS`).** This is a Python function, `_creature_run`, that:
   - runs your code with `exec`
   - uses `sys.settrace` to pause before every line. That's how the creature acts out one line at a time
   - takes a snapshot of every variable after each line
   - catches anything `print()` says
   - catches errors and notes which line broke

   It sends all of that back to JavaScript as JSON (a text format both languages understand).
5. **The editor.** Draws line numbers, highlights the line that's running, and swaps phone "curly quotes" for straight ones, because Python only understands `"` and `'`.
6. **Drawing the creature.** `applyVars()` makes the creature match your variables. If `name` exists, the egg hatches. `element` sets the colour. Each variable becomes a box on the shelf.
7. **Friendly errors.** `explainError()` turns Python's error messages into plain words. You see both, so you get used to reading real Python errors.
8. **Feedback panel.** Shows green (it worked), yellow (almost) or red (error).
9. **Running your code (`run()`).** Sends your code to Python, replays the snapshots line by line with a pause between each, then checks the mission. If the last run had an error and this one doesn't, you catch the bug.
10. **Moving through the level.** `nextStep()` adds the next mission's code to the editor. `finishLevel()` makes the creature evolve and shows the skill card.
11. **Start.** Puts your saved code back, draws everything, and starts loading Python.

## Bugs you can catch

| Error | Bug | Usually means |
|---|---|---|
| `NameError` | Namegnat | Forgot quotes around text, or misspelled a variable |
| `SyntaxError` | Syntick | A missing quote, bracket or `=` |
| `IndentationError` | Indentipede | Extra spaces at the start of a line |
| `TypeError` | Typemite | Mixed text and numbers with `+` |
| anything else | Mystery Moth | |

## Try changing it

Good first edits to the game itself:

- Add a fourth element. Add `"rock"` to the list in mission 2's `check()`, a colour in the CSS (`.creature-svg[data-element="rock"]`), and a head shape in the SVG.
- Change the creature's colours in the `--body` lines.
- Make the line-by-line replay slower: in `run()`, change `550` to `900`.
