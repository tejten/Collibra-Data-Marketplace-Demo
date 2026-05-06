# CPSH Build Runbook: OSINT Data Marketplace Demo

Environment: `https://ec2-3-85-153-127.compute-1.amazonaws.com:4444`

This runbook assumes a fresh Collibra Platform Self-Hosted environment and a novice administrator. It builds the OSINT marketplace demo from the demo assets in this folder.

## 0. What You Are Building

You are building a governed Data Marketplace for an open source intelligence agency.

The finished demo should show:

- An analyst searching Data Marketplace for OSINT data.
- Certified/approved public-source data assets with owners, stewards, glossary context, and quality/trust descriptions.
- Restricted raw-source assets that are visible as a governance contrast.
- A data basket checkout request.
- A steward/product-owner approval task.

## 1. Preflight

1. Sign in as `Admin`.
2. Use a wide browser window. Collibra tables are much easier above 1200 px wide.
3. Keep the default `Admin` account until you have created at least one other user with `Sysadmin`.
4. For a real or long-lived environment, change the default admin password after the demo setup.

Important: Collibra users do not receive useful access just because the user exists. They need global roles for applications and resource responsibilities/view permissions for communities, domains, and assets.

## 2. Recommended Demo Users

Create these users. Use your own email address aliases if outbound email is configured. If email is not configured, use placeholder emails and set passwords manually from the user row.

| Username | First name | Last name | Email | Demo role |
| --- | --- | --- | --- | --- |
| `maya.chen` | Maya | Chen | `maya.chen@example.com` | OSINT analyst / data consumer |
| `priya.nair` | Priya | Nair | `priya.nair@example.com` | Mission lead / consumer |
| `rafael.ortiz` | Rafael | Ortiz | `rafael.ortiz@example.com` | Data steward |
| `jordan.lee` | Jordan | Lee | `jordan.lee@example.com` | Data product owner |
| `alex.morgan` | Alex | Morgan | `alex.morgan@example.com` | Privacy/legal reviewer |
| `demo.admin` | Demo | Admin | `demo.admin@example.com` | Backup demo administrator |

Steps:

1. Click the products/app launcher icon.
2. Click the cogwheel `Settings`.
3. Open `Users and subscriptions`.
4. Open the `Users` tab.
5. Click `Add`.
6. Enter the user details.
7. Add users to groups later, not inside the first user creation flow, unless the groups already exist.
8. Click `Create`.
9. If passwords show `Unset`, use the reset/set password action on the user row.

Suggested temporary demo password pattern:

- Use a strong password that satisfies the local password policy.
- Do not reuse demo passwords in production.

## 3. Create User Groups

Go to `Settings` -> `Users and subscriptions` -> `Groups` -> `Add`.

Create these groups:

| Group | Purpose |
| --- | --- |
| `OSINT Marketplace Consumers` | Analysts and mission leads who search and request marketplace assets |
| `OSINT Data Stewards` | Stewards who curate glossary, metadata, and governance context |
| `OSINT Product Owners` | Owners who approve access and maintain data products |
| `OSINT Privacy Reviewers` | Privacy/legal reviewers for restricted assets |
| `OSINT Demo Admins` | Backup admins for the demo environment |

Add members:

| Group | Members |
| --- | --- |
| `OSINT Marketplace Consumers` | `maya.chen`, `priya.nair` |
| `OSINT Data Stewards` | `rafael.ortiz` |
| `OSINT Product Owners` | `jordan.lee` |
| `OSINT Privacy Reviewers` | `alex.morgan` |
| `OSINT Demo Admins` | `demo.admin` |

Leave the packaged `Data Custodians` group alone for now.

## 4. Assign Global Roles

Global roles let people use Collibra applications. They do not by themselves make someone the owner or steward of a specific community or asset.

Go to `Settings` -> `Roles and permissions` -> `Global roles`.

Add the groups to these packaged global roles:

