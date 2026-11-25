# ClinicalTrials.gov Scraper & Unofficial API (Python, Node.js, MCP)

[Run ClinicalTrials.gov Scraper - Clinical Study Data API on Apify](https://apify.com/evpp/clinicaltrials-gov) to export ClinicalTrials.gov data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/clinicaltrials-gov)

[Open the documentation and crawlable sample explorer](https://intius.github.io/evp-labs-data-extractors/actors/clinicaltrials-gov/) for quick inputs, integration links, real sample rows, and ready-made task examples.

## Why use this ClinicalTrials.gov scraper?

- Export ClinicalTrials.gov data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25+ row sample dataset to prototype before running the live Actor

Built for Pharma/biotech competitive intel teams, CROs, investors tracking pipelines, patient-recruitment agencies.

## Quick start on Apify

Open [https://apify.com/evpp/clinicaltrials-gov](https://apify.com/evpp/clinicaltrials-gov) and use this input:

```json
{
  "condition": "lung cancer",
  "status": "RECRUITING",
  "country": "United States",
  "maxItems": 10
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/clinicaltrials-gov"
    }
  }
}
```

Then ask your agent to run `evpp/clinicaltrials-gov`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/clinicaltrials-gov`.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `nctId` | string | NCT number, the unique ClinicalTrials.gov identifier |
| `briefTitle` | string | Short title of the study |
| `officialTitle` | string | Full official title of the study |
| `orgStudyId` | string | Sponsor's internal study identifier |
| `url` | string | ClinicalTrials.gov study page URL |
| `overallStatus` | string | Recruitment status (RECRUITING, COMPLETED, TERMINATED, ...) |
| `leadSponsor` | string | Name of the lead sponsor organization |
| `leadSponsorClass` | string | Sponsor class (INDUSTRY, NIH, OTHER_GOV, OTHER, ...) |
| `collaborators` | string[] | Collaborating organizations listed on the study |
| `conditions` | string[] | Conditions or diseases studied |
| `keywords` | string[] | Keywords assigned to the study |
| `phases` | string[] | Trial phases (PHASE1, PHASE2, PHASE3, PHASE4, NA) |
| `studyType` | string | Study type (INTERVENTIONAL, OBSERVATIONAL, EXPANDED_ACCESS) |
| `enrollmentCount` | integer | Planned or actual enrollment size |
| `enrollmentType` | string | Whether enrollmentCount is ESTIMATED or ACTUAL |
| `startDate` | string | Study start date (ISO) |
| `completionDate` | string | Study completion date (ISO, estimated or actual) |
| `lastUpdateDate` | string | Date the record was last updated on ClinicalTrials.gov |
| `locationsCount` | integer | Number of recruitment sites listed |
| `countries` | string[] | Unique countries where the study has sites |
| `interventionNames` | string[] | Unique intervention/drug names tested |
| `primaryOutcomes` | string[] | Primary outcome measures |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "nctId": "NCT07041606",
  "briefTitle": "An Observational Study of Molecular profIling of Advanced and aggRessive ENdometrial Cancer and 1-st Line Treatment Approaches in Russian Federation",
  "officialTitle": "Multicenter, Observational, Prospective Study of Molecular Profiling in Advanced and Aggressive Endometrial Cancer Patients and 1-st Line Treatment Approaches in Russian Federation",
  "orgStudyId": "D0817R00117",
  "url": "https://clinicaltrials.gov/study/NCT07041606",
  "overallStatus": "RECRUITING",
  "leadSponsor": "AstraZeneca",
  "leadSponsorClass": "INDUSTRY",
  "conditions": [
    "Endometrial Cancer"
  ],
  "studyType": "OBSERVATIONAL",
  "enrollmentCount": 500,
  "enrollmentType": "ESTIMATED",
  "startDate": "2025-06-24",
  "completionDate": "2027-06-30",
  "lastUpdateDate": "2026-09-08",
  "locationsCount": 19,
  "countries": [
    "Russia"
  ],
  "primaryOutcomes": [
    "The rate of POLEm positive status",
    "The rate of dMMR status and pMMR status detected by IHC and by combined approach of molecular classification",
    "The rate of p53abn positive status detected by IHC and by combined approach of molecular classification",
    "The rate of PD-L1 positive status detected by IHC",
    "The rate of HER2 expression 3+ detected by IHC"
  ]
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25+ row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/clinicaltrials-gov

## Responsible use

The Actor reads public data from `clinicaltrials.gov`. Review the source site's terms and applicable privacy rules before production use.
