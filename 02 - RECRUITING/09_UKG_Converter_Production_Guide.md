# Production Deployment Guide

## Overview

This guide explains how to run the UKG to Talentsoft converter for production deployment.

---

## Folder Structure

```
TS_Import_Output/
├── UAT/                                    ← Testing environment
│   ├── TS_Import_offer_<timestamp>.csv
│   ├── TS_Import_offeruser_<timestamp>.csv
│   ├── TS_Import_offercustomfields_<timestamp>.csv  ← NEW
│   ├── TS_Import_entity_<timestamp>.csv
│   └── Conversion_Report_<timestamp>.md
│
├── Archive/                                ← Archived production files
│   └── TS_Import_*_ARCHIVED_<timestamp>.csv
│
└── [PRODUCTION FILES]                      ← Current production files
    ├── TS_Import_offer_<timestamp>.csv
    ├── TS_Import_offeruser_<timestamp>.csv
    ├── TS_Import_offercustomfields_<timestamp>.csv  ← NEW
    ├── TS_Import_entity_<timestamp>.csv
    └── Conversion_Report_<timestamp>.md
```

---

## Running Production

### Step 1: Verify UAT First

Before running production, **always test in UAT**:

```bash
cd "UKG_to_Talentsoft_Converter"
python run_and_copy_to_uat.py
```

**Verify:**
- ✅ Record counts are correct
- ✅ Line of Business values are accurate (offercustomfields.csv)
- ✅ HTML is stripped from descriptions
- ✅ Publication dates are valid
- ✅ No critical errors in conversion report

---

### Step 2: Run Production Conversion

```bash
cd "UKG_to_Talentsoft_Converter"
python run_production.py
```

**What happens:**
1. Prompts for confirmation (safety check)
2. Archives existing production files to `Archive/` folder
3. Runs conversion
4. Copies new files to `TS_Import_Output/` (production)
5. Displays verification checklist

---

### Step 3: Production Verification Checklist

After production run, verify:

#### ✅ 1. Record Counts
- Check conversion report for record counts
- Compare with expected values from source

#### ✅ 2. Line of Business (NEW)
Open `TS_Import_offercustomfields_<timestamp>.csv`:
- Verify `CustomCodeTableValue1` values
- Expected distribution:
  - LOG (Contract Logistics): ~99.6%
  - FFW (Freight Management): ~0.2%
  - SCO (Supply Chain Optimization): ~0.2%

#### ✅ 3. HTML Stripping
Open `TS_Import_offer_<timestamp>.csv`:
- Check `Description1` and `Description2` columns
- Should contain NO HTML tags
- Text should be plain and readable

#### ✅ 4. Publication Dates
- Open offer.csv
- Verify: `DefaultPublicationEndDate` ≥ `DefaultPublicationBeginDate` + 1 day
- Check conversion report for number of date fixes

#### ✅ 5. Conversion Report
Open `Conversion_Report_<timestamp>.md`:
- Review field mappings
- Check for warnings
- Note any unmapped fields

#### ✅ 6. Unmatched Emails
Open `TS_Import_unmatched_emails_<timestamp>.txt`:
- Review users not found in backofficeuser.csv
- These won't be assigned to offers
- Coordinate with HR to add missing users

#### ✅ 7. File Sizes
Typical sizes for 34K offers:
- offer.csv: ~119 MB
- offeruser.csv: ~1.4 MB
- offercustomfields.csv: ~1.1 MB (NEW)
- entity.csv: ~39 KB

---

## Import to Talentsoft

### Files to Import (in order):

1. **TS_Import_entity_<timestamp>.csv**
   - Import entities/locations first
   - Module: Recruitment → Entities

2. **TS_Import_offer_<timestamp>.csv**
   - Main offer data
   - Module: Recruitment → Offers

3. **TS_Import_offercustomfields_<timestamp>.csv** ← **NEW**
   - Custom fields (Line of Business)
   - Module: Recruitment → Offers → Custom Fields

4. **TS_Import_offeruser_<timestamp>.csv**
   - User assignments (managers, recruiters)
   - Module: Recruitment → Offer Users

---

## Rollback Procedure

If issues are found after production import:

### Option 1: Restore from Archive
```bash
# Files are in TS_Import_Output/Archive/
# Copy archived files back to TS_Import_Output/
```

### Option 2: Re-run with Fixes
1. Fix the issue in converter or source data
2. Re-run production script
3. Old files are automatically archived
4. Import new files to Talentsoft

---

## Differences: UAT vs Production

| Aspect | UAT | Production |
|--------|-----|------------|
| **Output Folder** | `TS_Import_Output/UAT/` | `TS_Import_Output/` |
| **Runner Script** | `run_and_copy_to_uat.py` | `run_production.py` |
| **Confirmation** | No prompt | Requires "yes" confirmation |
| **Archive** | No archiving | Auto-archives old files |
| **Purpose** | Testing & validation | Live import to Talentsoft |

---

## Automation (Optional)

For scheduled production runs, create a Windows Task:

```bash
# Task: Daily UKG to Talentsoft Conversion
# Trigger: Daily at 2:00 AM
# Action: python "C:\...\run_production.py"
# Note: Bypasses confirmation (add --auto-confirm flag if needed)
```

⚠️ **Not recommended** without proper testing and monitoring

---

## Troubleshooting

### Issue: "Path too long" error
**Cause:** Windows 260-character limit
**Solution:** Files are first saved to temp folder, then copied via robocopy

### Issue: Archived files folder is full
**Solution:**
```bash
# Clean up archives older than 30 days
cd "TS_Import_Output/Archive"
# Manually delete old files
```

### Issue: Wrong Line of Business assigned
**Solution:**
1. Update mapping in `opportunity_converter.py`
2. Re-run UAT to test
3. Re-run production when verified

### Issue: Missing offercustomfields.csv
**Cause:** Old version of converter
**Solution:** Ensure you're using the updated version (v2.0+)

---

## Quality Metrics (Last Production Run)

Track these metrics for each production run:

| Metric | Expected | Actual |
|--------|----------|--------|
| Total Offers | ~34,000 | _____ |
| Offers with HTML stripped | 100% | _____ |
| Date fixes applied | ~4,000 | _____ |
| LOB = LOG | ~99.6% | _____ |
| LOB = FFW | ~0.2% | _____ |
| LOB = SCO | ~0.2% | _____ |
| Unmatched emails | ~800 | _____ |
| Entity codes | ~280 | _____ |

---

## Support & Contact

For issues during production:
- **Technical Issues:** Check converter logs and conversion report
- **Data Issues:** Review source UKG data
- **Mapping Issues:** Update opportunity_converter.py

**Emergency Rollback:** Use archived files from `TS_Import_Output/Archive/`

---

**Last Updated:** 2025-11-24
**Version:** 2.0
**Production Ready:** ✅ Yes