| Global role | Add these groups |
| --- | --- |
| `Data Marketplace` | `OSINT Marketplace Consumers`, `OSINT Data Stewards`, `OSINT Product Owners`, `OSINT Privacy Reviewers` |
| `Catalog` | `OSINT Marketplace Consumers`, `OSINT Privacy Reviewers` |
| `Catalog Author` | `OSINT Data Stewards`, `OSINT Product Owners` |
| `DataSteward` | `OSINT Marketplace Consumers`, `OSINT Privacy Reviewers` |
| `DataSteward Author` | `OSINT Data Stewards`, `OSINT Product Owners` |
| `Glossary` | `OSINT Marketplace Consumers`, `OSINT Data Stewards`, `OSINT Product Owners`, `OSINT Privacy Reviewers` |
| `Export` | `OSINT Data Stewards`, `OSINT Product Owners` |
| `Import` | `OSINT Data Stewards` |
| `Sysadmin` | `OSINT Demo Admins` only |

Then check workflow permissions:

1. In `Roles and permissions`, search global permissions for `Workflows`.
2. Confirm at least one role assigned to consumers has `Workflows > Start Workflow`.
3. Confirm users who will complete tasks have `Workflows > Participate in workflow`.
4. If needed, create a custom global role named `OSINT Workflow Participant`.
5. Add these global permissions to it:
   - `Workflows > Start Workflow`
   - `Workflows > Participate in workflow`
6. Add all four non-admin demo groups to `OSINT Workflow Participant`.

Why this matters: Data basket checkout starts the packaged access-request workflow. Without workflow permissions, the basket may be visible but checkout will fail or the user will be blocked.

## 5. Confirm the Operating Model

For a novice build, do not create custom asset types first. Use packaged asset types and tags.

Go to `Settings` -> `Operating model`.

Confirm these asset types exist:

| Asset type | Use in this demo |
| --- | --- |
| `Data Set` | Main requestable marketplace products |
| `Report` | Optional demo dashboard/report assets |
| `Data Product` | Optional wrapper/product story |
| `Data Contract` | YAML contract documentation assets |
| `Business Term` | OSINT glossary |
| `Table` | Optional sample CSV technical table |
| `Column` | Optional sample CSV fields/data elements |
| `Data Usage` | Created automatically by the data basket |

Confirm these domain types are available:

| Domain type | Use |
| --- | --- |
| `Data Asset Domain` | Data Sets, Tables, Columns, Data Product Ports |
| `Business Asset Domain` | Data Products if `Data Product Catalog` is not available |
| `Data Product Catalog` | Preferred for Data Products if available |
| `Glossary` | Business Terms |
| `Governance Asset Domain` | Data Contracts and governance controls |

Avoid changing `Data Usage` status assignments. The access workflow expects `Candidate` to be available for Data Usage assets.

## 6. Create the Community

Click the plus/create icon in the main toolbar.

1. Click `Organization`.
2. Select `Community`.
3. Leave parent community blank.
4. Name it `Open Source Intelligence Demo`.
5. Click `Create`.

Open the new community and add a short description:

`Demo community for governed discovery, approval, and reuse of synthetic open source intelligence data products.`

## 7. Create Domains

Inside the `Open Source Intelligence Demo` community, create these domains.

Use the plus/create icon -> `Organization` -> choose the domain type.

| Domain name | Domain type | Purpose |
| --- | --- | --- |
| `OSINT Marketplace Products` | `Data Asset Domain` | Requestable Data Set assets that appear in Data Marketplace |
| `OSINT Data Product Catalog` | `Data Product Catalog` if available, otherwise `Business Asset Domain` | Optional Data Product wrappers |
| `OSINT Business Glossary` | `Glossary` | OSINT business terms |
| `OSINT Governance and Contracts` | `Governance Asset Domain` | Data contracts, handling rules, policies |
| `OSINT Technical Sample Assets` | `Data Asset Domain` | Optional tables and columns representing the sample CSVs |
| `OSINT Restricted Source Validation` | `Data Asset Domain` | Restricted/raw-source contrast assets |

## 8. Add Responsibilities and View Permissions

Open the `Open Source Intelligence Demo` community and go to the `Responsibilities` tab.

Add these responsibilities at the community level:

| Group | Resource role |
| --- | --- |
| `OSINT Demo Admins` | `Community Manager` |
| `OSINT Data Stewards` | `Business Steward` or `Data Steward` |
| `OSINT Product Owners` | `Owner` |
| `OSINT Privacy Reviewers` | `Reviewer` |
| `OSINT Marketplace Consumers` | `Requester` or `Stakeholder` |

