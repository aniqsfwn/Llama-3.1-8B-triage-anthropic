# Triage score report

Test cases: 50 (standard 30, hard 20).
Wrong or unreadable answers count as wrong. Recall matters most for `needs_human`: a missed case reaches no person.

## All test cases

| Measure | tuned |
|---|---|
| Valid JSON in the right shape | 100% |
| Only the JSON, no extra text | 4% |
| Category correct | 92% |
| Urgency correct | 46% |
| needs_human correct | 52% |
| needs_human recall (missed a case that needs a person?) | 95% |
| needs_human precision | 44% |
| All three fields correct | 36% |

## Standard cases

| Measure | tuned |
|---|---|
| Valid JSON in the right shape | 100% |
| Only the JSON, no extra text | 0% |
| Category correct | 90% |
| Urgency correct | 53% |
| needs_human correct | 60% |
| needs_human recall (missed a case that needs a person?) | 100% |
| needs_human precision | 48% |
| All three fields correct | 40% |

## Hard cases (Malay, two issues, tone, an order inside the message)

| Measure | tuned |
|---|---|
| Valid JSON in the right shape | 100% |
| Only the JSON, no extra text | 10% |
| Category correct | 95% |
| Urgency correct | 35% |
| needs_human correct | 40% |
| needs_human recall (missed a case that needs a person?) | 88% |
| needs_human precision | 39% |
| All three fields correct | 30% |

## tuned: where it went wrong

- Urgency mistakes, gold->answer: high->low x1, low->high x1, low->medium x6, medium->high x17, medium->low x2

First wrong cases (8 of 32):

- X001 (standard): gold ['delivery', 'medium', False], got ['delivery', 'high', True]. "The estimated delivery for my order was yesterday, but I see no update since Tuesday."
- X002 (standard): gold ['delivery', 'low', False], got ['general_enquiry', 'low', False]. "Do you deliver to Labuan?"
- X004 (standard): gold ['delivery', 'medium', True], got ['delivery', 'high', True]. "The courier delivered to the wrong house and the neighbour does not want to give it back. "
- X005 (standard): gold ['delivery', 'low', False], got ['delivery', 'medium', True]. "Can I reschedule my delivery to next week? I will be away."
- X006 (standard): gold ['refund_return', 'low', False], got ['refund_return', 'medium', True]. "How do I return a jacket that does not fit?"
- X007 (standard): gold ['refund_return', 'medium', False], got ['refund_return', 'high', True]. "I returned the lamp 12 days ago and the status still says awaiting inspection."
- X008 (standard): gold ['refund_return', 'medium', True], got ['refund_return', 'high', True]. "You cancelled my order and said the refund of RM780 will arrive in 7 days. It has been 30 "
- X010 (standard): gold ['refund_return', 'low', False], got ['refund_return', 'medium', True]. "Can I get my refund as a bank transfer instead of store credit?"

