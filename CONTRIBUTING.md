# Contributing to the Fractal Architecture Framework (FAF)

Thank you for your interest in FAF. This repository contains a **specification**, not a library: every contribution changes text that defines what a conformant codebase is. These guidelines exist to keep the specification consistent, unambiguous and minimal.

## Before You Start

- The specification ([`FAF.md`](./FAF.md)) is a **Working Draft**: it may change substantially between drafts.
- The specification is currently written **in Italian**. Issues and pull requests may be written in **English or Italian**.
- Read the whole specification before proposing changes. Most rules depend on definitions given elsewhere (e.g. §4 Fondamenti, §6.8 containment matrix, §6.9 classification completeness).

## Kinds of Contribution

Every contribution belongs to exactly one of the following kinds. State the kind in the title of your issue or pull request.

| Kind              | Changes conformance? | Description                                                                                        | Process                                                              |
| :---------------- | :------------------: | :------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------- |
| **Editorial**     |          No          | Typos, grammar, formatting, broken links or anchors. The meaning does not change.                  | Open a pull request directly.                                        |
| **Erratum**       | Yes, restores intent | Contradictions between rules, between rules and examples, or between rules and the matrix in §6.8. | Open an issue, then a pull request.                                  |
| **Clarification** |          No          | Rewording an ambiguous rule so that it admits a single reading, without changing its outcome.      | Open an issue, then a pull request.                                  |
| **Proposal**      |         Yes          | Adding, removing or changing a concept, a norm, a recommendation or a reference model.             | Open an issue and wait for acceptance before writing a pull request. |
| **Translation**   |          No          | Work on the English translation.                                                                   | Open an issue to coordinate, then a pull request.                    |

If you are unsure whether a change alters conformance, treat it as a **Proposal**.

## Opening an Issue

### Errata and Clarifications

Include:

1. The affected section(s), quoted.
2. A concrete case (a directory tree or an import) where the text is contradictory or admits more than one reading.
3. The reading you believe is intended, and why.

### Proposals

Proposals are evaluated by **conceptual economy**, not by the size of the change: a proposal that removes a concept or a rule is as welcome as one that adds them. Include:

1. **Problem**: what a real codebase cannot express, or expresses badly, under the current specification. Provide a concrete directory tree.
2. **Why existing concepts are insufficient**: show that the problem cannot be solved with current Logical Domains, Roles, Horizontal Hierarchies or Declarations.
3. **Proposed text**: the exact wording, in Italian or English, and where it goes.
4. **Impact on conformance**: which currently conformant codebases become non-conformant, and vice versa.
5. **Affected sections**: definitions, laws, containment matrix (§6.8), classification completeness (§6.9), examples, Table of Contents.
6. **Alternatives considered**, including doing nothing.

Tooling (linters, static analysis, fitness functions) is out of scope for this repository: conformance is defined by the specification alone.

## Writing Guidelines for `FAF.md`

### Normative Language

- A **recommendation** is introduced by the formula _è raccomandato_. Every other prescription is a **norm**. Do not use other modal phrasing (e.g. _dovrebbe_, _si consiglia_) for prescriptions.
- Each concept has a **single, exact name**. Do not introduce synonyms for existing concepts.
- Do not introduce a concept that is not necessary to express a norm.
- A Declaration never derogates from a FAF norm: do not write rules that can be overridden by a Declaration unless the specification already provides for it explicitly.

### Terminology and Style

- FAF terms are in **English**, capitalized, and are not translated (e.g. _Logical Node_, _Fragment_, _Access Node_, _Horizontal Hierarchy_). Plurals follow English (e.g. _Fragments_, _Categories_).
- A term is written in _italics_ where it is defined.
- File and directory names, Roles and code are written in `code`.
- File and directory names in examples follow the specification itself (_kebab-case_, `_` prefix for Organizational Logical Domains).

### Examples

- Every example must be **conformant** to the specification as amended by your change.
- Directory trees use the existing format: box-drawing characters and an aligned `<--` annotation for **every** entry, stating its classification (and Rank where relevant).
- Every example is followed by a `> **Nota**:` paragraph that states the Declarations it assumes and the dependencies it allows or forbids.
- Number examples as `Esempio <section>.<n>.` and keep numbering sequential.

### Consistency Checklist

Before submitting a pull request that touches `FAF.md`, verify that:

- [ ] Every definition used is defined in the specification, and with the same name.
- [ ] The containment matrix (§6.8) matches the containment rules.
- [ ] Every file and directory of every example has a unique classification (§6.9).
- [ ] Every example's imports respect the laws of §5 and the visibility rules of the involved Logical Domains.
- [ ] Section numbers, cross-references and the Table of Contents are updated.
- [ ] [`README.md`](./README.md) is still accurate.

The maintainer updates the Working Draft date when merging normative changes.

## Translation

The English translation is in progress. To avoid duplicated work, open an issue stating which sections you intend to translate.

- A translation must preserve the meaning **exactly**. If you find a defect while translating, report it in a separate issue instead of fixing it in the translation.
- FAF terms are already in English: keep them unchanged.
- Translate _è raccomandato_ as **"it is recommended"**, and render norms in the indicative or with **"must"** / **"must not"** consistently.

## Pull Requests

- One pull request addresses one issue and one kind of contribution. Do not mix editorial changes with normative ones.
- Reference the related issue in the description.
- Commit messages follow the [Conventional Commits](https://www.conventionalcommits.org/) format, using the contribution kind as type: `editorial:`, `erratum:`, `clarification:`, `proposal:`, `translation:`, `docs:` (for files other than `FAF.md`), `chore:`.

## Conduct

Discuss ideas, not people. Critique of the specification is welcome and expected: arguments supported by concrete codebases weigh more than preferences.

## License

By contributing, you agree that your contributions are licensed under the same terms as the project: [Creative Commons Attribution 4.0 International](./LICENSE) for documentation, and the BSD 3-Clause License for portions incorporated into source code.
