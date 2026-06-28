# schedule-formatter

Normalizes and reformats AEC schedule exports from multiple sources into a consistent structure

```markdown
# Schedule Formatter

## Problem

AEC project teams can compare schedule exports from design
software against final bill schedules from suppliers or subcontractors.
These two documents don't always share the same column structure — different naming
conventions, different field ordering, different export formats across firms
and disciplines.

Before any comparison can happen, the formats need to be unified.

## What This Does

This tool is the first step in that comparison pipeline. It watches a Google
Drive folder for incoming schedule files, uses AI to automatically detect and
map column headers to a unified schema, and saves the normalized file back to
Google Drive, ready for the next step in the workflow.

No manual reformatting. No hardcoded column mappings. Any schedule format
in, consistent structure out.

**This specific tool runs on piping schedules, you can find sample files in the "samples" folder**

## How It Works

1. Drop a schedule Excel file into the watched Google Drive input folder
2. n8n detects the new file and downloads it
3. Claude analyzes the column headers and maps them to a standard schema
4. The normalized file is saved to the output folder
5. An email confirmation is sent with the original and output file names

## Stack

- n8n (workflow automation)
- Docker
- Claude API (column normalization)
- Google Drive (file trigger and storage)
- Gmail (email notifications)

## Setup

1. Clone the repo
2. Run `docker-compose up -d`
3. Open n8n at `http://localhost:5678`
4. Import `workflows/schedule_formatter.json`
5. Configure credentials and folders (see Configuration below)
6. Activate the workflow

## Configuration

Before running, update the following in the n8n workflow:

- **Google Drive Trigger:** point to your own input folder
- **Google Drive Upload:** point to your own output folder
- **HTTP Request node:** replace the Anthropic API key with your own (YOUR_ANTHROPIC_API_KEY)
- **Gmail node:** connect your own Gmail account

All folder connections are configured inside the n8n workflow UI —
no code changes needed.

## Sample Data

The `samples/` folder contains two realistic schedule files with deliberately
different column structures — one pipe schedule and one equipment schedule —
to demonstrate the normalization across formats.
```
