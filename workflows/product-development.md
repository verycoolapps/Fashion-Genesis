# PRODUCT DEVELOPMENT — SPEC → PROTOTYPE

## PURPOSE

Take an invention from concept (Master Format A–M) to a buildable prototype
path. Output: a spec sheet, a prototyping tier ladder, DFM checks, cost-driver
map, and a testing checklist. This workflow bridges design and manufacturing —
it produces documents, not physical objects.

## TRIGGERS

- "how do we make this", "spec sheet", "prototype", "build this", "can this be
  manufactured", "technical specs", "pattern", "sample"
- Follow-up after an invention when the user wants to realize it.

## STEP 1 — Assemble the input

Collect from the invention output:
- Section D (Visual Design) → silhouette, views, signature details
- Section E (Materials) → material candidates + rationale
- Section F (Functional Mechanism) → moving parts, transformations
- Section G (Technical Spec) → dimensions, components, targets
- Section I (Manufacturing Strategy) → any prior feasibility notes

If the invention lacks a technical spec, generate one FIRST (this workflow's
Step 2 does that).

## STEP 2 — Spec sheet template

Produce a structured spec document. Every numeric value is an ESTIMATE unless
measured — label them.

```
PRODUCT SPEC SHEET — [NAME] v0.1
Category · Target user · Innovation level · Originality score

1. DIMENSIONS (flat/garment) or LAST/SIZE GRADING (footwear)
   - Key measurements: [list 6–12 critical dims with target values + tolerance]
   - Sizing logic: [how it scales across body sizes]
   - Fit intent: [slim/regular/oversized + where ease lives]

2. CONSTRUCTION
   - Panel/cut list: [number of panels, seam types, seam placement map]
   - Closures: [type, location, operation force estimate]
   - Hardware: [type, material, finish, quantity, placement]
   - Stitching: [type, SPI estimate, thread spec]

3. MATERIALS
   - Shell/primary: [fiber, weight, construction, finish]
   - Lining/secondary: […]
   - Structural: [stays, reinforcements, bonding]
   - Trim: […]
   - For each: supplier category, MOQ estimate, lead time estimate, flagged risks

4. MECHANISMS / MOVING PARTS
   - [Each mechanism: type, actuation, range of motion, failure mode,
     repair path]

5. PERFORMANCE TARGETS
   - Durability: [abrasion cycles est., tear strength target]
   - Comfort: [weight target, breathability, pressure points]
   - Environmental: [water resistance level, UV, temperature range]
   - Safety: [skin-contact materials, sharp edges, fire behavior]

6. ELECTRONICS (if any)
   - Components, power source, connectivity, certifications needed

7. UNRESOLVED QUESTIONS
   - [What still needs research/prototype validation]
```

Rules:
- Never invent precise measurements and present them as real — label all as
  "target (estimate)".
- Every mechanism gets a failure mode. A mechanism without a failure mode
  isn't engineered yet.
- Flag every material whose supply chain or safety is unverified.

## STEP 3 — Prototype tier ladder

Map the path from cheapest proof to production-intent sample. Advise how far
to climb based on invention complexity.

| Tier | Name | Cost est. | Proves | Typical time |
|---|---|---|---|---|
| T0 | Sketch + drape mock | $0–50 | Silhouette, proportion | days |
| T1 | Cardboard/muslin/toile | $20–200 | Shape, fit, construction sequence | 1–2 wks |
| T2 | Proof-of-mechanism | $50–500 | Does the mechanism WORK | 1–3 wks |
| T3 | 3D-printed/fabricated parts | $100–2k | Mechanism durability, assembly | 2–6 wks |
| T4 | Functional sample (wearable) | $300–5k | Real materials, real use | 4–10 wks |
| T5 | Pre-production sample | $1k–20k | Production methods, QC | 6–16 wks |

Guidance:
- Garment with no mechanism: T0→T1→T4→T5.
- Mechanism-heavy (closures, actuators, transforms): T0→T2→T3→T4→T5 — never
  skip T2/T3; a mechanism that fails in cardboard fails everywhere.
- Footwear: T1 (last mock) is mandatory before anything else — last errors
  compound.
- Bags with hardware: T3 needed for hardware fit before T4.

Decision rule: climb ONE tier at a time; do not commission T4 until T3 (or
equivalent) validates the riskiest mechanism.

## STEP 4 — Design-for-Manufacturing (DFM) checks

Run this checklist against the spec. Each FAIL becomes a redesign note or a
flagged risk — never silently ship a known-unmanufacturable detail.

### Garments
- [ ] Seam types achievable on standard machines (no hand-work unless priced in)
- [ ] Panel count reasonable (≤12 for apparel; flag if more)
- [ ] No seam in high-stress location without reinforcement plan
- [ ] Closure operable with one hand if intended (test the force estimate)
- [ ] Hem/edge finishes achievable at target price point
- [ ] Print/embellishment compatible with material care requirements

### Footwear
- [ ] Last geometry moldable/lastable (no undercuts that trap the last)
- [ ] Sole attachment method chosen (cemented/welt/Goodyear/direct-inject)
      and compatible with materials
- [ ] Midsole geometry within foaming/molding limits (wall thickness ≥ spec)
- [ ] Upper pattern pieces nest efficiently (material yield estimate)
- [ ] Hardware (eyelets, buckles) standard or custom-molded — cost noted

