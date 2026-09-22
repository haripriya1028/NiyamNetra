# NiyamNetra 

### OCR-Based Packaged Commodity Compliance Checker

NiyamNetra is an OCR-powered compliance checking system designed to verify whether packaged commodity labels contain the declarations required under Legal Metrology and Packaged Commodities regulations.

The system takes images of a product package, extracts relevant information using OCR, validates the extracted declarations against predefined compliance rules, and generates an explainable compliance result highlighting missing, invalid, or potentially non-compliant information.

---

## Key Features

- **Image-Based OCR**
  - Extracts text from product package images.
  - Supports front and back label images.
  - Uses image preprocessing to improve OCR accuracy.

- **Declaration Extraction**
  - Identifies important packaged-commodity declarations such as:
    - Manufacturer / Packer / Importer details
    - Net quantity
    - Maximum Retail Price (MRP)
    - Date of manufacture / packing / import
    - Consumer care information
    - Other mandatory declarations

- **Compliance Validation**
  - Checks extracted information against predefined Legal Metrology compliance rules.
  - Detects missing or invalid declarations.
  - Evaluates whether required information is present in the expected format.

- **Explainable Results**
  - Provides a clear compliance status.
  - Identifies missing or problematic declarations.
  - Provides reasons behind the compliance result instead of only displaying a pass/fail outcome.

- **Risk Assessment**
  - Generates a compliance risk indication based on detected issues.

---

## System Workflow

```text
Product Package Images
        │
        │
        ▼
┌─────────────────────────┐
│   Image Preprocessing   │
│        OpenCV           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│       OCR Engine        │
│       PaddleOCR         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Text & Declaration     │
│      Extraction         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│   Compliance Engine     │
│   Rule-Based Validation │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│   Compliance Analysis   │
└────────────┬────────────┘
             │
       ┌─────┼─────┐
       ▼     ▼     ▼
    Status  Risk  Explanation
    Result  Level & Missing Items
```

## OCR Pipeline

NiyamNetra uses PaddleOCR to extract textual information from product packaging.

The OCR pipeline consists of:

1. Image Input

Front and back images of the product package are provided as input.

2. Image Preprocessing

OpenCV-based image preprocessing is used to improve the quality of package images and make text easier to detect.

3. Text Detection and Recognition

PaddleOCR detects text regions within the package image and recognizes the text present in those regions.

4. Text Processing

The extracted text is cleaned and processed before being passed to the compliance module.

5. Declaration Identification

Relevant declarations are identified from the extracted package information.

Examples include:

Manufacturer / Packer / Importer
Net quantity
MRP
Manufacturing / Packing / Import date
Consumer care details
6. Compliance Validation

The extracted declarations are passed to the compliance engine, where they are checked against predefined compliance rules.

## Compliance Engine

The compliance engine evaluates whether the required declarations are present and satisfy the defined validation rules.

## ⚖️ Compliance Engine

The compliance engine evaluates whether the required declarations are present and satisfy the defined validation rules.

| Declaration | Validation |
|-------------|------------|
| Manufacturer | Required details are present |
| Net Quantity | Quantity and unit are available |
| MRP | MRP declaration is present |
| Date | Manufacturing / packing / import date is provided |
| Consumer Care | Required consumer contact information is available |
| Mandatory Declarations | Required information is not missing |

The system maps extracted information to specific compliance requirements and generates an explanation of the detected issues.

## Compliance Result

A typical analysis can provide a result such as:

Compliance Status : Needs Attention

Risk Level        : Medium

Issues Detected:

✓ Manufacturer details found
✓ Net quantity found
✓ MRP found
✗ Consumer care information missing
✗ Date declaration incomplete

Recommendation:

Review the missing mandatory declarations
before the product is listed or distributed.

The explainable result allows users to understand why a package was flagged instead of receiving only a binary pass/fail result.

## User Portals

NiyamNetra supports different user roles through dedicated portals.

Consumer Portal

Allows consumers to check product packaging information and identify potential declaration issues.

Manufacturer Portal

Helps manufacturers and businesses verify package declarations before products are released or listed.

Government Authority Portal

Provides authorities with a dedicated interface to review compliance information and identify potential violations.

## Tech Stack
- **Backend**
  -Python
  -FastAPI
  -OCR and Image Processing
  -PaddleOCR
  -OpenCV
- **Database and Authentication**
  -MongoDB
  -JWT Authentication
- **Other**
  -REST APIs
  -Rule-Based Compliance Validation
  -Image Processing
  -Text Extraction
## Project Structure
```text
NiyamNetra/
│
├── backend/
│   ├── api/
│   ├── routes/
│   ├── services/
│   ├── ocr/
│   ├── compliance/
│   └── main.py
│
├── frontend/
│   ├── consumer/
│   ├── manufacturer/
│   └── authority/
│
├── models/
│
├── utils/
│
├── requirements.txt
└── README.md
```

## Example Use Case

A manufacturer uploads images of a packaged food product.

NiyamNetra performs the following steps:

Receives the package images.
Preprocesses the images.
Extracts text using PaddleOCR.
Identifies declarations such as MRP, net quantity, manufacturer details, and dates.
Compares the extracted information against defined compliance requirements.
Detects missing or potentially invalid declarations.
Generates a compliance status and risk level.
Provides an explanation of the detected issues.

This enables an initial compliance check before a product reaches consumers or enters the market.

## Objectives

NiyamNetra aims to:

Automate the initial verification of packaged commodity declarations.
Reduce the manual effort involved in checking product labels.
Use OCR to convert package images into structured compliance information.
Detect missing or potentially invalid declarations.
Provide explainable compliance results.
Support manufacturers, consumers, and regulatory authorities.
## Future Scope
Improve OCR accuracy for low-quality and curved package images.
Support multiple Indian languages.
Expand regulatory rule coverage.
Automate extraction of additional product attributes.
Improve handling of complex package layouts.
Add historical compliance reports and analytics.
Integrate with product listing and verification platforms.
Add advanced image and document quality checks.
## Project Highlights

NiyamNetra combines:

Computer Vision + OCR + Rule-Based Validation + Explainable Compliance

to transform product package images into actionable compliance insights.

The system focuses on making packaged-commodity compliance faster, structured, and easier to understand.
