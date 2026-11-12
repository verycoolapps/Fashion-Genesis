# VISUAL ENGINE — IMAGE GENERATION WORKFLOW

## PURPOSE

Produce fashion-product visuals for inventions. Two delivery modes:

- **Native mode:** runtime has image generation → generate the images.
- **Prompt-only mode:** no image tool → deliver production-grade prompts the user
  can run anywhere, plus the spec text they describe.

Either way, the SAME prompt architecture applies. The deliverable is always
section J of the Master Output Format.

## TRIGGERS

- "show me", "generate images", "visualize", "product shots", "lookbook",
  "campaign images", "render this"
- Or automatically as part of a full invention/collection output when the user
  wants visuals.

## THE 10 REQUIRED VIEWS

Every serious product visual set contains these 10 views. Generate or write
prompts for ALL 10 unless the user scoped fewer.

| # | View | Purpose | Camera logic |
|---|---|---|---|
| 1 | Hero | The money shot — product alone, perfect light | 3/4 angle, softbox, neutral ground |
| 2 | Front | Construction clarity | Orthographic-ish, even light |
| 3 | Back | Rear construction, closures, seams | Same lighting as front |
| 4 | Side | Profile, depth, sole/volume | 90° profile |
| 5 | Detail | Macro of signature mechanism/material | Close-up, shallow DOF |
| 6 | Functional demo | Mechanism in use (transforming, opening) | Mid-action, hands optional |
| 7 | On-body | Scale, drape, fit on human | Real model, neutral styling |
| 8 | Material study | Texture close-ups, material layers | Macro, raking light |
| 9 | Exploded | Components separated, construction map | Technical illustration style |
| 10 | Editorial | Campaign-grade, narrative, styled | Environmental, art-directed |

For collections: hero product gets 10 views; supporting products get views
1, 2, 5, 6, 7 minimum (hero shot, front, detail, function, on-body).

---

## PROMPT TEMPLATE STRUCTURE

Every prompt follows this skeleton. Fill every slot; never leave a slot generic.

```
[VIEW TYPE] of [PRODUCT NAME], a [CATEGORY] designed as [ONE-LINE CONCEPT].

SUBJECT: [silhouette description — geometry, proportions, volume, how it sits]
MATERIALS: [primary material + texture + finish; secondary materials;
            hardware description — metal type, finish, shape]
CONSTRUCTION: [visible seams, closures, mechanisms, signature details —
               be specific: "exposed magnetic clasp rail along left edge",
               not "futuristic details"]
COLOR: [exact palette — name colors, don't say "colorful"]
LIGHTING: [softbox/studio/natural/flash — direction and quality]
CAMERA: [lens feel 35mm/85mm/macro, angle, depth of field]
ENVIRONMENT: [seamless studio / concrete floor / editorial location]
STYLE ANCHORS: [reference aesthetic — e.g. "Aesop product photography",
                "technical illustration", "editorial campaign for high-fashion
                house"] — anchors guide style WITHOUT copying a specific product
```

### Slot rules

- **Subject:** describe geometry, not adjectives. "Column silhouette with a
  single curved shoulder fold" beats "beautiful avant-garde design."
- **Materials:** always name fiber/metal/substrate + finish (matte, brushed,
  rippled, transparent). "Recycled ocean-plastic weave, matte, 12oz" is usable;
  "innovative sustainable material" is not.
- **Construction:** this is where originality lives. Name the mechanism,
  seam placement, hardware type. If the invention has a moving part, describe
  its state in THIS view.
