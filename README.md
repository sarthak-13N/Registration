```mermaid
stateDiagram-v2
    direction TB

    [*] --> ApplicationSubmitted

    ApplicationSubmitted --> UnderPreliminaryValidation : Basic Data Validated
    ApplicationSubmitted --> Declined                     : Ineligible/Incomplete

    UnderPreliminaryValidation --> UnderCreditAssessment  : Eligibility Confirmed
    UnderPreliminaryValidation --> Declined               : Ineligible/Incomplete (Post‑Validation)

    UnderCreditAssessment --> Approved                    : Credit Checks Passed
    UnderCreditAssessment --> Rejected                    : Credit Checks Failed

    Approved --> DisbursementPreparation                  : Parameters Set
    Approved --> Cancelled                                : Customer Cancellation

    DisbursementPreparation --> Disbursed                 : Sanction Letter Signed
    DisbursementPreparation --> Cancelled                 : Customer Cancellation (Pre‑Disbursement)

    Disbursed --> Active                                  : Funds Transferred
    Disbursed --> Defaulted                               : Prolonged Non‑Payment

    Active --> Closed                                     : Fully Paid
    Active --> Delinquent                                 : EMI Missed (Beyond Grace Period)
    Active --> Closed                                     : Prepayment

    Delinquent --> Active                                 : EMI Paid (Recovered)
    Delinquent --> Defaulted                              : Prolonged Non‑Payment

    Defaulted --> Closed                                  : Legal Recovery/Settlement

    Rejected --> [*]                                      : Process Ends
    Declined --> [*]                                      : Process Ends
    Cancelled --> [*]                                     : Process Ends
    Closed --> [*]                                        : Process Ends
