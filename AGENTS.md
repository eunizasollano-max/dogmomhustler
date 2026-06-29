# AI Agent Instructions for Website Design Recreation

## Project Purpose

This workspace is for **recreating website designs from reference images** using HTML and CSS (Tailwind via CDN). The workflow involves generating a design, taking screenshots with Puppeteer, comparing against the reference, and iterating until pixel-perfect accuracy.

## Core Workflow

When a user provides a reference image (screenshot):

1. **Generate** a single `index.html` file
2. **Screenshot** the rendered page with Puppeteer
3. **Compare** screenshots for mismatches
4. **Fix** any differences found
5. **Repeat** steps 2–4 until accuracy is achieved (within ~2–3px)

**Important**: Always do at least 2 comparison rounds. Never stop after one pass.

See [rules/03-workflow.md](rules/03-workflow.md) for detailed workflow steps and measurement guidelines.

## Technical Stack & Defaults

- **CSS Framework**: Tailwind CSS via CDN (`<script src="https://cdn.tailwindcss.com"></script>`)
- **Screenshot Tool**: Puppeteer (`npx puppeteer screenshot index.html --fullpage`)
- **File Structure**: Single `index.html` file (no external files unless requested)
- **Images**: Use `https://placehold.co/` for placeholder images
- **Responsive Design**: Mobile-first approach

See [rules/02-technical-defaults.md](rules/02-technical-defaults.md) for complete technical specifications.

## Design Accuracy Rules

- **Fidelity**: Match the reference exactly—do not "improve" or add features
- **Content**: Do not add sections or content not present in the reference image
- **CSS**: If user provides CSS classes or style tokens, use them verbatim
- **Code Quality**: Keep code clean; inline Tailwind classes are acceptable
- **Precision**: When reporting mismatches, be specific (e.g., "heading is 32px but reference shows ~24px")

See [rules/01-design-rules.md](rules/01-design-rules.md) for complete design rules.

## Common Commands

```bash
# Screenshot the current page
npx puppeteer screenshot index.html --fullpage

# Screenshot a specific section (open in browser and measure)
npx puppeteer screenshot index.html --fullpage
```

## Comparison Process

When comparing your screenshot to the reference, check:
- Spacing and padding (measure in px)
- Font sizes, weights, line heights
- Colors (exact hex values)
- Alignment and positioning
- Border radii, shadows, effects
- Responsive behavior
- Image/icon sizing and placement

## Key Files

- **[CLAUDE.md](CLAUDE.md)**: Quick reference and navigation hub
- **[rules/01-design-rules.md](rules/01-design-rules.md)**: Design constraints and accuracy rules
- **[rules/02-technical-defaults.md](rules/02-technical-defaults.md)**: Technical stack and defaults
- **[rules/03-workflow.md](rules/03-workflow.md)**: Step-by-step workflow instructions
- **index.html**: The main deliverable file

## Tips for Success

1. Always set up the screenshot comparison before starting edits
2. Make targeted fixes based on specific measurements, not guesses
3. Take screenshots after each significant change
4. Compare at 100% zoom for accuracy
5. Use the browser's dev tools to inspect element dimensions
6. Document color values and spacing as you go

---

## Available Agents

### tell-me-the-time
Tells you the current time in Philippine time. Greets you with "Hi, Niza!"

**File**: [agents/tell-me-the-time.md](agents/tell-me-the-time.md)
