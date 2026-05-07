# Collibra Data Marketplace Demo: Trusted OSINT Products

This demo is designed for an open source intelligence agency audience. It shows how Collibra Data Marketplace can turn public-source chaos into governed, discoverable, reusable data products for mission analysts.

## Core Story

Mission analysts need to prepare a regional infrastructure disruption brief within one hour. Relevant signals exist across public news, weather alerts, port bulletins, public procurement notices, humanitarian advisories, and social/web discourse summaries. The challenge is not finding "more data"; it is finding trusted, lawful, explainable, and approved data quickly.

Collibra Data Marketplace becomes the mission storefront:

1. An analyst searches in plain language for public infrastructure disruption data.
2. The analyst compares trusted data products by certification, owner, lineage, source reliability, refresh cadence, handling caveats, and data quality score.
3. The analyst adds multiple curated products to the data basket and submits one access request with a stated mission purpose.
4. A data steward reviews the request, confirms permitted use, and routes approval based on policy tags such as `PUBLIC`, `LICENSE_RESTRICTED`, `AGGREGATED`, and `NO_RAW_PERSONAL_DATA`.
5. The analyst uses only approved, curated products in a notebook or dashboard, with provenance and auditability preserved.

## Plain-English Concepts

Think of the marketplace like a restaurant.

| Collibra concept | Restaurant analogy | What it means in this demo |
| --- | --- | --- |
| Data Product | The menu item | The business-facing package analysts understand and shop for, such as `Public Infrastructure Event Feed Product`. |
| Data Product Port | The serving window or pickup counter | The access doorway that explains how consumers get the product, such as `Public Infrastructure Event Feed Output Port` with `UI` access instructions. |
| Data Set or Table | The actual dish being served | The real requestable or technical data behind the product, such as `Public Infrastructure Event Feed - Curated` or `osint_public_event_feed`. |
| Data Contract | The order promise and kitchen standard | The rules for what the product contains, quality expectations, refresh expectations, and usage limits. |

In the OSINT demo:

```text
Data Product:
Public Infrastructure Event Feed Product
= the business-friendly package

Data Product Port:
Public Infrastructure Event Feed Output Port
= the access doorway / serving counter

Data Set or Table:
Public Infrastructure Event Feed - Curated / osint_public_event_feed
= the actual data being served

Data Contract:
Public Infrastructure Event Feed Contract
= the rules and promise for that data
```

Simple demo line:

`The Data Product is what the analyst shops for, the Port is how they access it, and the Contract is the promise that defines what they will receive and under what rules.`

## Demo Personas

| Persona | Role | What they care about |
| --- | --- | --- |
| Maya Chen | OSINT Mission Analyst | Fast discovery, confidence, source context, reusable products |
| Rafael Ortiz | Data Steward | Proper classification, access policy, business glossary alignment |
| Priya Nair | Mission Lead | Decision-ready brief, explainability, defensible sourcing |
| Alex Morgan | Privacy and Legal Reviewer | Lawful use, licensing constraints, minimization, audit trail |
| Jordan Lee | Data Product Owner | Product adoption, quality score, user feedback, refresh reliability |

## Demo Flow

1. Open Data Marketplace and show curated collections:
   - `Crisis Monitoring Starter Kit`
   - `Public Source Trust Framework`
   - `Narrative and Media Signals`
   - `Reference Data for Sanctions and Organizations`

2. Search for:
   - `infrastructure disruption public reports`
   - `source reliability score`
   - `aggregated geospatial event features`

3. Open `Public Infrastructure Event Feed - Curated`.
   - Show certification and quality score.
   - Show owner, steward, refresh cadence, and access method.
   - Show lineage from public sources through extraction, deduplication, human review, and curated publication.
   - Show business terms such as `Corroboration Count`, `Source Reliability Score`, and `Mission Purpose`.

4. Compare it with `Raw Public Web Mentions - Restricted`.
   - Use this as the governance contrast.
   - Explain why raw mentions are not the preferred marketplace product for most analysts.
   - Show handling caveats and the need for privacy/legal review.

5. Add approved products to the data basket:
   - `Public Infrastructure Event Feed - Curated`
   - `OSINT Source Registry`
   - `Source Reliability Scorecard`
   - `Geospatial Situation Features - Aggregated`

6. Check out the basket.
   - Mission purpose: `Regional infrastructure disruption brief for crisis response planning`.
   - Access duration: `30 days`.
   - Intended use: `Analytic reporting and dashboarding; no individual profiling`.

7. Switch to steward view.
   - Show policy-based approval.
   - Approve aggregated and curated products.
   - Route restricted/raw-source products to privacy/legal review.

8. Close with the value message:
   - Analysts get speed.
   - Stewards get control.
   - Leaders get trusted, explainable intelligence products.
   - The agency gets reuse, auditability, and reduced data risk.

## Demo Assets Included

| File | Purpose |
| --- | --- |
| `presenter_script.md` | Full talk track and click-by-click presenter script |
| `marketplace_listings.md` | Copy for Collibra Marketplace product cards |
| `asset_inventory.csv` | Import-friendly metadata inventory for demo assets |
| `business_glossary.csv` | OSINT governance glossary terms |
| `sample_data/source_registry.csv` | Synthetic source inventory sample |
| `sample_data/public_event_feed.csv` | Synthetic curated event feed |
| `sample_data/media_signal_extracts.csv` | Synthetic media/entity/topic signals |
| `sample_data/geospatial_aggregates.csv` | Synthetic aggregated geospatial features |
| `data_contracts/public_event_feed_contract.yaml` | Demo data contract for curated event feed |
| `data_contracts/source_reliability_scorecard_contract.yaml` | Demo data contract for reliability scores |

## Safety Positioning

This demo intentionally uses synthetic data and emphasizes aggregated, curated, and purpose-bound access. Avoid positioning the marketplace as a tool for identifying, tracking, or profiling private individuals. The strongest agency story is responsible OSINT: provenance, lawful use, source quality, minimization, auditability, and reuse.
