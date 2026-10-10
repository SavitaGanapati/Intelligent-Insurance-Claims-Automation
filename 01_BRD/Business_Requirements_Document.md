# Intelligent Insurance Claims Automation — Mini BRD

## Objective
Automate the repetitive First Notice of Loss / claim-intake flow using UiPath.

## Business flow
1. Claims arrive in an intake source.
2. Claim data is extracted and normalized.
3. Policy and mandatory-field validation is performed.
4. Business rules classify the transaction:
   - Straight-through eligible
   - Human review
   - Business exception
5. Eligible claims are entered into the core claims application.
6. Result and status are logged.
7. Queue/SLA/exception metrics are exposed for monitoring.

## Automation scope for portfolio
- UiPath Studio
- REFramework
- Orchestrator Queue
- Config-driven values
- Credential/Asset concept
- Retry
- Business vs Application exceptions
- Human-in-the-loop for borderline claims
- Core application UI automation
- CSV/Excel-style intake
- Audit logging
- Power BI-ready output

## Business rules
- Policy must be Active.
- Required documents must be complete.
- Amount <= configured auto-approval threshold can proceed if no fraud flag.
- FraudFlag = Yes => Human Review.
- Amount > threshold => Human Review.
- Invalid email => Business Exception.
- Inactive/unknown policy => Business Exception.

## SLA
Target: process each claim within 24 hours of queue arrival.
Risk condition: transaction approaching SLA is surfaced to operations.

## Expected KPIs
- Total claims received
- Successfully processed
- Business exceptions
- Application exceptions
- Human reviews
- Average processing time
- Retry count
- SLA breaches
- Estimated hours saved
- Estimated annual ROI
