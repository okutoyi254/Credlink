**MASINDE MULIRO UNIVERSITY OF SCIENCE AND TECHNOLOGY**
 
**[SCHOOL / FACULTY NAME]**
 
**DEPARTMENT OF [DEPARTMENT NAME]**
 
**BIT 420: IT PROJECT II**
 
**SOFTWARE REQUIREMENTS SPECIFICATION**
 
**AI-POWERED FINANCIAL IDENTITY AND CREDIT-ASSESSMENT MIDDLEWARE PLATFORM FOR INFORMAL TRADERS IN KENYA**
 
**Version 1.0**
 
**PREPARED BY**
 
[MEMBER 1 FULL NAME] – [REG. NO.]
 
[MEMBER 2 FULL NAME] – [REG. NO.]
 
[MEMBER 3 FULL NAME] – [REG. NO.]
 
SUPERVISOR(S): [SUPERVISOR NAME(S)]
 
**[MONTH, YEAR]**
 
# REVISION HISTORY
 
| **Version** | **Date**                           | **Author(s)**                      | **Description**                                     |
|-------------|------------------------------------|------------------------------------|-----------------------------------------------------|
| 0.1         | [date] | [team] | Initial draft from project description and proposal |
| 1.0         | [date] | [team] | Baseline for supervisor review                      |
 
# 1. INTRODUCTION
 
## 1.1 Purpose
 
This Software Requirements Specification (SRS) describes the functional and non-functional requirements of the AI-powered Financial Identity and Credit-Assessment Middleware Platform (“the System”). It is the agreed basis for design, implementation, testing and acceptance of the prototype, and is intended for the project team, the supervisors and examiners. It follows the structure recommended by ISO/IEC/IEEE 29148:2018 and is consistent with the BIT 420 project proposal.
 
## 1.2 Scope
 
The System helps informal traders (mama mboga, kiosk operators, milk vendors, small retailers, boda boda operators) record their business activity, understand their business through simple insights, and progressively build a verifiable financial history. From that history it generates a standardised Financial Credibility Profile, an explainable Low, Medium or High risk assessment, and a separate profile-confidence indicator. Authorised financial institutions can access a trader’s profile through a lender portal and secure APIs, only with the trader’s consent.
 
**In scope:** trader profile and record management; provenance classification and data-quality checks; dashboard insights and alerts; financial history; credibility profile; ML risk assessment with explanations; profile confidence; consent management; lender portal; secure API layer; access logging; system administration.
 
**Out of scope:** making or recording final lending decisions; disbursing loans; independently verifying physical cash; replacing credit reference bureau or KYC processes; production-scale integration with M-PESA or bank systems (handled through statement import and sandbox or simulated integrations in the prototype).
 
## 1.3 Definitions, Acronyms and Abbreviations
 
| **Term**                      | **Definition**                                                                                                                                                           |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Trader                        | An informal business owner who registers on the System and records business activity.                                                                                    |
| Institution                   | A bank, SACCO, microfinance institution or other lender registered to use the System.                                                                                    |
| Self-reported                 | Information entered by the trader that the System cannot independently verify (e.g. cash sales).                                                                         |
| Verifiable                    | Information obtained from an independently attributable source, such as an M-PESA/Till record or a bank record imported or integrated through an authorised channel.     |
| Derived                       | Information calculated by the System from other records (e.g. average monthly revenue).                                                                                  |
| Financial Credibility Profile | A standardised summary of a trader’s business information, financial indicators, verified and self-reported activity, data completeness, confidence and risk indicators. |
| Risk assessment               | An advisory classification (Low, Medium, High) produced by the ML model, with contributing factors.                                                                      |
| Profile confidence            | An indicator of how reliable the available evidence is, independent of risk.                                                                                             |
| Consent                       | A trader’s recorded authorisation for a specific institution to access specified profile data.                                                                           |
| API                           | Application Programming Interface.                                                                                                                                       |
| CRB                           | Credit Reference Bureau.                                                                                                                                                 |
| DPA                           | Kenya Data Protection Act, 2019.                                                                                                                                         |
| JWT                           | JSON Web Token.                                                                                                                                                          |
| ML                            | Machine Learning.                                                                                                                                                        |
| RBAC                          | Role-Based Access Control.                                                                                                                                               |
| SHAP                          | SHapley Additive exPlanations, a method for explaining model predictions.                                                                                                |
 
