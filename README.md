# Securit Incident Dashboard — V0.3

GitHub-ready static build, based on the Securit Training Compliance dashboard authentication and visual language.

## V0.2 changes
- Jotform Submission ID is now the visible Incident Ref; SharePoint row IDs are kept internal only.
- Approved PDFs are detected from SharePoint `{HasAttachments}` and linked using the standard attachment path `<jotformID>.pdf`.
- Incident detail shows Talos AI Overview, formatted AI Statement, and the original officer statement.
- `Tester McTest` records are clearly marked as TEST — IGNORE, remain visible, and are excluded from KPIs/charts.
- Client is inferred from the site name using the agreed client-prefix rules.
- Manager field supports an Estate DB site map if the API payload also returns a `sites` array containing `siteName` and `managerName` or `managerEmail`.
- Loading progress is tuned around the current ~20 second live-flow response time.
- PDF status clearly shows `No PDF has been generated` where an attachment is absent.
- PDF Open and Download controls are available where an approved PDF is attached.

## Current incident API response
The page continues to accept the current raw SharePoint array/body response.

For Estate DB manager matching, the preferred future response shape is:

```json
{
  "incidents": [ ...incident SharePoint rows... ],
  "sites": [
    {
      "siteName": "OHS Harelaw Industrial Estate Durham",
      "managerName": "Karl Taylor"
    }
  ]
}
```

`managerEmail` can be returned instead of `managerName`; the page will convert it to a display name.

## PDF behaviour
Production PDFs are attached to the incident SharePoint row with the filename `<Jotform Submission ID>.pdf`.
The page constructs the standard SharePoint attachment URL from:
- SharePoint item ID (internal)
- `jotformID`
- `{HasAttachments}`

Users may be asked to authenticate to Microsoft 365 when opening the SharePoint PDF.

## Files
- index.html
- config.js
- securit-logo.png


## V0.3
- Supports the actual Power Automate response wrapper: `body.incidents` and `body.sites.body`.
- Manager names are generated from `managerEmail` where needed.
  - `karl.taylor@securit.email` → `Karl Taylor`
  - `darrell.sloan@securit.email` → `Darrell Sloan`
- Talos CMS site matching is authoritative for manager assignment.
- Historical site-name variations get a conservative fallback after exact matching.
- Expanded client mapping for confirmed current and legacy clients, including typo variants.
