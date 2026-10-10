# Process Design Document (PDD) — Intelligent Insurance Claims Automation

## Applications
- Claims Intake Portal (local practice portal)
- Core Claims Processing App (local practice app)
- CSV input
- Orchestrator Queue (production-style design)

## REFramework mapping
Init:
- Read Config
- Initialize application/browser
- Validate configuration

Get Transaction Data:
- Get Transaction Item from InsuranceClaimsQueue
- Return No Data when queue is empty

Process Transaction:
- Read transaction fields
- Validate policy status/documents/email
- Apply business rules
- Submit eligible claim to core app
- Route human-review claims
- Update transaction result
- Log business and technical information

End Process:
- Close browser/application
- Final logs
- Metrics output

## Exception taxonomy
BusinessRuleException:
- Inactive/unknown policy
- Missing documents
- Invalid customer data
- Fraud flag / amount above threshold requiring manual review

ApplicationException:
- Portal unavailable
- Selector not found
- Timeout
- Unexpected application error

SystemException:
- Configuration missing
- Credential failure
- Orchestrator unavailable

## Interview-ready design decisions
- Queue item = one claim transaction.
- Reference = ClaimId.
- Unique reference enabled.
- Auto-retry configured for technical failures.
- Business exceptions are not blindly retried.
- Human-in-the-loop is used when deterministic rules cannot safely make the decision.
- All processing uses config-driven thresholds and URLs.