## 1.4 References
 
- Project Description and Scope Definition, BIT 420 IT Project II.
- BIT 420 IT Project II Proposal (this project).
- ISO/IEC/IEEE 29148:2018, Systems and software engineering – Life cycle processes – Requirements engineering.
- Government of Kenya. (2019). The Data Protection Act, 2019.
- Central Bank of Kenya. (2013). The Credit Reference Bureau Regulations, 2013.
## 1.5 Document Overview
 
Section 2 gives an overall description of the product. Section 3 specifies external interfaces. Section 4 specifies functional requirements by feature. Section 5 gives use cases. Section 6 specifies data requirements and business rules. Section 7 specifies non-functional requirements. Section 8 covers legal and ethical requirements. Appendices contain traceability and open issues.
 
# 2. OVERALL DESCRIPTION
 
## 2.1 Product Perspective
 
The System is a new, self-contained web-based platform that acts as middleware between traders and financial institutions. It does not replace institutional systems; it supplies an additional, structured source of information. It interacts with three external parties: traders (data owners), institutions (data consumers, via portal and API) and data sources (manual entry, M-PESA/Till statements and bank statements).
 
## 2.2 Product Functions (Summary)
 
- Register traders and maintain business profiles.
- Record, import and classify financial activity by source and verification level.
- Validate data quality and flag anomalies and conflicts.
- Provide dashboard insights and business alerts.
- Build a longitudinal financial history and credibility profile.
- Produce explainable ML risk assessments and a separate profile-confidence level.
- Manage trader consent and log every access.
- Expose profiles to institutions through a lender portal and secure APIs.
- Provide administration, monitoring and model-version management.
## 2.3 User Classes and Characteristics
 
| **User class**            | **Characteristics**                                                                                                                          | **Privileges**                                                                                                                    |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Trader                    | Informal business owner; limited technical skill; primarily uses a smartphone; may have low literacy in English (Swahili support desirable). | Own profile, records, dashboard, alerts, consent decisions.                                                                       |
| Institution user          | Credit officer or analyst; moderate technical skill; uses desktop.                                                                           | Search traders, request access, view consented profiles, use API.                                                                 |
| Institution administrator | Manages the institution’s users and API credentials.                                                                                         | Manage institution users and credentials.                                                                                         |
| System administrator      | Technical staff managing the platform.                                                                                                       | Manage users, institutions, models, permissions; view monitoring and logs. No access to profile content without a consent record. |
 
## 2.4 Operating Environment
 
- Server: Linux or Windows server (or cloud VM), Java 17 runtime, PostgreSQL, Python 3 ML service.
- Client: current versions of Chrome, Firefox or Edge on desktop; Android and iOS mobile browsers.
- Network: HTTPS over the internet; low-bandwidth tolerant.
## 2.5 Design and Implementation Constraints
 
- Must comply with the Kenya Data Protection Act, 2019.
- Backend in Java/Spring Boot; ML service in Python; PostgreSQL database; React front end (subject to team confirmation).
- Open-source tools only, to keep within the project budget.
- Delivery within the 28-week semester.
- Official M-PESA or bank API access may not be available; imports or simulation are used.
## 2.6 Assumptions and Dependencies
 
- Traders have access to an internet-enabled smartphone or computer.
- M-PESA/Till and bank statements can be exported in a known format (CSV or PDF) for import. [Confirm the format(s) you will support.]
- A synthetic dataset, informed by field research, is acceptable for training and evaluating the prototype model.
- Institutions in the prototype are simulated or pilot institutions.
## 2.7 Business Rules
 
**Table 2.1: Business rules**
 
