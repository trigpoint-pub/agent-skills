# Example ledger

This is a demonstration sample. The workflow below is made up for this example. The ledger after it was produced by running the skill on it in design mode; it is reproduced as written, except that a dash used for empty cells was replaced with "n/a".

## The input

A freelance consultant sends each of six retainer clients a monthly performance report. She wants to hand as much as is sensible to an AI assistant that can read her analytics exports, draft text, build a PDF and send email from her account.

Steps:
1. Export last month's figures from three tools (web analytics, ad platform, newsletter platform) into a shared folder.
2. Compare the figures with the previous month and with the client's targets; note what changed and the likely reasons.
3. Decide the two or three recommendations for next month.
4. Write the report: a one-page summary, charts, and the recommendations.
5. Send the report to the client's contact by email, with a short covering note.
6. Log the report as sent in her client tracker, which drives her invoice.

Who answers: she does, for every step; the client reads the report and pays for the retainer.

What an error costs:
- Step 1: a missing or wrong export gives wrong figures; it can be re-exported, but she only finds out if she notices.
- Step 2: a wrong comparison or a made-up reason misleads the client; clients sometimes forward reports to their own managers.
- Step 3: a poor recommendation wastes a month of the client's budget and her credibility.
- Step 4: errors in charts or text are embarrassing; she can send a correction, but the client has already read it.
- Step 5: an email to the wrong person or with the wrong client's report would leak one client's data to another; it cannot be recalled.
- Step 6: a wrong log entry delays an invoice; easy to fix.

Today: she does all six by hand; about four hours per client per month.

## The ledger

```text
Allocation ledger: Monthly client report (freelance marketing consultant)
Scope: This ledger holds only for the workflow and the error costs listed here.
Criterion: The two questions that set the levels (can an error be undone? does it travel on?) are a working rule from Trigpoint (2026), based on one documented case and adapted from Parasuraman, Sheridan & Wickens (2000).
Review by: 2027-01-31
Status: proposal until the consultant adopts it.
```

