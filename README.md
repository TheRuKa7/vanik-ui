# Vanik UI

A small neo-minimal design library: ink on paper, one accent, hairlines, quiet motion. Two files, no build step, no dependencies.

- **See it:** open `index.html`.
- **Read the rules:** [DESIGN_LANGUAGE.md](DESIGN_LANGUAGE.md).

## Use it

```html
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="vanik-ui.css">
<script src="vanik-ui.js"></script>

<button class="btn">Add an app</button>
<button class="btn ghost">Cancel</button>
<span class="chip ok"><i></i>Running</span>
```

## What is in it

| File | What |
|---|---|
| `vanik-ui.css` | Tokens (colour, type, space, shape, motion), light and dark, and the components: buttons, inputs, switch, choice, filter, chip, tag, card, row, table, tabs, notice, empty state, family mark, hint |
| `vanik-ui.js` | Hints: a "?" tag that opens a small moving picture explaining one thing |
| `index.html` | Every component on one page |
| `DESIGN_LANGUAGE.md` | The seven rules, the tokens, the components, patterns, do and do not |

## Hints

```html
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

Three to five steps, one sentence each. It pulses until opened once. With reduced motion on, it shows the steps as a list.

## Dark mode

Set `data-theme="dark"` on `<html>`, or leave it to the system setting.