| **ID** | **Rule**                                                                                                                                                                                                                                          |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BR-01  | The System is advisory. It shall not make, record or imply a final lending decision.                                                                                                                                                              |
| BR-02  | Cash transactions shall always be classified as self-reported. The System shall not claim to verify physical cash.                                                                                                                                |
| BR-03  | Mobile-money (M-PESA/Till) records obtained from an imported or integrated statement shall be classified as verifiable; bank records shall be verifiable only through an authorised integration or imported record.                               |
| BR-04  | Calculated indicators shall be classified as derived.                                                                                                                                                                                             |
| BR-05  | Risk assessment and profile confidence shall be computed and shown separately.                                                                                                                                                                    |
| BR-06  | An institution may view a profile only while a valid, unexpired and non-revoked trader consent exists for that institution and scope.                                                                                                             |
| BR-07  | Every access request and decision shall be logged, including denied requests.                                                                                                                                                                     |
| BR-08  | A Financial Credibility Profile shall be generated only for eligible traders: at least 30 days of recorded history and at least 20 transactions. [Thresholds are initial values to be confirmed with the supervisor.] |
| BR-09  | Default consent validity shall be 30 days, after which access ends unless the trader renews it.                                                                                                                                                   |
 
# 3. EXTERNAL INTERFACE REQUIREMENTS
 
## 3.1 User Interfaces
 
| **ID** | **Interface**                 | **Description**                                                                                                 |
|--------|-------------------------------|-----------------------------------------------------------------------------------------------------------------|
| UI-01  | Trader registration and login | Simple forms with validation messages; password reset.                                                          |
| UI-02  | Business profile screen       | Form for business details and payment channels.                                                                 |
| UI-03  | Record entry screens          | Quick entry for cash sales, expenses, stock, debts; import screen for statements.                               |
| UI-04  | Trader dashboard              | Revenue, expense, surplus, trends, cash-to-digital ratio, alerts, charts.                                       |
| UI-05  | Consent screen                | Pending requests with institution name, data requested and approve/reject; list of active consents with revoke. |
| UI-06  | Profile view (trader)         | The trader’s own credibility profile, confidence and risk factors.                                              |
| UI-07  | Lender portal                 | Search, request access, review profile, trends, risk, confidence, explanation factors.                          |
| UI-08  | Admin console                 | Users, institutions, permissions, model versions, logs, data-quality issues.                                    |
 
User interfaces shall be responsive, use consistent navigation, and use plain language. Swahili labels are a desirable enhancement.
 
## 3.2 Hardware Interfaces
 
The System has no direct hardware interfaces. It is accessed through standard devices with a web browser.
 
## 3.3 Software Interfaces
 
- PostgreSQL database accessed through JDBC/JPA.
- Internal REST interface between the Spring Boot backend and the Python ML service (JSON over HTTP).
- M-PESA/Till and bank statement import (CSV/PDF parsing); optional sandbox integration, e.g. the Safaricom Daraja sandbox, if access is obtained.
- Email or SMS gateway for notifications (optional, simulated in the prototype).
## 3.4 Communications Interfaces
 
- All client-server and API communication over HTTPS (TLS).
- Institution API uses token-based authentication (JWT or OAuth 2.0 client credentials) with JSON request and response bodies.
- API documented with OpenAPI/Swagger.
# 4. FUNCTIONAL REQUIREMENTS
 
Requirements are numbered to align with the FR identifiers in the project proposal (e.g. FR-03 in the proposal is detailed as FR-03.1 and FR-03.2 here). The words “shall” denote mandatory requirements.
 
## 4.1 Trader Registration and Business Profile
 
Allows a trader to create an account and maintain the business profile that forms the basis of their financial identity. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                                                                                  |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-01.1 | The System shall allow a trader to register using a phone number or email and a password, and shall verify the contact detail with a one-time code. [Confirm if OTP is simulated.]   |
| FR-01.2 | The System shall authenticate users and shall lock an account for 15 minutes after five consecutive failed logins.                                                                                               |
| FR-02.1 | The System shall allow a trader to enter and edit business type and category, operating duration, location, primary income sources, registered mobile-money/bank channels, operating pattern and basic expenses. |
| FR-02.2 | The System shall reject a business profile with missing mandatory fields and shall indicate which fields are missing.                                                                                            |
 
