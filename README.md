# Vehicle Insurance Data Model

This repository contains the final GitHub package for the vehicle insurance data modelling project. It keeps the submission focused: the report explains the work and the Oracle files show the model stages without uploading every working document from the local folder.

The project follows the normal modelling path:

1. Conceptual Data Model (CDM)
2. Logical Data Model (LDM)
3. Physical Data Model (PDM)
4. Oracle Database 21c DDL generation

## What is included

- `report/Final_Report.md` - final summary of the important steps, model changes, fixes, and final results.
- `oracle-files/cdm/B_CDM.zip` - Oracle SQL Developer Data Modeler export for the CDM stage.
- `oracle-files/ldm/Group B LDM.zip` - Oracle SQL Developer Data Modeler export for the LDM stage.
- `oracle-files/ldm/LDM.dmd` - Oracle model entry file available from the Oracle folder.
- `oracle-files/pdm/B_PDM.zip` - Oracle SQL Developer Data Modeler export for the PDM stage.
- `oracle-files/pdm/Oracle_B_PDM.zip` - Oracle folder copy of the PDM export.
- `oracle-files/pdm/B_DDL.ddl` - generated Oracle Database 21c DDL.

## Project summary

The model is for a vehicle insurance company. It supports customer and account management, quotes, underwriting decisions, policies, drivers, vehicles, premiums, invoices, payments, claims, endorsements, renewals, telematics, and no-claim bonus tracking.

The final physical model contains 26 tables, 32 foreign keys, primary keys for all tables, and unique constraints for important business identifiers such as vehicle registration, licence number, claim number, and agency licence number.

## Main design decisions

The design was cleaned up while moving from LDM to PDM. Fees and assistance were removed from the final physical model because they made the model heavier than needed. Payment was kept as a main entity, with Cash Payment, Card Payment, and Bank Transfer as subtypes. Customer and Account were separated properly to avoid duplication. Policy and Driver were linked through `Policy_Driver`, which makes it possible to handle main, named, and occasional drivers in a normalized way.

The final DDL was generated for Oracle Database 21c using Oracle SQL Developer Data Modeler.
