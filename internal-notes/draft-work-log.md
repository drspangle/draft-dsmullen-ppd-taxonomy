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
