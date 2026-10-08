# Prompt library

One entry per prompt version. Newest at the bottom. Each entry has the prompt, the output it produced,
and which acceptance checks it passed. Never edit an old entry: add a new version.

## T1-credit-summary | v1 | 2026-10-08

**Purpose:** Summarise an applicant for a credit committee
**Result:** 4/4 checks passed

### Prompt
- **Role:** You are a senior credit analyst writing for a credit committee.
- **Task:** Summarize the applicant,Evaluate the EMI-to-income ratio, then recommend 'approve' or 'refer' or 'decline'
- **Context:** Lending Policy:
Lending policy (personal loans):
1. Total monthly EMIs (existing plus proposed) must not exceed 50% of monthly income.
2. A credit score of 700 or above is required for approval.
3. Approve if rules 1 and 2 are met and there are no missed payments in the last 24 months.
4. Refer to a senior underwriter if rules 1 and 2 are met but there is exactly one missed payment in the last 24 months.
5. Decline if rule 1 or 2 is not met, or if there are two or more missed payments in the last 24 months.
- **Constraints:** Use at most 75 words; Use exactly 3 bullet lines.; State the total EMI-to-income ratio percentage: (existing EMIs + proposed EMI) divided by monthly income.; Only Recommend in 'approve', 'refer', or 'decline'.
- **Output format:** Exactly three bullet points starting with '-', no prefixes or extra text
- **Examples:** 0

### Output
> - Applicant Kavya Reddy, 34, software engineer, 6 years at same employer.  
> - Total EMIs 40,244/120,000 = 33.5% of income.  
> - Credit score 742, one missed payment → refer

### Checks
- [x] at most 80 words (29 words)
- [x] exactly 3 bullet lines (3 bullet lines)
- [x] states the total EMI-to-income ratio (about 33-34%)
- [x] recommends 'refer', as the policy requires

## T2-sms-declined | v1 | 2026-10-08

**Purpose:** Tell a customer their application was declined, by SMS
**Result:** 6/6 checks passed

### Prompt
- **Role:** You are a senior Loan Operations Specialist for a bank
- **Task:** Write an empathatic SMS notifying an applicant that their application has been declined
- **Context:** The customer reads this on a phone, in a hurry, possibly upset. Some of the facts you hold must never reach them.
- **Constraints:** Keep the number of characters under 290; Include the application exact reference in the SMS; Include the exact helpline number; mention the 90-day reapply period; Address the customer by their name; Internal credit reasons are confidential and must never be shared with customers
- **Output format:** Exactly one plain-text SMS message. No markdown, no extra text, no placeholders, no subject line
- **Examples:** 0

### Output
> Hi Rohan, we’re sorry to inform you that your loan application (APP-20931) has been declined. You may reapply after 90 days. For questions, call 1800-555-0199. We’re here to help.

### Checks
- [x] at most 300 characters (179 characters)
- [x] includes the application reference
- [x] includes the helpline number
- [x] mentions the 90-day reapply period
- [x] addresses the customer by name
- [x] does NOT reveal the confidential internal reason

## T3-complaint-triage | v1 | 2026-10-08

**Purpose:** Triage a complaint into JSON
**Result:** 4/4 checks passed

### Prompt
- **Role:** You are a  Complaint Triage Analyst at a bank's compliant desk
- **Task:** classify the customer's compliant
- **Context:** Categories:
- card: debit/credit card issues
- loan: loan issues
- account: transfers, UPI, statements, balances
- other: servicing, address or nominee updates

Urgency: high if money at risk or customer blocked within 24h; medium if action needed within a week; low otherwise.
- **Constraints:** reply is a JSON object only (no prose, no code fences); has exactly the keys ['category', 'urgency']; category is one of ['account', 'card', 'loan', 'other']; urgency is one of ['high', 'low', 'medium']
- **Output format:** {"category": "...", "urgency": "..."} only. No markdown, no prose.
- **Examples:** 0

### Output
> {"category":"card","urgency":"high"}

### Checks
- [x] reply is a JSON object only (no prose, no code fences)
- [x] has exactly the keys ['category', 'urgency']
- [x] category is one of ['account', 'card', 'loan', 'other'] and is 'card' (category = 'card')
- [x] urgency is one of ['high', 'low', 'medium'] and is 'high' (urgency = 'high')
