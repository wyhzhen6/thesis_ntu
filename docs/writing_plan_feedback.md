# v3 Review (Sharpened, vs v2 of 29-04-2026)

Document reviewed: `Question List--yihao--5.2-v3.md`. Compared against v2 (`../29-04-2026/Question List-2--yihao-new.md`), the prior agent review (`../29-04-2026/Question-List-2-yihao_review.md`), and ES's 30-04-2026 email reply on v2 (see `supervisor_notes.md`). Per the 30-04 directive, this review does not re-comment on the abstract: it is byte-identical to v2 and the prior abstract review still applies in full.

## §2.4 — ES's request, well executed

ES emailed on 30-04-2026: *"Ch 2.4 is too short -> it's the star of Ch 2!"* YiHao expanded §2.4 from 2 p / 3 generic SOTA-table bullets to 4 p / 7 diagnostic-thinking bullets. The new bullets probe (a) the Missed-Speech vs Speaker-Confusion ratio between modular and E2E systems, (b) plateauing evidence on AMI / CALLHOME, (c) low-density-prior overfitting, (d) zero-shot generalisation degradation, (e) why high benchmark scores mask high-density vulnerabilities. Question register is now consistent with Ch 3 §3.4 and §2.4 reads as the "star of Ch 2" ES asked for. Outside §2.4 and a new `marp: true` slide-export header, v3 is byte-identical to v2.

## New issue introduced by the §2.4 expansion

[MUST-FIX] **Ch 2 page-budget arithmetic.** Ch 2 is still declared `[20 pages]` but subsections now sum to 22 p (1 abstract + 13 §2.1 + 3 §2.2 + 1 §2.3 + 4 §2.4). Update the heading to `[22 pages]`. Do not trim §2.4: ES endorsed its expansion.

## 29-04 punch list — status

Items from the 29-04 review remain pending (YiHao prioritised ES's §2.4 directive on this round, which is correct). For the next iteration, the priority order is unchanged:

| #   | Item                                                     | Severity   | Status                      |
| --- | -------------------------------------------------------- | ---------- | --------------------------- |
| 1   | Ch 2 ordering reversed (Methods before Datasets)         | MUST-FIX   | pending                     |
| 2   | No Ch 2 → contribution mapping in chapter abstract       | MUST-FIX   | pending                     |
| 3   | Ch 2 abstract is signpost, not abstract                  | MUST-FIX   | pending                     |
| 4   | §1.3 declares 3 contributions vs 2 contribution chapters | MUST-FIX   | pending                     |
| 5   | Ch 3 page balance (14 p vs Ch 2 / Ch 4 at 20 p)          | SHOULD-FIX | pending                     |
| 6   | Ch 2 §2.5 Chapter Summary missing                        | SHOULD-FIX | pending                     |
| 7   | Ch 4 §4.5 → Ch 5 hand-off missing                        | SHOULD-FIX | pending                     |
| 8   | Total page math: body sums short of declared 68 to 73 p  | SHOULD-FIX | pending; gap widened by 2 p |
| 9   | §2.1 has 7 flat subsections                              | MINOR      | pending                     |
| B1  | §2.1.1 first bullet: PYRAMID + VERBOSE-Q                 | SHOULD-FIX | pending verbatim            |
| B2  | §1.2 sole bullet: VERBOSE-Q                              | SHOULD-FIX | pending verbatim            |
| B3  | §3.4 bullet 3: VERBOSE-Q                                 | SHOULD-FIX | pending verbatim            |
| B4  | §4.4.2 bullet 1: VERBOSE-Q                               | SHOULD-FIX | pending verbatim            |

Highest-leverage single fix for the next round remains item 1: reordering Ch 2 to Datasets → Methods forces §2.2 into the 5 to 6 p it needs to motivate Ch 3 and partially resolves the §2.1 flat-list (item 9).

## Slides hand-off (when YiHao sends them)

ES asked the agent to also process the Codex-generated slide draft for Ch 1-2. When the file arrives (PDF or PPTX), the agent will run a structural pass aligned with the question list: do slide section breaks match the §2.1 to §2.4 hierarchy, do Ch 1 contribution slides carry the per-contribution numbers the prior abstract review flagged, are the Ch 2 slides ordered to mirror Datasets → Methods (per item 1) regardless of how the document is currently ordered. No figure-placement commentary.

## Verdict

§2.4 fix lands cleanly and ES's "star of Ch 2" directive is satisfied. Outside §2.4, v3 is v2; the 29-04 punch list and the new Ch 2 page-math regression are the targets for the next iteration.