## 4.2 Financial Activity Recording
 
Allows the trader to record or import business financial activity. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-03.1 | The System shall allow entry of a cash sale with amount, date and time, optional note and category.                                                  |
| FR-03.2 | The System shall classify every cash transaction as self-reported (BR-02).                                                                           |
| FR-04.1 | The System shall allow import of M-PESA/Till statements and shall create transaction records classified as digitally verifiable.                     |
| FR-05.1 | The System shall allow import of bank statements and shall create records classified as verifiable through an imported record.                       |
| FR-06.1 | The System shall allow entry of business expenses and stock purchases with amount, date, category and supplier (optional).                           |
| FR-07.1 | The System shall allow entry of customer debts (receivables), business obligations, and loan or repayment records, with due dates and status.        |
| FR-07.2 | The System shall allow a trader to edit or void a manual record; edits and voids shall be retained in the record history and not physically deleted. |
 
## 4.3 Provenance and Data Validation
 
Maintains origin and reliability information for each record and checks data quality. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-08.1 | For each transaction the System shall store source, transaction type, date and time, amount, verification status, data-entry method and record status.                             |
| FR-09.1 | The System shall classify each record as self-reported, verifiable or derived according to BR-02 to BR-04.                                                                         |
| FR-10.1 | The System shall run the data-quality checks in Table 6.2 on every new or imported record.                                                                                         |
| FR-10.2 | The System shall mark a record that fails a check with a flag and reason, and shall exclude records flagged as invalid from indicator calculations until the trader corrects them. |
| FR-10.3 | The System shall detect conflicts between a manual record and an imported record for the same transaction and shall ask the trader to resolve them.                                |
| FR-10.4 | The System shall prevent duplicate imports of the same statement or transaction reference.                                                                                         |
 
## 4.4 Business Intelligence Dashboard and Alerts
 
Gives the trader immediate value from their records. Priority: High (dashboard), Medium (alerts).
 
| **ID**  | **Requirement**                                                                                                                                                                                                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-11.1 | The System shall display daily, weekly and monthly revenue, business expenses and estimated surplus.                                                                                                                                                                                                                        |
| FR-11.2 | The System shall display revenue and expense trends, transaction frequency and the cash-to-digital transaction ratio.                                                                                                                                                                                                       |
| FR-11.3 | The System shall allow the trader to filter dashboard data by date range.                                                                                                                                                                                                                                                   |
| FR-12.1 | The System shall generate alerts for significant revenue decline, unusual expense increase, significant cash-flow change, incomplete records, repayment-obligation changes and record inconsistencies. [Thresholds, e.g. a decline of more than 30% against the trailing average, to be tuned.] |
| FR-12.2 | The System shall generate trend-based alerts only where sufficient historical data exists (at least 30 days).                                                                                                                                                                                                               |
| FR-12.3 | The System shall notify the trader of alerts in the application and, optionally, by SMS or email.                                                                                                                                                                                                                           |
 
## 4.5 Financial History and Credibility Profile
 
Builds a longitudinal history and a standardised profile. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                                                                                                                                                   |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-13.1 | The System shall calculate and update length of financial history, average monthly revenue, revenue consistency, expense consistency, transaction frequency, digital transaction proportion, estimated cash-flow stability, repayment behaviour and business activity continuity. |
| FR-13.2 | The System shall keep reported, verified and derived information distinguishable in the history.                                                                                                                                                                                  |
| FR-14.1 | The System shall generate a Financial Credibility Profile for traders who meet BR-08.                                                                                                                                                                                             |
| FR-14.2 | The profile shall contain business information, history duration, revenue, expense and cash-flow indicators, transaction behaviour, verified and self-reported activity, data completeness, profile confidence and relevant risk indicators.                                      |
| FR-14.3 | The System shall timestamp each profile version and keep previous versions.                                                                                                                                                                                                       |
 