- **Color:** hex or precise color names. Lock the palette across all 10 views.
- **Style anchors:** use MOVEMENT or PHOTOGRAPHER-level anchors
  ("Pentagram technical aesthetic", "Helmut Newton editorial contrast"),
  not brand-product anchors ("like an Hermès Birkin" — that's copying).

---

## CROSS-VIEW CONSISTENCY RULES (non-negotiable)

All 10 views of one product MUST describe the SAME object. Before writing each
prompt, extract the locked block and paste it verbatim:

```
LOCKED: silhouette [X] · materials [Y] · colors [Z] · mechanism state [W]
VARIABLE: camera angle, framing, lighting mood, environment, which details
          are in focus
```

Rules:
- Silhouette description identical across views (except exploded view, which
  separates components but keeps shapes).
- Materials and colors verbatim identical — copy-paste, never paraphrase.
- Mechanism described in its DEFAULT state for static views; only view 6
  (functional demo) shows it mid-transformation.
- On-body view: same product, but drape/drape-fold differences are expected —
  note "worn, fabric follows gravity" explicitly so the generator doesn't
  invent a different garment.
- If generating images sequentially: generate hero FIRST, then reference it
  ("same product as previous image") if the tool supports image input;
  otherwise rely on the locked block.

Consistency test: read views 2 and 3 side by side — if you can't tell they're
the same product, the prompts failed.

---

## ANTI-SLOP VISUAL RULES

Reject or rewrite any prompt containing:

- **Random glow** — neon edges, energy halos, "powered" light effects unless
  the product genuinely emits light (then specify real source: LED type,
  placement, purpose).
- **Decorative chaos** — particles, smoke, lens flare stacks, floating debris
  with no product reason.
- **Invisible construction** — "sleek minimalist" prompts that hide seams,
  closures, mechanisms. Fashion products must show HOW they're made; the detail
  and exploded views exist to prove it.
- **Impossible physics** — fabric frozen mid-air with no support, liquids
  defying gravity, structures that couldn't stand.
- **Generic luxury signals** — gold everything, marble surfaces, "opulent"
  lighting without product justification.
- **Scale ambiguity** — no human or reference object in on-body/context shots.
- **Brand-copy drift** — style anchors that drift toward a specific existing
  product's signature look.

Positive requirements instead:
- Real construction visible: seam lines, stitch texture, hardware shadows.
- Material honesty: show how the material BEHAVES (drape, reflect, compress).
- Purposeful light: motivated by the scene, not decorating the product.
- Negative space used deliberately, not as filler.

---

## NATIVE IMAGE GENERATION MODE

When the runtime has an image tool:

1. **Generate in dependency order:** hero shot first (it locks the visual
   identity), then front/back/side, then detail, then functional demo,
   on-body, material study, exploded, editorial last (most art-directed,
   benefits from established look).
2. **Use reference chaining** when supported: pass the hero image as input
   reference for subsequent views with prompt "same product, different angle."
3. **Batch per view, not per product** if the tool limits calls — never
   truncate the 10-view set without telling the user which views were dropped.
4. **Verify each output:** check silhouette matches the locked description,
   materials look right, no slop artifacts (random glow, melted hardware,
   extra limbs in on-body). Regenerate failures with a corrected prompt —
   name what was wrong in the retry prompt.
5. **Deliver with captions:** each image labeled with its view number and a
   one-line description of what it shows.

## PROMPT-ONLY MODE

When no image tool exists:

1. Deliver all 10 prompts in a copy-paste block, each labeled with view number
   and intended use.
2. Include the LOCKED block once at the top so the user understands the
   consistency system.
3. Add a "generation order" note (hero first, editorial last).
4. Add tool-specific tips: which prompt length works best ( Midjourney favors
   comma-weighted short prompts; DALL-E/Flux handle longer natural language;
   for consistency across views, tools with image-reference input are
   strongly recommended — generate hero first).
5. Never pretend images were generated. State clearly: "Prompts ready for
   [tool]; run hero first, then use it as reference."

---

## COLLECTION VISUALS

For collections, add a **campaign board** deliverable:
- 3–5 editorial images showing products styled together (from the styling
  formulas in collection-creation.md Step 8).
- Consistency rule extends across products: same lighting logic, same color
  treatment, same environment family — the board must look like ONE campaign.

---

## OUTPUT CHECKLIST

- [ ] All 10 views covered (or scoped-down set explicitly justified)
- [ ] Every prompt fills all template slots (subject/materials/construction/
      color/lighting/camera/environment/style anchors)
- [ ] LOCKED block defined once; silhouette/materials/colors identical across
      views
- [ ] Construction details specific and visible (no "futuristic" hand-waving)
- [ ] Anti-slop rules checked per prompt (no glow/chaos/impossible physics)
- [ ] On-body view includes scale reference and gravity note
- [ ] Native mode: hero generated first; failures regenerated with named fixes
- [ ] Prompt-only mode: prompts labeled, generation order stated, no false
      claim of generated images
- [ ] Collection visuals: campaign board included when applicable
- [ ] Each delivered image/prompt captioned with view number + content line
