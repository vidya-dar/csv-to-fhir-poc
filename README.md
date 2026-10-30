# CSV-to-FHIR R4 ETL Pipeline (POC)

A production-style Proof of Concept (POC) demonstrating end-to-end data transformation from legacy tabular CSV datasets into standardized **HL7® FHIR® R4** JSON resources and bundle structures.

---

## 📌 Project Overview

In enterprise healthcare IT, clinical and demographic data frequently originate from disparate database exports and legacy file transfers. This repository demonstrates a modular, scalable Python-based ETL (Extract, Transform, Load) pipeline designed to extract flat clinical CSV files, map data elements according to HL7 FHIR R4 specifications, and output validated FHIR JSON resources.

### Key Capabilities
* **Multi-Resource Data Transformation:** Processes 5 relational healthcare domains:
  * `Patient` (Demographics & Patient Identifiers)
  * `Practitioner` (Provider Details & Identifiers)
  * `PractitionerRole` (Provider Specialties & Facility Affiliations)
  * `Encounter` (Clinical Visit Metadata, Linked to Patient & Provider)
  * `Observation` (Vitals & Clinical Findings, Linked to Patient & Encounter)
* **Relational Reference Mapping:** Establishes cross-resource references (e.g., linking an `Observation` to its parent `Encounter` and `Patient`).
* **Modular Codebase:** Implements single-responsibility mappers per resource for easy testing, debugging, and maintenance.

---

## 📂 Repository Structure

This repository follows standard software engineering layout practices for healthcare data integration:

```text
csv-to-fhir-poc/
├── README.md                      # Project documentation & overview
├── spec/                          # Data mapping specifications
│   └── fhir_5_resource_mapping.xlsx # Field-level source-to-target matrix
├── src/                           # Python ETL transformation logic
│   ├── patient_mapper.py          # CSV to FHIR Patient resource logic
│   ├── practitioner_mapper.py     # CSV to FHIR Practitioner resource logic
│   ├── practitioner_role_mapper.py# CSV to FHIR PractitionerRole resource logic
│   ├── encounter_mapper.py        # CSV to FHIR Encounter resource logic
│   └── observation_mapper.py      # CSV to FHIR Observation resource logic
├── schemas/                       # JSON Schema & FHIR validation profiles
│   └── fhir_r4_schemas.json       # Structural validation definitions
└── samples/                       # Test datasets & pipeline outputs
    ├── input/                     # Source CSV test files (5 domains)
    │   ├── patients.csv
    │   ├── practitioners.csv
    │   ├── practitioner_roles.csv
    │   ├── encounters.csv
    │   └── observations.csv
    └── output/                    # Transformed FHIR JSON outputs
        ├── patient_bundle.json
        ├── practitioner_bundle.json
        ├── role_bundle.json
        ├── encounter_bundle.json
        └── observation_bundle.json