Then open each domain and refine if needed:

| Domain | Responsibilities |
| --- | --- |
| `OSINT Marketplace Products` | Product Owners = `Owner`; Data Stewards = `Business Steward`; Consumers = `Requester` |
| `OSINT Data Product Catalog` | Product Owners = `Owner`; Data Stewards = `Business Steward`; Consumers = `Stakeholder` |
| `OSINT Business Glossary` | Data Stewards = `Business Steward`; Consumers = `Stakeholder` |
| `OSINT Governance and Contracts` | Privacy Reviewers = `Reviewer`; Data Stewards = `Business Steward`; Product Owners = `Owner` |
| `OSINT Technical Sample Assets` | Data Stewards = `Technical Steward`; Product Owners = `Owner`; Consumers = `Stakeholder` |
| `OSINT Restricted Source Validation` | Privacy Reviewers = `Reviewer`; Data Stewards = `Business Steward`; Product Owners = `Owner`; Consumers = `Stakeholder` only if you want them to see the restricted contrast asset |

If Collibra shows a warning that a group has a responsibility but lacks view permissions:

1. Open the same community/domain.
2. Go to `Responsibilities`.
3. Add or update the view permissions for that group.
4. Reopen the asset as a non-admin user to verify visibility.

## 9. Plan Tags for Handling Caveats

In Collibra, new tags are created from an asset page, not from the Stewardship `Tags` overview page. The `Tags` page lets you view, edit, merge, and delete tags after at least one asset uses them.

For now, keep this list ready. You will add each tag when you create or edit the related Data Set assets in section 13.

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

These are demo governance labels. Use tags first; do not customize the classification model unless you specifically want to demonstrate data classification.

How to add the first tag:

1. Create or open an asset, for example `Public Infrastructure Event Feed - Curated`.
2. In the latest UI, do not look for a page-level pencil. Asset pages use inline editing.
3. Click the circular `i` icon near the top-right of the asset page to open the `At a glance` sidebar.
4. Find `Tags` in the sidebar.
5. Click the add or edit control in the `Tags` section.
6. Type a tag name such as `PUBLIC`.
7. Press Enter or select `Create PUBLIC`.
8. Save or click away if the value saves inline.
9. Return to Stewardship -> `Tags`; the tag should now appear in the overview.

If the `Tags` field is missing or read-only:

1. Confirm the `At a glance` sidebar is open by clicking the circular `i` icon.
2. Go to `Settings` -> `Roles and permissions` -> `Global permissions`.
3. Find `Tags`.
4. Enable the tag add/update/remove permission for the resource roles you are using, such as `Owner`, `Business Steward`, or `Data Steward`.
5. Confirm your user or group has one of those responsibilities on the asset, domain, or community.
6. Confirm the user also has view access to the asset's community or domain.
7. Reopen the asset and try again.

If tags still do not appear, skip them for the first demo. They are useful labels, but they are not required for Data Marketplace search, the data basket, responsibilities, glossary links, or access-request flow.

## 10. Configure Data Marketplace Scope

Go to `Settings` -> `Search` -> `Data Marketplace Scope`.

Configure:

| Scope tab | Recommended values |
| --- | --- |
| `Asset types` | `Data Set`, `Report`; optionally `Data Product` after the base demo works |
| `Statuses` | `Accepted`, `Approved`, `Candidate` if available; include `Candidate` only if you want the restricted/candidate assets searchable |
| `Organization` | Select `Open Source Intelligence Demo` and its domains |
| `Asset Type Groups` | Leave blank for the first build unless you later configure relation-path filters |

Click `Save`.

Simple first-demo recommendation:

- Put approved requestable assets in status `Accepted` or `Approved`.
- Put restricted/raw assets in `Candidate` or `Under Review`.
- Include `Candidate` in the marketplace scope only if you want the analyst to see restricted assets as a contrast.

## 11. Configure the Data Basket

Go to `Settings` -> `Search` -> `Actions and Preview` -> `Data Basket`.

1. Select `Define whether users can add assets to data basket and request access`.
2. In configured asset types, keep:
   - `Data Set`
   - `Report`
