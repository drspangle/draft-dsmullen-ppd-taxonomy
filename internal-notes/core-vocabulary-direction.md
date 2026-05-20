# Core Vocabulary Direction

This note captures the current direction for the baseline PPD taxonomy core.
It is a working note, not settled draft text.

## Current Problems

The current taxonomy draft is too abstract in the wrong places:

- it presents many current terms as illustrative examples rather than a clear
  normative baseline vocabulary
- it does not yet show that the core vocabulary is complete enough for the
  real home-IoT privacy problem space
- it likely has dimensional overlap, especially between:
  - `action` and `constraints`
  - `destination` and trust-boundary qualifiers
  - generic and narrower terms where hierarchy or exact-match rules are not
    yet defined

## Working Rules

### 1. Do Not Overfit to the Demo

The current Habanero demo and the current protocol examples are useful
pressure tests, but they are not large enough to define the full shape of the
core vocabulary.

The baseline core must represent recurring home-IoT privacy dataflow concepts
more broadly than:

- the current DHT11 smart-bulb demo; or
- the current camera-oriented examples.

### 2. Do Not Build the Core from One External Source

No single external source is likely to fit PPD directly.

The PPD taxonomy should instead:

- define a compact PPD-native core vocabulary;
- draw conceptual input from multiple open sources; and
- define explicit extension and mapping expectations for non-core terms.

### 3. Use Open Sources as the Primary Semantic Basis

Primary semantic candidates:

- DPV for privacy purposes, processing, recipients, and many constraints
- SSN / SOSA for sensor-oriented data and source concepts
- SAREF for breadth across home-IoT device/capability families
- PROV-O for derivation/provenance distinctions
- WoT TD as a boundary check between capability description and privacy
  semantics
- ODRL for constraint and policy-shape sanity checks
- EDDY for privacy-rule semantics and flow reasoning

### 4. Use Public Ecosystem Material Only as a Breadth Check

Public ecosystem overviews can help identify missing smart-home categories, but
they should not be the normative basis for the core vocabulary if the
underlying standard is member-gated or otherwise not a clear open semantic
foundation for an IETF draft.

## Working Method

Before changing the draft text:

1. Build a dimension-by-dimension source matrix covering:
   - `data_type`
   - `purpose`
   - `action`
   - `source`
   - `destination`
   - `constraints`
2. For each dimension, classify candidate concepts as:
   - `Keep`
   - `Add`
   - `Question`
   - `Defer`
3. Only after that classification, write normative core term definitions.

## Likely Design Questions

- Which terms are fundamental enough for the interoperable core, and which
  should be extensions?
- Is the baseline matching model exact-match only, or does any broader/narrower
  relationship exist?
- Does `retention` belong only in constraints, or also in action semantics?
- Should trust-boundary concepts live primarily in `destination`, in a
  qualifier family, or in both with a tighter separation of concerns?
- What is the minimum extension/mapping contract that prevents semantic
  fragmentation while remaining feasible for constrained participants?

## Action and Qualifier Direction

The current working direction is that the PPD atomic dataflow should keep a
small action set at its core, with qualifiers handled separately.

### Action Direction

The current preferred baseline action family is:

- `collection`
- `use`
- `transfer`
- possibly `inference`

This is a better fit for privacy-relevant dataflow semantics than a broader
list that mixes dataflow acts with storage lifecycle or rule-management ideas.

### Qualifier Direction

The current preferred interpretation of the existing `constraints` object is
that it carries dataflow qualifiers rather than rule modality.

That means:

- qualifiers narrow or refine the meaning of a dataflow;
- rule effect such as `allow` or `deny` stays outside the dataflow, at the
  policy-rule level; and
- qualifiers must not become a catch-all bucket for every policy concern.

### Source Versus Provenance

The current preferred direction is:

- treat data origin primarily as a `source` problem inside the atomic dataflow;
- do not introduce a generic baseline `provenance` qualifier; and
- keep policy provenance separate from the taxonomy-bearing dataflow model.

### Jurisdiction / Residency Versus Sovereignty

The current preferred direction is:

- do not use a vague `sovereignty` qualifier bucket in the baseline;
- if this area is eventually needed, model it more concretely as
  jurisdictional or residency-style qualifiers; and
- defer that work unless it becomes necessary for a clear baseline use case.

### Qualifier Applicability

The current preferred direction is that qualifiers are action-sensitive rather
than universally valid across all actions.

That means:

- not every qualifier family applies coherently to every action;
- each qualifier family should declare the action contexts in which it is
  meaningful; and
- semantically inapplicable qualifier use should be treated as invalid in the
  baseline model rather than silently ignored.

Examples of the current reasoning:

- processing-location style qualifiers are most natural for `use` and possibly
  `inference`;
- `source` already carries origin semantics, so origin should not be modeled as
  a generic qualifier;
- `destination` already carries the receiving endpoint or trust boundary for
  `transfer`, so some location-style qualifiers may be redundant or incoherent
  there.

## Applicability Matrix Is Necessary but Not Sufficient

The current working direction is that a simple action-versus-qualifier
applicability matrix is a useful first-pass design tool, but it is not enough
to capture the full semantics.

In particular:

- `collection` can still interact meaningfully with `retention`, but only if
  the qualifier semantics make it clear whether the rule concerns ephemeral
  collection versus persistence of collected results after collection;
- `transfer` plus `retention` should be understood as a downstream retention
  condition on the receiving side rather than as a statement about the sender's
  local retention alone; and
- jurisdiction/residency can interact with both retention and processing
  location, so those concepts cannot be treated as fully independent matrix
  cells.

This means the design likely needs three layers:

1. an action-versus-qualifier applicability matrix;
2. per-qualifier semantics describing what the qualifier modifies for each
   applicable action; and
3. explicit notes on important qualifier interactions, especially where one
   qualifier changes the interpretation of another.

The current example to keep in view is downstream sharing:

- a transfer rule may constrain the first recipient's retention or
  jurisdictional placement;
- that does not necessarily mean the household policy fully enumerates all
  later fourth-party or fifth-party disclosures; and
- the baseline model should be careful not to imply richer downstream
  enumeration than the rule actually carries.

## Retention Direction

The current preferred direction is to avoid a fuzzy ladder of qualitative
retention classes.

Instead, the baseline retention model should likely use:

- `ephemeral` as a strong qualitative class meaning no durable persistence
  beyond the immediate handling context; and
- `indefinite` as a strong qualitative class meaning no bounded upper retention
  limit is expressed in the rule.

Everything between those poles should generally be expressed quantitatively
rather than by vague named classes such as `short-lived` or `persistent`.

That means the likely baseline retention shape is:

- a retention class value when the semantics are truly categorical; and/or
- explicit quantitative duration fields with units and measures when the
  retention bound is specific.

The current working rule is:

- if a bounded retention period matters, it should usually be stated
  explicitly;
- `ephemeral` should remain a special semantic class because it is stronger
  than merely "very short"; and
- `indefinite` should mean that no bounded upper limit is expressed, not merely
  "long-lived".

## Processing Boundary Direction

The current preferred direction is to replace the vague `locality` framing with
a narrower qualifier family centered on where processing is allowed to execute.

The current preferred family name is:

- `processing_boundary`

The current intended semantics are:

- this qualifier family constrains where `use` or `inference` may occur;
- it may be relevant to some collection-side processing cases, but it is not a
  generic destination or recipient model; and
- it should not do the main semantic work for `transfer`, because `destination`
  already carries the receiving endpoint or handling target.

Current candidate baseline values:

- `on-device-only`
- `in-home-only`
- `approved-remote-processing`

The current direction is that terms such as `thirdPartyProhibited` or
`householdApprovedRemoteService` are poor fits for this family because they are
recipient/trust-domain oriented rather than true processing-placement terms.

## Jurisdiction Direction

The current preferred direction is to keep `jurisdiction` as a qualifier family
name only if the relevant subcase is explicitly specified.

That means the baseline should avoid an underspecified flat form like:

- `jurisdiction = X`

and instead require the qualifier to say what aspect it governs, such as:

- processing
- storage
- transfer

This treats `sovereignty` as the broader motivating policy concern while
keeping the actual baseline qualifier more precise and machine-comparable.

## Comparison Direction

The current preferred direction is that comparison should be based on
subsumption rather than exact token equality alone.

That means:

- role-fillers and relevant qualifier values may stand in broader/narrower
  semantic relationships;
- equivalence should be understood as two-way subsumption; and
- comparison should be dimension-sensitive rather than treated as one generic
  string-matching problem.

This direction is important because:

- household policy may be stated at one level of abstraction while participant
  declarations are stated at another;
- exact-match only comparison is too weak for a serious privacy dataflow model;
  and
- the baseline PPD model needs a bounded semantic relationship model rather
  than open-ended ontology reasoning.

### Current Subsumption Participation Direction

The current preferred direction is:

- `data_type`: participates in subsumption
- `purpose`: participates in subsumption
- `source`: participates in subsumption
- `destination`: participates in subsumption
- `action`: does not participate in subsumption and should remain a flat
  enumerable action family
- `retention`: does not participate in subsumption in the same way as the core
  role-fillers; it is a specifier family whose comparison depends on its own
  categorical or quantitative semantics
- `processing_boundary`: participates in subsumption
- `jurisdiction`: participates in subsumption, but only within an explicitly
  scoped subcase such as processing, storage, or transfer

### Why Subsumption Matters

The key role of subsumption is not only comparison between already standardized
core terms.

It is also the mechanism that keeps extension terms interoperable.

If a deployment, vendor, or ecosystem introduces a non-core extension term for
one of the roles that participates in subsumption, that extension should be
required to declare its semantic relationship to the relevant core concept or
concepts.

In other words:

- extension is not just new naming;
- extension requires explicit placement relative to the core semantic model; and
- otherwise the extension term cannot be compared reliably against household
  policy or participant declarations built on the shared core.

This is one of the main reasons the taxonomy needs an explicit extension and
mapping contract rather than only a namespace mechanism.

## Near-Term Goal

The immediate goal is not to perfect the taxonomy. The goal is to make the
next draft revision defensible by showing:

- a clear theory for the baseline dimensions;
- a credible path to a complete core vocabulary; and
- a disciplined extension story that does not collapse interoperability.
