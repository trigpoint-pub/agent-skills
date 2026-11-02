# Sources

What the skill takes from published research, what it adds on its own, and how the references were checked.

## Published research

| Used for | Reference |
|---|---|
| Trust should match actual capability (calibration) and tell reliable situations from unreliable ones (resolution); performance and process information support this | Lee, J. D., & See, K. A. (2004). Trust in automation: Designing for appropriate reliance. *Human Factors*, 46(1), 50–80. https://doi.org/10.1518/hfes.46.1.50_30392 |
| As automation proves reliable, checking falls and silent failures go unseen; practice does not remove this; experience of failures may reduce it; explicit instructions to verify do not reliably prevent automation bias (a contested point) | Parasuraman, R., & Manzey, D. H. (2010). Complacency and bias in human use of automation: An attentional integration. *Human Factors*, 52(3), 381–410. https://doi.org/10.1177/0018720810376055 |
| Detection falls off during sustained watching | Mackworth, N. H. (1948). The breakdown of vigilance during prolonged visual search. *Quarterly Journal of Experimental Psychology*, 1(1), 6–21. https://doi.org/10.1080/17470214808416738 |
| Over-reliance and under-use have separate causes; false alarms drive under-use | Parasuraman, R., & Riley, V. (1997). Humans and automation: Use, misuse, disuse, abuse. *Human Factors*, 39(2), 230–253. https://doi.org/10.1518/001872097778543886 |
| The person's residual job is monitoring, which is hard | Bainbridge, L. (1983). Ironies of automation. *Automatica*, 19(6), 775–779. https://doi.org/10.1016/0005-1098(83)90046-8 |

## Statistics

The bound on a clean record ("no defect in n units means the rate could still be up to about 3/n at 95% confidence") is the standard rule of three for zero observed events, from the exact binomial bound 1 − 0.05^(1/n), which is close to 3/n for n of about 20 or more. It assumes independent units sampled at random.

## What the skill adds on its own

These are working choices from the studio that wrote the skill. They are not taken from the references above:

- **The starting rates, the floors, and the 20-unit clean run.** The cited research gives the direction (checks should not fall to nothing; trust should follow performance), not these numbers.
- **The three cost tiers** and the rule that a tier C step acting on its own is out of scope.
- **The idea that a sample check is a deliberate way of collecting failure experience.** Parasuraman and Manzey note that experience of automation failures may reduce complacency; they do not list sampling checks as a countermeasure. Treating sampling this way is the studio's inference.
- **The miss log format and the raise and lower rules.**

## How the references were checked

Each reference was taken from a node of the Human-Automation Interaction shelf at trigpoint.pub, where its bibliography was checked before publication. The verification status in `references/basis-index.md` is the status shown on that node's page. Points that the node's page marks as checked only against an abstract, or as contested, are stated here at that level.

## Third-party material

The skill text, the plan template and the example are written for this repository. The basis index reproduces each node's title and one-line intro from the public theory layer of the shelf, which is open for reuse with attribution and a link to the page; each row carries that link. No figures, tables or text from the papers are reproduced.
