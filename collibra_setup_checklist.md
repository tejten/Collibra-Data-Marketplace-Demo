# Collibra Setup Checklist

Use this checklist to turn the demo kit into a working Collibra Data Marketplace story.

## Community and Domains

Create a community:

- `Open Source Intelligence Demo`

Create domains:

- `OSINT Data Products`
- `OSINT Source Governance`
- `OSINT Business Glossary`
- `OSINT Data Contracts`
- `OSINT Sample Data Assets`
- `OSINT Access Requests`

## Recommended Asset Types

Use existing Collibra asset types where available:

- Data Product
- Data Set
- Data Contract
- Business Term
- Table
- Column
- Report or Dashboard
- Data Usage

If your environment has custom marketplace asset types, map the demo inventory to those rather than creating new types for the demo.

## Statuses

Use three visible statuses in the demo:

- `Certified`: Approved for repeated mission use.
- `Approved`: Usable with stated conditions.
- `Candidate`: Visible for discussion but not default for operational use.
- `Not certified`: Restricted or contrast asset.

## Classifications and Tags

Create or reuse classifications:

- `PUBLIC`
- `PUBLIC_METADATA`
- `PUBLIC_REFERENCE`
- `PUBLIC_DERIVED`
- `AGGREGATED`
- `LICENSE_RESTRICTED`
- `INTERNAL`
- `TRADECRAFT_SENSITIVE`
- `SENSITIVE_ANALYTIC_INFERENCE`
- `POSSIBLE_PERSONAL_DATA`
- `NO_RAW_PERSONAL_DATA`
- `NO_PERSON_LEVEL_LOCATION`
- `RETENTION_LIMITED`
- `RESTRICTED`

## Responsibilities

Assign demo responsibilities:

- Data Product Owner: Jordan Lee
- Data Steward: Rafael Ortiz
- Privacy Reviewer: Alex Morgan
- Media Signals Owner: Elena Brooks
- Geospatial Owner: Nadia Patel
- Reference Data Owner: Samir Khan

## Core Relationships

Create these relationships for the strongest story:

- `Public Infrastructure Event Feed - Curated` is governed by:
  - Publicly Available Information
  - Corroboration Count
  - Source Reliability Score
  - Mission Purpose

- `Public Infrastructure Event Feed - Curated` is derived from:
  - OSINT Source Registry
  - Media Signal Extracts - Entity and Topic

- `Geospatial Situation Features - Aggregated` is derived from:
  - Public Infrastructure Event Feed - Curated

- `Source Reliability Scorecard` scores:
  - OSINT Source Registry

- `Raw Public Web Mentions - Restricted` is related to:
  - Purpose Limitation
  - Sensitive Personal Data
  - Handling Caveat

## Marketplace Collections

Create these collections or featured groups:

- `Crisis Monitoring Starter Kit`
  - Public Infrastructure Event Feed - Curated
  - Geospatial Situation Features - Aggregated
  - OSINT Source Registry

- `Public Source Trust Framework`
  - OSINT Source Registry
  - Source Reliability Scorecard

- `Narrative and Media Signals`
  - Media Signal Extracts - Entity and Topic
  - Narrative Theme Monitor - Aggregated
  - Raw Public Web Mentions - Restricted

- `Reference Data for Sanctions and Organizations`
  - Public Sanctions and Organizations Reference Pack

## Access Policies

Suggested demo approvals:

- Self-service:
  - OSINT Source Registry

- Basket request with analyst role:
  - Public Infrastructure Event Feed - Curated
  - Source Reliability Scorecard
  - Geospatial Situation Features - Aggregated
  - Media Signal Extracts - Entity and Topic

- Privacy/legal review:
  - Narrative Theme Monitor - Aggregated
  - Raw Public Web Mentions - Restricted

## Demo Quality Rules

Show these as data quality checks or contract expectations:

- Event IDs are unique.
- Every event links to a valid source ID.
- Curated event feed has no raw personal data.
- Source reliability score is between 0 and 100.
- Source review date is within 90 days.
- License caveat is populated for restricted sources.

## Presenter Prep

Before the live demo:

1. Load `asset_inventory.csv` and `business_glossary.csv` as demo metadata.
2. Attach the sample CSV files as technical assets or documentation links.
3. Attach the YAML contracts to the related data products.
4. Create marketplace cards using `marketplace_listings.md`.
5. Feature `Public Infrastructure Event Feed - Curated` on the marketplace landing page.
6. Make sure the basket workflow is enabled for the demo asset types.
7. Prepare two users or browser profiles: analyst and steward.

