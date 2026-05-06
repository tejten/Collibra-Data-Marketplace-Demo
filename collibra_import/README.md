# Collibra Import Files

These CSV files are simplified import inputs for the CPSH OSINT demo.

Import order:

1. `01_marketplace_data_sets.csv`
2. `02_restricted_data_sets.csv`
3. `03_business_terms.csv`
4. `04_data_contracts.csv`
5. `05_technical_tables.csv`
6. `06_columns.csv`

For a first demo, files 1-3 are enough. Files 4-6 add depth for contracts and technical lineage.

Use Collibra's asset import from a domain or asset view. Map the core columns:

- `Full Name` -> asset full name
- `Name` -> asset display/name
- `Asset Type` -> asset type
- `Domain` -> domain
- `Community` -> community
- `Status` -> status
- `Description` or `Definition` -> description/definition attribute

Do not map helper columns such as `Owner`, `Steward`, `Reviewer`, `Tags`, `File To Attach`, `Sample File`, or `Demo Talking Point` during the first import unless your view already has matching columns. Use them as a checklist for manual enrichment after import.

