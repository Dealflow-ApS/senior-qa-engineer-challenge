
<img src="https://github.com/Dealflow-ApS/senior-front-end-engineer-challenge/blob/8d8b14e495eadacdd9e21c6a0da8038f757b9854/logo.gif" alt="logo" width="70"/>

# Senior QA engineer challenge 💻

Congratulations on making it this far :zap:. If you've received this, it means that you are now among the top 5% applicants who applied for this position 😎. 
<br /><br />All the best with this challenge; see you at the finish line :godmode:. <br /><br />
<img src="https://github.com/Dealflow-ApS/senior-front-end-engineer-challenge/blob/3b398947f88de3aa38fd13f5136f605391dc3c44/global.png" alt="logo" width="60"/>
<img src="https://github.com/Dealflow-ApS/senior-front-end-engineer-challenge/blob/3b398947f88de3aa38fd13f5136f605391dc3c44/limitless.png" alt="logo" width="70"/>

## Challenge Overview

Your mission encompasses several critical tasks:

### 1. **UI Consistency and State Management**:
- Identify inconsistencies at the component design level, particularly components serving the same purpose but depicted with different designs. Highlighting such discrepancies is crucial for both user experience (UX) and developer experience (DEVX).
- Examine provided UI designs for missing states, including `hover`, `active`, `focus`, `press`, `with-content`, `without-content`, `is-valid`, and `invalid`. Document these omissions as they are essential for a comprehensive design system.
- [Link 1](https://www.figma.com/file/a08zRDr9oom3zU6Zviakje/QA-challenge?type=design&node-id=8-12515&mode=design)
- [Link 2](https://www.figma.com/proto/a08zRDr9oom3zU6Zviakje/QA-challenge?page-id=0%3A1&type=design&node-id=7-6291&viewport=187%2C-714%2C0.18&t=rSOcJkzhjIgv1knn-1&scaling=min-zoom&starting-point-node-id=7%3A6291)

### 2. **Usability Testing**:
- Conduct a thorough usability review of the given workflow (Withdrawal/KYB/C flow). Assess its intuitiveness, ease of navigation, and overall user experience, providing detailed feedback and improvement suggestions.

### 3. **Automated Testing of a Web App Flow**:
- Select a flow within our web application designs provided. Assume that the code was present, Ideate test cases for different states and edge cases.

### 4. **Backend code Testing**:
- Select a flow within our web application designs provided. Assume that the API was present, Ideate test cases for different states and edge cases.
- Assume the following API's exist
##### 1. **Invoices API**:
- **Endpoint**: `GET {{baseUrl}}/invoices/v2?search_value=&invoice_type=all&invoice_status=&sort=id&order=desc&limit=100&offset`
- **Objective**: Verify the API's ability to retrieve a list of invoices with various filters applied. Ensure the response structure matches the expected format, and test for correct handling of sorting, filtering, and pagination.
- **Expected Response**:
    ```json
    {
        "total_records": 21,
        "has_more": false,
        "data": [
            {
                "id": 1054,
                "invoiced_amount": "1200.0000",
                "invoiced_currency": "GBP",
                "invoiced_currency_symbol": "£",
                "payee_amount": "1200.0000",
                "payee_currency": "GBP",
                "payee_currency_symbol": "£",
                "sent_on": "2024-02-16 22:12:15",
                "invoice_status": "payout_requested",
                "invoice_status_display_name": "Payout Requested",
                "invoice_type": "commission",
                "invoice_type_display_name": "Commission",
                "payor_id": 13,
                "payor_name": "test",
                "payout_id": 6,
                "payout_amount": "1403.7500",
                "payout_currency": "EUR",
                "payout_currency_symbol": "€"
            },
            {
                "id": 35,
                "invoiced_amount": "1200.0000",
                "invoiced_currency": "EUR",
                "invoiced_currency_symbol": "€",
                "payee_amount": "1200.0000",
                "payee_currency": "EUR",
                "payee_currency_symbol": "€",
                "sent_on": "2024-01-22 00:00:00",
                "invoice_status": "declined",
                "invoice_status_display_name": "Declined",
                "invoice_type": "recurring_invoice",
                "invoice_type_display_name": "Recurring invoice",
                "payor_id": 13,
                "payor_name": "test",
                "payout_id": null,
                "payout_amount": null,
                "payout_currency": null,
                "payout_currency_symbol": null
            }
        ]
    }
    ```
##### 2. **Profile and Wallet API**:
- **Endpoint**: `GET {{baseUrl}}/profile/v2/wallet`
- **Objective**: Test the retrieval of the user's profile and wallet information, focusing on KYC and KYB statuses, preferred currency, special activities, and wallet balances across different currencies.
- **Expected Response**:
    ```json
    {
        "id": 11,
        "kyc_status": "under_review",
        "kyb_status": "under_review",
        ...
    }
    ```

##### 3. **Withdrawal API**:
- **Endpoint**: `POST {{baseUrl}}/invoices/v2/withdraw`
- **Objective**: Validate the functionality for processing withdrawals, including error handling for conflicts, authorization issues, and non-existent invoices.
- **Request**:
    ```json
    [
        {
            "invoice_id": 533,
            "bank_account_id": 4,
            "currency": "USD"
        }
    ]
    ```
- **Expected Response**:
    ```json
    {
        "success": [...],
        "failure": [...]
    }
    ```
##### 4. **Bank Account Creation API**:
- **Endpoint**: `POST {{baseUrl}}/profile/v2/billing/bank-accounts`
- **Objective**: Assess the API's capability to add bank accounts, ensuring all optional and required fields are correctly processed and validated.
- **Request**:
    ```json
    {
        "country": "NOR",
        "account_holder_name": "Mary Doe",
        "bank_name": "Danske Bank",
        "account_number": "657567",
        "currency": "DKK",
        "is_primary": true,
        "swift_code": "DABADKKK",
        "iban": "DK1234567890",
        "bic": "DABADKKK",
        "routing_number": "routing_number_sample",
        "sort_code": "sort_code",
        "account_type": "Savings",
        "bank_account_status": "active",
        "reg_number": "",
        "clearing_number": "",
        "financial_institution_number": "",
        "transit_number": ""
    }
    ```
- **Expected Response**:
    ```json
    {
        "account_number": "1234567890",
        "bank_name": "Danske Bank",
        "currency": "DKK",
        "country": "NOR",
        "bank_details": {
            "account_holder_name": "John Doe",
            "swift_code": "DABADKKK",
            "iban": "DK1234567890",
            "routing_number": "routing_number_sample",
            "sort_code": "sort_code",
            "account_type": "Savings",
            "bic": "DABADKKK",
            "is_primary": true
        },
        "bank_account_status": "active"
    }
    ```

## Evaluation Criteria

Your submission will be evaluated on the following aspects:

- **Detail-Oriented Observation**: Precision in identifying UI inconsistencies and missing design states.
- **Analytical and Critical Thinking**: Quality of usability feedback, understanding of user experience, and practical improvement suggestions.
- **Technical Proficiency**: Skill in automating tests, demonstrating familiarity with testing frameworks and tools.
- **Integration Insight**: Ability to understand and test the integration between different parts of the system, ensuring seamless operation and consistency.
- **Security Awareness**: Vigilance in identifying potential security vulnerabilities and ensuring robust access control.

## Submission Process

- Complete the tasks within 2 days of receiving this challenge.
- Document your findings, observations, and test scripts comprehensively. Include:
    - A detailed report on UI consistency and state management findings.
    - Usability testing feedback and suggestions.
    - Automated testing scripts and results, highlighting any identified issues.
- Create a private GitHub repository for your submission, granting access to the specified usernames.
  - [siddharthmudgal](https://github.com/siddharthmudgal)
	- [ahmedemad242](https://github.com/ahmedemad242)

## Additional Notes

- Assume access to the necessary design files and application flows will be provided.
- Where specific details or access might be missing, document your assumptions and proposed testing strategies.
- Highlight any innovative or noteworthy features you identify during your testing.

This challenge is your opportunity to showcase your comprehensive QA skills, from detailed design evaluation to automated testing and security assessment. Good luck, and we look forward to your insightful submission!


## Eyebrows raised?
- We are here to listen if you want to roast this challenge and think we could have done a better job. :trollface:
  - Send out an email to siddharth@dealflow.live
