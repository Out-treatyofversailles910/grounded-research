# 🔍 grounded-research

> A Claude skill that enforces citation-first, source-grounded research discipline — so every factual claim is verified, explicitly uncertain, or openly declared unknown.

---

## The Problem

Ask any LLM to research a topic and you'll get confident-sounding output. Some of it will be wrong. The model won't tell you which parts.

This isn't a model quality problem. It's a discipline problem. Without structure, even the best models conflate stable facts with time-sensitive claims, present statistics without sources, and fill gaps with plausible-sounding guesses.

**grounded-research** fixes that by giving Claude a structured protocol it runs *before* writing a single sentence of output.

---

## What It Does

The skill enforces a 5-phase workflow on every research task:

| Phase | What happens |
|-------|-------------|
| **1 — Claim Taxonomy** | Classifies every claim as Stable / Time-sensitive / Domain-specific / Analytical *before* writing |
| **2 — Verification Loop** | Searches for any time-sensitive or domain-specific claim before stating it |
| **3 — Structured Output** | Inline citations, confidence signals, explicit "I don't know" declarations |
| **4 — Confidence Audit** | Post-generation scan — catches uncited claims before they reach you |
| **5 — Source Quality** | Tiered source hierarchy (Tier 1 primary → Tier 4 forum) with domain-specific guidance |

The result: outputs where you can see exactly what's sourced, what's uncertain, and what Claude couldn't verify.

---

## Example Output Comparison

**Without the skill:**
> The EU AI Act requires all high-risk AI systems to be compliant by August 2026, with fines up to €30 million for violations.

*(Sounds authoritative. The fine amount is wrong. The deadline picture is more nuanced. No source given.)*

**With the skill:**
> According to the European Commission's official AI Act page, full applicability for most high-risk AI systems takes effect on **2 August 2026**, with certain product-embedded systems having an extended transition until 2027. Fines for prohibited practices reach up to **€35 million or 7% of global turnover** under Article 99, per the latest legislative text. [High confidence — Tier 1 source: digital-strategy.ec.europa.eu]
>
> Note: A proposed Digital Omnibus amendment package may extend some deadlines further. As of May 2026, this has not been finalised — treat the August 2026 date as the current legally binding deadline.

---

## Skill Structure

```
grounded-research/
├── SKILL.md                          # Core skill — claim taxonomy, verification loop, audit
└── references/
    └── source-quality-tiers.md       # Tier 1–4 source guide with domain-specific table
```

---

## Installation

### Claude.ai (Web / Desktop)
1. Download the `.zip` from [Releases](../../releases)
2. Go to **Claude.ai → Settings → Skills → Upload ZIP**
3. Done — the skill activates automatically on research tasks

### Claude Code
```bash
# Clone into your skills directory
git clone https://github.com/YOUR_USERNAME/grounded-research ~/.claude/skills/grounded-research

# Or copy manually
cp -r grounded-research ~/.claude/skills/
```

### Via npx (coming soon)
```bash
npx skills add YOUR_USERNAME/grounded-research
```

---

## When It Triggers

The skill activates on phrases like:

- *"Research X for me"*
- *"What does the evidence say about Y?"*
- *"Is it true that Z?"*
- *"Fact-check this claim"*
- *"What are the current regulations on..."*
- *"Summarise recent findings on..."*
- *"What's the deal with X?"*

It also triggers on implicit research requests — any question where the answer requires facts that could be wrong or outdated.

---

## Source Quality Tiers

The skill uses a four-tier hierarchy for evaluating sources:

| Tier | Examples | Usage |
|------|----------|-------|
| **Tier 1** | Official publications, peer-reviewed journals, government data, CVE/NVD, IETF RFCs | Primary authority |
| **Tier 2** | Reuters, AP, FT, specialist press (Ars Technica, Krebs on Security), vendor advisories | Acceptable when Tier 1 unavailable |
| **Tier 3** | Quality general news, verified expert blogs, Wikipedia (as pointer only) | Use with explicit caveat |
| **Tier 4** | Reddit, forums, AI-generated summaries | Never cite — use as leads only |

Domain-specific preferred sources are listed in [`references/source-quality-tiers.md`](references/source-quality-tiers.md), covering cybersecurity, PKI/TLS, EU law, German regulatory bodies, medical research, and more.

---

## Confidence Signals

The skill adds inline markers where confidence level isn't obvious:

| Signal | Meaning |
|--------|---------|
| `[High confidence — primary source]` | Sourced from Tier 1 |
| `[Medium confidence — secondary source]` | Sourced from Tier 2–3 |
| `[Low confidence — unverified]` | Couldn't find a strong source |
| `[Analytical — my interpretation]` | Synthesis/opinion, not a sourced fact |
| `[Contested — sources disagree]` | Multiple credible sources conflict |

---

## Anti-Patterns It Prevents

| Pattern | Why it's dangerous |
|---------|-------------------|
| *"Studies show..."* with no citation | Fabricated authority |
| *"It is widely believed that..."* | Vague appeal hiding a missing source |
| *"As of my last update..."* + specific fact | Presenting stale knowledge as verified |
| Statistics without a source | Numbers are the most frequently hallucinated element |
| Confidently resolving a contested claim | Misrepresents genuine expert disagreement |

---

## Compatibility

| Platform | Status |
|----------|--------|
| Claude.ai (web/desktop) | ✅ Full support |
| Claude Code | ✅ Full support |
| OpenAI Codex CLI | ✅ Universal SKILL.md format |
| Cursor | ✅ Universal SKILL.md format |
| Gemini CLI | ✅ Universal SKILL.md format |

---

## Contributing

Contributions welcome — especially:

- **Domain modules** — additional `references/` files for specific fields (legal, finance, life sciences, etc.)
- **Trigger improvements** — better `description` phrasing for edge-case activation
- **Anti-pattern additions** — documented hallucination patterns not yet covered
- **Translations** — the skill body works in any language Claude supports; a German or French `SKILL.md` would be valuable

Open an issue to discuss before submitting large changes.

---

## Roadmap

- [ ] Domain-specific sub-skills (cybersecurity, medical, legal, financial)
- [ ] `npx` installer
- [ ] Structured JSON output mode for pipelines
- [ ] Eval set for automated trigger-rate testing

---

## License

Apache 2.0 — same as Anthropic's official skill releases. Free to use, fork, and build on.

---

## Author

Built by [@moonpiesheldon1337](https://github.com/moonpiesheldon1337) — cybersecurity consultant, PKI architect, and occasional builder of things that make AI less confidently wrong.

*Part of a growing collection of domain-focused Claude skills. Star the repo if it's useful — it helps others find it.*
