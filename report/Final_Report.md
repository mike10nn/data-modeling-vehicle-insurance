# Final Data Modeling Report

## Scope of Review

This report summarizes the important steps, decisions, corrections, and final results found across the files in this directory. The original Word documents, PDFs, model folders, XML files, DDL files, and ZIP archives were reviewed in place. No original source data was reorganized or changed.

The directory contains the project evolution from conceptual data model (CDM), to logical data model (LDM), to physical data model (PDM), plus supporting study material and exported Oracle SQL Developer Data Modeler files.

## Files and Model Artifacts Reviewed

- Word documents reviewed: 9
- PDFs reviewed: 2
- Oracle SQL Developer Data Modeler project files: 6 `.dmd` files
- Oracle/Data Modeler XML files reviewed through model folders: 810
- DDL files reviewed: 2
- ZIP archives reviewed: 4

Main project files and folders:

- `B_CDM` and `B_CDM.zip`
- `Group B LDM` and `Group B LDM.zip`
- `B_PDM` and `B_PDM.zip`
- `Oracle`
- `GroupB_Report.docx`
- `Presentation decision.docx`
- `LDM.docx`
- `LDM attributes.docx`
- `LDM_attributes_normalized_plus relationship.docx`
- `LDM relationships modified.docx`
- `LDM presentation.docx`
- `Changes made.docx`
- `Errors.docx`
- `Data Modelling Study Guide CA2 2025-2026.pdf`
- `Data_Modelling_CA2_Answers_2025.pdf`

## Overall Project Purpose

The project models the data requirements for a vehicle insurance company. The database is intended to support policy management, customer and account management, driver and vehicle records, quotes, underwriting, premiums, invoices, payments, claims, renewals, endorsements, telematics, and no-claim bonus tracking.

The project began with a business-focused conceptual model, then moved into a normalized logical model, and finally produced an Oracle physical model with generated DDL.

## Conceptual Data Model Step

The CDM stage focused on identifying the major business objects and their relationships without committing to implementation details. The CDM report explains that the model was designed to represent what the business manages and how the main business concepts interact.

Important CDM entities included:

- Policy
- Account
- Customer
- Vehicle
- Driver
- Claim
- Payment
- Invoice
- Premium
- Quote
- Underwriting Decision
- Assistance
- Telematics
- Coverage
- Agency
- Renewal
- Location
- No Claim Bonus

The original CDM model folder contains 25 entities and 25 relationships.

Important CDM conclusions:

- The model is centered on policy lifecycle management.
- Customer, policy, vehicle, driver, claim, payment, and renewal data are the core business areas.
- The model is intended to improve data consistency, reduce ambiguity, support reporting, and provide a foundation for later logical and physical modeling.
- The design is business-focused and technology-neutral at this stage.

One presentation document explains that the team chose entities based on real vehicle insurance operations: policies, customers, vehicles, claims, renewals, payments, quotes, underwriting, and related services. It also states that normalization was used so real-world concepts such as account, driver license, and party/customer data could be represented separately.

Note: `B_CDM/Presentation decision.docx` contains an unprofessional/offensive closing sentence after the useful presentation content. It should not be included in a formal submission or presentation.

## Assumptions and Business Rules

The CDM report and LDM notes show several important assumptions:

- The model focuses on private/personal customers rather than commercial customers.
- A customer can hold multiple policies.
- A policy can involve multiple drivers and vehicles.
- A claim belongs to a policy and may involve a specific driver.
- Agencies can act as brokers, direct branches, or partners.
- The core insurance processes are assumed to remain stable: quote, underwriting, policy issue, billing, payment, claim handling, endorsement, and renewal.
- The model is intended to support Irish/EU-style compliance, reporting, and data governance needs.
- Many-to-many policy-driver logic is resolved through an associative entity.

Key business benefits identified in the report:

- Improved data consistency.
- Better decision-making through linked policy, claim, and payment data.
- Clearer development requirements.
- Better governance and compliance reporting.

## Logical Data Model Step

The LDM stage expanded the business model into a more detailed normalized structure with entities, attributes, data types, primary keys, foreign keys, and relationship rules.

The LDM model folders contain 25 entities and 38 relationships. The main LDM entities are:

- Account
- Agency
- Assistance
- Claim
- Coverage
- Customer
- Driver
- Driver_License
- Driver_Penalty
- Endorsement
- Fee
- Invoice
- Location
- No_Claim_Bonus
- Payment
- Policy
- Policy_Driver
- Premium
- Quote
- Renewal
- Staff
- Telematics
- Transaction
- Underwriting_Desion
- Vehicle

Important LDM design results:

- `Policy_Driver` was introduced as an associative entity between Policy and Driver.
- `Location` was used to store risk-related location details such as garaging, residential, or business use.
- `Driver_Penalty` stores offences and penalty points for risk assessment.
- `No_Claim_Bonus` stores claim-free history and discount-related data.
- `Telematics` stores vehicle usage and driving data that can influence renewal premium.
- `Endorsement` records mid-term policy changes.
- `Renewal` records the renewal process and new premium decisions.
- `Quote` and `Underwriting_Decision` support the pre-policy approval process.
- `Invoice`, `Payment`, and `Transaction` were used to represent billing and financial flows in the LDM.

The LDM presentation describes the intended operational flow:

1. A customer requests a quote through staff, website/direct channel, or agency.
2. Customer, account, vehicle, and driver details are collected.
3. The quote records vehicle value, coverage options, risk score, premium estimate, and staff involvement.
4. Underwriting reviews risk factors such as driver history, location risk, claims history, and vehicle risk.
5. An accepted quote becomes a policy.
6. The policy links to customer, agency, coverage, premiums, drivers, and vehicles.
7. Premium, invoice, payment, and transaction records support billing.
8. Claims are created when incidents occur and are linked back to policy and driver.
9. Endorsements record policy changes.
10. Renewals use risk changes, claim history, telematics, and no-claim bonus information.

## Relationship Step

`LDM relationships modified.docx` lists the relationship structure as all one-to-many relationships. Important relationships include:

- Customer to Policy, Quote, Invoice, Payment, No_Claim_Bonus, and Driver.
- Agency to Policy and Quote.
- Policy to Coverage, Claim, Premium, Payment, Invoice, Transaction, Renewal, Endorsement, Assistance, No_Claim_Bonus, and Telematics.
- Quote to Underwriting_Decision.
- Underwriting_Decision to Policy.
- Driver to Driver_License, Vehicle, Policy_Driver, and Claim.
- Vehicle to Telematics.
- Policy to Policy_Driver.
- Staff to Quote and Staff.
- Account to Customer and Staff.
- Payment to Transaction.
- Invoice to Transaction.
- Transaction to Fee and Renewal.

This relationship step shows that the LDM attempted to make each process traceable from customer quote through policy, billing, claims, and renewal.

## Changes Made During Refinement

`Changes made.docx` documents important model corrections made before the final physical model:

- Removed `Fees` and `Assistance` because they were considered overkill for the final design.
- Changed `Transaction` into `Sales_Transaction`.
- Connected `Sales_Transaction` to `Policy` to record sales transactions instead of general financial transactions.
- Connected `Endorsement` to `Driver_License` instead of Policy.
- Removed the relationship between Staff and Account.
- Fixed duplication between Account and Customer.
- Connected Payment only to Invoice because payments are made against invoices.
- Added unique constraints for:
  - `Vehicle_Reg`
  - `License_Number`
  - `Claim_Number`
  - `Agency.License_Number`
- Added a payment supertype/subtype structure:
  - `Payment` as the supertype.
  - `Cash_Payment`, `Card_Payment`, and `Bank_Transfer` as subtypes.