3. Do not add `Data Product` for the first novice build.
4. Select `Restrict to Data Marketplace scope`.
5. Save.

Why not `Data Product` yet? The packaged basket and access workflow are designed around Data Set/Report by default. Adding extra asset types may require workflow changes.

## 12. Confirm Workflow

Go to `Settings` -> `Workflows`.

Find and confirm the packaged workflow is enabled:

- `Request Assets Access`

If you see an older name such as `Request Data Sets Access`, use that packaged access-request workflow.

Do not edit the workflow for the first build.

## 13. Create Requestable Marketplace Assets

Fast path: use the prepared import files in `collibra_import/` and follow `collibra_import/import_playbook.md`. Import files 1-3 first:

- `01_marketplace_data_sets.csv`
- `02_restricted_data_sets.csv`
- `03_business_terms.csv`

Then return here to add tags, responsibilities, attachments, and relationships manually.

Create these as `Data Set` assets in the `OSINT Marketplace Products` domain.

Use plus/create -> asset/data asset -> `Data Set`.

| Asset name | Status | Tags | Owner | Steward |
| --- | --- | --- | --- | --- |
| `Public Infrastructure Event Feed - Curated` | `Accepted` or `Approved` | `PUBLIC`, `AGGREGATED`, `NO_RAW_PERSONAL_DATA` | `jordan.lee` or `OSINT Product Owners` | `rafael.ortiz` or `OSINT Data Stewards` |
| `OSINT Source Registry` | `Accepted` or `Approved` | `PUBLIC_METADATA`, `LICENSE_RESTRICTED` | `jordan.lee` | `rafael.ortiz` |
| `Source Reliability Scorecard` | `Accepted` or `Approved` | `INTERNAL`, `TRADECRAFT_SENSITIVE` | `jordan.lee` | `rafael.ortiz` |
| `Geospatial Situation Features - Aggregated` | `Accepted` or `Approved` | `PUBLIC_DERIVED`, `AGGREGATED`, `NO_PERSON_LEVEL_LOCATION` | `jordan.lee` | `rafael.ortiz` |
| `Media Signal Extracts - Entity and Topic` | `Approved` | `PUBLIC_DERIVED`, `LICENSE_RESTRICTED` | `jordan.lee` | `rafael.ortiz` |
| `Public Sanctions and Organizations Reference Pack` | `Approved` | `PUBLIC_REFERENCE` | `jordan.lee` | `rafael.ortiz` |

Create this contrast asset in `OSINT Restricted Source Validation`:

| Asset name | Status | Tags | Owner | Reviewer |
| --- | --- | --- | --- | --- |
| `Raw Public Web Mentions - Restricted` | `Candidate` or `Under Review` | `RESTRICTED`, `POSSIBLE_PERSONAL_DATA`, `RETENTION_LIMITED` | `jordan.lee` | `alex.morgan` |

For each asset:

1. Paste the matching description from `marketplace_listings.md`.
2. Add owner and steward responsibilities directly on the asset if they are not inherited.
3. Attach the relevant sample CSV from `sample_data/`.
4. Add a note such as `Synthetic demo data only`.

## 14. Optional but Recommended: Create Technical Tables and Columns

This makes the marketplace demo more realistic and helps with workflows that expect data elements.

Create these `Table` assets in `OSINT Technical Sample Assets`:

| Table asset | Attach/source file |
| --- | --- |
| `osint_public_event_feed` | `sample_data/public_event_feed.csv` |
| `osint_source_registry` | `sample_data/source_registry.csv` |
| `osint_media_signal_extracts` | `sample_data/media_signal_extracts.csv` |
| `osint_geospatial_aggregates` | `sample_data/geospatial_aggregates.csv` |

Create a few `Column` assets under each table or in the same domain:

| Table | Suggested columns |
| --- | --- |
| `osint_public_event_feed` | `event_id`, `event_date`, `region`, `event_type`, `severity`, `confidence`, `primary_source_id` |
| `osint_source_registry` | `source_id`, `source_name`, `source_category`, `license_family`, `allowed_use`, `source_reliability_score` |
| `osint_media_signal_extracts` | `signal_id`, `event_id`, `entity_text`, `entity_type`, `topic`, `extraction_confidence` |
| `osint_geospatial_aggregates` | `grid_id`, `region`, `date`, `event_count`, `hazard_score`, `aggregation_level` |