## 4.6 AI/ML Risk Assessment and Profile Confidence
 
Produces explainable, advisory risk classification and a separate confidence measure. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-15.1 | The System shall classify an eligible trader as Low, Medium or High risk using a trained ML model, using the features in Table 6.3.                      |
| FR-15.2 | Each assessment shall record the model version and generation time.                                                                                      |
| FR-15.3 | The assessment shall be labelled as advisory wherever displayed and shall never be presented as a lending decision (BR-01).                              |
| FR-16.1 | The System shall present, for every assessment, the main factors contributing to the result, with direction of influence, in plain language.             |
| FR-17.1 | The System shall compute a profile-confidence level (Low, Medium, High) and numeric score from the factors in Table 6.4, separately from the risk class. |
| FR-17.2 | The System shall display profile confidence alongside, but separately from, the risk class.                                                              |
| FR-17.3 | The System shall recompute assessment and confidence when new records change the profile materially, and at least monthly.                               |
 
## 4.7 Consent Management
 
Ensures controlled, trader-authorised data sharing. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                    |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| FR-18.1 | The System shall notify a trader when an institution requests access, showing the institution, data scope and purpose.             |
| FR-18.2 | The System shall allow the trader to approve or reject each request, and to revoke an approved consent at any time.                |
| FR-18.3 | The System shall store each consent with trader, institution, scope, status, grant time, expiry (BR-09) and revocation time.       |
| FR-18.4 | The System shall enforce consent on every portal and API access, and shall deny access when consent is absent, expired or revoked. |
 
## 4.8 Lender Portal
 
Provides authorised institution users with a separate interface to review profiles. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                                                                                            |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-19.1 | The System shall allow an authorised institution user to search for a trader by an agreed identifier (e.g. phone number or registered business ID).                                                                        |
| FR-19.2 | Search results shall not reveal financial data before consent is granted.                                                                                                                                                  |
| FR-19.3 | The System shall allow the institution user to request access to an authorised financial profile.                                                                                                                          |
| FR-20.1 | For consented profiles the portal shall show financial-history indicators, verified and self-reported activity, business-performance trends, risk indicators, profile confidence and the factors behind the AI assessment. |
| FR-20.2 | The portal shall state that the final credit decision remains the institution’s responsibility.                                                                                                                            |
 
## 4.9 Secure API / Middleware Layer
 
Exposes standardised information to institutions’ own systems. Priority: High.
 
| **ID**  | **Requirement**                                                                                                                                                          |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-21.1 | The API shall authenticate each institution client and authorise each call by role and scope.                                                                            |
| FR-21.2 | The API shall provide trader-profile lookup, credit-profile request, financial-profile retrieval, verification-status retrieval and risk-indicator retrieval operations. |
| FR-21.3 | The API shall return standard HTTP status codes and structured error messages, and shall apply rate limiting per client.                                                 |
| FR-21.4 | The API shall return profile data in a documented, versioned JSON schema.                                                                                                |
| FR-22.1 | The System shall log for each request who requested, what was requested, when, and whether the trader authorised it.                                                     |
| FR-22.2 | Access logs shall be append-only and viewable by the trader (for their own data), the institution (for its own requests) and administrators.                             |
 
## 4.10 System Administration
 
Supports management, monitoring and governance. Priority: High (users, roles), Medium (others).
 
| **ID**  | **Requirement**                                                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| FR-23.1 | The System shall allow administrators to create, suspend and reactivate users, institutions and trader accounts.                                                       |
| FR-23.2 | The System shall allow administrators to manage access permissions and roles.                                                                                          |
| FR-24.1 | The System shall let administrators monitor data-processing jobs, system events and API activity.                                                                      |
| FR-24.2 | The System shall let administrators review data-quality issues in aggregate without viewing a trader’s financial content unless a valid consent exists.                |
| FR-25.1 | The System shall let administrators register, activate and roll back ML model versions and view each version’s evaluation metrics.                                     |
| FR-26.1 | The System shall enforce role-based access on every function, so that traders, institution users and administrators can access only functions permitted to their role. |
 
