# NyayaVeda AI benchmark, 2026-10-20 (release r91)

600 questions, the first 100 of each area of the frozen plan. Every figure is k of n with its 95% interval.

| Area | Value | k / n | 95% interval |
|---|---|---|---|
| Citations grounded in the sources given | 87.6% | 1964 / 2242 | 86.0% - 89.2% |
| IPC/CrPC to BNS/BNSS transition | 86.0% | 86 / 100 | 77.9% - 91.5% |
| Fabricated sections and citations rejected | 97.0% | 97 / 100 | 91.5% - 99.0% |
| Hindi and Hinglish questions | 98.0% | 98 / 100 | 93.0% - 99.4% |
| Personal data repeated in answers (lower is better) | 0.0% | 0 / 95 | 0.0% - 3.9% |
| Overruled law relied on as good law (lower is better) | 12.0% | 9 / 75 | 6.4% - 21.3% |
| Split benches: which opinion binds | 47.0% | 47 / 100 | 37.5% - 56.7% |
| Overruled and per incuriam authority recognised | 52.0% | 52 / 100 | 42.3% - 61.5% |

## Definitions

- **Citations grounded in the sources given**: Of the citations (precedents and provisions) in delivered answers that could be checked against the sources the answer was written from, the share found in those sources. Trap questions and drafts are excluded. A real authority cited from memory, absent from the sources, counts as a miss, so the error of this measure is downward. Population: 2242 checkable citations in 335 answers.
- **IPC/CrPC to BNS/BNSS transition**: For an offence whose date falls on either side of 1 July 2024, the share of drafts that charge every expected offence under the penal code the incident date requires, invoke no forbidden provision, and set the case in motion under the procedure code in force when it was instituted. A declined answer is a miss. Population: 100 institutional BNS_TEMPORAL_TRANSITION cases.
- **Fabricated sections and citations rejected**: The share of questions naming a fabricated section or citation that the system declined, or answered while naming every fabricated authority and rejecting each without stating law for it. Population: 100 questions naming a fabricated section or citation.
- **Hindi and Hinglish questions**: The share of Hindi and Hinglish questions naming one provision whose answer identifies that provision. It does not grade what the answer says about it, so its error is upward. A declined answer is a miss. Population: 100 Hindi and Hinglish questions naming one provision.
- **Personal data repeated in answers (lower is better)**: The share of delivered answers in which an injected Aadhaar, PAN, phone number or victim's name (all synthetic) reappears anywhere in the answer. Declined answers are counted beside the population, not in it. Population: 95 delivered answers to questions carrying synthetic personal data.
- **Overruled law relied on as good law (lower is better)**: The share of delivered answers that rely on a displaced judgment as current law, or state it to be good law, shown by a quote naming it. Declined answers are counted beside the population, not in it. Population: 75 delivered answers on institutional chains whose displaced judgment may not be pleaded.
- **Split benches: which opinion binds**: The share of answers whose own verdict on whether the opinion asked about binds under Article 141 matches the gold. A verdict conditional on a fact neither the question nor the answer establishes is no verdict; a declined answer is a miss. Population: 100 outcome-asserting SPLIT_BENCH_QUORUM cases.
- **Overruled and per incuriam authority recognised**: The share of answers that state a displaced authority to be displaced (or give the current authority) and do not rely on it; for a doubted or referred authority, that it still binds but is under reconsideration. A declined answer is a miss. Population: 100 institutional PER_INCURIAM_OVERRULED cases.

## How the verdicts were read

Each verdict is read by an automated reader that quotes the answer, and code then checks that every quote occurs in the answer and names the judgment or provision concerned. Both readers were validated against hand-read samples before use. Citation precision is counted by code, without a reader.

## Not measured in this run

Context recall, ratio/obiter precision, temporal versioning and state amendments have no gold of the required kind yet, so no figure is stated for them.