Then relate the requestable Data Sets to their columns:

1. Open the Data Set asset.
2. Find a section such as `Data Elements`, `Contains`, or `Related Assets`.
3. Add the relevant Column assets.
4. Save.

If your environment does not show that section, skip this for now and rely on attachments/descriptions. Return to it only if data basket checkout complains about missing data elements.

## 15. Create Data Product Wrappers

This is optional for the first demo. It helps you tell the "data product" story while keeping the data basket simple.

The requestable assets you already imported as `Data Set` assets are what users add to the data basket. The wrapper assets in this section are higher-level `Data Product` assets that explain the reusable mission package.

Fast path: import `collibra_import/07_data_product_wrappers.csv` into the `OSINT Data Product Catalog` domain.

Create or import these as `Data Product` assets:

- `Public Infrastructure Event Feed Product`
- `Source Reliability Scorecard Product`
- `Geospatial Situation Features Product`

For each Data Product:

1. Paste the product-card copy from `marketplace_listings.md`.
2. Create or import a matching `Data Product Port`.
3. Relate the Data Product to the Data Product Port with the output-port relation.
4. Relate the Data Product Port to the matching requestable `Data Set` if your operating model allows it.
3. Add owners and stewards.
4. Add tags.

Fast path for ports: import `collibra_import/08_data_product_ports.csv` into the `OSINT Data Product Catalog` domain.

Suggested wrapper and port relationships:

| Data Product wrapper | Output Port | Requestable Data Set |
| --- | --- | --- |
| `Public Infrastructure Event Feed Product` | `Public Infrastructure Event Feed Output Port` | `Public Infrastructure Event Feed - Curated` |
| `Source Reliability Scorecard Product` | `Source Reliability Scorecard Output Port` | `Source Reliability Scorecard` |
| `Geospatial Situation Features Product` | `Geospatial Situation Features Output Port` | `Geospatial Situation Features - Aggregated` |

Manual relationship pattern:

1. The Data Product `exposes data as` the Data Product Port.
2. The Data Product Port `is implemented as` the output asset.

If Collibra does not let you choose a `Data Set` as the implemented output asset, use the matching `Table` asset from `OSINT Technical Sample Assets`, or skip the final port-to-output relation for the first demo. The core marketplace basket flow still works from the requestable Data Sets.

In the live demo, say: "The Data Product is the business-facing package; the requestable output is represented as a Data Set in the basket."

## 16. Create Business Glossary Terms

Create terms in `OSINT Business Glossary` using `business_glossary.csv`.

Minimum terms for the demo:

- `Open Source Intelligence`
- `Publicly Available Information`
- `Source Reliability Score`
- `Corroboration Count`
- `Analytic Confidence`
- `Mission Purpose`
- `Handling Caveat`
- `Purpose Limitation`
- `License Restriction`
- `Source Citation`
- `Aggregation Level`
- `No Raw Personal Data`
- `Sensitive Analytic Inference`
- `Data Product`
- `Lineage`

For each key marketplace Data Set, add related terms:

| Data Set | Related terms |
| --- | --- |
| `Public Infrastructure Event Feed - Curated` | `Publicly Available Information`, `Corroboration Count`, `Source Reliability Score`, `Mission Purpose`, `No Raw Personal Data` |
| `OSINT Source Registry` | `Source Reliability Score`, `License Restriction`, `Source Citation` |
| `Source Reliability Scorecard` | `Source Reliability Score`, `Analytic Confidence`, `Corroboration Count` |
| `Geospatial Situation Features - Aggregated` | `Aggregation Level`, `No Raw Personal Data`, `Purpose Limitation` |
| `Raw Public Web Mentions - Restricted` | `Purpose Limitation`, `Handling Caveat`, `Sensitive Analytic Inference` |

Where to enter related terms in the current UI:

1. Open the marketplace `Data Set` asset, for example `Public Infrastructure Event Feed - Curated`.
2. Open `Summary`.
3. In the left-side section list, stay on `Overview`.
4. Scroll to `Details`.
5. Find `related to Business Asset`.
6. Click the `+` icon next to `related to Business Asset`.
7. Search for a glossary term, for example `Publicly Available Information`.
8. Select the matching `Business Term` from `OSINT Business Glossary`.
9. Save or add the relation.
10. Repeat for the rest of the related terms.

For `Public Infrastructure Event Feed - Curated`, add:

- `Publicly Available Information`
- `Corroboration Count`
- `Source Reliability Score`
- `Mission Purpose`
- `No Raw Personal Data`

After adding terms, the `related to Business Asset` table should show the selected glossary terms instead of the message `Be the first to add a relation using the plus icon (+)`.

If Collibra asks for relation direction, keep the default direction if it reads like `Data Set related to Business Asset`. The goal is simply to make the glossary terms visible from the marketplace asset.

## 17. Create Data Contract Assets

Create these as `Data Contract` assets in `OSINT Governance and Contracts`:

| Data Contract asset | Attach file |
| --- | --- |
| `Public Infrastructure Event Feed Contract` | `data_contracts/public_event_feed_contract.yaml` |
| `Source Reliability Scorecard Contract` | `data_contracts/source_reliability_scorecard_contract.yaml` |

Relate each contract to its Data Set or Data Product if your asset page offers a relation section. If not, add a clear description:

`Contract for the requestable Data Set Public Infrastructure Event Feed - Curated.`

## 18. Configure Marketplace Text and Landing Experience

Use `marketplace_listings.md` for descriptions.

Recommended featured collection labels:

- `Crisis Monitoring Starter Kit`
- `Public Source Trust Framework`
- `Narrative and Media Signals`
- `Reference Data for Sanctions and Organizations`

If your CPSH environment supports Data Marketplace landing-page configuration:

1. Go to `Settings` -> `Search` -> Data Marketplace-related settings.
2. Configure search suggestions:
   - `infrastructure disruption public reports`
   - `source reliability score`
   - `aggregated geospatial event features`
   - `license restricted media signals`
3. Configure or simulate featured assets with saved filters if available.

If landing-page configuration is not obvious, skip it. The demo still works through search.

## 19. Smoke Test as Admin

As Admin:

1. Search for `Public Infrastructure Event Feed - Curated`.
2. Confirm the asset opens.
3. Confirm it has:
   - Description
   - Status
   - Tags
   - Owner/steward responsibilities
   - Attachment or related technical fields
4. Search for `Source Reliability Score`.
5. Confirm glossary term appears.
6. Search for `Raw Public Web Mentions - Restricted`.
7. Confirm the restricted governance contrast asset appears if you included its status in Data Marketplace scope.

## 20. Smoke Test as Maya

Open an incognito/private browser or sign out and sign in as `maya.chen`.

1. Open Data Marketplace.
2. Search `infrastructure disruption public reports`.
3. Open `Public Infrastructure Event Feed - Curated`.
4. Confirm Maya can see the asset preview.
5. Click `Add to Basket`.
6. Add these assets:
   - `Public Infrastructure Event Feed - Curated`
   - `OSINT Source Registry`
   - `Source Reliability Scorecard`
   - `Geospatial Situation Features - Aggregated`
7. Open the data basket icon.
8. Click `Check out Data Basket`.
9. Use this purpose:
   - `Regional infrastructure disruption brief for crisis response planning`
10. Use this intended use:
   - `Analytic reporting and dashboarding; no individual profiling`
11. Submit.

Expected result:

- A request is submitted.
- A Data Usage asset is created automatically.
- An approval task appears for the owner/steward depending on workflow configuration.

## 21. Smoke Test as Jordan or Rafael

Sign in as `jordan.lee` or `rafael.ortiz`.

1. Open the tasks icon.
2. Look for the access request task.
3. Open it.
4. Approve the curated/aggregated products.
5. If the request includes `Raw Public Web Mentions - Restricted`, reject it or route it to privacy/legal review in your talk track.

If no task appears:

1. Confirm the requestable Data Sets have an `Owner` responsibility.
2. Confirm the owner user/group has view permissions.
3. Confirm the workflow is enabled.
4. Confirm `maya.chen` has workflow start permissions.
5. Confirm Data Basket is enabled and restricted to the correct scope.

