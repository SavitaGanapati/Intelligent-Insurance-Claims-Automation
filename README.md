# Intelligent Insurance Claims Automation — REFramework

## Project Overview

**Intelligent Insurance Claims Automation** is a UiPath Robotic Enterprise Framework (REFramework) project designed to automate insurance claim processing using structured claim data, business rules, exception handling, and operational logging.

The project is intended to demonstrate how an enterprise RPA solution can process multiple insurance claims consistently, handle expected business exceptions, recover from application failures, and maintain transaction-level traceability.

## Business Problem

Manual insurance claim processing can involve repetitive data entry, policy verification, claim submission, and status tracking. These activities can be time-consuming and prone to human error.

This project aims to automate the repeatable parts of the process while distinguishing business-rule outcomes from unexpected technical failures.

## Objectives

- Automate insurance claim submission through a web portal.
- Process claims from a CSV input file.
- Use REFramework's initialization, transaction processing, exception handling, and shutdown structure.
- Apply business rules such as policy-status validation.
- Log claim-processing outcomes for audit and troubleshooting.
- Design the solution for future integration with reporting and operational monitoring.

## Technology Stack

| Technology | Purpose |
|---|---|
| UiPath Studio | RPA workflow development |
| UiPath REFramework | Transaction orchestration and exception handling |
| VB.NET expressions | Workflow conditions and data manipulation |
| CSV | Claims transaction input |
| JSON | External configuration |
| Web UI Automation | Insurance portal interaction |
| Git and GitHub | Version control and project documentation |
| Power BI | Planned operational reporting enhancement |

## High-Level Architecture

```text
Claims_Input.csv
       |
       v
REFramework Initialization
       |
       +---- Read Config.json
       |
       +---- Load Claims Data
       |
       v
GetTransactionData.xaml
       |
       v
Process.xaml
       |
       +---- Validate Claim Data
       |
       +---- Check Business Rules
       |
       +---- Submit Claim Through Web Portal
       |
       v
SetTransactionStatus.xaml
       |
       +---- Record Transaction Outcome
       |
       v
Next Transaction
       |
       v
Close Applications and Finish
```

*Note: The CSV-driven transaction flow and its integration with the framework are the intended design and remain subject to implementation and testing.*

## REFramework Components

| Component | Responsibility |
|---|---|
| `Main.xaml` | Controls the REFramework state machine and overall execution |
| `Framework/InitAllSettings.xaml` | Reads configuration and prepares settings |
| `Framework/InitAllApplications.xaml` | Initializes applications used by the process |
| `Framework/GetTransactionData.xaml` | Retrieves the next transaction |
| `Framework/Process.xaml` | Processes an individual claim |
| `Framework/SetTransactionStatus.xaml` | Handles transaction status updates |
| `Framework/CloseAllApplications.xaml` | Closes applications at the end of execution |
| `Framework/TakeScreenshot.xaml` | Supports troubleshooting of system exceptions |
| `Framework/RetryCurrentTransaction.xaml` | Supports framework retry handling |

The exact transaction data type and the workflow arguments must be configured consistently when adapting the default template for CSV-based transactions.

## Input Data

The planned input file is `Claims_Input.csv`.

Expected columns include:

- ClaimId
- PolicyNumber
- ClaimantName
- Email
- ClaimType
- DateOfLoss
- LossType
- ClaimAmount
- PolicyStatus
- DocumentsComplete
- FraudFlag

The CSV contains the information required to identify and process each claim. The workflow must validate that the required columns exist before processing transactions.

## Exception Handling Strategy

### Business Exceptions

Business exceptions represent expected business outcomes, for example:

- Inactive policy.
- Invalid claim information.
- A claim that cannot be submitted because of a business rule.

These outcomes should be recorded clearly and should not automatically trigger retries intended for technical failures.

### System Exceptions

System exceptions represent unexpected technical failures, for example:

- The insurance portal becomes unavailable.
- A required page element cannot be located.
- An application interaction fails unexpectedly.

The framework should log the error and apply an appropriately bounded recovery or retry strategy. Before retrying a claim submission, the process should establish whether the previous attempt succeeded to reduce the risk of duplicate submissions.

## Configuration

The project uses `Data/Config.json` for settings and framework constants.

The claims CSV path is configured through the `ClaimsCsvPath` setting.

Example:

```json
{
  "Settings": {
    "logF_BusinessProcessName": "Framework",
    "ClaimsCsvPath": "D:\\Career_Projects\\Intelligent-Insurance-Claims-Automation\\02_TestData\\Claims_Input.csv"
  }
}
```

Update the file path if the project or input data is moved to another location.

## Project Structure

```text
InsuranceClaims_REFramework/
├── Data/
│   └── Config.json
├── Exceptions_Screenshots/
├── Framework/
│   ├── CloseAllApplications.xaml
│   ├── GetTransactionData.xaml
│   ├── InitAllApplications.xaml
│   ├── InitAllSettings.xaml
│   ├── KillAllProcesses.xaml
│   ├── Process.xaml
│   ├── RetryCurrentTransaction.xaml
│   ├── SetTransactionStatus.xaml
│   └── TakeScreenshot.xaml
├── Tests/
├── Main.xaml
├── project.json
└── README.md
```

The structure reflects the framework template; additional files and folders may be added during implementation.

## Implementation Roadmap

- [ ] Configure CSV loading during initialization.
- [ ] Adapt transaction retrieval to return one CSV row at a time.
- [ ] Connect claim submission logic to `Process.xaml`.
- [ ] Configure transaction status handling.
- [ ] Implement and test business and system exception paths.
- [ ] Verify retry behavior and prevent duplicate submissions.
- [ ] Test the complete input file from start to finish.
- [ ] Document execution results and known limitations.
- [ ] Add operational reporting and Power BI integration.

## Expected Benefits

Once implemented and tested, the solution is intended to provide:

- More consistent claim processing.
- Reduced repetitive manual data entry.
- Clearer separation of business exceptions and technical failures.
- Improved transaction traceability.
- A reusable framework structure suitable for future expansion.

## Disclaimer

This repository is a learning and portfolio project. It is not a production insurance-processing system. Production deployment would require appropriate security controls, access management, audit requirements, business approval, and thorough testing.

## Author

**Savita Ganapati**

UiPath RPA | Intelligent Automation | Data Science and Analytics
