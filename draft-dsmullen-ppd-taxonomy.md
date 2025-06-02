---
title: "Privacy Preference Declaration Taxonomy"
abbrev: "PPDTaxonomy"
category: info

docname: draft-dsmullen-ppd-taxonomy-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
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

This document defines a standardized taxonomy for describing data handling practices of Internet-connected devices within home networks. It complements the Privacy Preference Declaration (PPD) Protocol by providing the necessary vocabulary and semantic structure to represent and reason about data types, purposes, actions, sources, and destinations. This taxonomy supports both machine reasoning and human interpretation and can be implemented using ontological frameworks such as OWL-DL.


--- middle

# Introduction

The effectiveness of the Privacy Preference Declaration (PPD) architecture depends on a shared understanding of the semantics of privacy preferences. (TODO: reference the main architecture i-d here.)
A well-structured taxonomy enables the clear articulation of user-defined privacy constraints and provides a common language for devices to report their data handling practices.

This document introduces such a taxonomy, allowing policy declarations to express what kind of data is being handled, why it is being handled, how it is used, where it originates and is sent, and who is involved.
These taxonomic categories enable reasoning over complex privacy configurations and enforceable policies.

To support interoperability and consistency, the taxonomy defined herein is coupled with a centralized registry governed by IANA or a designated authority.
This registry ensures that all terms used in privacy declarations are semantically defined, unambiguous, and maintained through a community-driven process.
The registry plays a critical role in policy validation, enforcement logic, and device interoperability across ecosystems.



# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Design Goals

* Semantic Clarity: Enable precise and unambiguous expression of privacy concepts.
* Machine Reasoning: Support ontology-based reasoning to detect policy violations or mismatches.
* Extensibility: Allow addition of new concepts without disrupting existing deployments.
* Alignment: Reflect terminology familiar from privacy regulations (e.g., GDPR, CCPA).
* Registry Governance: Ensure terms are publicly documented, versioned, and governed through a formal review process to maintain ecosystem coherence.
* Validation Support: Facilitate automated validation of policies and declarations using machine-readable registry definitions.
* Interoperability: Promote uniform understanding of privacy semantics across diverse vendors and devices, backed by a shared taxonomy registry.


# Core Taxonomy Structure

The taxonomy consists of five orthogonal but interrelated categories.
These categories reference the concepts defined by Contextual Integrity theory in describing data flows. (TODO: cite this properly as an informative reference)

## Data Type (What)

Defines the nature of the data being collected, used, or transmitted.

Examples:

* temperatureReading
* videoCapture
* locationCoordinate
* audioTranscript
* deviceIdentifier
* healthStatus

This dimension aligns with data classification in privacy laws and informs sensitivity.

## Purpose (Why)

Describes the rationale for processing the data.

Examples:

* coreFunctionality (e.g., heating control)
* analytics
* advertising
* securityMonitoring
* personalization
* diagnostics

Each purpose can be mapped to categories of lawful basis for processing under regulations like GDPR (e.g., contract, consent, legitimateInterest).

## Action (How)

Specifies what is being done with the data.

Subclasses:

* collection (retrieval or ingestion)
* usage (processing or decision-making)
* transfer (sharing externally)
* retention (storage over time)
* deletion (erasure procedures)

These actions enable both auditing and fine-grained controls.

## Source and Destination (Where and To Whom)

Defines the data origin and endpoint.

Source may be, in the abstract:

* userInput
* sensor
* inferred (e.g., derived from other data)
* thirdPartyImport

Destination may include, in the abstract:

* localProcessing
* cloudStorage
* manufacturerServer
* thirdPartyPartner
* dataBroker

Concrete examples of these abstract categories of source and destination may also be used, such as {{!RFC3986}}.
This classification enables constraints on data flow (e.g., local-only, no third-party sharing).


# Ontological Representation

To support semantic reasoning, the taxonomy is expressed in OWL-DL (Web Ontology Language - Description Logic). (TODO: perhaps add a normative reference to this?)
This allows:

* Inference of non-compliance: e.g., if a device claims to process only temperatureReading for coreFunctionality, but attempts to collect locationCoordinate for advertising.
* Subclassing and equivalence: Allowing extension through subClassOf and equivalentClass definitions.
* Integration with existing vocabularies: Such as Data Privacy Vocabulary (DPV), and schema.org. (TODO: add an informative reference to DPV)

## Example OWL Classes

~~~
<owl:Class rdf:ID="DataType"/>
<owl:Class rdf:ID="temperatureReading">
  <rdfs:subClassOf rdf:resource="#DataType"/>
</owl:Class>

<owl:Class rdf:ID="Purpose"/>
<owl:Class rdf:ID="coreFunctionality">
  <rdfs:subClassOf rdf:resource="#Purpose"/>
</owl:Class>

<owl:ObjectProperty rdf:ID="hasPurpose">
  <rdfs:domain rdf:resource="#DataHandlingAction"/>
  <rdfs:range rdf:resource="#Purpose"/>
</owl:ObjectProperty>
~~~

# Use in Privacy Policies

Policies referencing this taxonomy can be expressed in a structured format such as JSON-LD or RDF/XML, allowing for both enforcement at runtime and static policy analysis. (TODO: add normative references here)

## Sample Policy Statement (JSON-LD)

~~~
{
  "@context": "http://example.org/ppd-taxonomy",
  "@type": "Policy",
  "appliesTo": "device:smart-thermostat-123",
  "allows": {
    "action": "collection",
    "data": "temperatureReading",
    "purpose": "coreFunctionality",
    "destination": "localProcessing"
  },
  "prohibits": [
    {
      "action": "transfer",
      "data": "temperatureReading",
      "destination": "thirdPartyPartner"
    },
    {
      "action": "collection",
      "data": "locationCoordinate"
    }
  ]
}
~~~



# Security Considerations

## Tamper resistance

Devices must not forge or misrepresent declared purposes.
Term identifiers MAY include cryptographic hashes for integrity.
All entries MUST be tamper-resistant and digitally signed where applicable.
Devices SHALL reject policies using unrecognized or invalid terms.

## Immutable references

Policy enforcement relies on exact matching; hash-based identifiers may be used.

## Cross-device reasoning

Shared taxonomy supports detecting conflicts or inconsistencies in multi-device settings.



# IANA Considerations

This specification requests the creation of a new IANA registry titled:

Privacy Preference Declaration (PPD) Taxonomy Registry

This registry defines structured terms for use in Privacy Preference Declarations, organized across five core categories: DataType, Purpose, Action, Source, and Destination.
It is intended to support semantic validation, enforcement, and interoperability in privacy-aware networked systems.

## Purpose and Justification

The Privacy Taxonomy Registry described in this document serves as the authoritative catalog of privacy-related semantic terms used across the Privacy Preference Declaration (PPD) architecture.
Managed under the Internet Assigned Numbers Authority (IANA), this registry provides a consistent, governed vocabulary to ensure interoperability, enforcement, and semantic alignment among privacy declarations, devices, and policy engines.

Unlike many traditional IANA registries that define protocol-level constructs such as status codes or media types, the Privacy Taxonomy Registry defines semantically rich terms suitable for reasoning over privacy constraints.
Each term is designed to be both human-readable and machine-processable, enabling automated policy enforcement, auditing, and semantic validation in distributed environments like home networks.
The registry helps prevent semantic drift, ensures privacy declarations are interpretable across vendor ecosystems, and provides a compliance anchor point for policy analysis and device certification.
It supports a unified approach to policy expression that is extensible yet constrained by formal definitions, such as those expressed in OWL-DL.
This registry distinguishes itself by supporting semantic reasoning and structured validation, not just name-value mappings.
It is foundational to privacy-preserving automation.

## Registry and Extension Mechanism

