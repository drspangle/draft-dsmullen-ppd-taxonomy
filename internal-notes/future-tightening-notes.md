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
- determine whether the current `localProcessing` term is the right floor
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

For example, a destination like "Google" could plausibly map to multiple
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
