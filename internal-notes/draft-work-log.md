# Taxonomy Draft Work Log

This file records drafting work for `draft-dsmullen-ppd-taxonomy.md`.
It is not part of the rendered Internet-Draft.

## 2026-05-19

- Added `internal-notes/README.md` so this repository now has the same basic
  note-taking structure as the architecture and protocol draft repos.
- Added `internal-notes/source-material.md` to track the most relevant local
  PPD materials that should shape the taxonomy, including protocol examples and
  current Habanero demo capability notes.
- Added `internal-notes/external-taxonomy-sources.md` to track open external
  standards and research sources that may inform the PPD taxonomy model.
- Added `internal-notes/core-vocabulary-direction.md` to capture the current
  direction that the taxonomy core vocabulary should not be derived narrowly
  from the current demo or from a few contrived examples.
- Recorded the current critique that the draft's biggest weakness is not
  editorial quality but semantic thinness: the draft names dimensions and
  example terms, but does not yet define a complete normative core vocabulary.
- Recorded the current critique that the dimension model likely has overlap,
  especially between `action` and `constraints`, and between `destination` and
  trust-boundary style qualifiers.
- Recorded the working rule that proprietary or member-gated ecosystem
  specifications must not be treated as the normative basis for the PPD
  taxonomy, even when public ecosystem overviews are used as breadth checks.
- Recorded EDDY as a serious candidate source of insight for privacy
  dataflow-rule semantics, especially around actors, information types,
  purposes, operations, and flow reasoning.
- Recorded the current direction that the atomic PPD dataflow is the core
  semantic unit, with `data_type`, `purpose`, `action`, `source`,
  `destination`, and optional qualifiers as the main structure.
- Recorded the current direction that the preferred baseline action set should
  be centered on `collection`, `use`, `transfer`, and possibly `inference`.
- Recorded the current direction that the existing `constraints` concept should
  be treated as dataflow qualifiers rather than rule modality.
- Recorded the current direction that data origin should be treated primarily
  as a `source` problem, while generic `provenance` should not be a baseline
  qualifier.
- Recorded the current direction that vague `sovereignty` terminology should be
  avoided in favor of more concrete future jurisdiction/residency qualifiers if
  those become necessary.
- Recorded the current direction that qualifier families are action-sensitive:
  they should declare which actions they meaningfully modify, and semantically
  inapplicable qualifier use should be invalid rather than silently ignored.
- Recorded the current direction that an action-versus-qualifier applicability
  matrix is necessary but not sufficient: qualifier semantics and qualifier
  interactions also need to be modeled explicitly.
- Recorded the specific direction that `transfer` plus `retention` should be
  interpreted as a downstream retention condition on the receiving side, while
  avoiding any implication that a baseline rule fully enumerates all later
  fourth-party or fifth-party sharing.
- Recorded the current direction that the retention qualifier should probably
  avoid fuzzy qualitative ladders and instead center on two strong named
  classes, `ephemeral` and `indefinite`, with intermediate bounded cases
  expressed quantitatively.
- Added `internal-notes/cross-draft-coordination.md` to record the current
  architecture/protocol/taxonomy coordination findings and the recommended
  sequencing for future draft edits.
- Recorded the current direction that the second qualifier family should be
  reframed away from vague `locality` language and toward a narrower
  `processing_boundary` concept focused on where `use` and `inference` may
  execute.
- Recorded the current direction that `jurisdiction` can work as a qualifier
  family only if the relevant subcase, such as processing, storage, or
  transfer, is explicitly specified rather than left implicit.
- Recorded the current direction that comparison should be grounded in
  subsumption rather than exact token equality, with equivalence understood as
  two-way subsumption.
- Recorded the current direction that `action` should remain a flat enumerable
  family rather than a subsumption hierarchy.
- Recorded the current direction that `retention` is a specifier family rather
  than a normal subsumption hierarchy, while `processing_boundary` and
  `jurisdiction` should participate in subsumption.
- Recorded the current direction that extension terms filling roles that
  participate in subsumption must declare their semantic relationship to the
  relevant core concepts or they cannot be compared reliably.

## 2026-05-20

- Tightened the rendered taxonomy draft so `data_type` now follows a single
  classification axis and no longer mixes derivation history into the
  `data_type` family.
- Tightened the rendered taxonomy draft so `jurisdiction` is no longer
  overstated as a fully populated baseline value hierarchy; in this revision it
  is a structured qualifier family shell with scoped semantics awaiting later
  vocabulary/profile work.
- Tightened the rendered taxonomy draft so `destination` and
  `processing_boundary` are distinguished explicitly rather than being left to
  implication.
- Tightened the rendered taxonomy draft so genuinely multi-purpose handling is
  described as separate atomic dataflows, both for machine comparison and for
  better human transparency.
- Added `internal-notes/future-tightening-notes.md` to capture the next
  non-blocking areas of work:
  - refining baseline destination terms;
  - improving conformance/validation to reduce taxonomy abuse or deliberate
    misclassification; and
  - working out how named entities such as specific companies should relate to
    semantic destination categories without collapsing those concerns into one
    taxonomy term.
- Tightened the rendered taxonomy draft so `purpose`, `source`, and
  `destination` each carry clearer classification rules, explicit invalidity
  boundaries, and small concrete examples that make the floor model easier to
  follow.
- Added a short reader-orientation map and a compact running dataflow example
  near the front of the draft so first-time readers can understand the model
  before they hit the denser semantic-validity and extension sections.
- Compressed the richer-semantic-framework discussion so it states the
  participant-facing boundary without spending much space on ontology or graph
  background that is not necessary to read the draft.
- Current near-term status: the taxonomy draft looks close to a defensible
  next Datatracker revision, but before submitting again it should get one
  more human read focused on compression, repeated phrasing, and whether `Use
  in PPD Messages` still carries more explanation than it needs.

## 2026-05-22

- Replaced `destination` with `handling_context` across the taxonomy draft and
  tightened the term so it works coherently for `collection`, `use`,
  `inference`, and `transfer`.
- Defined the baseline `jurisdiction` qualifier as a declarative structured
  family with `scope`, `countrycode`, and `subdivisioncode`, using the RFC
  code formats already referenced by the draft.
- Tightened the opening `Core Semantic Model` section so the taxonomy no
  longer appears to define protocol object names, and the opening field
  definitions now stand on their own.
- Added clearer signaling-vs-enforcement boundary text: household policy rules
  express preferences for signaling and comparison, while enforcement depends
  on deployment-specific control points, trust models, and participant
  capabilities and remains out of scope for the baseline draft.
- Strengthened the extension/core-floor discussion so the draft explicitly
  tolerates local semantic variability, including vendor ambiguity, while
  requiring participant-facing terms to collapse back to a declared,
  computable shared core.
- Continued editorial cleanup in the rendered taxonomy draft:
  - smoothed the `Core Semantic Model` opening so it no longer appears to
    define protocol object names directly;
  - clarified that `handling_context` is defined by the taxonomy and carried by
    protocol objects rather than inferred from examples;
  - clarified that household-side rules express preferences for signaling and
    comparison, not baseline enforcement semantics; and
  - clarified that the shared core is intended to absorb both honest semantic
    variation and broader or intentionally ambiguous vendor vocabulary without
    forcing the household to normalize those terms manually.
- Current near-term status: the full taxonomy review pass is complete.
  Deferred local cleanup notes remain for Section `6.7.3 Processing
  Boundary`, especially its opening wording and the clarity of its closing
  example, but no broader taxonomy reread is pending before the next targeted
  edit pass.
