> See [`strategist.md`](./strategist.md) for the core role and load trigger.

# Strategist Image Planning

Conditional extension for formula assets, proposed / confirmed image elaboration, and `design_spec.md §VIII` resource planning.

**Trigger**: Core first derives proposed `recommend.image_usage`. Load this module before Stage-2 direction construction when that proposal contains any non-`none` source, when the user supplied an explicit non-`none` image constraint, or when formula handling is triggered. After confirmation, the confirmed sources bound production: confirmed `none` with no formula trigger stops before resource authoring. On a formula-only path, read §3 and the formula-row rules in §4; skip non-formula planning. [`strategist.md`](./strategist.md) owns source recommendation; this module owns image-dependent candidates, production detail, and §VIII rows.

---

## 1. Proposed and Confirmed Image Plan

Before Stage 2, use proposed sources only for candidate construction. After confirmation, discard candidate-only sources, map the confirmed set through [`strategist.md`](./strategist.md) §h, and honor every explicit role or page instruction in `image_notes`; this module never adds a source. The confirmed set is a production requirement, not a fresh candidate list: represent every confirmed non-`none` source at least once. Asset inventory and later aesthetic judgment may shape the unconfirmed count, subject, placement, and composition, but must not delete, substitute, or demote a confirmed source.

For illustration, apply this precedence: confirmed `none` → explicit user intent → the locked visual style's `Illus.` propensity (`core` / `supportive` / `sparse`) → none. Propensity controls the lean, not the source or a page quota. When illustration is active, prefer one coherent motif family across hero/section anchors and local spots, but only when the confirmed assets can form that family.

## 2. Formula Asset Policy

Formula rendering is a conditional choice surfaced in Stage 3 production confirmation. Recommend one policy and let the user confirm or override it:

| Policy | Behavior | Use |
|---|---|---|
| `mixed` (default) | Render complex expressions to PNG; keep simple inline math as editable text / Unicode | Most academic, engineering, educational, and technical decks |
| `render-all` | Render every formula-worthy expression to PNG | Formula-heavy teaching / research decks where consistency matters more than editability |
| `text-only` | Keep expressions as editable text / Unicode | Business decks, light technical briefs, or an explicit editability preference |

`$...$` / `$$...$$` in source material are input signals only. Never scan output files for dollar-delimited formulas. Fractions, radicals, integrals, sums, limits, matrices, multiline derivations, and complex super/subscripts are formula-worthy; short variables, simple assignments, percentages, and expressions such as `O(n log n)` normally remain text. Never invent an equation for decoration.

For `mixed` or `render-all`, write selected source expressions to `<project_path>/images/formula_manifest.json` before writing the final spec, then run:

```bash
python3 skills/ppt-master/scripts/latex_render.py <project_path>
python3 skills/ppt-master/scripts/analyze_images.py <project_path>/images
```

Follow `latex_render.py --help` for the manifest fields. The renderer writes dimensions, ratio, file, provider, and status back into it. Formula PNGs default to transparent; use an opaque final background only when the asset requires it.

## 3. Image Resource List

Add §VIII for every confirmed non-`none` source and selected formula; a formula-only plan contains only formula rows. Fill the scaffold's filename, dimensions/ratio, layout suggestion/pattern, purpose/type, acquisition, and status. `Acquire Via` is `web`, `user`, `formula`, or `placeholder`; status follows [`svg-image-embedding.md`](./svg-image-embedding.md). When an asset is not yet available, retain its confirmed-source row as `Pending` or `Needs-Manual`; never remove the row or change `Acquire Via` to make the Design Spec look complete. Only after §VIII passes the final-confirmation fidelity gate, project the same planned filenames and acquisition sources into `spec_lock.md images`; do not redesign the image plan while writing the lock. References describe visual intent: web uses a concrete subject plus a few positive quality descriptors; formula preserves the source LaTeX and placement intent.

🚧 **GATE — non-formula rows**: read every entry in [`image-layout-patterns.md`](./image-layout-patterns.md). Copy one primary `#<id> <name>` plus any modifier names verbatim into each row; no empty, paraphrased, or invented ids. For decks with at least four image-bearing pages, use an Image-as-Canvas + Native Overlay pattern at least once unless every image is purely a cover, divider, or atmospheric backdrop; record the legitimate exception below the table. Reconsider a plan that collapses every row to the same left/right or top/bottom split.

Choose narrative intent before dimensions: hero/full-bleed, atmosphere/background, side-by-side, or accent/inline. Only side-by-side containers follow native ratio; portrait and multi-image calculations belong to [`image-layout-spec.md`](./image-layout-spec.md). Most assets are croppable. Add `no-crop` in `spec_lock.md images` only for screenshots, charts, certificates/contracts, dense diagrams, and every formula; formula rows use `Type: Latex Formula`, `Acquire Via: formula`, and `Rendered` or `Needs-Manual`.

Step 5 dispatches pending `web` rows to Image_Searcher; formula rows bypass image search.
