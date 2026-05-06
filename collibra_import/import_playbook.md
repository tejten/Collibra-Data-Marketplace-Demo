# Import Playbook for the OSINT Demo Assets

Use these files instead of the original `asset_inventory.csv` for the first Collibra import:

- `01_marketplace_data_sets.csv`
- `02_restricted_data_sets.csv`
- `03_business_terms.csv`
- `04_data_contracts.csv`
- `05_technical_tables.csv`
- `06_columns.csv`
- `07_data_product_wrappers.csv`

For a first working marketplace demo, import only files 1-3. Files 4-7 add polish later.

## Before You Import

Confirm you have already completed:

- Community: `Open Source Intelligence Demo`
- Domain: `OSINT Marketplace Products`
- Domain: `OSINT Restricted Source Validation`
- Domain: `OSINT Business Glossary`
- Domain: `OSINT Governance and Contracts`
- Domain: `OSINT Technical Sample Assets`
- Global role with `Import` permission
- Resource responsibilities that allow you to create assets in those domains

If you are signed in as `Admin`, you should be fine.

## Import 1: Marketplace Data Sets

File:

`01_marketplace_data_sets.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Marketplace Products`

Steps:

1. Open Stewardship.
2. Go to `Organization`.
3. Open `Open Source Intelligence Demo`.
4. Open the domain `OSINT Marketplace Products`.
5. Open the `Assets` tab or asset table view.
6. Click the upload/import icon.
7. Choose `Import` -> `Assets`.
8. Upload `01_marketplace_data_sets.csv`.
9. CSV options:
   - Column separator: `,`
   - Quote: `"`
   - Escape character: keep the default
10. Click `Next`.
11. For asset unique identifier, choose:
   - `Full Name, Community, Domain`
12. Map these columns:
   - `Full Name` -> asset full name
   - `Name` -> asset name or display name
   - `Asset Type` -> asset type
   - `Domain` -> domain
   - `Community` -> community
   - `Status` -> status
   - `Description` -> description attribute
13. Leave these unmapped for the first pass:
   - `Tags`
   - `Owner`
   - `Steward`
   - `Quality Score`
   - `Refresh Cadence`
   - `Access Policy`
   - `Demo Talking Point`
14. Import options:
   - Enable `Create new assets if they don't yet exist`.
   - For existing assets, choose `Update existing assets with any new values from the file`.
   - For existing attributes, choose `Only add new values`.
   - Do not select `Delete existing assets from the domain that are not in the file`.
   - Enable `Test import`.
15. Click `Test Import`.
16. If the preview says it will create 6 assets, click `Import`.

Expected assets:

- `Public Infrastructure Event Feed - Curated`
- `OSINT Source Registry`
- `Source Reliability Scorecard`
- `Geospatial Situation Features - Aggregated`
- `Media Signal Extracts - Entity and Topic`
- `Public Sanctions and Organizations Reference Pack`

## Import 2: Restricted Contrast Assets

File:

`02_restricted_data_sets.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Restricted Source Validation`

Use the same wizard steps as Import 1.

Expected assets:

- `Raw Public Web Mentions - Restricted`
- `Narrative Theme Monitor - Aggregated`

If you do not want analysts to see restricted assets in Data Marketplace, keep their status out of Data Marketplace scope.

## Import 3: Business Glossary

File:

`03_business_terms.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Business Glossary`

Map:

- `Full Name` -> asset full name
- `Name` -> asset name or display name
- `Asset Type` -> asset type
- `Domain` -> domain
- `Community` -> community
- `Status` -> status
- `Definition` -> definition attribute
- `Acronym` -> acronym attribute, if available
- `Example` -> example attribute, if available
- `Classification Notes` -> description or notes attribute, if available

Only map columns that Collibra offers in the mapping dialog. It is fine to leave extra columns unmapped.

Expected result:

15 `Business Term` assets in the glossary domain.

## Optional Import 4: Data Contracts

File:

`04_data_contracts.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Governance and Contracts`

Map the basic asset columns and `Description`.

After import, manually attach:

- `data_contracts/public_event_feed_contract.yaml`
- `data_contracts/source_reliability_scorecard_contract.yaml`

## Optional Import 5: Technical Tables

File:

`05_technical_tables.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Technical Sample Assets`

Map the basic asset columns and `Description`.

After import, manually attach the sample CSV files referenced in the `Sample File` column.

## Optional Import 6: Columns

File:

`06_columns.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Technical Sample Assets`

Map:

- `Full Name` -> asset full name
- `Name` -> asset name or display name
- `Asset Type` -> asset type
- `Domain` -> domain
- `Community` -> community
- `Status` -> status
- `Description` -> description attribute

Leave `Parent Table` unmapped in the first pass unless your view has a table/column relation available. Add table-column relations manually later if you want lineage polish.

## Optional Import 7: Data Product Wrappers

File:

`07_data_product_wrappers.csv`

Target domain:

`Open Source Intelligence Demo` -> `OSINT Data Product Catalog`

Map:

- `Full Name` -> asset full name
- `Name` -> asset name or display name
- `Asset Type` -> asset type
- `Domain` -> domain
- `Community` -> community
- `Status` -> status
- `Description` -> description attribute

Leave `Tags`, `Related Requestable Data Set`, and `Demo Talking Point` unmapped in the first pass.

Expected assets:

- `Public Infrastructure Event Feed Product`
- `Source Reliability Scorecard Product`
- `Geospatial Situation Features Product`

After import, manually relate each Data Product to its requestable Data Set:

- `Public Infrastructure Event Feed Product` -> `Public Infrastructure Event Feed - Curated`
- `Source Reliability Scorecard Product` -> `Source Reliability Scorecard`
- `Geospatial Situation Features Product` -> `Geospatial Situation Features - Aggregated`

These wrapper assets are not required for the data basket. They are for the demo narrative: the Data Product is the business-facing package, and the Data Set is the requestable output.

## After the First Three Imports

Open each imported Data Set and manually add:

- Tags from the `Tags` column.
- Owner responsibility:
  - `OSINT Product Owners` or `jordan.lee`
- Steward responsibility:
  - `OSINT Data Stewards` or `rafael.ortiz`
- Reviewer responsibility for restricted assets:
  - `OSINT Privacy Reviewers` or `alex.morgan`

Then search Data Marketplace for:

- `infrastructure disruption public reports`
- `source reliability score`
- `aggregated geospatial event features`

## Common Import Problems

Problem: Import button is missing.

- You are probably not in a view/table that supports import.
- Open a domain, then its `Assets` tab.
- Confirm your user has the `Import` global permission.

Problem: Test import says zero assets will be created.

- Check that `Create new assets if they don't yet exist` is enabled.
- Check that `Full Name`, `Community`, and `Domain` are mapped.
- Check that domain names exactly match your domains.

Problem: Status mapping fails.

- Use `Accepted` for the first pass.
- If your environment does not have `Accepted`, change the CSV status values to a status you see in the UI, such as `Candidate` or `Approved`.

Problem: Attribute columns do not appear in the mapping dialog.

- Skip them.
- Import only the basic asset shell first.
- Add descriptions, tags, responsibilities, and attachments manually on the asset page.
