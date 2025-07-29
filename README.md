```mermaid
stateDiagram-v2
    direction TB

    %% Start
    [*] --> "Application Received"

    %% Application branch
    "Application Received" --> "Under Review"  : Submit Application
    "Application Received" --> "Cancelled"     : Customer Cancellation

    %% Review
    "Under Review" --> "Approved"              : Approve
    "Under Review" --> "Rejected"              : Reject

    %% Post‑approval
    "Approved" --> "Disbursed"                 : Disburse Funds
    "Approved" --> "Cancelled"                 : Cancel Pre‑Disbursement

    %% Disbursal
    "Disbursed" --> "In Repayment"             : Funds Transferred
    "Disbursed" --> "Defaulted"                : Prolonged Non‑Payment

    %% Repayment
    "In Repayment" --> "Closed"                : Final Payment Made
    "In Repayment" --> "Defaulted"             : Default (Non‑Payment)
    "In Repayment" --> "Closed"                : Prepayment

    %% Terminal states
    "Rejected" --> [*]                         : Process Ends  
    "Cancelled" --> [*]                        : Process Ends  
    "Defaulted" --> [*]                        : Process Ends  
    "Closed" --> [*]                           : Process Ends