The success of the Privacy Preference Declaration framework depends on a shared, extensible, and authoritative vocabulary of privacy-related concepts.
A unified taxonomy ensures that:

* Users can write meaningful, enforceable policies with well-understood terms.
* Device manufacturers can interpret and comply with these policies using standard semantics.
* Policy processing engines can reason over device declarations and user constraints for compatibility, conflicts, or enforcement.

Without a centralized governance model, the ecosystem risks semantic drift — where different devices interpret similar terms differently, or invent new, incompatible terms — undermining both interoperability and policy clarity.

### Taxonomy Registry

A central Privacy Taxonomy Registry SHALL be established and governed by a standards organization (e.g., IETF/IANA, or an independent Privacy Policy Consortium).
This registry SHALL:

* Host the canonical definitions for core taxonomy terms.
* Publish OWL-DL and JSON-LD serializations for tooling.
* Allow versioning and deprecation of terms.
* Accept vetted community-submitted extensions via a structured process.
* Provide a human-readable portal and machine-readable API for lookup and validation.

## Registry Structure

Each entry in the registry MUST include the following fields:

* term_id: Globally unique identifier (e.g., ppd:purpose.analytics, ppd:dataType.temperature)

* category: One of: DataType, Purpose, Action, Source, Destination

* definition: Human-readable description of the term

* owl_definition: OWL-DL class or property definition

* examples: At least one real-world usage scenario

* status: Enum: active, deprecated, or experimental

* submitted_by: Name of contributing entity (organization or individual)

* date_registered: ISO timestamp of official inclusion

* version: Semantic versioning identifier (e.g., 1.0.0)

* references: Optional legal or technical citations (e.g., GDPR, RFCs)

All entries MUST conform to this structure and be encoded in both machine-readable (JSON-LD, RDF/XML) and human-readable formats.

## Initial Registry Contents

IANA SHALL initialize the registry with the baseline terms defined in this document's core taxonomy. These include:

* Core Data Types: temperatureReading, locationCoordinate, audioRecording, videoStream, deviceIdentifier, userPreference, biometricData, healthData, presenceIndicator

* Core Purposes: coreFunctionality, security, personalization, analytics, advertising, diagnostics, regulatoryCompliance

* Core Actions: collection, usage, transfer, retention, deletion

* Core Sources: sensor, userInput, thirdPartyImport, derivedData

* Core Destinations: localProcessing, cloudStorage, manufacturerServer, thirdPartyPartner, dataBroker

Each of these SHALL be registered with complete metadata as described above.

## Registry Management

The registry SHALL be maintained under the “Expert Review” policy defined in {{!RFC8126}}.
The designated expert(s) will evaluate submissions for:

* Conformance with the OWL-DL ontology

* Semantic clarity and non-ambiguity

* Necessity and non-duplication

* Privacy and security impact (if applicable)

The review process MUST include a public comment period and the ability to appeal decisions.

### Extension Mechanism

To support innovation and domain-specific specialization, the taxonomy MUST allow third parties to register custom terms via a controlled submission process.

#### Extension Requirements

An extension submission MUST:

* Declare a unique namespace (e.g., vendorX:, industryGroupY:).
* Clearly define its relationship to existing concepts (e.g., subClassOf, equivalentClass).
* Include all required registry fields (as above).
* Demonstrate necessity: why existing terms are insufficient.
* Include privacy risk assessment if the term introduces sensitive or novel data practices.


#### Extension and Deprecation Policy

Extensions: Entities MAY submit new terms with a custom namespace (e.g., vendorX:) as long as relationships to core terms (e.g., subClassOf) are clearly declared.

Deprecation: Deprecated terms remain in the registry with status marked as deprecated. These terms MUST NOT be used in future policy declarations but MAY be preserved for historical validation.

### Access Methods

The registry SHALL be made publicly available via:

* A web-accessible HTML directory with search and browse capabilities

* A machine-readable API for tool and device integration

* Regular snapshots for offline validation


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