# 5. USE CASES
 
## 5.1 Use Case Summary
 
**Table 5.1: Use case summary**
 
| **ID** | **Use case**                                     | **Actor**                               |
|--------|--------------------------------------------------|-----------------------------------------|
| UC-01  | Register and create business profile             | Trader                                  |
| UC-02  | Record a business transaction                    | Trader                                  |
| UC-03  | Import mobile-money or bank statement            | Trader                                  |
| UC-04  | View dashboard and alerts                        | Trader                                  |
| UC-05  | Generate credibility profile and risk assessment | System                                  |
| UC-06  | Request access to a trader profile               | Institution user                        |
| UC-07  | Approve, reject or revoke access                 | Trader                                  |
| UC-08  | View consented profile                           | Institution user                        |
| UC-09  | Retrieve profile through API                     | Institution system                      |
| UC-10  | Manage users, institutions and models            | Administrator                           |
| UC-11  | Review access logs                               | Trader, Institution user, Administrator |
 
## 5.2 Selected Use Case Descriptions
 
**UC-02: Record a business transaction**
 
| **Item**         | **Description**                                                                                                                                                                                                                               |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Actor            | Trader                                                                                                                                                                                                                                        |
| Precondition     | Trader is logged in and has a business profile.                                                                                                                                                                                               |
| Main flow        | 1\. Trader selects the record type (e.g. cash sale). 2. Trader enters amount, date/time and details. 3. System validates the entry. 4. System tags provenance (self-reported for cash). 5. System saves the record and updates the dashboard. |
| Alternative flow | 3a. Validation fails: the System shows the error and asks for correction. 3b. A possible duplicate is detected: the System asks the trader to confirm or cancel.                                                                              |
| Postcondition    | A record with metadata and provenance is stored; indicators are updated.                                                                                                                                                                      |
 
**UC-06/07/08: Request, consent and view a profile**
 
| **Item**         | **Description**                                                                                                                                                                                                                                                                    |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Actors           | Institution user, Trader                                                                                                                                                                                                                                                           |
| Precondition     | Institution user is authenticated; the trader has an eligible profile.                                                                                                                                                                                                             |
| Main flow        | 1\. Institution user searches for the trader. 2. User requests access, specifying scope and purpose. 3. System notifies the trader. 4. Trader approves. 5. System records the consent and logs the event. 6. Institution user views the profile, risk, confidence and explanation. |
| Alternative flow | 4a. Trader rejects or does not respond: access is denied and logged. 6a. Consent expires or is revoked: access ends immediately.                                                                                                                                                   |
| Postcondition    | Consent and access events are recorded in the access log.                                                                                                                                                                                                                          |
 
**UC-05: Generate credibility profile and risk assessment**
 
| **Item**         | **Description**                                                                                                                                                                                                                                                         |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Actor            | System (triggered by new data or schedule)                                                                                                                                                                                                                              |
| Precondition     | Trader meets eligibility (BR-08).                                                                                                                                                                                                                                       |
| Main flow        | 1\. System aggregates validated records. 2. System computes history indicators. 3. System sends features to the ML service. 4. ML service returns the risk class and contributing factors. 5. System computes profile confidence. 6. System stores the profile version. |
| Alternative flow | 3a. ML service unavailable: the System keeps the previous assessment, marks it as stale and retries.                                                                                                                                                                    |
| Postcondition    | A new profile version exists with risk, factors and confidence.                                                                                                                                                                                                         |
 
# 6. DATA REQUIREMENTS
 
## 6.1 Logical Data Entities
 
**Table 6.1: Logical data entities**
 
