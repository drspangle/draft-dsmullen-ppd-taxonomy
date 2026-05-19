# Source Material

This note tracks the most relevant local PPD design artifacts that should
shape the taxonomy draft. These are typically checked out as sibling
repositories under `../`.

## Primary Inputs

- `../draft-dsmullen-ppd-protocol/draft-dsmullen-ppd-protocol.md`
  - baseline participant-facing object model
  - the current `data_type` / `purpose` / `action` / `source` /
    `destination` / `constraints` dimensional split
  - compact term identifiers, taxonomy context, and taxonomy-bearing error
    handling
- `../draft-dsmullen-ppd-architecture/draft-dsmullen-ppd-architecture.md`
  - overall privacy-signaling problem framing
  - household policy and participant declaration boundary
  - constraints imposed by home-IoT deployments and resource-constrained
    participants

## Secondary Inputs

- `../habanero-ppd-gateway/design/ppd-taxonomy.md`
  - local prototype taxonomy/rule ideas that may still contain useful examples
    or anti-patterns
- `../habanero-ppd-gateway/design/ppd-client-requirements.md`
  - participant expectations that pressure-test which categories are actually
    needed for comparison and enforcement
- `../habanero-ppd-clients/devices/esp32-smart-bulb/docs/capability-model.md`
  - the current live demo's narrow but concrete dataflow story
- `../habanero-ppd-clients/devices/esp32-smart-bulb/docs/bringup.md`
  - purpose-specific mock-cloud disclosure walkthrough details

## Use Rule

These local materials are useful pressure tests, but they must not become the
sole basis for the core vocabulary. The taxonomy needs to cover home-IoT
privacy dataflows more broadly than the current demo and current examples.
