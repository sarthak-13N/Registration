```mermaid
stateDiagram-v2
    direction TB
    %% start
    [*] --> "Application Received"

    %% application branch
    "Application Received" --> "Under Review"            : submit application
    "Application Received" --> "Terminated"               : cancel request

    %% review
    "Under Review" --> "Approved"                         : approve
    "Under Review" --> "Rejected"                         : reject

    %% approval branch
    "Approved" --> "Disbursed"                            : disburse
    "Approved" --> "Cancelled"                            : cancel request

    %% disbursal
    "Disbursed" --> "In Repayment"                        : funds transferred
    "Disbursed" --> "Defaulted"                           : prolonged non‑payment

    %% repayment
    "In Repayment" --> "Closed"                           : final payment made
    "In Repayment" --> "Terminated"                       : cancel request / default

    %% terminal states
    "Rejected" --> [*]                                     : process ends
    "Terminated" --> [*]                                   : process ends
    "Cancelled" --> [*]                                    : process ends
    "Defaulted" --> [*]                                    : process ends
    "Closed" --> [*]                                       : process ends
