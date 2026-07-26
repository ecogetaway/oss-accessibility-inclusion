# Citation audit

Verification of every legal and regulatory claim in this repository's public
documentation against primary sources.

**Audited:** 2026-07-26
**Scope:** `README.md`, `ACCESSIBILITY.md`, `problem-definition.md`
**Method:** each claim checked against the official text or the issuing body's own
publication. Where only a secondary source could be reached, that is stated
explicitly rather than passed off as verified.

**Summary:** four sub-claims examined. Two verified. One overstated (a standard
described as if it were legislation). One out of date (US position changed in April
2026, after which this repository was first published).

---

## Claim 1 — `README.md`, "The Accessibility Review Gap"

> Accessibility is now a legal requirement in a growing share of the world: the ADA
> in the US, EN 301 549 in the EU, and the European Accessibility Act (in force since
> 2019; obligations applying since June 28, 2025).

Four separable assertions. Assessed individually below.

---

### 1a. EAA "in force since 2019" — **verified**

Directive (EU) 2019/882 was adopted 17 April 2019, published in the Official Journal
7 June 2019 (OJ L 151), and entered into force twenty days after publication.

- **Source:** EUR-Lex, Directive (EU) 2019/882 — https://eur-lex.europa.eu/eli/dir/2019/882/oj/eng
- **Accessed:** 2026-07-26
- **Verdict:** accurate as written.

---

### 1b. EAA "obligations applying since June 28, 2025" — **verified**

Article 2(2) states the Directive applies to the listed services provided to
consumers after 28 June 2025. Article 31 set the Member State transposition deadline
at 28 June 2022.

- **Source:** EUR-Lex, as above
- **Accessed:** 2026-07-26
- **Verdict:** accurate as written.

*Optional addition:* there is a transition allowance to 28 June 2030 for products and
services already on the market before the application date, provided they are not
substantially modified. Not required for our argument, but relevant to any reader
assessing how binding the obligation currently is.

---

### 1c. "EN 301 549 in the EU" — **overstated**

EN 301 549 is a **harmonised European standard**, developed by CEN, CENELEC and ETSI.
It is not legislation and imposes no obligation by itself.

Its legal effect is indirect. Directive (EU) 2016/2102 (the Web Accessibility
Directive, covering public sector bodies) provides that content conforming to
harmonised standards published in the Official Journal is *presumed* to conform with
the Directive's accessibility requirements. EN 301 549 was published in the OJ for
that purpose. The EAA operates through the same presumption-of-conformity mechanism.

So the sentence places a technical standard in a list of laws, as though the standard
were itself the mandate. The obligation comes from the directives; EN 301 549 is the
yardstick by which compliance is demonstrated.

This is the kind of error that costs disproportionately: a reviewer with any
regulatory background reads it as a sign we do not understand the instruments we are
citing, and then discounts the rest.

- **Sources:**
  - ETSI, EN 301 549 V3.2.1 (2021-03), harmonised European standard —
    https://www.etsi.org/deliver/etsi_en/301500_301599/301549/03.02.01_60/en_301549v030201p.pdf
  - W3C WAI, European Union policy page —
    https://www.w3.org/WAI/policies/european-union/
- **Accessed:** 2026-07-26
- **Verdict:** requires rewording.

**Also missing:** no version is cited. The version currently in legal effect is
V3.2.1 (March 2021), cited in the Official Journal via Commission Implementing
Decision (EU) 2021/1339. A revision (V4.1.1) has been anticipated for 2026 — worth
tracking, since it would change what "conformance with EN 301 549" means.

> **Unverified:** the Implementing Decision reference and the V4.1.1 timing came from
> secondary sources. Both should be confirmed against EUR-Lex and the ETSI work
> programme before the corrected text is published.

---

### 1d. "the ADA in the US" — **out of date, and underspecified**

Two problems.

**Underspecified.** The ADA itself (1990) does not address web content. The specific
regulatory requirement comes from the DOJ's Title II final rule of 24 April 2024,
which adopted WCAG 2.1 Level AA as the technical standard for web content and mobile
apps provided by state and local government entities. Title III — private sector —
rulemaking remains paused; obligations there arise through litigation rather than
regulation. Naming "the ADA" flatly obscures a distinction that matters for our
argument, since open source components sit inside private-sector products far more
often than government ones.

**Out of date.** On 20 April 2026 the DOJ issued an Interim Final Rule extending the
Title II compliance dates by one year:

| Entity | Was | Now |
| --- | --- | --- |
| Population ≥ 50,000 | 24 April 2026 | 26 April 2027 |
| Population < 50,000, and special district governments | 26 April 2027 | 26 April 2028 |

The technical standard (WCAG 2.1 AA) is unchanged, and the underlying Title II
obligation remains in force — only the dated compliance requirement moved.

This repository was first published in July 2026, after that change.

- **Source:** Federal Register, "Extension of Compliance Dates for Nondiscrimination
  on the Basis of Disability; Accessibility of Web Information and Services of State
  and Local Government Entities," 91 FR 20902, published 20 April 2026 —
  https://www.federalregister.gov/documents/2026/04/20/2026-07663/extension-of-compliance-dates-for-nondiscrimination-on-the-basis-of-disability-accessibility-of-web
- **Accessed:** 2026-07-26
- **Verdict:** requires rewording.

> **Unverified:** a parallel HHS extension for federally funded healthcare providers
> (to May 2027 / May 2028) appeared in secondary sources. Not currently cited in our
> documentation, so it does not need correcting — but confirm before adding it.

---

## Claim 2 — `ACCESSIBILITY.md`

> We target **WCAG 2.2 Level AA** as the baseline for all user-facing content.

Not a legal claim — a statement of our own commitment, so nothing to verify.

Worth one clarifying sentence, though. Both regimes cited in the README reference
**WCAG 2.1** AA (the DOJ Title II rule, and EN 301 549 V3.2.1). We target 2.2, which
is stricter and therefore raises no conflict. But a reader who notices the mismatch
may wonder whether it is deliberate. Saying so removes the doubt.

---

## Proposed replacement text

For `README.md`:

> Accessibility is increasingly a legal requirement. In the EU, Directive (EU)
> 2016/2102 covers public sector websites and mobile applications, and the European
> Accessibility Act (Directive (EU) 2019/882, in force since 2019) has applied to a
> range of consumer products and services since 28 June 2025; conformance with the
> harmonised standard EN 301 549 (V3.2.1) creates a presumption of conformity with
> both. In the US, the Department of Justice's 2024 rule under Title II of the ADA
> requires state and local government web content to meet WCAG 2.1 Level AA, with
> compliance dates now falling in April 2027 and April 2028 following a one-year
> extension issued in April 2026; Title III rulemaking for the private sector remains
> paused, and obligations there continue to be shaped by litigation.

Longer than the original, and deliberately so — the precision is the point. If a
shorter version is needed, the safest cut is the Title III sentence, not the
distinction between the standard and the directives.

For `ACCESSIBILITY.md`, one added line:

> We target WCAG 2.2 Level AA, one version above the 2.1 Level AA referenced by
> EN 301 549 V3.2.1 and the DOJ's 2024 Title II rule. This is deliberate.

---

## Maintenance

Re-run before each external submission, not once. Two items are known to move:

- **EN 301 549 V4.1.1**, anticipated 2026. Would change what conformance means.
- **DOJ Title II.** The April 2026 extension came with a comment period, and the
  Department signalled it may revisit the technical standard. Dates in this document
  should be treated as current-as-of, not settled.

Any claim added to public documentation should arrive with its primary source and an
access date, so this audit is a check rather than a reconstruction.