## 22. Recommended Demo Script

Use `presenter_script.md`.

Short version:

1. Maya searches Data Marketplace for `infrastructure disruption public reports`.
2. Maya opens `Public Infrastructure Event Feed - Curated`.
3. Show description, status, tags, owner, steward, related glossary terms, and attachment/technical fields.
4. Open `Raw Public Web Mentions - Restricted`.
5. Explain why raw public web mentions are restricted.
6. Add four curated assets to the data basket.
7. Submit request with mission purpose.
8. Switch to steward/product owner and approve.
9. Close: Collibra gives analysts speed, stewards control, leaders trusted and explainable data.

## 23. Troubleshooting

Problem: `Add to Basket` is not visible.

- Check `Settings` -> `Search` -> `Actions and Preview` -> `Data Basket`.
- Make sure Data Basket is enabled.
- Make sure the asset type is `Data Set` or `Report`.
- Make sure the asset is inside the Data Marketplace scope if basket is restricted to scope.

Problem: Asset does not appear in Data Marketplace search.

- Check `Settings` -> `Search` -> `Data Marketplace Scope`.
- Confirm asset type, status, and organization are in scope.
- Confirm the user has view permission on the community/domain/asset.
- Wait briefly or refresh/reindex if search results lag.

Problem: User can log in but sees almost nothing.

- Add application global roles such as `Data Marketplace`, `Catalog`, and `Glossary`.
- Add resource responsibilities/view permissions on the OSINT community and domains.

Problem: Checkout fails.

- Confirm the user has `Workflows > Start Workflow`.
- Confirm participants have `Workflows > Participate in workflow`.
- Confirm the packaged access workflow is enabled.
- Confirm requestable Data Sets have owners.
- If the workflow expects data elements, relate Column assets to the Data Sets.

Problem: No approval task appears.

- Confirm each requested Data Set has an `Owner` responsibility.
- Confirm the owner can view the asset.
- Sign in as the owner, not just the steward.
- Check workflow status from the Data Usage asset or workflow/admin pages.

## 24. Keep the Demo Safe

Use this sentence if the customer asks about OSINT risk:

`This demo is intentionally built around synthetic, aggregated, purpose-bound OSINT products. The marketplace is positioned as a responsible-use control point: provenance, source reliability, licensing, minimization, approval, and auditability.`

Do not position the demo as individual tracking, person-level targeting, or raw public-web surveillance.

## 25. Official Reference Links

- CPSH users, roles, permissions: https://productresources.collibra.com/docs/cpsh/latest/Content/Settings/UsersAndGroups/co_user-roles-permissions.htm
- Create user: https://productresources.collibra.com/docs/collibra/latest/Content/Settings/UsersAndGroups/Users/ta_create-user.htm
- Create group: https://productresources.collibra.com/docs/collibra/latest/Content/Settings/UsersAndGroups/Groups/ta_create-group.htm
- Global roles: https://productresources.collibra.com/docs/collibra/latest/Content/Settings/RolesAndPermissions/Roles/GlobalRoles/to_global-roles.htm
- Resource roles: https://productresources.collibra.com/docs/collibra/latest/Content/Settings/RolesAndPermissions/Roles/ResourceRoles/to_resource-roles.htm
- Responsibilities: https://productresources.collibra.com/docs/cpsh/latest/Content/Responsibilities/to_responsibilities.htm
- Create communities: https://productresources.collibra.com/docs/collibra/latest/Content/Communities/ta_manage-community.htm
- Create domains: https://productresources.collibra.com/docs/collibra/latest/Content/Domains/ta_manage-domain.htm
- Operating model settings: https://productresources.collibra.com/docs/collibra/latest/Content/Settings/OperatingModel/to_operating-model-settings.htm
- Data Marketplace scope: https://productresources.collibra.com/docs/cpsh/latest/Content/DataMarketplace/ta_conf-scope.htm
- Data basket access requests: https://productresources.collibra.com/docs/collibra/latest/Content/Catalog/DataSets/ta_request-access-to-data-set.htm
- Data basket in Data Marketplace: https://productresources.collibra.com/docs/collibra/latest/Content/DataMarketplace/co_s4d-add-to-data-basket.htm
