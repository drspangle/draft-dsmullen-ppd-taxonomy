---
title: "Privacy Preference Declaration Taxonomy"
abbrev: "PPDTaxonomy"
category: info

docname: draft-dsmullen-ppd-taxonomy-latest
number:
date:
consensus: false
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - privacy preferences
 - home networks
 - internet of things
 - data taxonomy
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "drspangle/draft-dsmullen-ppd-taxonomy"
  latest: "https://drspangle.github.io/draft-dsmullen-ppd-taxonomy/draft-dsmullen-ppd-taxonomy.html"

author:
 -
    fullname: "Daniel Smullen"
    organization: CableLabs
    email: "d.smullen@cablelabs.com"

 -
    fullname: "Brian Scriber"
    organization: CableLabs
    email: "brian.scriber@computer.org"

normative:

informative:


--- abstract

This document defines the core vocabulary, comparison model, and extension
discipline used by Privacy Preference Declarations (PPDs) to express atomic
privacy-relevant dataflows in home networks. It complements the companion PPD
architecture and protocol work by standardizing the semantic roles used in
participant declarations and household policy rules. The core vocabulary is
the mandatory shared semantic floor for baseline participant-facing
interoperability. Richer ecosystem-specific vocabularies remain possible, but
comparison-relevant non-core terms need explicit relationships to the shared
core so they remain computable. Baseline participant-facing protocol messages
use compact identifiers plus taxonomy context rather than requiring full
ontology exchange on the wire.


--- middle

# Introduction

The Privacy Preference Declaration (PPD) architecture depends on a shared
understanding of privacy-related semantics.
{{?I-D.draft-dsmullen-ppd-architecture}} defines the roles, trust boundaries,
and lifecycle. {{?I-D.draft-dsmullen-ppd-protocol}} defines the
participant-facing message flow and object structure. This document defines the
semantic roles and qualifier families used by those messages.

The baseline PPD protocol carries atomic descriptive statements from
device-side participants and atomic effective-policy rules from the household
side. This taxonomy treats those statements and rules as atomic
privacy-relevant dataflows. It defines the meaning of the role-fillers used in
those dataflows and the minimum semantic discipline needed to compare them
coherently across devices, vendors, and household deployments.

The taxonomy is designed to be useful in constrained operational environments.
It therefore separates the stable meaning of core terms from any richer
external semantic framework that might also describe them. Implementations MAY
use richer vocabularies, ontology representations, or local policy-analysis
artifacts where useful, but baseline participant-facing interoperability
depends on a shared computable semantic floor rather than on a full external
reasoning stack.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Core Semantic Model

The foundational semantic unit in this taxonomy is an atomic privacy-relevant
dataflow.

In the baseline PPD model:

* a Device Declaration Statement describes one participant-side dataflow case;
* a Policy Rule describes one household-side normative dataflow case; and
* comparison between participant behavior and household policy is grounded in
  comparison of those dataflows.

A baseline atomic dataflow contains these five core role-fillers:

* `data_type`
* `purpose`
* `action`
* `source`
* `destination`

It can also carry structured dataflow qualifiers.

The rule effect, such as `allow` or `deny`, is not part of the dataflow tuple
itself. It belongs to the household-side policy-rule layer defined by
{{?I-D.draft-dsmullen-ppd-protocol}}.

This document does not define a household policy authoring workflow, a full
conflict-resolution procedure, or a general reasoning engine. It defines the
minimum semantic structure needed so participant declarations and household
policy can be compared in an interoperable way.

# Design Goals

* Semantic Clarity: Provide stable, unambiguous meanings for privacy-related
  terms used in PPD messages.
* Core Primitive Coverage: Standardize the semantic roles needed by the
  baseline protocol rule and statement model.
* Compact Operational Use: Support compact identifiers in participant-facing
  JSON messages.
* Extensibility Without Fragmentation: Allow organization-specific
  vocabularies while requiring comparison-relevant extensions to remain
  reducible to the shared core.
* Validation and Comparison Support: Enable comparison of participant
  assertions and household policy without forcing every deployment to use a
  single heavy semantic framework.
* Interoperability: Preserve a shared computable semantic floor across
  vendors, device classes, and household deployments.

# Core Semantic Floor and Extension Model

The baseline PPD core vocabulary is not intended to be the only vocabulary
used in real deployments. Device vendors, service providers, vertical
ecosystems, and user-facing policy tools are expected to introduce richer
concepts over time.

The purpose of the core vocabulary is different. It provides the minimum
shared semantic substrate against which participant declarations and household
policy can still be interpreted and compared when those richer vocabularies
are present.

For baseline participant-facing interoperability:

* core terms define the shared semantic floor;
* richer non-core terms MAY be used through the taxonomy context mechanism
  defined by {{?I-D.draft-dsmullen-ppd-protocol}}; and
* when a non-core term or qualifier fills a comparison-relevant role, it MUST
  be defined with an explicit relationship or reduction to one or more core
  concepts sufficient to keep the term computable against the shared core
  model.

Terms that do not carry such a relationship can still be locally meaningful,
but they are outside baseline interoperable computation.

# Core Taxonomy Structure

The baseline taxonomy consists of five core role-filler families plus selected
dataflow qualifier families. These are used together in atomic declaration
statements and atomic effective-policy rules.

The baseline core is intentionally small. It is not meant to exhaust the full
space of home-IoT data categories, service roles, or policy-authoring
concepts. Its purpose is to define the minimum shared set of computable
primitives to which richer vocabularies can be related.
Later taxonomy releases can add terms, but the initial core terms defined here
are the mandatory baseline floor for interoperable computation.

## Data Type (What)

Data Type terms identify the kind of data involved in the dataflow.
Data Type participates in semantic comparison and can support
broader-than/narrower-than relationships.

The initial core term set is:

* `ppd:temperatureReading`: a measured temperature value associated with the
  participant device, its immediate environment, or an observed space.
* `ppd:humidityReading`: a measured humidity value associated with the
  participant device, its immediate environment, or an observed space.
* `ppd:videoFrame`: image or video-capture content obtained from a camera-like
  sensing path.
* `ppd:eventClip`: a bounded media segment retained or emitted because a
  triggering event or condition occurred.
* `ppd:audioSample`: audio-capture content obtained from a microphone-like
  sensing path.
* `ppd:deviceIdentifier`: an identifier associated with a device, participant,
  or device instance.

## Purpose (Why)

Purpose terms identify the reason or operational objective for the handling.
Purpose participates in semantic comparison and can support broader-than/
narrower-than relationships.

The initial core term set is:

* `ppd:coreFunctionality`: handling directly necessary to deliver the primary
  user-facing function of the device or service.
* `ppd:remoteMonitoring`: handling used to expose current or recent device or
  environment state to an authorized remote observer.
* `ppd:motionDetection`: handling used to detect, classify, or respond to
  motion or occupancy-related events.
* `ppd:remoteViewing`: handling used to present captured media or live capture
  output to an authorized remote viewer.
* `ppd:productImprovement`: handling used to improve the quality, reliability,
  or performance of the product or service beyond the immediate user session.
* `ppd:analytics`: handling used to derive operational, behavioral, or
  statistical insight beyond immediate device operation.
* `ppd:advertising`: handling used to target, deliver, measure, or optimize
  promotional or marketing activity.
* `ppd:diagnostics`: handling used to troubleshoot, maintain, secure, or
  repair the device or service.

## Action (How)

Action terms identify the privacy-relevant operation being performed.
Unlike several of the other role-fillers, the baseline action family is
intentionally flat rather than hierarchical.

The initial core term set is:

* `ppd:collection`: acquiring, observing, or accepting data into the handling
  context of the participant or service.
* `ppd:use`: operating on data within the current handling context without
  disclosing it to a different recipient.
* `ppd:transfer`: disclosing, transmitting, or otherwise making data available
  to a different recipient or handling context.
* `ppd:inference`: deriving new data, classifications, or conclusions from
  existing data.

## Source (From Where)

Source terms identify the origin of the handled data in the relevant
processing path. Source participates in semantic comparison and can support
broader-than/narrower-than relationships.

The initial core term set is:

* `ppd:userInput`: data intentionally provided by a user through direct
  interaction with the participant, service, or associated control surface.
* `ppd:sensor`: data directly observed from a sensing path associated with the
  participant or its environment.
* `ppd:cameraSensor`: data directly observed from an image- or video-capture
  sensing path.
* `ppd:microphone`: data directly observed from an audio-capture sensing path.
* `ppd:derivedData`: data produced from prior data through transformation,
  aggregation, inference, or similar derivation.

## Destination (To Where)

Destination terms identify the receiving endpoint or handling target to which
the dataflow applies. Destination participates in semantic comparison and can
support broader-than/narrower-than relationships.

The initial core term set is:

* `ppd:localProcessing`: a handling target that remains on the participant or
  within a household-local processing environment rather than a remote service.
* `ppd:vendorCloud`: a remote service environment operated by the device or
  service vendor.
* `ppd:thirdPartyService`: a remote service environment operated by an entity
  other than the device or service vendor.
* `ppd:dataBroker`: a recipient whose role includes acquiring, exchanging, or
  redisclosing data as a commercial data asset.

## Dataflow Qualifiers

The baseline protocol also allows structured qualifiers through the
`constraints` object. This document defines the initial qualifier families
used by that object.

