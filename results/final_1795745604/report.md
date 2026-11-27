# Triage score report

Test cases: 50 (standard 30, hard 20).
Wrong or unreadable answers count as wrong. Recall matters most for `needs_human`: a missed case reaches no person.

## All test cases

| Measure | base | final_1795745604 | change |
|---|---|---|---|
| Valid JSON in the right shape | 100% | 100% | +0 points |
| Only the JSON, no extra text | 4% | 100% | +96 points |
| Category correct | 92% | 100% | +8 points |
| Urgency correct | 46% | 94% | +48 points |
| needs_human correct | 52% | 98% | +46 points |
| needs_human recall (missed a case that needs a person?) | 95% | 95% | +0 points |
| needs_human precision | 44% | 100% | +56 points |
| All three fields correct | 36% | 94% | +58 points |

## Standard cases

| Measure | base | final_1795745604 | change |
|---|---|---|---|
| Valid JSON in the right shape | 100% | 100% | +0 points |
| Only the JSON, no extra text | 0% | 100% | +100 points |
| Category correct | 90% | 100% | +10 points |
| Urgency correct | 53% | 93% | +40 points |
| needs_human correct | 60% | 100% | +40 points |
| needs_human recall (missed a case that needs a person?) | 100% | 100% | +0 points |
| needs_human precision | 48% | 100% | +52 points |
| All three fields correct | 40% | 93% | +53 points |

## Hard cases (Malay, two issues, tone, an order inside the message)

| Measure | base | final_1795745604 | change |
|---|---|---|---|
| Valid JSON in the right shape | 100% | 100% | +0 points |
| Only the JSON, no extra text | 10% | 100% | +90 points |
| Category correct | 95% | 100% | +5 points |
| Urgency correct | 35% | 95% | +60 points |
| needs_human correct | 40% | 95% | +55 points |
| needs_human recall (missed a case that needs a person?) | 88% | 88% | +0 points |
| needs_human precision | 39% | 100% | +61 points |
| All three fields correct | 30% | 95% | +65 points |

## base: where it went wrong

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

## final_1795745604: where it went wrong

- Urgency mistakes, gold->answer: high->medium x1, medium->low x2

First wrong cases (3 of 3):

- X021 (standard): gold ['account_access', 'medium', False], got ['account_access', 'low', False]. "I forgot which email I used to register. Can you look it up with my phone number?"
- X023 (standard): gold ['account_access', 'medium', False], got ['account_access', 'low', False]. "My account was locked after I tried to log in from a hotel. Please unlock it, I am travell"
- X034 (hard): gold ['payment_billing', 'high', True], got ['payment_billing', 'medium', False]. "Duit dah kena potong dua kali untuk order yang sama! Tolong cepat, saya takde duit lagi da"

