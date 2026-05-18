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

This document defines the core vocabulary and extension model used by Privacy Preference Declarations (PPDs) to describe data handling in home networks. It complements {{?I-D.draft-dsmullen-ppd-architecture}} and {{?I-D.draft-dsmullen-ppd-protocol}} by standardizing term spaces for data types, purposes, actions, sources, destinations, and selected constraints. Stable term identifiers are the primary semantic hook. Baseline participant-facing protocol messages use compact identifiers plus taxonomy context rather than requiring full ontology exchange on the wire.


--- middle

# Introduction

The Privacy Preference Declaration (PPD) architecture depends on a shared understanding of privacy-related semantics. {{?I-D.draft-dsmullen-ppd-architecture}} defines the roles, trust boundaries, and lifecycle. {{?I-D.draft-dsmullen-ppd-protocol}} defines the participant-facing message flow and object structure. This document defines the vocabulary those messages use.

The baseline PPD protocol carries atomic descriptive statements from device-side participants and atomic effective-policy rules from the household side. This taxonomy defines the meaning of the terms used in those statements and rules. It does not define a household policy authoring workflow, a conflict-resolution procedure, or a full reasoning engine.

The taxonomy is designed to be useful in constrained operational environments. It therefore separates the stable meaning of terms from any richer external semantic framework that might also describe them. Implementations can map these terms to richer vocabularies or ontology representations where useful, but such machinery is not required for baseline participant-facing interoperability.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Design Goals

* Semantic Clarity: Provide stable, unambiguous meanings for privacy-related terms used in PPD messages.
* Core Primitive Coverage: Standardize the dimensions needed by the baseline protocol rule and statement model.
* Compact Operational Use: Support compact identifiers in participant-facing JSON messages.
* Extensibility Without Fragmentation: Allow organization-specific vocabularies while requiring mapping back to shared core primitives.
* Validation and Comparison Support: Enable comparison of participant assertions and household policy without forcing every deployment to use a single heavy semantic framework.
* Interoperability: Preserve a shared vocabulary floor across vendors, device classes, and household deployments.

# Core Taxonomy Structure

The baseline taxonomy consists of five core dimensions plus selected qualifier terms. These dimensions are used together in atomic declaration statements and atomic effective-policy rules.

## Data Type (What)

Data Type terms identify the kind of data being collected, used, transferred, retained, or deleted.

Illustrative core terms include:

* ppd:temperatureReading
* ppd:videoFrame
* ppd:eventClip
* ppd:audioSample
* ppd:deviceIdentifier

## Purpose (Why)

Purpose terms identify the reason or operational objective for the handling.

Illustrative core terms include:

* ppd:coreFunctionality
* ppd:motionDetection
* ppd:remoteViewing
* ppd:analytics
* ppd:advertising
* ppd:diagnostics

## Action (How)

Action terms identify what is being done with the data.

Illustrative core terms include:

* ppd:collection
* ppd:usage
* ppd:transfer
* ppd:retention
* ppd:deletion

## Source (From Where)

Source terms identify the origin of the handled data in the relevant processing path.

Illustrative core terms include:

* ppd:userInput
* ppd:sensor
* ppd:cameraSensor
* ppd:microphone
* ppd:derivedData

## Destination (To Where)

Destination terms identify the endpoint or trust boundary to which the handling applies.

Illustrative core terms include:

* ppd:localProcessing
* ppd:vendorCloud
* ppd:thirdPartyPartner
* ppd:dataBroker

## Constraint Qualifiers

The baseline protocol also allows structured qualifiers through the constraints object. This document defines the initial qualifier term spaces used by that object.

### Retention

Retention terms qualify how long the described or allowed handling can persist.

Illustrative core terms include:

* ppd:ephemeral
* ppd:shortLived
* ppd:householdDefinedRetention

### Locality

Locality terms qualify the trust boundary or placement within which the described or allowed handling can occur.

Illustrative core terms include:

* ppd:inHomeOnly
* ppd:householdApprovedRemoteService
* ppd:thirdPartyProhibited

# Identifier Model

## Stable Term Identifiers