The protocol wire object remains named `constraints`, but its members are
semantically qualifiers on atomic dataflows.

Qualifier families are action-sensitive. They are not a free-form bag of
attributes that apply equally to every action. A qualifier family is only
valid where this document or a later specification defines its meaning for the
relevant action context. Baseline participant-facing uses that attach a
qualifier family outside its defined applicability are invalid.

### Retention

Retention qualifies how long the relevant data or resulting artifact may
persist after the action in question.

Retention is action-sensitive. In particular:

* for `collection`, retention qualifies whether the collected result is
  allowed to persist after collection;
* for `use`, retention qualifies how long the data or resulting artifact may
  remain available for that use;
* for `transfer`, retention qualifies downstream persistence by the receiving
  side rather than only the sender's local storage duration; and
* for `inference`, retention qualifies how long inferred output may persist.

The baseline retention model distinguishes two strong named poles:

* ppd:ephemeral
* ppd:indefinite

`ppd:ephemeral` means the handling is not intended to result in durable
persistence beyond the immediate handling context.

`ppd:indefinite` means no bounded upper retention limit is expressed in the
rule.

Bounded retention periods are expected to require more specific quantitative
refinements, including explicit duration values and units, in later revisions
or deployment profiles. The baseline compact participant-facing form defined
here therefore standardizes only the categorical retention values above.

Retention comparison does not use a generic taxonomy subsumption hierarchy in
the same way as `data_type`, `purpose`, `source`, or `destination`.

### Processing Boundary

Processing Boundary qualifies where a processing operation may execute or
remain. This family is most natural for `use` and `inference`. It is not the
primary semantic mechanism for describing transfer recipients, because
`destination` already fills that role.

In the baseline model, `processing_boundary` is therefore primarily a
qualifier on `use` and `inference` dataflows rather than a general qualifier
on `transfer`.

Initial core terms include:

* ppd:onDeviceOnly
* ppd:inHomeOnly
* ppd:approvedRemoteProcessing

Processing Boundary participates in semantic comparison and can support
broader-than/narrower-than relationships.

### Jurisdiction

Jurisdiction qualifies the legal or regulatory domain relevant to the
dataflow.

Jurisdiction is intentionally not treated as a single flat label. Any use of a
jurisdiction qualifier MUST identify the scoped subcase it constrains, such as:

* processing
* storage
* transfer

The scoped subcase is part of the qualifier meaning. A jurisdiction
constraint on processing is not automatically equivalent to the same
jurisdiction constraint on storage or transfer.

This keeps the qualifier machine-comparable while still allowing broader
sovereignty concerns to be expressed through more concrete baseline semantics.

Jurisdiction participates in semantic comparison, but only within a clearly
identified scoped subcase.

This document defines the qualifier family and the scoped-semantics rule, but
it does not yet define a closed baseline set of jurisdiction vocabulary
values.

# Subsumption and Comparison

Baseline comparison is not limited to exact token equality.

For comparison-relevant role-fillers and qualifier families that participate in
subsumption:

* a term can be broader than another term;
* a term can be narrower than another term; and
* two terms are equivalent when each subsumes the other.

In the current baseline model:

* `data_type` participates in subsumption;
* `purpose` participates in subsumption;
* `source` participates in subsumption;
* `destination` participates in subsumption;
* `processing_boundary` participates in subsumption;
* `jurisdiction` participates in subsumption within a fixed scoped subcase;
* `action` remains a flat enumerable family and therefore compares by exact
  identity or exact reduction to a core action value rather than by
  broader-than/narrower-than subsumption; and
* `retention` uses its own categorical or quantitative comparison semantics
  rather than a generic taxonomy hierarchy.

This document does not define a full conflict-resolution procedure. It defines
the semantic basis that allows comparison to remain computable and
interoperable.

# Identifier Model

## Stable Term Identifiers

Stable term identifiers are the primary semantic hook in this taxonomy. The baseline core vocabulary uses the reserved prefix ppd:. A term such as ppd:temperatureReading or ppd:localProcessing derives its meaning from the stable taxonomy definition associated with that identifier.

A taxonomy release identifier can identify the vocabulary snapshot used for validation, reproducibility, or documentation. For example, a deployment might use a release identifier such as `ppd-core-2026-05`. However, release metadata does not replace the term identifier itself as the source of meaning.

## Stability of Term Meanings

Once published, a stable term identifier MUST NOT be silently reassigned an
incompatible meaning in a later taxonomy release.

Later releases MAY:

* add new terms;
* clarify the prose associated with an existing term when the clarification
  does not change its comparison semantics; and
* deprecate a term for future use while preserving its published meaning for
  reproducibility and comparison of existing content.

