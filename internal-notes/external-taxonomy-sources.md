# External Taxonomy Sources

This note tracks open external sources that may inform the PPD taxonomy model.
The goal is not to import one source wholesale. The goal is to learn from the
strongest open work for each PPD dataflow dimension and then define a compact
PPD-native core vocabulary.

## Source Selection Rules

- Prefer open, citable standards and openly published research.
- Do not treat member-gated or proprietary ecosystem specifications as the
  normative basis for the PPD taxonomy.
- Public ecosystem overviews can be used as breadth checks, but not as the
  primary semantic source for the core vocabulary.

## Candidate Sources

### W3C DPV

- Scope:
  privacy semantics for purpose, processing, recipient, storage, duration,
  deletion, location, risk, and related controls
- Likely value to PPD:
  strongest open source for `purpose`, `action`, `destination`, and many
  `constraints`
- Caution:
  broader and richer than the compact participant-facing PPD baseline needs

Source:
- <https://www.w3.org/community/reports/dpvcg/CG-FINAL-dpv-20240801/>

### W3C SSN / SOSA

- Scope:
  sensing, observations, actuators, samples, and observed properties
- Likely value to PPD:
  strongest open source for sensor-oriented `data_type` and parts of `source`
- Caution:
  not a privacy vocabulary, so it does not solve purpose or recipient
  semantics by itself

Source:
- <https://www.w3.org/TR/vocab-ssn-2023/>

### ETSI SAREF

- Scope:
  smart applications and IoT device/function/property ontology work
- Likely value to PPD:
  breadth check for real smart-home capability families and device-adjacent
  semantic categories
- Caution:
  more useful for coverage pressure-testing than for direct privacy-term import

Source:
- <https://saref.etsi.org/index.html>

### W3C PROV-O

- Scope:
  provenance and derivation relationships
- Likely value to PPD:
  source/provenance distinctions such as observed, derived, or generated data
- Caution:
  likely too general to map directly into the compact PPD participant-facing
  vocabulary

Source:
- <https://www.w3.org/TR/prov-o/>

### W3C WoT Thing Description

- Scope:
  protocol-agnostic device capability and interaction description
- Likely value to PPD:
  boundary check so the taxonomy does not collapse into a generic device model
- Caution:
  not a privacy taxonomy

Source:
- <https://www.w3.org/TR/wot-thing-description11/>

### W3C ODRL

- Scope:
  policy, permissions, prohibitions, duties, and constraints
- Likely value to PPD:
  constraint-model and policy-shape sanity checks
- Caution:
  weaker fit for the core home-IoT data-type and purpose inventory

Sources:
- <https://www.w3.org/TR/odrl-model/>
- <https://www.w3.org/TR/odrl-vocab/>

### EDDY Privacy Requirements Specification Language

- Scope:
  formal privacy requirements specifications over acts to collect, use,
  transfer, and retain information, with actors, information types, and
  purposes represented in analyzable logic
- Likely value to PPD:
  strong input for understanding privacy dataflow rule semantics, especially:
  - actor / information-type / purpose relationships
  - collection / use / transfer / retain action families
  - flow reasoning and conflict analysis
  - the semantic distinction between privacy policy rules and observed dataflow
- Caution:
  a requirements/specification language is not the same thing as a compact
  on-the-wire taxonomy, so its ontology should inform the PPD model rather
  than be copied directly into it

Sources:
- EDDY project page: <https://cmu-relab.github.io/eddy/>
- Breaux, Hibshi, Rao journal paper pointer: <https://www.cs.cmu.edu/~hhibshi/pdf/BHR14.pdf>
- CCC overview handout: <https://cra.org/ccc/wp-content/uploads/sites/2/2015/05/Workshop-Info-Sheet-eddy.pdf>
- Related Ontology of Personal Information: <https://opi.cs.cmu.edu/>

## Structural Inspiration from IETF Work

These are not privacy-taxonomy sources, but they are useful precedents for
how an IETF effort can define a compact common core and support augmentation or
mapping for external ecosystems:

- ASDF SDF: <https://datatracker.ietf.org/doc/draft-ietf-asdf-sdf/>
- ASDF SDF Supplements / Mapping:
  <https://datatracker.ietf.org/doc/draft-ietf-asdf-sdf-mapping/>
- ASDF SDF Protocol Mapping:
  <https://datatracker.ietf.org/doc/draft-ietf-asdf-sdf-protocol-mapping/>
- YANG Model Classification / RFC 8199:
  <https://datatracker.ietf.org/doc/rfc8199/>
