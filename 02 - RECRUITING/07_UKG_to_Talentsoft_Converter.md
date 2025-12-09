# UKG to Talentsoft Converter

## Overview

This converter transforms UKG recruitment data exports into Talentsoft-compatible CSV import files. It was developed as part of the GEODIS HCM migration project.

## Generated Files

The converter produces the following output files:

| File | Description | Records Generated |
|------|-------------|-------------------|
| `TS_Import_offer_*.csv` | Talentsoft offer/vacancy records | 33,952 |
| `TS_Import_offeruser_*.csv` | Manager/Recruiter/Supervisor assignments | 116,101 |
| `TS_Import_entity_*.csv` | Company/Location entity records | 278 |
| `Conversion_Report_*.md` | Detailed mapping and conversion report | - |

## Field Mapping (UKG -> Talentsoft)

### Offer Fields

| Talentsoft Field | UKG Source Field | Status |
|------------------|------------------|--------|
| OfferReference | Requisition Number | Mapped |
| CreationDate | Created Date | Mapped |
| JobTitle | Opportunity Title | Mapped |
| Description1 | Detailed Description | Mapped |
| Description2 | Short Description | Mapped |
| EEOCode | EEO Category Code | Mapped |
| ProfessionalCategory | EEO Category | Mapped |
| JobTime | Full-Time Or Part-Time | Mapped |
| Contract | Salary Or Hourly | Mapped |
| NumberOfVacancies | Maximum Headcount | Mapped |
| BeginningDate | Target Start Date | Mapped |
| RecruitingReason | Reason For Opening | Mapped |
| Entity | Company Code | Mapped |
| JobLocation | Location Name | Mapped |
| EducationLevel | Education Required | Mapped |
| ExperienceLevel | Minimum Years | Mapped |
| OperationalManagerEmail | Email Address (Opportunity Hiring Manager) | Mapped |
| DefaultPublicationBeginDate | First Published Date | Mapped |
| DefaultPublicationEndDate | Closed Date | Mapped |
| FreeCriteria1 | Job Family Code | Mapped |
| FreeCriteria2 | Job Family | Mapped |

### Value Transformations

**JobTime:**
- Full-Time -> `_TS_CO_JobTime_FullTime`
- Part-Time -> `_TS_CO_JobTime_PartTime`

**Contract:**
- Salary -> `FTRCDI` (Permanent)
- Hourly -> `FTTCDD` (Temporary)

**ProfessionalCategory:**
- Executive/Senior-Level Officials and Managers -> `_TS_CO_ProfessionalCategory_Executive`
- First/Mid-Level Officials and Managers -> `_TS_CO_ProfessionalCategory_Manager`
- Professionals -> `_TS_CO_ProfessionalCategory_Professional`
- Technicians -> `_TS_CO_ProfessionalCategory_Technician`
- Sales Workers -> `_TS_CO_ProfessionalCategory_Sales`
- Administrative Support Workers -> `_TS_CO_ProfessionalCategory_Admin`
- Operatives -> `_TS_CO_ProfessionalCategory_Operative`

## Usage

### Command Line

```bash
python opportunity_converter.py "path/to/Opportunity Detail.csv"
```

### Output Location

Files are generated in: `C:\Users\<username>\AppData\Local\Temp\UKG_TS_Convert\`

## Files in this Directory

- `opportunity_converter.py` - Main converter script for Opportunity Detail reports
- `ukg_to_talentsoft_converter.py` - Generic converter framework
- `README.md` - This documentation file

## Source Data Requirements

### UKG Opportunity Detail.csv

Expected columns (58 total):
- Requisition Number
- Created Date
- Opportunity Title
- Detailed Description
- Short Description
- EEO Category Code / EEO Category
- Full-Time Or Part-Time
- Salary Or Hourly
- Maximum Headcount
- Target Start Date
- Company Code
- Location Name
- Email Address (Opportunity Hiring Manager)
- Email Address (Recruiter)
- Email Address (Opportunity Supervisor)
- Email Address (Opportunity Onboarding Owner)
- Job Family Code / Job Family
- And more...

## Talentsoft Import Format

The output files follow the Talentsoft recruitment module import specifications:
- CSV format (comma-delimited with UTF-8 BOM)
- Date format: `DD/MM/YYYY HH:MM:SS.000`
- Reference values use `_TS_CO_*` prefix

## Related Documentation

- `UKG_Talentsoft_Holistic_Mapping_CORRECTED.xlsx` - Complete field mapping
- `UKG_Talentsoft_Gap_Analysis_UPDATED.md` - Gap analysis documentation
- `UKG_Talentsoft_Field_Definitions.md` - Field definitions and WordPlus tags
- `Doc_Export_Import_Rec_FR.xlsx` - Talentsoft import specifications

## Version History

- **v1.0** (2025-11-23): Initial release with Opportunity Detail converter
  - Converted 34,296 source records
  - Generated 33,952 unique offers
  - Extracted 278 entities
  - Created 116,101 user role assignments

## Author

GEODIS HCM Migration Team