- Added `Payment_Method` to `Payment`.
- Added a check constraint so `Payment_Method` can only use cash, card, or bank transfer values.
- Removed insurance start and expiry details from Customer.

Important conclusion from this step:

The model became more normalized and more implementation-ready by removing over-complex entities, fixing duplicated customer/account data, clarifying payment structure, and adding uniqueness rules.

## Error-Fixing Step

`Errors.docx` records that the team initially had 13 errors:

- 8 unknown datatype errors.
- 2 column/name length errors.
- 3 supertype/subtype discriminator or ARC-related errors.

Datatype fixes:

- `Agency.License_Number` was assigned a description-style domain using `VARCHAR(60)`.
- `Driver.Continuous_Insurance` was assigned a domain.
- `Driver_License.License_Number` was assigned a domain because license values can include alphanumeric characters.
- `Invoice.Billing_Address_ID` was assigned an address domain.
- `Payment.Currency` was given a new currency domain using `VARCHAR(3)`.
- `Policy.Renewal_Count` was assigned a numeric domain.
- `Quote.Note` was assigned a description domain.
- `Underwriting_Decision.Note` was assigned a description domain.

Name-length fixes:

- `Underwriting_Decision_Underwriting_ID` was shortened to `UW_ID`.
- `Bank_Transfer_Payment` was shortened to `Bank_Transfer`.

Supertype/subtype fix:

- Payment subtypes created ARC/discriminator errors.
- The final solution was to delete the ARC from the diagram and then generate the DDL.

Important conclusion from this step:

The model was corrected so Oracle SQL Developer Data Modeler could generate valid DDL. The main fixes were domain assignment, shorter names, and simplifying the payment subtype implementation.

## Physical Data Model Step

The PDM stage produced Oracle Database 21c DDL. The generated DDL appears in:

- `B_PDM/B_DDL.ddl`
- `Oracle/B_PDM/B_DDL.ddl`

Both DDL files contain the same generated physical model.

The generated DDL was produced by Oracle SQL Developer Data Modeler 24.3.1.351.0831 for Oracle Database 21c.

Final PDM result:

- Tables: 26
- Foreign keys: 32
- Unique constraints: 4
- Primary keys: one defined for each table

## Final Physical Tables

| Table | Main purpose | Key results |
| --- | --- | --- |
| Account | Stores customer account contact/location details | Primary key `Account_ID` |
| Agency | Stores broker/direct/partner agency details | Unique `License_Number` |
| Bank_Transfer | Payment subtype for bank transfers | Primary key and foreign key `Payment_ID` references Payment |
| Card_Payment | Payment subtype for card payments | Primary key and foreign key `Payment_ID` references Payment |
| Cash_Payment | Payment subtype for cash payments | Primary key and foreign key `Payment_ID` references Payment |
| Claim | Stores policy/driver claim events and amounts | Unique `Claim_Number`; links to Policy and Driver |
| Coverage | Stores policy coverage details | Links to Policy |
| Customer | Stores personal customer details | Links to Account |
| Driver | Stores driver details and insurance history | Links to Customer |
| Driver_License | Stores driving license details | Unique `License_Number`; links to Driver |
| Driver_Penalty | Stores driver offences and points | Links to Driver |
| Endorsement | Stores approved policy/license-related changes | Links to Driver_License |
| Invoice | Stores billing and invoice totals | Links to Customer and Policy |
| Location | Stores address/risk location details | Primary key `Location_ID` |
| No_Claim_Bonus | Stores no-claim bonus evidence/history | Links to Customer and Policy |
| Payment | Stores payment records against invoices | Links to Invoice; includes `Payment_Method` |
| Policy | Central policy table | Links to Customer, Agency, Location, and Underwriting_Decision |
| Policy_Driver | Associative table between Policy and Driver | Links Policy and Driver with role and effective dates |
| Premium | Stores premium amount and payment schedule | Links to Policy |
| Quote | Stores quotation details | Links to Customer, Agency, and Staff |
| Renewal | Stores policy renewal details | Links to Policy |
| Sales_Transaction | Stores sales transaction records | Links to Policy |
| Staff | Stores staff details | Primary key `Staff_ID` |
| Telematics | Stores vehicle usage/telematics data | Links to Policy and Vehicle |
| Underwriting_Decision | Stores underwriting outcome and risk score | Primary key `UW_ID`; links to Quote |
| Vehicle | Stores insured vehicle details | Unique `Vehicle_Reg`; links to Driver |

