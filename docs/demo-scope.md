# 513 Property Services Demo Scope

## Demo Story

A homeowner or small-business customer submits a service request through the 513 Property Services website. The automation platform receives the lead, understands the request, acknowledges the customer, and presents the owner with a useful next action.

## Input

The initial form should support:

- Customer name
- Email address
- Phone number
- Service address or ZIP code
- Preferred contact method
- Service category
- Free-text description
- Desired timing
- Optional photos or attachment references

## Automated Processing

The system should:

1. Validate required fields.
2. Normalize phone, email, and category values.
3. Detect spam or clearly invalid submissions.
4. Classify the likely service category.
5. Estimate urgency using defined rules and AI assistance.
6. Summarize the request for the operator.
7. Recommend the next action.
8. Store the original request and derived fields.

## Outputs

### Customer Output

- Confirmation that the request was received
- Clear expectation for follow-up
- No unsupported promises about price or scheduling

### Operator Output

- Customer contact details
- Concise job summary
- Service category
- Urgency
- Missing information
- Recommended next action
- Link or identifier for the lead record

## Human Review

The first version should not autonomously:

- Commit to pricing
- Confirm an appointment
- Reject a potentially valid customer
- Make safety-critical recommendations

## Demo Scenarios

- Standard drywall repair request
- TV mounting and home-networking request
- Urgent door or lock problem
- Out-of-scope landscaping request
- Incomplete submission
- Duplicate submission
- Simulated AI-provider failure
- Simulated notification failure

## Demo Exit Criteria

- Each scenario has a predictable result.
- All state changes are reviewable.
- Failures are visible and retryable.
- The demo can be reset without manual database surgery.
