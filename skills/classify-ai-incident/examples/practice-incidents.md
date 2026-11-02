# Practice incidents

Six short incident accounts for trying the skill. This is a demonstration sample.

Classify each one on its own, then compare with the answer key in `docs/classify-ai-incident/VALIDATION.md` in the skill's repository. Do not open the answer key until you have written your records.

## P1. Invoice reminders

A bookkeeping assistant drafts payment reminders each Monday from the accounts ledger. The owner of a small agency set it up so that nothing is sent until she presses Approve, and the approval screen shows each reminder in full, amounts included. For five months the drafts were right, and her approvals went from a few minutes to a few seconds. One Monday the assistant read last month's ledger export by mistake. She approved the batch, and three clients received reminders for amounts they had already paid. Two of them phoned to complain. The assistant's file-selection bug was fixed the same week.

## P2. Action-item flags

A meeting-notes tool marks sentences it thinks are action items. In its first two months it flagged many sentences that were not actions, and the team stopped reading the flags; several people turned the flag panel off. A vendor update then made the flags accurate; the team was told by email. Three weeks later, a flagged item ("send the revised quote to the client by Friday") was not acted on, and the quote went out four days late. When the team checked, the tool had flagged that sentence correctly.

## P3. Automatic dependency updates

An engineering manager required every repository to run an AI agent that opens and merges dependency updates on its own when the test suite passes. The teams were told to "watch the dashboard" for anything odd. Two of the repositories had thin test suites, which the teams had pointed out before the rollout. An update that passed those tests broke a payment page in production for two hours. Nobody had been looking at the dashboard at the time.

## P4. Date format in exports

A translation service turns product pages into four languages. Reviewers check every translated page against a checklist of meaning, tone and product terms before it is published, and the service's error rate on that checklist has been low and stable for a year. After a service update, the export step began writing dates in month-day order for a market that uses day-month order. The reviewers' checklist did not include date formats, and the review tool showed the text before the export step ran. Customers noticed the dates after publication. The service fixed the export step the next day.

## P5. Email agent

A founder gave an AI agent access to her mailbox to "clear the backlog". She had connected it that morning, and this was the first batch of replies it would send for her. The agent planned to reply to forty messages and showed her the plan as a one-line summary per message. She glanced at the summary and approved it. Among the replies, the agent accepted a speaking invitation on her behalf and declined a client's meeting request. The agent's setup had no step where she saw the actual text of a reply before it was sent, and replies could not be recalled.

## P6. Calendar assistant

A scheduling assistant was configured to suggest times for meeting requests and let the user accept them. A newer version added a feature, switched on by default, that changed it to accept requests automatically whenever the user's week was more than 70% booked, "to reduce load". Nobody on the team had chosen this. During a busy week it accepted two overlapping client meetings, and one client was left waiting in a video call.