| Step | Stage | Level | Reason (Q1 · Q2) | Residual work | Check | Takeover | Basis | Evidence |
|---|---|---|---|---|---|---|---|---|
| 1 Export | Gather (export three tools' figures to the shared folder) | 2 | Q1: yes. She or the assistant re-exports, up to the point the report is sent. Q2: no at the recommended levels: the comparison built on the export goes to her (step 2 at 2) before anything reaches a client. Ceiling 3. Recommended 2, below the ceiling, because its result only prepares her review. | She reads the export summary the assistant attaches to the comparison: date range, account name and row count for each of the 18 files. Practice: the monthly comparison in Check keeps her in the tools. | Every month, every client: she compares one headline figure per tool (18 figures) with that tool's own dashboard. Starting rate; revisit 2026-12-15. | Notices: she, at step 2. Takes over: she exports by hand at step 1. | B1, B4 | theory |
| 2 Compare | Analyse (changes against last month and targets; likely reasons) | 2 | Q1: yes until the report is sent; she corrects it. After sending, a correction does not unread it, and clients forward reports to their managers. Q2: no at the recommended levels: the comparison reaches her before the report goes out (step 5 Act at 1). Ceiling 3. Recommended 2, below the ceiling, because its result only prepares her report, and by Step 3: likely reasons need context the exports do not hold, a made-up reason reads as well as a true one, and this analysis is what her clients pay for, so she has to keep doing it. The assistant being faster at the arithmetic is not a reason to raise the level. | The assistant computes the changes and lists candidate reasons, each marked as a hypothesis with the figure behind it; she keeps, rewrites or drops each one. | Every reason in every report (100%) confirmed by her against evidence she can name. Figures: she recomputes 3 changes per client from the exports. One client a month (rotating) she analyses by hand first, then compares with the assistant's. Starting rate; revisit 2026-12-15. | Notices: she at review; otherwise the client, too late. Takes over: she does the comparison by hand at step 2. | B2, B3, B6 | theory |
| 3 Recommend | Decide (two or three recommendations for next month) | 1 | Decide stage: ceiling 1. Q1: no. A poor recommendation, once acted on, spends a month of the client's budget. Q2: yes, to the client. The assistant may list options with the figures behind each; she chooses. | n/a (level 1) | n/a (below level 2) | Notices: she, or the client next month. Takes over: she at step 3. | B6, B5 | theory |
| 4 Write | Analyse (draft summary, charts and recommendation text; build the PDF) | 2 | Q1: yes until sent; after sending she can only send a correction, and the client has already read it. Q2: no. The whole report is in front of her before step 5, which she does herself. Ceiling 3. Recommended 2, below the ceiling, because it only prepares what she sends. | Her work becomes proofing and figure-tracing, not writing: she reads the whole report and checks the summary numbers and each chart against the comparison table. That time replaces part of the four hours per client; it does not disappear. | Every report (6 a month): every number in the summary, and each chart's period, axis and client name, checked against the comparison table, which the assistant supplies with a source for each number. Starting rate; revisit 2026-12-15. | Notices: she at the proof; otherwise the client. Takes over: she writes or fixes the report by hand at step 4. | B7, B6, B3 | theory |
| 5 Send | Analyse (draft the covering note) | 2 | Q1: yes until sent. Q2: no. She reads it before she sends. Ceiling 3. Recommended 2, below the ceiling, because it only prepares her email. | She reads and edits the note. | Every note (100%) read before sending, as part of the send. Starting rate; revisit 2026-12-15. | Notices: she. Takes over: she writes the note at step 5. | B1 | theory |
| 5 Send | Act (address, attach, send) | 1 | Speaks for her and cannot be undone: ceiling 1 on both counts. Q1: no. A sent email cannot be recalled. Q2: yes. A wrong recipient or attachment leaks one client's data to another at once. The assistant may alert, for example when the PDF's client name does not match the recipient on file; she chooses the recipient, attaches the file and presses send. The assistant's ability to send from her account is not used for this step. | n/a (level 1) | n/a (below level 2) | Notices: she, or the recipient. Takes over: she contacts the wrong recipient and the affected client the same day. | B1 | theory |
| 6 Log | Act (mark the report as sent in the client tracker) | 3 | Q1: yes. She edits the tracker until the invoice is issued. Q2: no. A wrong or missing entry delays an invoice, and the invoice is read as reviewed by her before it goes out (see Not covered). Ceiling 3. Not 4: logging follows her send, so she is present, and no unattended reconciliation is described. The assistant writes the entry once it sees the email in her sent folder, with a link to it as the receipt. | She checks the month's entries before invoicing. | Monthly, before invoicing: the 6 tracker entries matched against the 6 sent emails (100%, a few minutes). Starting rate; revisit 2026-12-15. | Notices: she, at invoicing. Takes over: she corrects the entry at step 6. | B1 | theory |

Basis

```text
[B1] Levels of automation · “Automation is either on or off”: it is not that simple. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/levels-of-automation
[B2] Fitts list (MABA-MABA) · “Hand the task to the AI and that is one job off my plate”: not necessarily. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/fitts-list
[B3] Ironies of automation · Design the human out, and the hardest leftover work still lands on the human. · Human-Automation Interaction · Checked against the sources · https://trigpoint.pub/collections/hai/ironies-of-automation
[B4] Out-of-the-loop performance problem · When the automation failed during the navigation task, the fully automated group took over worst. · Human-Automation Interaction · Abstracts checked · https://trigpoint.pub/collections/hai/out-of-the-loop
[B5] Situation awareness · Seeing the situation and deciding what to do are two abilities; the first is only the input to the second. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/situation-awareness
[B6] Automation complacency & bias · Missing things while monitoring, deferring while deciding: two effects, both rooted in attention. · Human-Automation Interaction · Abstracts checked · https://trigpoint.pub/collections/hai/automation-complacency
[B7] Mental workload (NASA-TLX) · Workload cannot be seen, so people rate their own, yet one overall score hides where the load comes from. · Human-Automation Interaction · Bibliography checked · https://trigpoint.pub/collections/hai/mental-workload-nasa-tlx
```

Not covered:

- Whether the assistant can export from the three tools. Its listed abilities are reading exports, drafting, building a PDF and sending email. If it cannot export, step 1 stays with her (level 0) and the assistant only checks the files.
- Whether invoices go out from the tracker without her review. If they do, a wrong entry travels to the client and step 6 drops to 2.
- Whether the assistant may read her sent folder (used for the step 6 receipt).
- Whether client contracts allow their analytics data to be handled by an AI assistant. Not assessed; this ledger is not a compliance review.
- The error costs are stated without amounts, and the time saved is not estimated; the checks above add review time against the four hours per client.