Stable term identifiers are the primary semantic hook in this taxonomy. The baseline core vocabulary uses the reserved prefix ppd:. A term such as ppd:temperatureReading or ppd:localProcessing derives its meaning from the stable taxonomy definition associated with that identifier.

A taxonomy release identifier can identify the vocabulary snapshot used for validation, reproducibility, or documentation. For example, a deployment might use a release identifier such as `ppd-core-2026-05`. However, release metadata does not replace the term identifier itself as the source of meaning.

## Compact Wire Form

{{?I-D.draft-dsmullen-ppd-protocol}} defines compact term identifiers as the participant-facing wire format. The protocol's Taxonomy Context Object carries:

* a taxonomy release identifier; and
* any required non-core prefix declarations.

This keeps participant-facing messages compact while preserving stable semantics.

## Extension Namespaces and Core-Primitive Mapping

Organizations MAY define additional terms outside the baseline ppd: vocabulary. When such terms appear in participant-facing protocol messages, the sender MUST provide the required non-core prefix declarations through the protocol's taxonomy context.

Extension terms SHOULD document how they map to the shared core primitives defined in this document. That mapping is what allows vendor- or ecosystem-specific vocabulary to coexist with interoperable baseline processing.

For example, an organization might define:

* vendorx:airQualityIndex
* vendorx:buildingOccupancyEstimate
* vendorx:regionalComplianceArchive

Such terms can be useful, but they SHOULD still explain how they relate to shared core dimensions and qualifiers so that participants and household policy services can compare them meaningfully.

# Use in PPD Messages

The protocol and taxonomy have different jobs:

* the protocol carries which atomic combinations a participant asserts or a household policy applies; and
* the taxonomy defines what the terms used in those combinations mean.

This distinction matters. A flat bag of supported data types, purposes, actions, and destinations is not enough to describe which combinations actually apply to a participant. The protocol therefore carries atomic declaration statements and atomic policy rules, while this taxonomy defines the term spaces and qualifier meanings used in those objects.

A declaration statement example is:

~~~ json
{
  "statement_id": "event-clip-remote-viewing",
  "data_type": "ppd:eventClip",
  "purpose": "ppd:remoteViewing",
  "action": "ppd:transfer",
  "source": "ppd:cameraSensor",
  "destination": "ppd:vendorCloud",
  "constraints": {
    "retention": "ppd:shortLived"
  }
}
~~~

A corresponding effective-policy rule example is:

~~~ json
{
  "rule_id": "r2",
  "data_type": "ppd:eventClip",
  "purpose": "ppd:remoteViewing",
  "action": "ppd:transfer",
  "source": "ppd:cameraSensor",
  "destination": "ppd:vendorCloud",
  "effect": "allow",
  "constraints": {
    "retention": "ppd:shortLived",
    "locality": "ppd:householdApprovedRemoteService"
  }
}
~~~

The taxonomy defines the meaning of the identifiers in these objects. The protocol defines how those objects are carried, validated, acknowledged, and kept current.

# Relationship to Richer Semantic Frameworks

This taxonomy is intentionally lighter than a full ontology language or rights-expression framework. Implementations MAY publish auxiliary representations, mappings, or tool-specific serializations when useful. For example, organizations might maintain internal ontology, graph, or policy-analysis artifacts that map to the stable identifiers defined here.

However, baseline participant-facing interoperability does not require OWL, RDF, JSON-LD, or comparable machinery on the wire. The participant-facing contract remains compact term identifiers plus the protocol-defined taxonomy context.

# Security Considerations

Semantic drift, ambiguous extensions, and unresolved terms can undermine privacy signaling even when transport security is strong.

Organizations publishing extension vocabularies SHOULD document stable meanings and mappings back to shared core primitives. Participant-facing services and participants SHOULD NOT silently treat unresolved or unusable taxonomy terms as equivalent to known terms.

When unresolved or unsupported terms appear in participant-facing protocol messages, the handling defined by {{?I-D.draft-dsmullen-ppd-protocol}} applies. In particular, unresolved terms in normative policy content are more serious than unresolved descriptive detail because they can change the meaning of an allowed or denied handling path.

# IANA Considerations

This document requests no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The authors thank the participants in the related PPD architecture, protocol, and implementation discussions for the feedback that shaped this taxonomy direction.
