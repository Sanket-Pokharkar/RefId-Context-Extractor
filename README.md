# RefId Context Extractor

A lightweight, browser-based log analysis tool for searching and highlighting transaction reference IDs and financial posting types in log files.

## Overview

This tool helps system administrators and developers quickly extract and analyze relevant context from large log files by:
- Searching for exact value matches (RefID, EndToEndId, or any identifier)
- Extracting surrounding context (configurable lines before/after)
- Highlighting financial transaction types (Debit, Credit, Fees Posting)
- Tracking batch accounting entries (PAYMENTHUB_TEST.BATCH_ACCOUNTING)
- Exporting extracted logs with intelligent filename generation

## Features

### Search Capabilities
- **Flexible RefID Input**: Supports 6 different formats
  - Plain text: `123456`
  - XML tags: `<refId>123456</refId>` or `<anyTag>value</anyTag>`
  - JSON (double quotes): `"key": "value"`
  - JSON (single quotes): `'key': 'value'`
  - Curly braces: `{key: "value"}`
  - Square brackets: `[value]`

- **Intelligent Parsing**: Automatically extracts values and handles:
  - Quoted strings with surrounding quotes
  - Trailing commas
  - Case-insensitive matching (optional)

### Context Extraction
- Configurable lines before first match (default: 100)
- Configurable lines after last match (default: 100)
- Displays extracted line range and statistics

### Highlighting
- **RefID match**: Sky blue highlight
- **Debit Posting** (DP1/DP2/DP3): Red highlight (up to 3 occurrences)
- **Credit Posting** (CP1/CP2/CP3): Orange highlight (up to 3 occurrences)
- **Fees Posting** (FP1/FP2/FP3): Pink highlight (up to 3 occurrences)
- **BATCH_ACCOUNTING** (BA): Blue highlight

### File Operations
- **Upload**: Load .txt log files
- **Download**: Export extracted logs as `.txt`
- **Smart Naming**: 
  - If `fileName:` field exists in logs: `ACH_[name]_Logs.txt`
  - Otherwise: `refid_context_[timestamp].txt`
- **Copy**: Copy extracted text to clipboard
- **Select All**: Select all output text

## Project Structure

```
.
├── index.html          # HTML markup (main UI)
├── styles.css          # CSS styling (clean, responsive design)
├── script.js           # JavaScript logic (file I/O, searching, highlighting)
└── README.md           # This file
```

## Usage

1. **Open** `index.html` in a web browser
2. **Upload** a `.txt` log file using the file input
3. **Enter** your search value (supports 6 format types)
4. **(Optional)** Adjust context lines (before/after match)
5. **(Optional)** Enable case-insensitive matching
6. **Click** "Extract Context" to search and highlight
7. **Navigate** using posting type buttons (DP1, CP1, FP1, BA, etc.)
8. **Download** or copy the extracted results

## Technical Details

### Core Functions

| Function | Purpose |
|----------|---------|
| `extractValueFromTag()` | Extracts value from any of 6 input formats |
| `parseRightSide()` | Parses colon-separated key:value pairs |
| `navigateToOccurrence()` | Scrolls to Nth occurrence of a highlight |
| `setStatus()` | Updates user feedback messages |

### File Handling
- Reads `.txt` files in browser (no server upload)
- Handles both Windows (`\r\n`) and Unix (`\n`) line endings
- Displays file statistics (line count, character count)

### Performance
- Works entirely in browser (no backend required)
- Handles files with thousands of lines
- Smooth scrolling with centered focus

## Browser Compatibility

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Requires JavaScript enabled
- Uses standard HTML5 File API

## Security

- **Runs locally**: All processing happens in your browser
- **No data transmission**: Files never leave your computer
- **No server required**: Completely offline-capable

## Future Enhancements

- [ ] Multiple file comparison
- [ ] Export to CSV/JSON formats
- [ ] Search history/saved queries
- [ ] Advanced regex support
- [ ] Dark mode theme
- [ ] Batch file processing

## Author Notes

This tool is optimized for payment system log analysis, specifically for:
- ACH (Automated Clearing House) processing
- Financial transaction reconciliation
- Payment hub audit trails

Last Updated: March 2026
