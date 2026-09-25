# nbinlineai GitHub notebook rendering probe

A synthetic notebook used to check how GitHub's native `.ipynb` preview handles AI-cell color. [View the probe notebook](render-probe.ipynb).

Observed in GitHub's notebook viewer on 2026-09-25:

- `metadata.nbinlineai.isPromptCell` and `isOutputCell` do not change appearance. GitHub renders those Markdown cells like ordinary cells.
- Inline `style` on a Markdown cell's HTML block retains background, border, and padding. A block can use `color-mix()` and the viewer's `--jp-brand-color1`, `--jp-success-color1`, and `--jp-layout-color0` variables to follow its light or dark theme.
- Markdown inside the styled HTML block remains rendered as Markdown, including bold text, lists, and fenced code.
- A `<style>` tag in Markdown does not style the notebook; a `class` on the following block alone has no effect. A `bgcolor` table attribute also produced no visible background in this probe.
- Saved `text/html` code output can use inline styles, but it remains code output rather than an AI Markdown cell.

The probe changes cell **source** to carry the inline HTML. That is a meaningful trade-off for an AI question, because nbinlineai submits the question's source to the model. A separate export copy could add the HTML for GitHub while leaving the working notebook unchanged.