## Final Foreign Key Structure

The final PDM links the model as follows:

- Customer references Account.
- Driver references Customer.
- Driver_License references Driver.
- Driver_Penalty references Driver.
- Vehicle references Driver.
- Policy references Customer, Agency, Location, and Underwriting_Decision.
- Policy_Driver references Policy and Driver.
- Coverage references Policy.
- Premium references Policy.
- Invoice references Customer and Policy.
- Payment references Invoice.
- Cash_Payment, Card_Payment, and Bank_Transfer each reference Payment.
- Claim references Policy and Driver.
- No_Claim_Bonus references Customer and Policy.
- Telematics references Policy and Vehicle.
- Renewal references Policy.
- Sales_Transaction references Policy.
- Quote references Customer, Agency, and Staff.
- Underwriting_Decision references Quote.
- Endorsement references Driver_License.

## Important Normalization Results

The files show that normalization was applied to reduce duplication and clarify ownership of data:

- Customer data was separated from Account data.
- Driver data was separated from Customer data.
- Driver licenses and penalties were separated from Driver.
- Policy and Driver were connected through `Policy_Driver` to support multiple drivers on one policy.
- Payment method details were separated into payment subtypes.
- Vehicle, location, telematics, no-claim bonus, claims, invoices, renewals, and endorsements were modeled as separate entities instead of being stored directly inside Policy.

The conclusion is that the final design is more scalable and easier to update than an unnormalized model because major business concepts are stored independently and connected through foreign keys.

## Reference Material

The study guide PDF lists the CA2 concepts expected for the assessment, including entity types, attributes, keys, relationships, cardinality, optionality, referential integrity, supertypes/subtypes, redundancy, data integrity, CDM/LDM/PDM, normalization, SQL, DDL, DML, DBMS, OLTP/OLAP, data SLA, ELT/ETL, data warehouse, data mart, data cube, data mining, and data quality.

The answer PDF gives short prepared answers for several of those topics. The project work applies many of them directly:

- Entity and relationship modeling through CDM and LDM.
- Primary keys and foreign keys in the PDM.
- Referential integrity through 32 foreign keys.
- Normalization through separate entities and associative tables.
- Supertype/subtype modeling through Payment and its payment method subtypes.
- DDL generation for Oracle Database 21c.

## Final Conclusion

The project successfully developed a vehicle insurance database model from a conceptual business design into a logical model and then into an Oracle physical database design.

The final model supports the main insurance lifecycle:

1. Customer and account setup.
2. Quote creation.
3. Underwriting decision.
4. Policy issue.
5. Driver and vehicle management.
6. Coverage and premium tracking.
7. Invoice and payment processing.
8. Claims handling.
9. Endorsements.
10. Renewals.
11. Telematics and no-claim bonus tracking.

The final PDM result is a 26-table Oracle Database 21c design with primary keys, foreign keys, unique constraints, payment subtypes, and generated DDL. The most important refinement work was removing unnecessary entities, fixing duplicate customer/account logic, clarifying the payment and transaction structure, assigning missing datatypes/domains, shortening invalid names, and resolving supertype/subtype generation errors.

Overall, the final database model is a coherent insurance operations model that connects customers, policies, vehicles, drivers, payments, claims, underwriting, and renewals in a way that supports both day-to-day transaction processing and later reporting or analysis.
