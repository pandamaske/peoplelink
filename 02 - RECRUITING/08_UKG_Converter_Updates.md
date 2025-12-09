# UKG to Talentsoft Converter - Updates Summary

## What's New

### 1. **offercustomfields.csv Generation**
The converter now generates `offercustomfields.csv` with the **Line of Business** field mapping.

#### Line of Business Mapping (CustomCodeTableValue1)
| Code | Name | Source |
|------|------|--------|
| **LOG** | Contract Logistics | Default for US, Location ending with " - CL" |
| **FFW** | Freight Management | Company Code: "SCO", Location with " - FF" |
| **SCO** | Supply Chain Optimization | Company Code: "SCO", Location with " - SCO" |
| **DIS** | Distribution & Express | Location with " - DIS" |
| **ROAD** | Road Transport | Location with " - ROAD" |
| **CORP** | Corporate | Location with " - CORP" or "Brentwood" |

**Default:** LOG (Contract Logistics) for all US operations

### 2. **HTML Stripping from Descriptions**
All HTML tags are automatically removed from `Description1` and `Description2` fields:
- Strips all HTML tags (`<p>`, `<br>`, `<div>`, etc.)
- Converts HTML entities (`&nbsp;`, `&amp;`, etc.) to plain text
- Cleans up extra whitespace

### 3. **Publication Date Validation**
Ensures data integrity for publication dates:
- **Rule:** `DefaultPublicationEndDate` must be ≥ `DefaultPublicationBeginDate` + 1 day
- **Auto-fix:**
  - Missing end date → set to begin + 30 days
  - Invalid end date → set to begin + 1 day

**Last run fixed:** 4,102 date issues

---

## How to Use

### Option 1: Run with Auto-Copy to UAT (Recommended)

```bash
cd "UKG_to_Talentsoft_Converter"
python run_and_copy_to_uat.py
```

This will:
1. Convert UKG data (outputs to temp folder)
2. Automatically copy all files to `TS_Import_Output/UAT`
3. Display summary with file locations

### Option 2: Manual Run

```bash
cd "UKG_to_Talentsoft_Converter"
python opportunity_converter.py
```

Files will be in: `C:\Users\<username>\AppData\Local\Temp\UKG_TS_Convert`

---

## Generated Files

| File | Records | Description |
|------|---------|-------------|
| `TS_Import_offer_<timestamp>.csv` | 33,952 | Main offer data |
| `TS_Import_offeruser_<timestamp>.csv` | 53,784 | User assignments (managers, recruiters) |
| `TS_Import_offercustomfields_<timestamp>.csv` | 33,952 | **NEW** - Custom fields with Line of Business |
| `TS_Import_entity_<timestamp>.csv` | 278 | Entity/location data |
| `Conversion_Report_<timestamp>.md` | - | Detailed conversion report |

---

## Line of Business Distribution (Last Run)

| LOB | Count | Percentage |
|-----|-------|------------|
| LOG (Contract Logistics) | 33,808 | 99.6% |
| FFW (Freight Management) | 83 | 0.2% |
| SCO (Supply Chain Optimization) | 61 | 0.2% |

---

## Technical Notes

### Path Length Limitations
- Windows has a 260-character path limit
- Output defaults to temp folder to avoid OneDrive long paths
- Use `run_and_copy_to_uat.py` to automatically copy to UAT folder
- Robocopy is used for copying (handles long paths better)

### File Format
- **Separator:** Semicolon (`;`) for offercustomfields.csv
- **Encoding:** UTF-8 with BOM (utf-8-sig)
- **Date Format:** `dd/mm/YYYY HH:MM:SS.000`
- **DefaultLCID:** 2057 (English UK) for consistency with existing data

---

## Example: offercustomfields.csv Structure

```csv
OfferReference;ShortText1;ShortText2;ShortText3;LongText1;LongText2;LongText3;CustomCodeTableValue1;CustomCodeTableValue2;CustomCodeTableValue3;Date1;Date2;Date3;DefaultLCID
QUALI036206;;;;;;;LOG;;;;;;2057
BUSIN048485;;;;;;;FFW;;;;;;2057
TECHN012345;;;;;;;SCO;;;;;;2057
```

### Field: CustomCodeTableValue1 (Line of Business)
- **Type:** `_TS_a04e8ea6-1965-4037-9991-fae8faa9b05b`
- **Values:** CORP, LOG, DIS, FFW, ROAD, SCO
- **Mandatory:** Yes (defaults to LOG if not determinable)

---

## Troubleshooting

### Issue: "Path too long" error
**Solution:** Use `run_and_copy_to_uat.py` which handles long paths automatically

### Issue: Files not in UAT folder
**Solution:** Check temp folder at `C:\Users\<username>\AppData\Local\Temp\UKG_TS_Convert`

### Issue: Wrong Line of Business assigned
**Solution:** Update mapping in `opportunity_converter.py`:
- `LINE_OF_BUSINESS_MAPPING` - for Company Code patterns
- `LOCATION_LOB_PATTERNS` - for Location Name patterns

---

## Support

For issues or questions:
1. Check the `Conversion_Report_<timestamp>.md` file
2. Review the `TS_Import_unmatched_emails_<timestamp>.txt` for email lookup issues
3. Contact GEODIS HCM Migration Team

---

**Last Updated:** 2025-11-24
**Version:** 2.0
