---
name: custom-codex-pet-styles
description: Style-router for custom Codex pets. Use when a user wants to turn an uploaded photo, character image, logo mascot, object image, or text-described subject into a better-looking Codex pet using one of three fixed visual styles, then automatically hand the reference image and structured visual brief to $hatch-pet for a complete animated pet package. Use when users ask for custom Codex pet styles, pet style previews, soft sticker pets, black-and-white doodle pets, or modern pixel pets.
---

# Custom Codex Pet Styles

## Role

Guide the user through a reference-first style choice, then hand a structured brief to `$hatch-pet`. Do not generate spritesheets, implement atlas logic, or replace `$hatch-pet`.

Supported styles:

- `soft-sticker` / 软萌扁平贴纸风
- `doodle-plush` / 黑白手绘涂鸦风
- `modern-pixel` / 现代像素宠物风

## Workflow

1. Welcome the user briefly. Tell them to upload a reference photo, character image, logo mascot, or object image to start. Text-only descriptions are allowed, but warn that results are usually less faithful than image-grounded pets.
2. Ask whether they already know which of the three styles they want. List the three styles with one short phrase each.
3. If they are unsure, ask whether they want a single preview image comparing all three styles. If yes, use `$imagegen` to create one three-column preview of the same subject in a static full-body pose. Preview labels are allowed because the preview is not the final pet.
4. After showing the preview, explicitly ask which style they want to use. They may choose one style, or choose one primary style with a small influence from another style. Keep blends anchored to the three fixed recipes; do not create a fourth style or a vague equal-weight mix.
5. Once a reference and style direction are available, analyze the uploaded image or text description for identity anchors, then draft a concise final style brief.
6. Before invoking `$hatch-pet`, show a short final-check summary covering selected style, any blend/tweaks, identity anchors, and key avoidances. Ask whether the user wants any changes. If they approve or ask for no changes, continue automatically.
7. Automatically invoke `$hatch-pet` with the reference image and the `Hatch-pet handoff brief`. Do not ask for extra confirmation unless the user explicitly says they only want a prompt or preview.

## Style Choice Rules

Allow:

- one fixed style with optional small tweaks
- one primary style plus one narrow borrowed quality from another fixed style, such as `soft-sticker with slightly wobblier doodle outlines`
- minor user preferences that do not weaken identity lock, sprite readability, transparency, or state consistency

Do not allow:

- a fourth custom style
- an undefined blend such as `mix all three`
- changes that make the pet too detailed, non-transparent, hard to animate, or inconsistent across states

## Identity Anchors

Extract and preserve:

- subject type, species, object type, or mascot category
- whole-body silhouette and main proportions
- key face structure, eyes, mouth/nose placement, expression cues
- signature shapes, markings, appendages, hair, ears, tail, wings, limbs, or object parts
- essential palette and high-contrast identity colors
- essential clothing, accessories, or logos only when they are truly part of the subject identity

## Universal Pet Rules

Use these constraints for every style:

- Preserve the uploaded subject's recognizable identity while simplifying it into a compact animated pet. Keep the same identity across every animation state.
- Keep the pet compact, centered, fully visible, and readable at small sprite size with a clear whole-body silhouette and generous padding.
- Maintain the same face, body proportions, palette, material/style, markings, and defining traits across `idle`, `running-left`, `running-right`, `waving`, `jumping`, `failed`, `waiting`, `running/work`, and `review`.
- Show each state through pose, expression, posture, and body movement only. Keep actions simple, readable, and loop-friendly.
- Use transparent background only. No scenery, floor, cast shadow, contact shadow, drop shadow, frame, border, guide mark, watermark, or background texture.
- Do not add text, logos, UI, readable symbols, floating icons, props, accessories, extra characters, speed lines, motion trails, dust clouds, impact bursts, or decorative effects unless explicitly part of the uploaded subject's essential identity.
- Simplify complex textures, markings, fur, feathers, materials, or surface details into larger readable shapes. Preserve the idea of the detail, not every tiny element.
- The selected style recipe controls the final visual language. Do not fall back to generic `$hatch-pet` aesthetics if they conflict with the selected style.
- Preserve identity first when the reference and style conflict, then adapt the style around it.
- Do not invent a new mascot, alternate costume, new species, new object type, new hair/face, or unrelated cute character.
- Use clean outer contours and enough contrast for both light and dark Codex UI backgrounds.

State semantics:

- `idle`: calm micro-motion only.
- `running-left/right`: directional travel motion only.
- `waving`: friendly greeting gesture only.
- `jumping`: vertical hop through body position only.
- `failed`: cute disappointed posture only.
- `waiting`: patient expectant user-input pose only.
- `running/work`: focused working-in-place state, not literal running.
- `review`: careful inspecting/thinking posture only.

## Style Recipes

### soft-sticker / 软萌扁平贴纸风

Recommended `$hatch-pet` style preset: `sticker`.

Create a soft kawaii flat-vector sticker pet. Use rounded smooth forms, squat compact proportions, large readable shape groups, warm thick brown outlines, cozy muted colors, simple face, minimal details, and gentle cute personality.

Favor circular cheeks, rounded paws or hands, softened corners, simplified appendages, and a slightly plush toy-like silhouette. Use flat color blocks with minimal shading only when needed for separation. Use simple soft eyes, a small mouth, and subtle cheek or cute expression cues.

Avoid pixel art unless the reference is already pixel art. Avoid glossy 3D, realistic fur, complex textures, painterly lighting, thin linework, high-detail illustration, sticker white borders, and decorative sticker effects.

### doodle-plush / 黑白手绘涂鸦风

Recommended `$hatch-pet` style preset: `auto`.

Create a loose black-and-white doodle plush pet, like a tiny handmade character sketched with a black felt-tip pen.

Use black hand-drawn ink lines with visibly imperfect uneven stroke weight, slight wobble, organic asymmetry, small contour gaps, and harmless overlaps. Keep the silhouette readable even when the line is imperfect. Use soft rounded plush proportions, compact squishy body shapes, naive handmade forms, and fluffy or scalloped edges only when they match the subject.

Use mostly white fill with black outlines and sparse black accents. Add color only when an essential identity marking would be lost without it, and keep that color minimal. Use tiny dot eyes, a small simple nose or equivalent facial mark, minimal mouth, and shy sweet expressions.

Avoid clean vector art, smooth digital outlines, polished icon art, geometric symmetry, crisp corporate mascot style, realistic fur texture, gradients, 3D rendering, manga/anime line art, and high-detail hatching.

### modern-pixel / 现代像素宠物风

Recommended `$hatch-pet` style preset: `pixel`.

Create a clean modern pixel-art mascot pet: true low-resolution pixel art on a small grid, scaled up with nearest-neighbor. Use crisp square pixels, hard edges, chunky silhouette, limited tasteful palette, bold black pixel outline, clean interior shapes, minimal dithering, and no anti-aliasing.

Make it cute, compact, polished, and contemporary, like a tiny desktop companion. It should feel designed and premium, not old arcade, tacky retro, cheap clipart, or messy game asset.

Simplify markings, textures, clothing, fur, feathers, or object details into clear pixel blocks. Preserve identity through silhouette, palette, key facial structure, and signature shapes rather than tiny scattered pixels.

Avoid muddy colors, noisy dithering, excessive highlights, pillow shading, fake 3D, gradients, blur, soft edges, soft shading, painterly texture, realistic texture, scenery, shadows, text, logos, props, accessories, and extra characters unless essential to the uploaded subject.

## Handoff Brief

Use this structure when invoking `$hatch-pet`:

```markdown
Use $hatch-pet to create a complete Codex pet package.

Reference:
- Use the uploaded image(s) as the primary identity source. If no image exists, use the text description but note that fidelity may be weaker.

Selected style:
- <style id and display name>
- Recommended style preset: <sticker|auto|pixel>
- User tweaks or blend rule: <none, or one primary style plus one narrow borrowed quality>

Identity anchors:
- <compact bullets extracted from the reference>

Universal rules:
- Preserve identity across every animation state.
- Keep the pet compact, centered, whole-body, transparent, and readable at small sprite size.
- Keep state semantics simple: idle, running-left/right, waving, jumping, failed, waiting, running/work, review.
- Do not add backgrounds, shadows, text, symbols, effects, extra props, or extra characters unless essential to the reference identity.

Style recipe:
- <copy the selected style recipe, shortened only if necessary>

Production requirement:
- Treat this brief as the authoritative visual spec.
- Do not fall back to generic hatch-pet styling when it conflicts with the selected style.
- Generate the full animated Codex pet package, validate it, QA the final contact sheet/previews, and install or place the package so the pet is available in Codex settings.
```

Before sending this handoff, ask:

```text
Final check before I hand this to hatch-pet: do you want to change the style, blend/tweaks, identity details, or avoidances?
```

If the user says no or approves, invoke `$hatch-pet` immediately.
