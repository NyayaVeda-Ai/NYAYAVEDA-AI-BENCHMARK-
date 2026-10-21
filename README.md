# NyayaVeda AI — Legal Accuracy Benchmark

Institutional benchmark data, KPI evaluations, and validation outputs for NyayaVeda AI.

Published for independent verification by lawyers, law faculties, law firms, researchers, auditors and investors.

[![NyayaVeda AI](https://img.shields.io/badge/NyayaVeda_AI-nyayaveda.co.in-D97706?style=flat-square)](https://www.nyayaveda.co.in)
[![Benchmark Date](https://img.shields.io/badge/Benchmark-20_October_2026-blue?style=flat-square)]()
[![Questions](https://img.shields.io/badge/Questions-600-green?style=flat-square)]()
[![NVIDIA Inception](https://img.shields.io/badge/NVIDIA_Inception-member-76B900?style=flat-square&logo=nvidia&logoColor=white)]()

The results page on the website: **[nyayaveda.co.in/benchmark](https://www.nyayaveda.co.in/benchmark)**.

**Everything a figure below rests on is in this repository:** every question, every answer exactly as the user received it, every grade with the quotes from the answer it rests on, and every score with its population and 95% interval. Pick any row and check it.

---

## Results: 600 questions, 20 October 2026

Asked of the production pipeline of NyayaVeda AI (release r91: the code, corpus and models that serve users), Enterprise plan, answer cache off, each question once: 100 in each of 6 areas of Indian law. 488 answered, 111 declined, 1 timed out. Time per answer, in process: median 32.0 s, 95th percentile 50.4 s.

| Area | What it measures | Result | k / n | 95% interval |
|---|---|---|---|---|
| **Citations grounded in the sources given** | of the citations an answer makes, the share found in the sources it was written from (higher is better) | **87.6%** | 1,964 / 2,242 | 86.0 - 89.2% |
| **IPC/CrPC to BNS/BNSS transition** | drafts that charge under the code the offence date requires and register under the code in force at filing (higher is better) | **86.0%** | 86 / 100 | 77.9 - 91.5% |
| **Fabricated citations and sections rejected** | questions naming a citation or section that cannot exist, rejected (higher is better) | **97.0%** | 97 / 100 | 91.5 - 99.0% |
| **Hindi and Hinglish questions** | answers that identify the provision a Hindi or Hinglish question names (higher is better) | **98.0%** | 98 / 100 | 93.0 - 99.4% |
| **Personal data repeated in the answer** | answers that repeat an injected (synthetic) Aadhaar, PAN, phone number or victim's name (lower is better) | **0.0%** | 0 / 95 | 0.0 - 3.9% |
| **Overruled law relied on as good law** | answers that rely on a displaced judgment as current law (lower is better) | **12.0%** | 9 / 75 | 6.4 - 21.3% |
| **Overruled and per incuriam authority recognised** | answers that state a displaced authority to be displaced and do not rely on it (higher is better) | **52.0%** | 52 / 100 | 42.3 - 61.5% |
| **Split benches: which opinion binds** | answers whose verdict on which opinion binds under Article 141 matches the bench (higher is better) | **47.0%** | 47 / 100 | 37.5 - 56.7% |

**How to read a row.** The result is a share: k of n questions (or citations). The 95% interval is the range the true value lies in, given these n. A *decline* is the system stating that its sources do not support an answer, which it does rather than guess; in the accuracy areas a decline counts as a miss. Full definitions: [METHODOLOGY.md](METHODOLOGY.md).

The run's own page, with every file: [`runs/2026-10-20_release-r91_600-cases/`](runs/2026-10-20_release-r91_600-cases/) (one-page PDF included).

## Earlier runs on the same plan

| Area | 1 Oct 2026 (1,959 questions, r49) | 9 Oct 2026 (60, r74) | 20 Oct 2026 (60, r91) | **20 Oct 2026 (600, r91)** |
|---|---|---|---|---|
| Citations grounded in the sources given | 76.0% (5,880 / 7,732) | 87.7% (179 / 204) | 90.8% (226 / 249) | **87.6%** (1,964 / 2,242) |
| IPC/CrPC to BNS/BNSS transition | 76.2% (234 / 307) | 90.0% (9 / 10) | 100.0% (10 / 10) | **86.0%** (86 / 100) |
| Fabricated citations and sections rejected | 99.5% (379 / 381) | 100.0% (10 / 10) | 100.0% (10 / 10) | **97.0%** (97 / 100) |
| Hindi and Hinglish questions | 95.5% (364 / 381) | 100.0% (10 / 10) | 100.0% (10 / 10) | **98.0%** (98 / 100) |
| Personal data repeated in the answer | 19.3%\* (70 / 363) | 10.0% (1 / 10) | 0.0% (0 / 10) | **0.0%** (0 / 95) |
| Overruled law relied on as good law | 9.2% (21 / 229) | 0.0% (0 / 5) | 11.1% (1 / 9) | **12.0%** (9 / 75) |
| Overruled and per incuriam authority recognised | 50.3% (150 / 298) | 40.0% (4 / 10) | 80.0% (8 / 10) | **52.0%** (52 / 100) |
| Split benches: which opinion binds | 52.6% (111 / 211) | 30.0% (3 / 10) | 40.0% (4 / 10) | **47.0%** (47 / 100) |

Every run here is drawn from the same frozen plan as the 1 October run (the 600-question run takes its first 100 of each area; the 60-question runs, its first 10). The runs in [`runs/`](runs/) carry all their data; the 1 October figures come from that run's own report and its data is not part of this release. With 10 questions an area a difference smaller than about 25 to 45 points is not established, with 100 about 8 to 14. \* Measured before a masking fix; re-measured on 3 October 2026 after it: 0.3%.

## What is in this repository

```
README.md            this page
METHODOLOGY.md       how the questions were built, how each area is scored, how the readers were validated, limits
NOTICE.md            data attribution and licences
CITATION.cff         how to cite this benchmark
runs/
  <date>_release-<release>_<n>-cases/
    README.md        the run's table and definitions
    questions.jsonl  every question: area, the facts it is built on, what a correct answer must do, the gold
    answers.jsonl    every answer as the user received it, answered or declined, and its time
    grades.jsonl     the reader's verdict on each graded answer, with the exact quotes from the answer
    scores.json      each area's value, k, n, 95% interval, definition and population
    SHA256SUMS       a checksum of every file in the folder
```

## How to verify a result yourself

1. **Integrity.** In a run folder: `sha256sum -c SHA256SUMS`. Every file must report OK.
2. **A grade.** Pick an `id` in `grades.jsonl`. Every quote under `evidence_quoted_from_the_answer` occurs word for word in the answer with the same `id` in `answers.jsonl`, and the verdict follows the criteria the question carries in `questions.jsonl` (`a_correct_answer_must`, `gold`).
3. **The law.** Look up any precedent or provision an answer cites in the official reports and check that it says what the answer says it does. An answer marks each citation it could not verify against its own sources (`[CITATION UNVERIFIED]`, `[AUTHORITY NOT CONFIRMED]`).
4. **A score.** Count the verdicts of an area and compare with `scores.json`. Hindi/Hinglish, and personal data for the injected names, are scored by code alone and can be recomputed from the answers and the gold. The injected Aadhaar, PAN and phone numbers are synthetic but have real formats, so they are withheld (`[PHONE withheld]` ...); that part of the check is available for an audit on request.
5. **Another system.** Ask it the questions in `questions.jsonl` and score its answers by [METHODOLOGY.md](METHODOLOGY.md).

## What this benchmark does not show

- **No advocate has reviewed the grades yet.** They are automated and validated against hand reading by our engineering team. We invite advocates, law faculties and firms to review any of them.
- Retrieval recall against a gold set, ratio/obiter precision, the provision in force on a given date, and state amendments are not yet measured, for want of gold of the required kind.
- Writing style, conversational quality and unreported judgments are not measured.
- Citation precision measures grounding in the sources given, not whether an authority exists: a real authority cited from memory counts as a miss.

## Comparison policy

NyayaVeda AI does not publish comparisons against named competitors. The benchmark is system-agnostic: any legal AI can be evaluated on the same questions with the same rubric. If you evaluate another system and publish the results, please follow [METHODOLOGY.md](METHODOLOGY.md) without modification so the results are comparable.

## Citation

If you use this benchmark in research, please cite:

> NyayaVeda AI Legal Accuracy Benchmark, 20 October 2026. Tripathi, Abhay. NyayaVeda AI. https://github.com/NyayaVeda-Ai/NYAYAVEDA-AI-BENCHMARK-

(also in [CITATION.cff](CITATION.cff)).

## Data attribution

The answers were written from a corpus compiled from public Indian court records and legislation; several sources grant use on the condition of attribution. Details in [NOTICE.md](NOTICE.md). The law text itself is a Government work under s.17(d) of the Copyright Act, 1957.

## Contact

| | |
|---|---|
| Verification enquiries | support@nyayaveda.co.in |
| Research partnerships | abhay@nyayaveda.co.in |
| Website | [nyayaveda.co.in](https://www.nyayaveda.co.in) |
