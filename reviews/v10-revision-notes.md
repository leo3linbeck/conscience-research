# "Conscience is All You Need" v10: Revision Notes

**Date:** 5 November 2026
**Source draft:** `drafts/Conscience is All You Need.v4.docx` (the only manuscript in the repository; the v9 manuscript reviewed in `peer-review-v9-2026-04-08.md` is not checked in)
**Outputs:** `drafts/Conscience is All You Need.v10.md` (source), `drafts/Conscience is All You Need.v10.docx`, figures in `drafts/media-v10/`
**Branch:** `jev` (rebased from `ga-alpha-phase0`; `jev` carries the newer trial)
**Evidence base:** `guardian-angel/README.md` on `jev` (trial results and harness caveats), commit history of September 2026, `tests/wrappers/default.txt`, `tests/scenarios/`
**Runs used:** production run-20260922-221812 (headline: current production prompt, conditions C and D); reference run-20260922-053624 (conditions A/B/C, per-tier breakdown, ground truth 163/177)

## Before submission: values to fill in

These are marked ⟦pending⟧ / ⟦…⟧ in the manuscript. Condition A was run in run-20260922-053624, but its figures are not committed to the repository.

1. **Table 6, condition A column**: harm prevented, sensitivity, benign scenarios unblocked, and specificity for built-in safety, all from `tests/results/run-20260922-053624/report.md`. Once these are in, decide whether to restore a head-to-head claim and a McNemar test (the v9 peer review asked for one) in Sections 1, 6.6, 7.7, 7.9 (item 2) and 8.
2. **Section 7.4, Latency**: per-tier median, p95 and p99, plus end-to-end scenario overhead against condition A, from the runs' `summary.json`. Only the mean System 2 time per scenario for the production run (5.7 s) is in the repository.
4. **Production run's A/B results, if any.** The `jev` README reports only conditions C and D for run-20260922-221812. If A and B were run, use them in place of the reference run's ground truth.
3. **Tier of the one tool-call FP.** The README gives FP = 1 overall without saying which tier made it. The manuscript makes no per-tier zero-error claim for the champion run.

## What changed and why

| Area | v4 | v10 | Driver |
|---|---|---|---|
| Headline result | 97–98% vs. 92.7% sensitivity against Claude, 220 scenarios | Production prompt: 0 harmful scenarios produced harm; specificity 99.4% (178/179); 4.8% of tool calls reach the principal. Reference run: 163/163 verified harms blocked (CI 97.8–100%) | run-20260922-221812 and run-20260922-053624 |
| April figures | Presented as results | **Withdrawn**, with an explanation (Section 7.3) | Harness defects: shared mock-server network, evidence-checker bugs, download counted as execution, and a run that mixed two configurations |
| Architecture | System 1 = whitelist/blacklist; System 2 = LLM with an Ambiguity × Stakes score | System 0 reflex → System 1 jev classifier → System 2 LLM → principal. One shared morality prompt, APPROVE/REJECT/ESCALATE at every tier | GA v5/v6 commits |
| Moral judgment | Ambiguity × Stakes matrix | Two axes: Step A (moral status: GOOD/BAD/INTRINSICALLY EVIL/UNCLEAR) and Step B (what the principal directed), combined by fixed rules (Step C) | commit e867176: trial false negatives where "they asked" collapsed into APPROVE |
| Synderesis list | Theft, vandalism, lying (sketched) | Full current list, including impersonation/hijack and the "a label is not proof" destination rule; flow direction, named harm, deception by stated-purpose mismatch, and the ESCALATE ceiling on re-attempts | `default.txt`, commits d39062b, b621b34, e7e9249, 25a9e14 |
| Illative sense | Mapped to the Ambiguity × Stakes score | Mapped to convergence within Step A and to the inter-tier dissent guard ("Newman's cable") | GA README |
| Cross-model | Claude Haiku as System 2 (limitation) | Gemini 2.5 flash as System 2: partial cross-vendor evidence (Section 7.7, RQ4) | Revision plan item 20 |
| Metrics | Scenario-level only | Per-tier FP / FN / escalation rate, plus scenario-level metrics | GA v6 |
| Bad-faith principal (6.2) | `rm -rf /` escalated to the principal | Intrinsic evil is rejected even when requested; the principal can still act outside the agent; three cases distinguished | Step C rules |
| New sections | none | 6.8 Attacks on the conscience itself (threat model, salami and work-around attacks, System 1 firewall blind spot); 7.6 run-to-run noise band and prompt compression; 7.1 table of tested vs. proposed components; 7.3 measurement integrity; 7.5 failure analysis; 7.6 prompt tuning and the key-set noise lesson; 7.8 toward deployment (alpha) | Revision plan items 2, 9, 12, 22; trial history |
| Framing | "matches or exceeds"; "structurally incapable" | Primary mechanism, with Levels 2–3 scoped; parity and superiority claims held until condition A is in | v9 peer review, major comment 1 |
| Intro | Scope stated late | Scope and four research questions (RQ1–RQ4) in Section 1 | Revision plan items 6 and 16 |
| Related work | No agent-safety benchmarks | AgentDojo, InjecAgent, AgentHarm, ToolEmu, R-Judge, Agent-SafetyBench; why virtue ethics; Arrow's theorem developed | Revision plan items 10, 17, 18 |
| Ostrom (3.4) | Mapping only | Acknowledges the limits of a bounded commons and collective risk; diffuse principals in 6.6 | Revision plan items 13 and 19 |
| Figure 3 | Two-tier Ambiguity × Stakes diagram | New three-tier diagram with run counts (`media-v10/figure3-architecture.{html,png}`) | Architecture change |
| Footnotes | Note 45 empty; Constitutional AI credited to Amodei | Note 45 filled; Constitutional AI credited to Bai et al.; notes 37, 48, 49, 50 and 53 dropped because their text was removed; notes 56–63 added | Housekeeping |

## Still open (not addressed in v10)

- Independent red-teaming, a held-out test set, and evaluation on public benchmarks (Limitations 1 and 4).
- Abstract length: about 250 words, down from about 350. Trim further if the venue requires 200.
- Sections 3.1–3.2: lightly tightened, not cut by the full ~20% the revision plan suggested.
- Figure 1 (top-down vs. CSM comparison, EMF) is carried over from v4 unchanged. Check that it still matches the text.
- Figure 2 (principal-agent model) is carried over from v4 unchanged.
