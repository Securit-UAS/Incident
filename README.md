# Securit Incident Dashboard — V0.1

GitHub-ready static incident dashboard using the same authentication flows and localStorage session key as the Securit Training Compliance dashboard.

## Files
- `index.html`
- `config.js`
- `securit-logo.png`

## Current behaviour
- Reuses the same login / PIN change / session validation flows as Training Compliance.
- Reuses the same localStorage key (`securitTrainingAuthV1`) so a valid browser session can carry across between the two dashboards.
- Loads the current incident Power Automate endpoint.
- Supports 30/14/7/1-day client-side period filtering.
- Filters by site, client, manager, incident type and subtype.
- Search across ref, site, officer, client, manager, type, subtype and statement.
- KPI cards and simple top-type / top-site summaries.
- Full incident detail dialog.
- Jotform PDF button appears automatically if the API later provides `pdfUrl`, `PDFUrl`, `jotformPdfUrl` or `JotformPDF`.

## Data fields currently mapped
Raw SharePoint fields supported:
- `ID` -> incident ref
- `field_6` -> site
- `field_5` -> officer
- `field_7` -> incident date/time
- `field_8` -> incident type
- `field_15` -> statement
- `SITEWORK` -> subtype
- `Created` -> created timestamp

Optional enriched fields supported if added to the flow later:
- `client` / `Client` / `clientName`
- `manager` / `Manager` / `managerName`
- `pdfUrl` / `PDFUrl` / `jotformPdfUrl` / `JotformPDF`

## Important
`config.js` currently contains signed Power Automate URLs. Treat it as a test/internal build and rotate signed endpoints before any broader production deployment.