| **Entity**       | **Key attributes**                                                                                                              | **Notes**                                               |
|------------------|---------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| User             | user_id, role, contact, password_hash, status                                                                                   | Passwords hashed with a strong algorithm (e.g. bcrypt). |
| BusinessProfile  | trader_id, business type, category, location, start date, income sources, channels, operating pattern                           | One per trader.                                         |
| Transaction      | txn_id, trader_id, source, type, timestamp, amount, verification status, entry method, record status, external reference, flags | Never physically deleted.                               |
| Obligation       | obligation_id, trader_id, type, amount, due date, status                                                                        | Includes loan and repayment records.                    |
| FinancialProfile | profile_id, trader_id, version, indicators, completeness, confidence score/level, generated_at                                  | Versioned.                                              |
| RiskAssessment   | assessment_id, profile_id, risk class, factors, model_version, generated_at                                                     | Advisory.                                               |
| Institution      | institution_id, name, status, client credentials                                                                                |                                                         |
| ConsentRecord    | consent_id, trader_id, institution_id, scope, status, granted_at, expires_at, revoked_at                                        | BR-06, BR-09.                                           |
| AccessLog        | log_id, requester, institution_id, trader_id, data requested, timestamp, authorised                                             | Append-only.                                            |
| Alert            | alert_id, trader_id, type, message, created_at, read                                                                            |                                                         |
| ModelVersion     | model_id, version, metrics, status, created_at                                                                                  |                                                         |
 
## 6.2 Data-Quality Rules
 
**Table 6.2: Data-quality checks**
 
| **Check**           | **Rule (initial)**                                                                                                                          | **Action**                                      |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| Duplicate           | Same trader, source, amount and external reference, or same amount within 2 minutes from the same source.                                   | Flag; ask trader to confirm or discard.         |
| Invalid value       | Amount ≤ 0, non-numeric, or above a configured maximum.                                                                                     | Reject or flag as invalid.                      |
| Missing information | Mandatory field (amount, date, type) is empty.                                                                                              | Reject until completed.                         |
| Inconsistent date   | Date in the future, or before the declared business start date.                                                                             | Flag; ask for correction.                       |
| Abnormal pattern    | Amount greater than 5 times the trader’s 90-day median for that type, or a sudden volume spike. [Tune on data.] | Flag as anomaly; lowers confidence.             |
| Conflicting records | Same external reference with different amounts, or a manual entry contradicting an imported record.                                         | Flag; ask to resolve; prefer verifiable source. |
 
## 6.3 ML Input Features
 
**Table 6.3: Candidate model features**
 
| **Feature group** | **Examples**                                                          |
|-------------------|-----------------------------------------------------------------------|
| Revenue           | Average monthly revenue, revenue stability (coefficient of variation) |
| Cash flow         | Net surplus variability, cash-flow stability index                    |
| Activity          | Transaction frequency, business activity continuity, history length   |
| Expenses          | Expense ratio and expense consistency                                 |
| Repayment         | On-time repayment ratio, number of missed repayments                  |
| Obligations       | Existing obligations relative to income                               |
| Evidence          | Verified-transaction proportion                                       |
 
## 6.4 Profile-Confidence Factors
 
**Table 6.4: Initial confidence scoring (weights to be tuned)**
 
| **Factor**                                      | **Initial weight** |
|-------------------------------------------------|--------------------|
| Percentage of digitally verifiable transactions | 30                 |
| Length of recorded history                      | 20                 |
| Completeness of records                         | 20                 |
| Consistency between data sources                | 15                 |
| Frequency of record updates                     | 10                 |
| Absence of anomalous or conflicting records     | 5                  |
| **Total score (0–100)**                         | **100**            |
 
Initial mapping: 0–39 Low, 40–69 Medium, 70–100 High. [Confirm and justify with supervisor.]
 
# 7. NON-FUNCTIONAL REQUIREMENTS
 
**Table 7.1: Non-functional requirements and verification**
 
