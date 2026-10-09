# Vanik design language

Version 1.0, October 2026. One small library for every Vanik product: the console, VanikGPT, Vanik Sense, Vanik Scout, Vanik MeasureBook, Vanik Desk, Document Processing.

The style is neo-minimal: ink on paper, one accent, hairlines instead of boxes, and motion only where it explains something.

- **Library:** `vanik-ui.css` and `vanik-ui.js`. No build step. No dependencies.
- **Live page:** open `index.html`, or the published page of this repository.
- **Fonts:** Plus Jakarta Sans for text, IBM Plex Mono for numbers and codes.

## 1. Seven rules

| # | Rule | In practice |
|---|---|---|
| 1 | **One thing per screen** | Each screen answers one question. The main action is the only filled button. Extras live in a menu |
| 2 | **Ink, paper, one accent** | Text and actions are ink. Surfaces are paper. Green is the only accent, used for "on", "done" and the family mark. State colours are for state only |
| 3 | **Hairlines, not boxes** | A 1px line separates things. Cards have a border and no shadow. Only things that float (menus, dialogs, hints) cast one soft shadow |
| 4 | **Type does the hierarchy** | Size and weight carry importance. No coloured headings, no underlines, no all-caps except the small label |
| 5 | **Space is the layout** | Everything sits on a 4px grid. When in doubt, add space and remove a line |
| 6 | **Motion explains** | Movement is short (120 to 200 ms) and shows cause and effect. The only looping motion is a hint, and it stops when the person asks for less motion |
| 7 | **Plain words** | Short sentences. The word a person would say. No internal names on screen |

## 2. Tokens

All tokens are CSS variables on `:root`. Dark values switch with `data-theme="dark"` or the system setting.

### Colour

| Token | Light | Use |
|---|---|---|
| `--vnk-bg` | `#fafaf8` | The page |
| `--vnk-surface` | `#ffffff` | Cards, inputs, menus |
| `--vnk-surface-2` | `#f3f3f0` | Hover, quiet fills |
| `--vnk-border` | `#e7e7e2` | Hairlines |
| `--vnk-border-2` | `#d3d3cd` | Input and button outlines |
| `--vnk-ink` | `#0c0d0d` | Text, the main button |
| `--vnk-ink-2` | `#55574f` | Secondary text |
| `--vnk-ink-3` | `#8d8e86` | Labels, hints |
| `--vnk-brand` | `#1fa350` | The one accent |
| `--vnk-ok`, `--vnk-warn`, `--vnk-err` | green, amber, red | State only, each with a `-bg` pair |

### Type

| Use | Size and weight |
|---|---|
| Page title (`h1`) | 28px, 700, tight |
| Section (`h2`) | 20px, 700 |
| Card title (`h3`) | 15px, 600 |
| Body | 14px, 400, line height 1.5 |
| Small (`.small`) | 12.5px |
| Label (`.cap`) | 10.5px, 600, spaced capitals |
| Numbers and codes (`.mono`) | 12px mono |

### Space, shape, motion

| Token | Value |
|---|---|
| `--vk-1` to `--vk-7` | 4, 8, 12, 16, 24, 32, 48 px |
| `--vk-r-s`, `--vk-r`, `--vk-r-l` | 6, 10, 14 px corners |
| `--vk-fast`, `--vk-base` | 120 ms, 200 ms |
| `--ease` | `cubic-bezier(.2, .7, .2, 1)` |
| `--ring` | The focus ring: a soft green halo |

## 3. Components

| Component | Class | Notes |
|---|---|---|
| Main button | `.btn` | One per screen. Pill shape, ink fill |
| Quiet button | `.btn.ghost`, `.btn.text` | Everything else |
| Destructive | `.btn.danger` | Only inside a confirm dialog |
| Icon button | `.icon-btn`, `.icon-btn.sm` | Always with an `aria-label` |
| Input | `.input` inside `.field` | The label is a `span` above the input |
| Switch | `.switch`, `.switch.on` | For a setting that takes effect at once |
| Choice of one | `.seg` with buttons | Two to four options |
| Filter | `.toggle`, `.toggle.on` | Shows a dot when on, so it never looks like a label |
| State | `.chip`, with `.ok`, `.warn`, `.err` | A word, not a sentence |
| Tag | `.tag`, `.tag.on` | A value a person chose or can remove |
| Card | `.card`, `.card.next` | `.next` marks the one thing to do now |
| Row | `.set-row` | A label on the left, one control on the right |
| Table | `table.list` | No vertical lines |
| Tabs | `.tabs` with links | The current one has `.on` |
| Notice | `.banner` | One line, with at most one button |
| Nothing here | `.empty` | Says what will appear and how to make it appear |
| Family mark | `.vk-brand` | "Vanik Edge" small, then the product name |
| Hint | `.vk-hint` | See below |

## 4. The family mark

Every product header reads the same way: the Vanik Edge mark first, then the product.

```html
<span class="vk-brand"><small>Vanik Edge</small><b>Sense</b></span>
```

## 5. Hints: a moving picture instead of a manual

A hint is a small "?" tag. It opens a card with a few steps on a line. The steps light up one after another, each with one sentence. A person learns how a screen works in ten seconds without leaving it.

**When to use one**

- Once per product, beside its title: "how this works".
- On a screen whose idea is not obvious: access, knowledge, a review queue.
- Never to explain a single control. Rename the control instead.

**Rules**

- Three to five steps. One sentence each.
- It pulses until the person opens it once, then stays quiet.
- With reduced motion on, it shows all steps as a list and does not move.

```html
<script src="vanik-ui.js"></script>
<script>
  VanikUI.hint.define('ask', {
    title: 'How asking works',
    steps: [
      { label: 'Ask', text: 'Type a question in your own words.' },
      { label: 'Look', text: 'It searches only the documents you can read.' },
      { label: 'Answer', text: 'You get an answer with its sources, or "not found".' },
    ],
  });
</script>
<button class="vk-hint" data-vk-hint="ask" aria-label="How asking works"></button>
```

`VanikUI.hint.tag('ask')` returns the same button as HTML, for apps that build their pages in script. A step may carry an `icon` (any small HTML); without one it shows its number.

## 6. Patterns

| Pattern | How |
|---|---|
| Page head | `h1`, one line under it, the main button on the right |
| First run | One card, `.card.next`, with one button. Never a tour of five screens |
| Empty state | `.empty` with one sentence and one button |
| Confirm | A small centred dialog. The safe choice is the quiet button |
| Something failed | Say what, in one sentence, with one button to try again. Raw details go under "Details" |
| Long list | A table with a search box. No more than three filters visible |

## 7. Do and do not

| Do | Do not |
|---|---|
| One filled button per screen | Two filled buttons side by side |
| A hairline between sections | A box inside a box |
| Green for "on" and "done" | Green for decoration |
| A sentence under a title | A paragraph under a title |
| A hint beside the title | A help page |
| Plain numbers in mono | Charts where a number would do |

## 8. Using it

1. Add the fonts and the two files:

```html
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="vanik-ui.css">
<script src="vanik-ui.js"></script>
```

2. Use the classes. There is nothing to configure.
3. For dark mode, set `data-theme="dark"` on `<html>`, or leave it to the system.

## 9. Changing it

- A new colour needs a reason that the seven rules cannot meet.
- A new component starts in one product, proves itself, then moves here.
- Tokens keep their names. Values may change in a new version.
