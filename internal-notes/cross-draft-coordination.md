# Cross-Draft Coordination

This note records the current coordination findings across the taxonomy,
protocol, and architecture drafts.

## Current Direction

The current working direction is that the foundational semantic unit for PPD
is an atomic privacy-relevant dataflow.

The role-fillers currently in view are:

- `data_type`
- `purpose`
- `action`
- `source`
- `destination`
- optional dataflow qualifiers

The current direction is also that:

- declarations carry descriptive atomic dataflow statements;
- effective policy carries normative atomic dataflow rules;
- conflict and compatibility analysis are grounded in comparison of those
  dataflows; and
- some role-fillers may need broader/narrower relationships so comparison can
  work across different abstraction levels.

## Coordination Findings

### Architecture Draft

The architecture draft is not currently in direct conflict with this
direction.

It is already high-level enough to accommodate:

- governance of privacy-relevant data flows rather than hidden internal
  behavior;
- separate descriptive participant declarations and normative household policy;
- diagnostic-only comparison outcomes at the participant-facing boundary.

Likely future architecture edits are mostly wording alignment:

- describe the taxonomy as defining the semantic dimensions of atomic
  privacy-relevant dataflows, not just a vocabulary list;
- keep conflict-resolution procedure out of scope while still making the basis
  for comparison clearer; and
- align any future terminology changes if the protocol/taxonomy layer keeps the
  wire object name `constraints` while conceptually treating it as qualifiers.

### Protocol Draft

The protocol draft is where coordinated changes are most likely to be needed.

The current protocol draft already assumes:

- atomic declaration statements and atomic policy rules;
- a shared object currently named `constraints` for structured qualifiers;
- initial standardized qualifier members `retention` and `locality`.

That means taxonomy changes can ripple directly into:

- declaration and rule object prose;
- the `Constraints Object` definition;
- taxonomy-bearing JSON examples; and
- protocol internal direction notes that currently treat `retention` and
  `locality` as the preferred initial baseline qualifiers.

## Current Collision Points

The main currently known protocol/taxonomy collision points are:

1. whether the wire object should remain named `constraints` even if the
   underlying concept is now treated as dataflow qualifiers;
2. the current `locality` concept, which likely needs reframing or renaming;
3. the current example terms such as `ppd:shortLived`, which may become stale
   if retention moves to stronger named poles plus explicit quantitative
   refinement; and
4. the need to make comparison more clearly grounded in atomic dataflow
   statements and rules rather than only in coarse high-level comparison
   outcomes.

## Sequencing Recommendation

The current recommended coordination order is:

1. settle the taxonomy-side semantic model in notes first:
   - atomic dataflow structure
   - action set
   - qualifier families
   - retention semantics
   - replacement or refinement of the current `locality` idea
2. update protocol internal direction notes to match;
3. update protocol draft prose and examples;
4. perform a lighter wording-alignment pass in the architecture draft.

This sequencing reduces the risk that the three drafts drift while the
taxonomy model is still moving.
