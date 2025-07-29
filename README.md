stateDiagram-v2
    direction LR
    [*] --> ApplicationSubmitted

    state ApplicationSubmitted {
        ApplicationSubmitted --> UnderPreliminaryValidation : Basic Data Validated
        ApplicationSubmitted --> Declined : Ineligible/Incomplete
    }

    state UnderPreliminaryValidation {
        UnderPreliminaryValidation --> UnderCreditAssessment : Eligibility Confirmed
        UnderPreliminaryValidation --> Declined : Ineligible/Incomplete (Post-Validation)
    }

    state UnderCreditAssessment {
        UnderCreditAssessment --> Approved : Credit Checks Passed
        UnderCreditAssessment --> Rejected : Credit Checks Failed
    }

    state Approved {
        Approved --> DisbursementPreparation : Parameters Set
        Approved --> Cancelled : Customer Cancellation
    }

    state DisbursementPreparation {
        DisbursementPreparation --> Disbursed : Sanction Letter Signed
        DisbursementPreparation --> Cancelled : Customer Cancellation (Pre-Disbursement)
    }

    state Disbursed {
        Disbursed --> Active : Funds Transferred
        Disbursed --> Default : Prolonged Non-Payment (Edge Case)
    }

    state Active {
        Active --> Closed : Fully Paid
        Active --> Delinquent : EMI Missed (Beyond Grace Period)
        Active --> Closed : Prepayment
    }

    state Delinquent {
        Delinquent --> Active : EMI Paid (Recovered)
        Delinquent --> Default : Prolonged Non-Payment
    }

    state Default {
        Default --> Closed : Legal Recovery/Settlement
    }

    state Rejected
    state Declined
    state Cancelled
    state Closed

    Rejected --> [*] : Process Ends
    Declined --> [*] : Process Ends
    Cancelled --> [*] : Process Ends
    Closed --> [*] : Process Ends
