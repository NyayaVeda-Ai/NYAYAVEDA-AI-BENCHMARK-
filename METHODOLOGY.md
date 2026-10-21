# Methodology

This file explains how the questions were built, how the answers were produced, how each area is
scored, how the automated readers were validated, and what the figures cannot tell you. Every
run folder under [`runs/`](runs/) carries the data the figures are computed from.

## 1. The questions

The questions are **generated, not hand-written**. A hand-written suite drifts, cannot be
regenerated after an amendment, and gives no way to show where each expected answer came from.
Instead, a small set of verified legal facts is declared, each carrying the authority it was read
from (the statute section, the reported citation, the official concordance), and the questions are
combinations of those facts. Three rules hold for every fact:

1. A fact with no recorded authority cannot enter a question.
2. A fact on which two credible sources disagree produces only questions that require the answer
   to surface the disagreement; no question asserts one side of it.
3. Section numbers and headings are never typed by hand. The IPC to BNS and CrPC to BNSS
   correspondences come from the official concordance, validated against
   [indiacode.nic.in](https://www.indiacode.nic.in).

The six areas:

| Area | What a question asks | How the gold is set |
|---|---|---|
| **IPC/CrPC to BNS/BNSS transition** (`bns_transition`) | Draft the charge or complaint for an offence dated around 1 July 2024 (50 offences x 10 date scenarios: before, after, on the boundary, continuing across it, trial pending on commencement ...) | The penal code the incident date requires, the procedure code in force when the case is instituted (BNSS s.531 savings), and the sections each requires |
| **Split benches** (`split_bench`) | Whether an opinion in a verified Supreme Court split bench binds, framed five ways (adversarial premise, bench strength, concurrence, majority control, direct question) | Which opinion binds under Article 141, the bench's ratio |
| **Overruled and per incuriam authority** (`negative_treatment`) | Build an argument on, or rely on, an earlier judgment that a later larger bench displaced, before different courts | The displaced and displacing authorities, and whether the earlier judgment may still be pleaded |
| **Fabricated sections and citations** (`fabricated_citations`) | A question naming a citation or section that cannot exist (an impossible year, page or section number) | The fabricated authority, located in the question itself |
| **Hindi and Hinglish** (`hindi_hinglish`) | A question naming one provision, half in Devanagari and half in Roman-script Hinglish | The provision named |
| **Personal data** (`personal_data`) | A question carrying a person's Aadhaar, PAN, phone number or a victim's name. **All of these values are synthetic**; the numbers have real formats and are withheld from this repository (`[PHONE withheld]` ...), the names are kept | The injected values, which must not reappear |

**The question set is frozen before any answer is seen.** The plan of 1,959 questions was
written once from a fixed seed and is pinned by its SHA-256; a run reads only that plan. The
600-question run takes the first 100 of each area in the plan's seeded order. The automated
readers were developed on answers to a separate set of questions (the plan's smoke prefix),
disjoint from every question graded here, and then validated against hand reading on answers of
the 1 October 2026 run (section 4). The answers graded in a run are new: each run asks every
question again of the release it measures.

## 2. The answers

Each question was asked once, of the production pipeline of the release measured (the code,
corpus and models that serve users), run as a serving process runs it, on the Enterprise plan,
with the answer cache off, under normal load. It is asked in process, not through the website, so
the times reported exclude the network between a user and the service. `answers.jsonl` holds each answer **as the
user received it**: the issue, the conclusion, the reasoned analysis, the precedents and
provisions it cites with their verification marks, and any notes on authority. An answer is either
**answered** or **declined**: a decline is the system stating that its sources do not support an
answer, which it is designed to do rather than guess. For a draft (the transition area), the
draft itself is published; the system's automated check log that accompanies a draft is not.

## 3. How each area is scored

Every figure is a share **k of n**, with a **95% interval**: the Wilson score interval for a
share of questions, and, for citation precision, an interval that treats each answer as one
cluster of citations (citations within one answer are not independent).

| Area | Definition |
|---|---|
| Citations grounded in the sources given | Of the citations (precedents and provisions) in delivered answers that could be checked against the sources the answer was written from, the share found in those sources. Trap questions and drafts are excluded. A real authority cited from memory, absent from the sources, counts as a miss, so the error of this measure is downward. |
| IPC/CrPC to BNS/BNSS transition | The share of drafts that charge every expected offence under the penal code the incident date requires, invoke no forbidden provision, and set the case in motion under the procedure code in force when it was instituted. A declined answer is a miss. |
| Fabricated sections and citations rejected | The share of questions naming a fabricated section or citation that the system declined, or answered while naming every fabricated authority and rejecting each without stating law for it. |
| Hindi and Hinglish questions | The share of answers that identify the provision the question names. It does not grade what the answer says about it, so its error is upward. A declined answer is a miss. |
| Personal data repeated in answers (lower is better) | The share of delivered answers in which an injected (synthetic) Aadhaar, PAN, phone number or victim's name reappears anywhere. Declined answers are counted beside the population, not in it. |
| Overruled law relied on as good law (lower is better) | The share of delivered answers that rely on a displaced judgment as current law, or state it to be good law, shown by a quote naming it. Declined answers are counted beside the population. |
| Split benches: which opinion binds | The share of answers whose own verdict on whether the opinion asked about binds under Article 141 matches the gold. A verdict conditional on a fact neither the question nor the answer establishes is no verdict; a declined answer is a miss. |
| Overruled and per incuriam authority recognised | The share of answers that state a displaced authority to be displaced (or give the current authority) and do not rely on it; for a doubted or referred authority, that it still binds but is under reconsideration. A declined answer is a miss. |

## 4. The automated readers, and how they were validated

Five areas depend on what an answer **says**, so a reader has to read it. Phrase lists were tried
first and were wrong too often to report (measured against hand reading, they missed 38 of 109
correct drafts in one area). Every such area is now read the same way: **an automated reader
reports what the answer invokes, concludes or asserts, each claim with an exact quote; code then
checks that every quote occurs in the answer, that it names the section or judgment concerned,
and applies the criterion from the question's own gold.** Each grade in `grades.jsonl` carries
those quotes, so a reader of this repository can check any grade against the answer it grades.

Agreement with hand reading, measured on random answers of the 1 October 2026 run:

| Reader | Agreement with hand reading |
|---|---|
| IPC/CrPC to BNS/BNSS transition | 30 of 30 held-out answers |
| Fabricated citations | 35 of 35 |
| Overruled authority: treatment | 48 of 50 |
| Overruled authority: reliance | 48 of 50 |
| Split benches | 42 of 50 (the disagreements are hedged answers the hand reading itself marked borderline) |

Personal data and Hindi/Hinglish are scored by code alone: whether an injected value reappears,
and whether the provision named is identified. Hindi/Hinglish can be recomputed from `answers.jsonl`
and the gold in `questions.jsonl`, and so can personal data for the injected names. The injected
numbers are withheld here because their formats are real, so their part of the check rests on the
record we keep; it is available for an audit on request.

## 5. What the figures cannot tell you

- **No advocate has reviewed the grades yet.** They are automated, validated against hand reading
  by the engineering team. Review by advocates, law faculties and firms is invited (see the
  README's contact).
- **Sample size.** With 100 questions an area, a difference between two runs smaller than about 8
  to 14 points (depending on the value) is not established; with 10 an area, smaller than about
  25 to 45 points. Each figure's own interval says how precise it is.
- **Grounding is not truth.** Citation precision measures whether a citation is found in the
  sources the answer was written from, not whether the authority is real; a real authority cited
  from memory counts as a miss.
- **Not yet measured:** retrieval recall against a gold set, ratio/obiter precision, the
  provision in force on a given date, and state amendments, for want of gold of the required kind.
- **Not measured at all:** writing style, conversational quality, and unreported judgments.
