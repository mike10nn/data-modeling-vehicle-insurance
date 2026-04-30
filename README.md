# Vehicle Insurance Data Model

This repository presents a full database modelling project for a vehicle insurance company. The work covers the move from business requirements to a conceptual data model, logical data model, physical data model, and generated Oracle Database 21c DDL.

The project follows the standard modelling path:

1. Conceptual Data Model (CDM)
2. Logical Data Model (LDM)
3. Physical Data Model (PDM)
4. Oracle Database 21c DDL generation

## Project aim

The aim was to design a structured database model that can support common insurance operations, including customer onboarding, quote creation, underwriting, policy management, driver and vehicle records, billing, payments, claims, endorsements, renewals, telematics, and no-claim bonus tracking.

## What is included

- `report/Final_Report.md` - final report covering the main steps, design decisions, corrections, and final results.
- `oracle-files/cdm/B_CDM.zip` - Oracle SQL Developer Data Modeler export for the conceptual model stage.
- `oracle-files/ldm/Group B LDM.zip` - Oracle SQL Developer Data Modeler export for the logical model stage.
- `oracle-files/ldm/LDM.dmd` - Oracle model entry file from the logical model work.
- `oracle-files/pdm/B_PDM.zip` - Oracle SQL Developer Data Modeler export for the physical model stage.
- `oracle-files/pdm/Oracle_B_PDM.zip` - Oracle folder copy of the physical model export.
- `oracle-files/pdm/B_DDL.ddl` - generated Oracle Database 21c DDL.

## Final model result

- 26 physical tables
- 32 foreign keys
- Primary keys defined for all tables
- Unique constraints for key business identifiers
- Payment supertype/subtype structure
- Oracle Database 21c DDL generated from the physical model

## Main skills shown

- Data modelling from business requirements
- CDM, LDM, and PDM design
- Normalisation and relationship modelling
- Primary key, foreign key, and unique constraint design
- Oracle SQL Developer Data Modeler
- Oracle Database 21c DDL generation
- Clear documentation of model decisions and corrections

## Main design decisions

The model was cleaned up while moving from LDM to PDM. Fees and assistance were removed from the final physical model because they made the design heavier than needed. Payment was kept as a main entity, with Cash Payment, Card Payment, and Bank Transfer as subtypes. Customer and Account were separated to avoid duplication. Policy and Driver were linked through `Policy_Driver`, which makes it possible to handle main, named, and occasional drivers in a normalised way.

The final DDL was generated for Oracle Database 21c using Oracle SQL Developer Data Modeler.

## CV summary

Designed a complete vehicle insurance database model from CDM to LDM and PDM, using Oracle SQL Developer Data Modeler and generating Oracle Database 21c DDL. The final model includes 26 tables, 32 foreign keys, payment subtypes, and documented design decisions.