| **ID** | **Category**    | **Requirement**                                                                                                                                                                                                 | **Verification**            |
|--------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------|
| NFR-01 | Security        | Passwords hashed; JWT authentication; HTTPS/TLS; RBAC on every endpoint; protection against common web vulnerabilities (OWASP Top 10).                                                                          | Security tests, code review |
| NFR-02 | Privacy         | Personal and financial data processed per the DPA 2019; data minimisation; no profile access without valid consent; sensitive fields encrypted at rest. [Confirm encryption scope.] | Consent tests, review       |
| NFR-03 | Performance     | Pages load within 3 s and API profile responses return within 2 s for 50 concurrent users; risk assessment completes within 10 s.                                                                               | Load test                   |
| NFR-04 | Reliability     | Target 99% availability during demonstrations; daily database backups; graceful handling of ML service failure.                                                                                                 | Test, backup restore        |
| NFR-05 | Usability       | A new trader can record a first transaction within 5 minutes unaided; SUS ≥ 68.                                                                                                                                 | UAT                         |
| NFR-06 | Explainability  | Every assessment shows main factors in plain language.                                                                                                                                                          | Inspection                  |
| NFR-07 | Auditability    | All access and admin actions logged; logs append-only.                                                                                                                                                          | Test                        |
| NFR-08 | Scalability     | Modular services allowing ML and API layers to scale independently.                                                                                                                                             | Design review               |
| NFR-09 | Maintainability | Version-controlled, documented code; unit test coverage of at least 60% on core services. [Confirm target.]                                                                         | Coverage report             |
| NFR-10 | Compatibility   | Latest two versions of Chrome, Firefox and Edge; responsive down to 360 px width.                                                                                                                               | Cross-browser test          |
| NFR-11 | Data integrity  | Validation rules and database constraints prevent invalid records; transactions are not physically deleted.                                                                                                     | Test                        |
| NFR-12 | Model quality   | Macro-F1 of at least 0.75 on held-out test data; no single feature dominating the explanation by design flaw.                                                                                                   | Model evaluation            |
 
# 8. LEGAL, ETHICAL AND OTHER REQUIREMENTS
 
- The System shall comply with the principles of the Data Protection Act, 2019: lawful and transparent processing, purpose limitation, data minimisation, accuracy, storage limitation and security.
- The System shall give traders access to their own data and the ability to correct it, and shall provide a way to request account closure. [Confirm data-retention approach.]
- The model shall be documented, and its limitations (synthetic training data, advisory nature) shall be stated in the portal and in the project report.
- Research participants shall give informed consent and their data shall be anonymised.
# APPENDIX A: TRACEABILITY TO PROJECT OBJECTIVES
 
| **Proposal objective**                                                  | **Related requirements**                              |
|-------------------------------------------------------------------------|-------------------------------------------------------|
| Objective 1: Requirements gathering and SRS                             | Whole document; Sections 1 to 8                       |
| Objective 2: Design and provenance model                                | BR-02 to BR-04; FR-08, FR-09; Section 6               |
| Objective 3: Trader module with six record types and six quality checks | FR-01 to FR-10; Table 6.2                             |
| Objective 4: Dashboard and alerts                                       | FR-11, FR-12, FR-13                                   |
| Objective 5: ML risk model and confidence                               | FR-14 to FR-17; Tables 6.3 and 6.4; NFR-06, NFR-12    |
| Objective 6: API, consent, lender portal, admin                         | FR-18 to FR-26; NFR-01, NFR-02, NFR-07                |
| Objective 7: Testing and usability evaluation                           | NFR-03, NFR-05, NFR-09, NFR-10; all FRs as test cases |
 
# APPENDIX B: OPEN ISSUES AND ITEMS TO CONFIRM
 
| **No.** | **Issue**                                                               | **Owner**       |
|---------|-------------------------------------------------------------------------|-----------------|
| 1       | Supported statement formats for M-PESA/Till and bank imports.           | Team            |
| 2       | Eligibility thresholds (30 days, 20 transactions) and alert thresholds. | Team/Supervisor |
| 3       | Confidence weights and mapping to Low, Medium, High.                    | Team/Supervisor |
| 4       | Method for labelling synthetic risk classes.                            | Team/Supervisor |
| 5       | Swahili language support in the prototype.                              | Team            |
| 6       | Encryption scope and data-retention approach.                           | Team            |
| 7       | Whether SMS/email notifications are simulated or real.                  | Team            |
 
