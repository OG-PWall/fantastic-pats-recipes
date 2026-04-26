# Add Recipe

Add a new recipe to the personal recipe site at `/Users/johnwall/fantastic-pats-recipes/site/`.

## Rules — always, no exceptions
- All temperatures in **Fahrenheit** (convert from Celsius if needed)
- All measurements in **grams** (convert from cups, oz, lbs, ml if needed)
- No stories, no prose narrative, no "tips" sections — just what to do and when
- **Choose the right format:**
  - **Schedule format** — use when timing matters: bread, fermentation, multi-stage bakes, anything with rests or temperature windows. Uses `.day-label` + `.event` blocks.
  - **Numbered steps format** — use for simple recipes where steps just happen in order with no meaningful timing (sauces, dressings, rubs, quick sides). Uses `.steps` `<ul>` with `.step-name` / `.step-detail` inside each `<li>`.

## Step 1 — Get the recipe

If given a URL, fetch it with WebFetch. Extract:
- Recipe name and yield
- All ingredients with weights → convert everything to grams
- All temperatures → convert to Fahrenheit
- Process steps with timing (rest times, fermentation windows, bake temps and durations)

For sourdough specifically, note:
- Total hydration %
- Levain build details (separate from final dough)
- Bulk fermentation time and fold schedule
- Proof time and whether cold or room temp

## Step 2 — Create the HTML file

File path: `/Users/johnwall/fantastic-pats-recipes/site/recipes/<slug>.html`

Slug: kebab-case from recipe name (e.g. "White Sandwich Loaf" → `white-sandwich-loaf.html`)

Use `/Users/johnwall/fantastic-pats-recipes/site/recipes/whole-wheat-sourdough-schedule.html` as the structural template. Always include:
- `<link rel="stylesheet" href="../style.css">`
- Nav with `← Recipes` back link to `../index.html`
- Page title and sub — include source link if a URL was provided: `· <a href="URL" target="_blank" rel="noopener">original ↗</a>`
- "Ingredients at a glance" section using `.ing-table` with grouped rows

Then for the method, use whichever format fits:

**Schedule format** (timing matters):
- `.day-label` + `.event` blocks with `.event-time` / `.event-name` / `.event-detail`
- Times are illustrative — pick a realistic start time for that type of recipe, and note to adjust

**Numbered steps format** (order-only, no meaningful timing):
```html
<ul class="steps">
  <li>
    <div>
      <span class="step-name">Step name</span>
      <span class="step-detail">Details here.</span>
    </div>
  </li>
</ul>
```
Note: the `<div>` wrapper is required — without it, `step-name` and `step-detail` become separate grid items and the text collapses into a narrow column.

## Step 3 — Add to index

Read `/Users/johnwall/fantastic-pats-recipes/site/index.html`. Add a new `.card` entry inside `.card-list`:

```html
<a class="card" href="recipes/<slug>.html">
  <span class="card-tag">Category</span>
  <div class="card-name">Recipe Name</div>
  <div class="card-desc">yield · key stat · key stat</div>
</a>
```

Categories: Sourdough, Bread, Enriched, Flatbread, Other — pick the most accurate one.

The card should link directly to the schedule HTML (no format picker — schedule is the standard format).

## Step 4 — Confirm

Report back:
- The file created
- The ingredients (with gram weights and Fahrenheit temps)
- Any conversions that were uncertain or estimated
