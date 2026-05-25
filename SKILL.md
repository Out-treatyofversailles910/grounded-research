---
name: grounded-research
description: >
  Enforces source-grounded, citation-first research discipline. Use this skill whenever
  the user asks to research a topic, fact-check a claim, summarize recent findings,
  look up current information, explain what the evidence says about something, or
  produce any factual output where accuracy and verifiability matter. Trigger even
  on conversational phrasing like "what's the deal with X", "is it true that Y",
  "what do experts say about Z", or "can you check if..." — if the answer requires
  facts that could be wrong or outdated, this skill applies. When in doubt, use it.
---

# Grounded Research Skill

This skill enforces a structured, citation-first discipline to produce outputs where
every factual claim is either verified, explicitly uncertain, or openly declared unknown.
The goal: no confident-sounding hallucinations. Ever.

---

## Phase 1 — Claim Taxonomy (do this before writing anything)

Before producing any output, mentally classify every claim the response will make:

| Type | Description | Handling |
|------|-------------|----------|
| **A — Stable** | Well-established, timeless facts (laws of physics, historical events pre-2020, definitions) | State directly, no search needed |
| **B — Time-sensitive** | Current status, prices, positions, policies, recent events, statistics that change | **Must search before stating** |
| **C — Domain-specific** | Technical claims, research findings, medical/legal/security facts, statistics | **Must find a source before stating** |
| **D — Analytical** | Opinions, comparisons, interpretations, synthesis | Label clearly as analysis/opinion |

Never mix types silently. If a paragraph contains a Type C claim presented with Type A
confidence, that's a hallucination risk. Classify first, then write.

---

## Phase 2 — Pre-Response Verification Loop

For every Type B and Type C claim identified in Phase 1:

1. **Search before writing** — run a web search targeting that specific claim
2. **Extract the key fact** — find the specific sentence or data point that supports it
3. **Note the source tier** — see `references/source-quality-tiers.md`
4. **Flag if unverifiable** — if no reliable source is found after 2 searches, the claim
   must be either dropped or explicitly marked as unverified

Only after verification is complete for all B and C claims, proceed to Phase 3.

**Verification shortcuts to never take:**
- Do not state a statistic without a source, even if you are "pretty sure"
- Do not state someone's current job title, role, or status without searching
- Do not describe a product's current features or pricing without searching
- Do not summarize a study's findings without finding the actual study or a primary report

---

## Phase 3 — Structured Output

Structure all research responses as follows:

### 3a. Lead with the answer
Give the direct answer first. Do not bury it in preamble.

### 3b. Inline citations
Every Type B and C claim gets an inline source reference immediately after it.
Format: state the claim in your own words, then note the source naturally in prose.
Never reproduce long quotes — paraphrase and attribute.

Example (correct):
> The ECB held rates steady in April 2026, according to its official press release.

Example (wrong):
> The ECB held rates steady in April 2026. [This is stated confidently with no source]

### 3c. Confidence signals
Use these inline markers when precision matters:

- `[High confidence — primary source]` — sourced from official/primary publication
- `[Medium confidence — secondary source]` — sourced from reputable but secondary coverage
- `[Low confidence — unverified]` — couldn't find a strong source; treat as uncertain
- `[Analytical — my interpretation]` — this is synthesis/opinion, not a sourced fact

You do not need to add these markers to every sentence — use them where the
confidence level is non-obvious or where a reader might otherwise mistake analysis
for established fact.

### 3d. "I don't know" declarations
If a claim cannot be verified and is important to the answer, say so explicitly:

> I could not find a reliable source for [X]. This should be verified before acting on it.

This is always better than a confident-sounding guess.

---

## Phase 4 — Confidence Audit

After drafting the response, do a final pass:

1. Scan for any factual claim that lacks a source or uncertainty marker
2. For each: either add attribution, add an uncertainty signal, or remove the claim
3. Check that no Type D (analytical) claim is presented as if it were Type A (established fact)
4. Verify the response does not contradict itself across sections

This audit step is not optional. It's the difference between a grounded response
and a plausible-sounding one.

---

## Phase 5 — Source Quality

Read `references/source-quality-tiers.md` for the full tier guide.

Quick reference:
- **Tier 1** (strongest): Official publications, primary studies, government data, company IR
- **Tier 2**: Major wire services, peer-reviewed journals, established specialist press
- **Tier 3**: Quality general news, well-sourced blog posts from known experts
- **Tier 4**: Aggregators, wikis, forums — only as pointers to Tier 1–3, never as the final source

When sources conflict, report the conflict. Do not silently pick one.

---

## Special Cases

### Rapidly changing topics (breaking news, live events)
- State the timestamp of your most recent source explicitly
- Add: "This situation may have developed since [date/time of source]"
- Do not speculate about what "probably" happened after your last source

### Technical / security claims
- Prefer CVE databases, vendor advisories, NIST, and official security bulletins
- Do not paraphrase vulnerability details in ways that could introduce inaccuracy
- If the claim involves a specific version, configuration, or exploit, find the primary advisory

### Medical / legal claims
- Always source to peer-reviewed literature, official guidelines, or regulatory bodies
- Always add: "This is not medical/legal advice. Consult a qualified professional."
- Never state a treatment or legal position as settled if the primary literature shows debate

### Historical research (pre-cutoff, no search needed)
- Type A claims can be stated without search
- But if the user is researching something where recent scholarship might have updated
  the consensus (e.g. archaeology, historical attribution, economic history), flag it

---

## Anti-Patterns to Avoid

| Anti-pattern | Why it's a problem |
|---|---|
| "Studies show..." with no citation | Fabricated authority |
| "It is widely believed that..." | Vague appeal that hides a missing source |
| "As of my last update..." followed by a specific fact | Framing stale knowledge as verified |
| Summarising a document you haven't read | High hallucination risk on specific details |
| Quoting statistics without a source | Numbers are the most frequently hallucinated element |
| Confidently resolving a contested claim | Misrepresents genuine expert disagreement |

---

## Output Length Guidance

- For quick fact checks: 2–4 sentences + source. Do not pad.
- For research summaries: structured prose, one section per sub-topic, sources inline.
- For contested topics: present multiple positions with their respective sources. Do not collapse to one view unless the evidence is overwhelming and sourced.
- Always prioritise precision over comprehensiveness. A shorter, accurate answer beats a longer, partly-hallucinated one.
