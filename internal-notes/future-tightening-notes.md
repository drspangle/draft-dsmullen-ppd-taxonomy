# Future Tightening Notes

This note captures follow-up work that should happen after the current
taxonomy revision is submitted. These items are important, but they are not
blocking this revision.

## 1. Destination Term Refinement

The current `destination` floor is serviceable, but it is not yet the final
cut.

Follow-up work should:

- refine the baseline destination categories so recipient role, handling
  context, and trust/domain distinctions are as clear as the rest of the
  taxonomy;
- continue pressure-testing the split between `destination` and
  `processing_boundary`; and
- determine whether the current `householdContext` term is the right floor
  category or whether it still hides too much structure.

The main risk is that destination terms remain broad enough to be useful but
not precise enough to prevent inconsistent refinement.

## 2. Preventing Taxonomy Abuse or Misclassification

The draft now defines stronger refinement discipline, but more work is still
needed to reduce the risk that a human author, vendor, or policy tool
introduces terms that fit the wrong semantic family or break the intended
structure.

Follow-up work should explore:

- stronger authoring and conformance guidance for refinement definitions;
- machine-checkable validation rules for field-family assignment;
- examples of invalid refinements and invalid field placement;
- stricter rules or profiles for who can publish participant-facing
  refinements; and
- whether a later registry, profile model, or conformance document is needed
  to reduce intentional or accidental semantic drift.

The core issue is not only ambiguity. It is also preventing actors from
deliberately introducing semantically misleading terms while still claiming
baseline interoperability.

## 3. Named Entities Versus Semantic Categories

Named entities such as a specific company, service brand, or product family
do not fit cleanly into the same layer as the semantic destination categories
defined by the taxonomy.

For example, a destination like "ExampleServices" could plausibly map to multiple
semantic destination categories depending on which service, role, or handling
context is actually involved.

Follow-up work should determine:

- whether named entities belong outside the taxonomy entirely as a separate
  identifier layer;
- whether named entities can appear only as non-core refinements with explicit
  semantic reduction to a destination category;
- how the model should represent one organization that spans multiple semantic
  roles; and
- whether policy rules should classify the semantic role and name the entity
  separately rather than trying to collapse both into one term.

The current direction should remain conservative: semantic taxonomy terms
classify what kind of destination or handling context is involved, while
entity identity is likely a distinct concern.

## 4. Section 6.7.3 Wording Cleanup

The current `Processing Boundary` subsection still has two prose issues worth
revisiting in a later editorial pass:

- the opening sentence still uses the slightly awkward inline "classification
  rule" style that has been getting smoothed out elsewhere in the draft; and
- the example near the end of the subsection is harder to parse than it should
  be and does not explain its reasoning or implication clearly enough.

Follow-up work should tighten that subsection without changing the underlying
model:

- restate the opening rule in plain prose rather than as a visibly separate
  stylistic formula;
- simplify the example sentence structure; and
- make the consequence of the example clearer, especially how
  `processing_boundary` narrows `handling_context` without replacing it.

## 5. Taxonomy Authoring and Validation Tooling

The current taxonomy draft is now explicit enough that a substantial part of
taxonomy correctness could likely be validated computationally, especially for
non-core extensions meant to remain baseline-interoperable.

Follow-up work should explore a tooling path for authoring and validation of
taxonomy extensions, such as a linter or schema-backed authoring workflow that
can check:

- field-family assignment and whether a term is being introduced in the right
  semantic family;
- whether a family that supports subsumption declares exactly one immediate
  broader term;
- whether broader-than chains terminate at the required core floor;
- whether a non-core term attempts to collapse multiple semantic axes into one
  refinement;
- whether a term improperly encodes policy modality;
- whether qualifier families are used only in semantically valid scoped
  contexts; and
- whether required reduction metadata is present for participant-facing
  interoperability.

This could make the draft's semantic discipline more practical in real authoring
work, especially when vendors or ecosystems publish richer local vocabularies
that still need to compare cleanly against household policy.

## 6. Provenance and Lineage-Sensitive Policy

The current `source` model is intentionally limited to immediate origin in the
current handling step. It does not attempt to encode full provenance or
multi-step lineage.

This keeps the baseline participant-facing model compact and computable, but
it leaves open later work for policies that care about deeper derivation
history or inherited sensitivity.

Follow-up work should determine:

- whether a later taxonomy revision needs an explicit provenance or lineage
  concept distinct from `source`;
- whether lineage-sensitive policies are common enough in home-IoT practice to
  justify that added complexity;
- how such a concept would interact with `data_type`, `source`, and
  `inference`; and
- whether deeper provenance should remain out of the baseline participant-
  facing model and only appear in richer profiles or auxiliary metadata.
