# browserslist-ga-export

## Overview

Generate `browserslist-stats.json` using [Browserslist-GA](https://github.com/browserslist/browserslist-ga) without logging into a Google Account.

browserslist-ga-export allows you to generate the same [Browserslist](https://github.com/browserslist/browserslist) [custom usage data file](https://github.com/browserslist/browserslist#custom-usage-data) that Browserslist-GA would generate for a [Google Analytics view](https://support.google.com/analytics/answer/2649553?hl=en) without requiring you to log into a Google Account. Instead of logging into a Google Account, you must provide a CSV export of a [Google Analytics custom report](https://support.google.com/analytics/answer/1151300?hl=en). You may optionally provide multiple CSV files to generate a custom usage data file representing the merged data of multiple views.

## Installation

```bash
npm install browserslist-ga-export --save-dev
```

## Usage

### 1) Check user language setting

Ensure that language is set to "English (United States)" in [user language settings](https://support.google.com/analytics/answer/3210078?hl=en). See [#5](https://github.com/browserslist/browserslist-ga-export/pull/5) and [#14](https://github.com/browserslist/browserslist-ga-export/issues/14) for an explanation of why this is necessary.

### 2) Create custom report

[Create a custom report](https://support.google.com/analytics/answer/1151300?hl=en) with the specifications listed below. You will be able to use this custom report for one or more desired [Google Analytics view(s)](https://support.google.com/analytics/answer/2649553?hl=en) associated with a [Google Analytics account](https://support.google.com/analytics/topic/1009690?hl=en&ref_topic=1726911).

  - **Type**: Flat Table
  - **Dimensions** (in this order):
    1. Operating System
    2. Operating System Version
    3. Browser
    4. Browser Version
    5. Device Category
  - **Metrics**: Pageviews

### 3) Export custom report CSV file(s)

For each desired view, follow these steps to export the custom report as a CSV file:

1. View the custom report.
2. Sort the report by Browser column ascending alphabetically (arrow in column header facing up).
3. Select the desired date range for the report.
4. Show 5000 rows for the report.
5. [Export the report as a CSV file](https://support.google.com/analytics/answer/1038573?hl=en).

### 4) Convert CSV file(s) into custom usage data file

Use the browserslist-ga-export CLI to convert the CSV file(s) into a custom usage data file (`browserslist-stats.json` by default). See CLI documentation for more details.

```bash
browserslist-ga-export --reportPath {String} [options]
```

## CLI

### Commands

#### `browserslist-ga-export`

Create or update a custom usage data JSON file from one or more report CSV files given a report path and an output path.

### Options

#### `--reportPath` (`-r`)

Path or [glob](https://www.npmjs.com/package/fast-glob) path pattern of report CSV file(s) to process.

- Required
- Type: string

#### `--ignoreRows` (`-i`)

Number of rows at beginning of report CSV file(s) to exclude from processing. Default value is based on the default format of Google Analytics custom report CSV exports.

- Optional
- Type: number
- Default: `7`

#### `--outputPath` (`-o`)

Output path for generated custom usage data file.

- Optional
- Type: string
- Default: `'browserslist-stats.json'`

### Examples

```bash
browserslist-ga-export --reportPath browserslist-report.csv
```

```bash
browserslist-ga-export -r browserslist-reports/*.csv
```

```bash
browserslist-ga-export -r browser-report.csv -o browser-stats.json
```
 
```bash
browserslist-ga-export -r browser-report.csv -i 0
```
