# Contributing to the PH Education Data Standards Handbook

Thank you for your interest in contributing. This handbook is a community-proposed standard and improves through open, evidence-based discussion. All backgrounds are welcome — you don't need to be a developer or data scientist to contribute.

---

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Ground Rules](#ground-rules)
- [How to Propose a Change (Pull Request)](#how-to-propose-a-change-pull-request)
- [How to Report an Error or Ask a Question (Issue)](#how-to-report-an-error-or-ask-a-question-issue)
- [How to Start a Broader Discussion](#how-to-start-a-broader-discussion)
- [What Makes a Good Proposal](#what-makes-a-good-proposal)
- [Review Process](#review-process)
- [Style Guide](#style-guide)

---

## Ways to Contribute

| Type | How |
|------|-----|
| Fix a typo or formatting error | Pull Request |
| Correct a factual error (wrong code, outdated standard) | Pull Request + Issue explaining the correction |
| Propose a new data element or field | GitHub Discussion first, then Pull Request |
| Propose a change to an existing standard | GitHub Discussion first, then Pull Request |
| Report that a referenced standard has been updated | Issue |
| Add a missing Philippine-specific code table or reference | Pull Request |
| Translate a section to Filipino | Pull Request (place in `translations/` folder) |

---

## Ground Rules

1. **Be respectful.** This is a collaborative effort. Critique ideas, not people.
2. **Cite your sources.** Every normative change (a change to what is required or recommended) must reference a supporting standard, law, regulation, or documented practice. "I think it should be this way" is not sufficient on its own.
3. **Separate discussion from changes.** If you are unsure whether a change should be made, open a Discussion first. Pull Requests are for changes you are confident are correct and supportable.
4. **One concern per issue or PR.** Keep things focused so they can be reviewed and resolved cleanly.
5. **Normative vs. informative.** Be clear whether your contribution is normative (defines a requirement) or informative (provides explanation or guidance). Use "shall" for normative requirements and "should" or "may" for recommendations.

---

## How to Propose a Change (Pull Request)

1. **Fork** this repository to your GitHub account.
2. **Create a branch** with a descriptive name, e.g., `fix/psgc-region-codes` or `add/ip-community-field`.
3. **Make your changes** in the relevant Markdown file(s) under `handbook/`.
4. **Update `CHANGELOG.md`** with a one-line description of your change under the `[Unreleased]` section.
5. **Open a Pull Request** against the `main` branch. Fill in the PR template.

### PR Template

When opening a PR, please include:

```
## Summary
What does this change, and why?

## Standard or Legal Basis
Which ISO standard, Philippine law, PSA publication, or agency regulation supports this change?
(e.g., ISO 8601:2019, PSA PSGC Q1 2026 release, RA 10173 IRR Section X)

## Type of Change
- [ ] Typo / formatting fix (no review required)
- [ ] Factual correction (requires one maintainer approval)
- [ ] New field or data element (requires Discussion + two maintainer approvals)
- [ ] Change to existing normative requirement (requires Discussion + two maintainer approvals)

## Related Issue or Discussion
Closes #[issue number] / See discussion #[discussion number]
```

---

## How to Report an Error or Ask a Question (Issue)

Use the [Issues](https://github.com/cair-philippines/ph-education-data-standards/issues) tab.

**Choose the appropriate template:**
- 🐛 **Correction** — a field format, code, or reference is wrong
- 📋 **New Field Proposal** — a data element is missing
- ⚠️ **Outdated Standard** — a referenced standard has been revised
- ❓ **Question** — you need clarification on how to apply a standard

---

## How to Start a Broader Discussion

For larger questions — should we add a field for IP/indigenous community affiliation? How should we handle foreign schools in student transfer records? — use [GitHub Discussions](https://github.com/cair-philippines/ph-education-data-standards/discussions).

Discussions that reach consensus may be formalized into a Pull Request.

---

## What Makes a Good Proposal

✅ **Good proposals:**
- Are specific ("The region_code field in Section 4.4 should use a 2-digit string, not integer, because PSGC codes include leading zeros")
- Cite a source (ISO standard, PSA publication, CHED memorandum, law)
- Explain the impact ("Without this change, region '01' Ilocos would be stored as '1', breaking sort order and joins")
- Are scoped to one issue

❌ **Proposals that will be returned for revision:**
- Do not cite any supporting standard or practice
- Propose removing a field without explaining the rationale
- Combine multiple unrelated changes in one PR
- Introduce fields that collect unnecessary personal data without a privacy justification

---

## Review Process

| Change Type | Required Approvals | Typical Timeline |
|-------------|-------------------|-----------------|
| Typo / formatting | 1 maintainer | 2–5 days |
| Factual correction | 1 maintainer | 1–2 weeks |
| New field (non-sensitive) | 2 maintainers | 2–4 weeks |
| New sensitive/personal data field | 2 maintainers + Discussion period (min. 2 weeks) | 4–6 weeks |
| Change to normative requirement | 2 maintainers + Discussion period (min. 2 weeks) | 4–6 weeks |

Maintainers may request additional review from domain experts (PSA, NPC, CHED, DepEd, TESDA practitioners) for significant changes.

---

## Style Guide

- Write in **plain English**. Avoid jargon where a simpler word works.
- Use **"shall"** for mandatory requirements, **"should"** for recommendations, **"may"** for options.
- Field names always in `code formatting` (backticks).
- Standards always cited with full name and year on first use: *ISO 8601:2019* — subsequent references may use the short form *ISO 8601*.
- Philippine laws cited as: *Republic Act No. XXXXX (Short Title)*, e.g., *Republic Act No. 10173 (Data Privacy Act of 2012)*.
- Tables are preferred over prose lists for field specifications.
- Keep each handbook section self-contained — do not rely on readers having read other sections first.

---

Thank you for helping make Philippine education data better. 🇵🇭