If a later release needs materially different semantics, it MUST define a new
term identifier rather than repurposing the old one.

## Compact Wire Form

{{?I-D.draft-dsmullen-ppd-protocol}} defines compact term identifiers as the participant-facing wire format. The protocol's Taxonomy Context Object carries:

* a taxonomy release identifier; and
* any required non-core prefix declarations.

This keeps participant-facing messages compact while preserving stable
semantics.

## Extension Namespaces and Core-Primitive Mapping

Organizations MAY define additional terms outside the baseline `ppd:`
vocabulary. When such terms appear in participant-facing protocol messages, the
sender MUST provide the required non-core prefix declarations through the
protocol's taxonomy context.

For comparison-relevant roles and qualifier families, namespace declaration
alone is not enough. When a non-core term fills `data_type`, `purpose`,
`action`, `source`, or `destination`, or supplies a non-core `retention`,
`processing_boundary`, or scoped `jurisdiction` qualifier value, that term
MUST be defined with the semantic relationship or exact reduction by which it
is reduced to one or more shared core concepts.

That relationship can include equivalence or broader/narrower placement where
the role participates in subsumption, or exact reduction where it does not, so
long as it preserves computable comparison against the shared core floor.

For example, an organization might define:

* vendorx:airQualityIndex
* vendorx:buildingOccupancyEstimate
* vendorx:regionalComplianceArchive

Such terms can be useful, but they remain baseline-interoperable only when
their relationship to the relevant core roles is explicit enough that
participants and household policy services can compare them meaningfully.

# Use in PPD Messages

The protocol and taxonomy have different jobs:

* the protocol carries which atomic combinations a participant asserts or a household policy applies; and
* the taxonomy defines what the terms used in those combinations mean.

This distinction matters. A flat bag of supported data types, purposes, actions, and destinations is not enough to describe which combinations actually apply to a participant. The protocol therefore carries atomic declaration statements and atomic policy rules, while this taxonomy defines the term spaces and qualifier meanings used in those objects.

The protocol wire object for qualifiers is named `constraints`, but the
semantics described here are qualifier semantics on those atomic dataflows.

When those objects use non-core comparison-relevant terms, the objects remain
baseline-computable only if those terms are reducible to the shared core model
through the extension and mapping rules above.

A declaration statement example is:

~~~ json
{
  "statement_id": "temperature-product-improvement",
  "data_type": "ppd:temperatureReading",
  "purpose": "ppd:productImprovement",
  "action": "ppd:transfer",
  "source": "ppd:sensor",
  "destination": "ppd:vendorCloud",
  "constraints": {
    "retention": "ppd:indefinite"
  }
}
~~~

A corresponding effective-policy rule example is:

~~~ json
{
  "rule_id": "r1",
  "data_type": "ppd:videoFrame",
  "purpose": "ppd:motionDetection",
  "action": "ppd:use",
  "source": "ppd:cameraSensor",
  "destination": "ppd:localProcessing",
  "effect": "allow",
  "constraints": {
    "processing_boundary": "ppd:onDeviceOnly"
  }
}
~~~

The taxonomy defines the meaning of the identifiers in these objects. The protocol defines how those objects are carried, validated, acknowledged, and kept current.

# Relationship to Richer Semantic Frameworks

This taxonomy is intentionally lighter than a full ontology language or
rights-expression framework. Implementations MAY publish auxiliary
representations, mappings, or tool-specific serializations when useful. For
example, organizations might maintain internal ontology, graph, or
policy-analysis artifacts that map to the stable identifiers defined here.

However, baseline participant-facing interoperability does not require OWL,
RDF, JSON-LD, or comparable machinery on the wire. The participant-facing
contract remains compact term identifiers plus the protocol-defined taxonomy
context, backed by the shared core semantic floor defined here.

# Security Considerations

Semantic drift, ambiguous extensions, and unresolved terms can undermine privacy signaling even when transport security is strong.

Organizations publishing extension vocabularies for comparison-relevant roles
need stable meanings and explicit reduction back to the shared core primitives.
Participant-facing services and participants SHOULD NOT silently treat
unresolved, unmapped, or unusable taxonomy terms as equivalent to known terms.

When comparison-relevant extension terms cannot be reduced to the shared core,
the correct baseline result is failure or indeterminate handling, not silent
fallback to a broader local guess.

When unresolved or unsupported terms appear in participant-facing protocol messages, the handling defined by {{?I-D.draft-dsmullen-ppd-protocol}} applies. In particular, unresolved terms in normative policy content are more serious than unresolved descriptive detail because they can change the meaning of an allowed or denied handling path.

# IANA Considerations

This document requests no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The authors thank the participants in the related PPD architecture, protocol, and implementation discussions for the feedback that shaped this taxonomy direction.
