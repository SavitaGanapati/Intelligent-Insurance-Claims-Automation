# Build Sequence — do this in UiPath Studio

## Phase 1 — Browser smoke test
1. Double-click `start_server.bat`.
2. Open `http://127.0.0.1:8000/` in Chrome/Edge.
3. In UiPath Studio create `INS_Claims_Automation`.
4. Create a simple sequence and use `Use Application/Browser`.
5. Indicate `Claim ID`, `Policy Number`, `Claimant Name`, `Email`, and `Submit Claim`.
6. Run once successfully.
7. Do NOT build REFramework until this smoke test works.

## Phase 2 — Data-driven intake
1. Read `Claims_Input.csv` with `Read CSV`.
2. For each row, validate required columns.
3. Add one queue item per claim.
4. Queue name: `InsuranceClaimsQueue`.
5. Queue reference: `ClaimId`.

## Phase 3 — REFramework
1. Create a new project from the REFramework template.
2. Move configuration into `Config.xlsx` later; use `Config.json` as the initial reference.
3. Init: initialize browser/app and load config.
4. Get Transaction Data: `Get Transaction Item`.
5. Process Transaction:
   - map queue item to claim fields
   - validate business rules
   - open core app
   - update claim
   - log status
6. Close/End: close applications and produce summary.

## Phase 4 — Exceptions
Create tests for:
- invalid email -> Business Exception
- inactive policy -> Business Exception
- missing documents -> Business Exception
- fraud flag -> Human Review
- amount > threshold -> Human Review
- simulated selector timeout -> Application Exception -> retry

## Phase 5 — Human-in-the-loop
For Human Review:
- create an Action/Task later using UiPath Apps/Action Center if available
- send claim ID, reason, amount, and recommended decision
- resume automation after reviewer decision

## Phase 6 — Production-style Orchestrator
Create:
- Queue: `InsuranceClaimsQueue`
- Asset/credential for portal login
- Process/package
- trigger
- monitoring dashboard
- retry configuration
- SLA configuration

## Phase 7 — Reporting
Generate `Claim_Processing_Log.csv` with:
ClaimId, StartTime, EndTime, Status, ExceptionType, RetryCount, ReviewRequired, ClaimAmount, ProcessingSeconds
