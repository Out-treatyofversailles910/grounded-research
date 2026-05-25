# Source Quality Tiers

Use this reference when evaluating whether a source is strong enough to support
a Type B or Type C claim. When sources of different tiers conflict, prefer higher
tiers and report the conflict rather than silently resolving it.

---

## Tier 1 — Primary / Official Sources (Strongest)

Use as the final authority wherever available.

**What counts:**
- Official government publications, legislation, regulatory filings (EUR-Lex, Bundesanzeiger, Federal Register, etc.)
- Company investor relations pages, official press releases, annual reports
- Peer-reviewed journal articles (access the actual paper, not just an abstract or news summary)
- Standards bodies: ISO, NIST, IETF RFCs, OWASP, CVE/NVD databases
- Central bank publications, international organisation data (ECB, IMF, WHO, UN)
- Official product documentation and changelogs (for technical claims)
- Court judgments and official legal instruments

**How to use:**
State findings in your own words, cite the publication name and date.
Do not reproduce large blocks of text. One precise paraphrase + attribution.

---

## Tier 2 — High-Quality Secondary Sources

Acceptable when Tier 1 is unavailable, but note it's secondary.

**What counts:**
- Major wire services with strong editorial standards: Reuters, AP, AFP, Bloomberg
- Specialist/trade press with editorial standards: Ars Technica (tech), The Lancet (medicine),
  Security Week / Krebs on Security (cybersecurity), Financial Times, The Economist
- Well-established research institutions with published methodology: Pew, Eurostat summaries,
  academic working papers from named institutions
- Vendor security advisories (e.g. Microsoft MSRC, Cisco Talos) — still secondary to CVE/NVD

**How to use:**
Mark as secondary where relevant. "According to Reuters, citing [source]..."
If the secondary source quotes primary data, try to find and cite the primary directly.

---

## Tier 3 — Acceptable with Caveats

Use only when Tier 1–2 unavailable, and flag explicitly.

**What counts:**
- Quality general news outlets with established fact-checking (BBC, Der Spiegel, NRC)
- Expert blog posts where the author's credentials are clear and verifiable
- Company technical blogs (Google Security, Cloudflare Blog, AWS News) — credible for
  their own products, not as neutral third-party sources
- Official Wikipedia articles for stable, well-referenced topics (use as a pointer
  to Tier 1–2 sources listed in its references, not as the source itself)

**How to use:**
Always note Tier 3 provenance: "According to [outlet] — original source not located."
Never treat a Tier 3 source as settled authority for a contested or high-stakes claim.

---

## Tier 4 — Pointers Only (Never Cite as Authority)

Do not cite these as the final source for any factual claim.

**What counts:**
- Reddit threads, Hacker News discussions, Stack Overflow answers
- Personal blogs without clear authorship or credentials
- SEO content farms, listicle aggregators
- Unverified social media posts
- AI-generated content (including summaries produced by other AI tools)

**How to use:**
These can help you find the right search terms or point toward a Tier 1–3 source.
Never cite them as the basis for a factual claim. If you found a lead from Tier 4
and then verified it at Tier 1–2, cite Tier 1–2.

---

## Conflict Resolution

When sources disagree:

1. Prefer higher tier sources
2. If two Tier 1 sources conflict, report both positions:
   > "The WHO guideline states X, while a 2025 Lancet meta-analysis argues Y. The
   > evidence is contested."
3. Never silently resolve a real conflict by picking the answer that fits the narrative

---

## Domain-Specific Preferred Sources

| Domain | Preferred Tier 1–2 Sources |
|--------|---------------------------|
| Cybersecurity / CVEs | NVD (nvd.nist.gov), MITRE CVE, vendor advisories, CERT |
| PKI / TLS | IETF RFCs, CA/Browser Forum, NIST SP 800-series |
| Mobile security | OWASP MASTG, vendor security bulletins, CVE |
| EU law / GDPR | EUR-Lex, BSI (Germany), official DPA publications |
| German regulatory | Bundesnetzagentur, BNetzA, official Bundesanzeiger |
| Medical | PubMed, Cochrane, WHO, EMA, RKI (Germany) |
| Financial / macro | ECB, Bundesbank, Eurostat, Bloomberg, Reuters |
| AI / ML | ArXiv preprints (flag as preprint), NeurIPS/ICML proceedings |