### Bags / leather goods
- [ ] Panel shapes cuttable from standard hides/sheets (yield estimate)
- [ ] Edge paint/piping achievable at scale
- [ ] Hardware load ratings exceed expected use load (state the load)
- [ ] Lining attachment method chosen and durable
- [ ] Stitch density SPI appropriate for material (leather vs. coated fabric)

### Mechanisms (all categories)
- [ ] Moving parts count minimized — each adds cost + failure point
- [ ] Actuation method has off-the-shelf component path OR custom-fab plan
- [ ] Tolerance stack-up considered (can parts actually assemble?)
- [ ] Serviceability: can it be opened/repaired without destroying the product?

### Smart/tech elements
- [ ] Battery accessible or replaceable (not glued-in unless disposable-by-design)
- [ ] Electronics sealed appropriately for the product's environment claim
- [ ] Certifications identified (CE, FCC, UL, UN38.3 for batteries, etc.)
- [ ] Washability/care path defined if textile-integrated

## STEP 5 — Cost-driver identification

Do NOT fabricate exact costs. Identify WHAT drives cost and give order-of-magnitude
ranges with assumptions stated.

For each product, list:

```
COST DRIVERS
- Material cost driver: [which material, why it's expensive — e.g. "3D-knit
  upper: machine time + yarn cost; estimate $8–25/unit at 500+ MOQ"]
- Labor/complexity driver: [hand-finishing? multi-stage assembly? mechanism
  assembly? — estimate operations count]
- Tooling/NRE driver: [custom molds, dies, last, printed patterns — one-time
  cost range + amortization note]
- Hardware driver: [custom vs. catalog hardware — catalog = cheap, custom =
  $5k–50k+ tooling]
- Certification driver: [which certs apply, rough cost range, timeline]
- Yield/scrap driver: [complex cutting, alignment-critical assembly → scrap %]

UNIT COST HYPOTHESIS (ranges only):
- Prototype unit: $X–Y (tier T4/T5)
- Low-volume (100–500): $X–Y
- Scale (1k–10k): $X–Y
ASSUMPTIONS: [labor rate region, material prices at date, yield %, no exotic
custom tooling beyond stated]
```

Rules:
- Always give ranges, never point estimates, unless citing a real quote.
- State region assumptions (labor costs vary 5–10x by country).
- Flag the single biggest cost risk per product.

## STEP 6 — Testing checklist

Define what must be proven before the product is "real." Organize by domain.

### Durability
- [ ] Abrasion (Taber or equivalent for textiles; flex for soles)
- [ ] Tear/rupture strength at seams and stress points
- [ ] Closure cycle test (open/close × target count — e.g. 5,000 cycles)
- [ ] Mechanism fatigue test (transform cycles × target count)
- [ ] Colorfastness (rub, wash, light per intended care)
- [ ] Hardware corrosion/salt test if environmental claim exists

### Safety
- [ ] Skin-contact materials: irritation/sensitization review
- [ ] Sharp edges/points: post-assembly inspection standard
- [ ] Fire behavior: meet intended-use standard (flame retardant if required)
- [ ] Small parts choking hazard if child-usable
- [ ] Electrical/battery: UN38.3, transport, charge safety if applicable
- [ ] Chemical: AZO dyes, formaldehyde, PFAS per target market regs

### Fit & Function
- [ ] Fit test on size-run across body diversity (not just one fit model)
- [ ] Range-of-motion test: full activity set the user claimed
- [ ] Mechanism operation force within ergonomic limits (state N range)
- [ ] Thermal comfort: wear test in intended climate conditions
- [ ] Maintenance test: can the user actually clean/repair per care label?

### Environmental claim verification
- [ ] If "recyclable" claimed: disassembly test proves material separation
- [ ] If "bio-based" claimed: certification path identified
- [ ] If "modular/repairable" claimed: spare parts list + repair procedure written

## STEP 7 — Iteration protocol

Define how prototype findings flow back:

1. **Log every failure** with: tier, component, failure mode, suspected cause,
   proposed fix. A failure log is the most valuable document in prototyping.
2. **Classify fixes:**
   - Pattern-level (cardboard/muslin fixable) → fix at current tier, re-test
   - Construction-level (seam/hardware/finish) → note for T4
   - Mechanism-level → return to T2/T3 before proceeding
   - Spec-level (dimension/system wrong) → update spec sheet, restart affected tier
3. **Version everything:** spec v0.1 → v0.2 with change log. Never silently
   edit — the delta is the engineering record.
4. **Decision gates between tiers:** proceed only when current tier's "proves"
   column is satisfied. Document the gate decision.
5. **Escalation rule:** if the same failure survives two fix iterations at a
   tier, stop climbing — redesign the mechanism/approach instead of polishing
   a broken concept.

---

## OUTPUT CHECKLIST

- [ ] Spec sheet complete: dimensions, construction, materials, mechanisms,
      performance targets, unresolved questions
- [ ] All numeric values labeled estimate/target unless measured
- [ ] Every mechanism has a failure mode + repair path
- [ ] Prototype tier ladder mapped; starting tier justified by invention type
- [ ] DFM checklist run; every FAIL converted to redesign note or flagged risk
- [ ] Cost drivers identified with ranges + assumptions; no fabricated prices
- [ ] Single biggest cost risk flagged per product
- [ ] Testing checklist covers durability, safety, fit, environmental claims
- [ ] Iteration protocol defined (failure log, fix classification, versioning,
      gate decisions, escalation rule)
- [ ] Unresolved questions listed honestly — no fake certainty
- [ ] Offer next step: commercialization pass or deeper mechanism spec
