---
ticket: jarda-ai-start/cluster-6-appendix-depth
status: superseded
superseded-by: 2026-04-21-round-2-master.md
appetite: M
risk_score: 3
project: jarda-ai-start
updated: 2026-04-21
depends_on: cluster-1-market-map-correction
target_file: /Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/2026-04-21-cluster-6-appendix-depth.md
---

# Cluster 6 — Appendix Depth

## Problem

User feedback on the v2b appendix: "for the appendix — don't we have a little more comprehensive and impressive research reports, how we derived these competitors, what did we learn about their tools, business opportunities and opportunities for automation-inspirations?"

Current appendix (3 blocks, ~900w): Tool landscape (~280w), Market map (~440w — being corrected in Cluster 1), Why these six stops? (~170w).

The existing appendix is thin on the "research report" dimension. It states conclusions (tool list, market map, stop rationale) but doesn't surface the synthesis work behind them — the patterns of automation leverage a creator can read off the market map, or the signal for when Cowork stops being the right surface.

Outcome test: a reader who skims the appendix should come away with two new mental models — (a) where time-saving opportunities cluster in a solo-creator 2026 stack, and (b) when to graduate from Cowork to Code. Proxy metric (word-count targets) is a sanity bound, not the test.

## Verified Assumptions

| # | Claim | Source | Verify |
|---|-------|--------|--------|
| 1 | Research material exists in `discovery-plan.md` lines 77-119 (9 numbered growth gaps), 434-472 ("Graduating to Claude Code" section) | Content-agent findings | `sed -n '77,119p' /Users/profile_1/Coding/jarda/discovery-plan.md` + `sed -n '434,472p' /Users/profile_1/Coding/jarda/discovery-plan.md` |
| 2 | Current appendix has 3 blocks totaling ~900w | Content-agent framing | `grep -c 'research-block' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html` (expect ≥3) + wc on appendix section |
| 3 | Market map block will be revised by Cluster 1 before Cluster 6 executes | Dependency declaration | `grep -l 'cluster-1-market-map-correction' /Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/` + check status:completed |
| 4 | Appendix uses `<div class="research-block">` + `<h3 class="research-subtitle">` pattern | Content-agent convention | `grep -A1 'research-block' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html \| head -20` |
| 5 | Voice grep (banned markers list) and privacy audit scripts exist | Slice 7 pattern | `ls /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/ \| grep -E 'voice\|privacy'` |
| 6 | Research bullets in discovery-plan.md are author's own work (no external attribution needed) | Content-agent note | N/A — policy decision documented in plan |

## Shape Decision — Bundle B (2 new blocks)

Two new appendix blocks, ~750 new words total, appendix total ~1650w.

**"Where the time goes" — automation opportunities (~400w)** inserted after the (revised) Market map block. Structurally it's a market-map follow-on: given those voices, what opportunities does a creator see? 3-4 categorized patterns distilled from the 9 numbered growth gaps in `discovery-plan.md:77-119`, abstracted away from Jarda-specific photography-business framing to generic solo-creator patterns.

**"When to leave Cowork" (~350w)** appended after "Why six stops". Forward-looking consequence: the primer opens with Stop 1 mentioning Code, so the appendix should close the loop with signals for when to graduate. Draws from `discovery-plan.md:434-472`.

**Rejected:** Bundle A (adding "How SEO moved in 2026" block as third). SEO is off-primer-theme and risks feeling like tangent. Defer to possible v2.5.

**Rejected:** Bundle C (one block only). User's ask explicitly names "business opportunities AND how we derived these competitors AND tools" — a single "automation opportunities" block doesn't close the graduation-to-Code loop the primer opens in Stop 1.

**Rejected rationale note for SEO block:** The SEO material in `discovery-plan.md:292-343` is solid and citation-backed, but the primer is short-lived (≤30 days) with no SEO investment of its own, so teaching SEO here reads as off-register. If a v2.5 extends shelf life, revisit.

## Block order (final)

1. Tool landscape (existing, unchanged)
2. Market map (revised by Cluster 1, unchanged by this cluster)
3. **NEW: Where the time goes**
4. Why these six stops? (existing, unchanged)
5. **NEW: When to leave Cowork**

## Source-material → synthesis policy

Research in `discovery-plan.md` is raw — bullet lists, Jarda-specific growth gaps, competitor observations. Appendix must SYNTHESIZE: abstract from "photography business" specifics to patterns any solo creator can apply. Examples:
- "anniversary engine" → "a recurring trigger for outreach based on past customer data"
- "book-to-leads" → "long-form IP that converts readers to inquirers"
- "Rexby / photo marketplaces" → "distribution surfaces that pay on volume rather than brand"

Research bullets are author's own; no external attribution needed. Paraphrase freely.

## Acceptance Criteria

- [ ] New `<div class="research-block">` for "Where the time goes" inserted after the (revised) Market map block
- [ ] New `<div class="research-block">` for "When to leave Cowork" appended after "Why these six stops?"
- [ ] Each block has an `<h3 class="research-subtitle">` + body prose in existing appendix HTML pattern
- [ ] Word count 350-450 for "Where the time goes" (target 400)
- [ ] Word count 300-400 for "When to leave Cowork" (target 350)
- [ ] Privacy audit exits 0 (no emails, no phone numbers, no unintended PII)
- [ ] Voice grep clean (no banned markers from existing banned-phrases list)
- [ ] Generic enough that a non-Jarda reader understands — no "your photography business", no "wedding shoots", no "Slovenian tourism" etc.
- [ ] Formal reviewer pass (same pattern as Slice 7): confirms voice/evaluative/infomercial checks
- [ ] Total appendix word count ≤2000

## Slices

### Slice 1 — both blocks in one subagent dispatch + formal reviewer (~60 min)

Executor subagent writes both blocks in one pass. Reviewer subagent reads both in one pass. Single slice because:
- Blocks are small and share voice register
- Neither block has internal dependencies on the other
- Reviewer benefits from reading them together (voice consistency check)

**Sub-steps:**
1. Verify Cluster 1 dependency status=completed before starting (read plan frontmatter)
2. Dispatch executor with block outlines + voice brief + generic-abstraction rule + forbidden-specifics list
3. Executor inserts both `<div class="research-block">` into `index.html` at designated locations
4. Dispatch formal reviewer (Slice-7-pattern) reading both new blocks
5. Fold reviewer findings if any
6. Run privacy audit + voice grep + word count checks
7. Verify total appendix word count ≤2000

## Draft outlines (executor writes full prose)

### "Where the time goes" (~400w)

**Opening framing (40-50w):** Given the voices above, where does a creator find automation leverage in 2026? The pattern is less "build a product" and more "stitch connectors around the work you already repeat."

**Pattern 1 — Inbox triage + response drafting (80-100w):** derived from growth gap #1 (inbox triage). Abstract: incoming-message routing + first-draft reply generation. Who it helps: anyone whose inbox is both discovery channel and work queue. Mechanism: connectors read mail, an LLM classifies and drafts, the human approves or edits.

**Pattern 2 — Anniversary / milestone engine (80-100w):** derived from gap #4. Abstract: a recurring trigger for outreach based on past customer data. Who it helps: anyone with a book of past clients and seasonal relevance. Mechanism: a scheduled job reads the customer record, an LLM drafts, the human approves send.

**Pattern 3 — Long-form IP → leads (80-100w):** derived from gap #5 (book-to-leads). Abstract: IP you've already written that can convert readers to inquirers. Who it helps: anyone with a book, deep post, paper, or substantial public artifact. Mechanism: connectors handle form + CRM; the IP does the selling.

**Pattern 4 — Audience segmentation (60-80w):** derived from gap #11 (4-audience segmentation). Abstract: one brand, several audiences, differentiated by channel and language rather than product. Mechanism: the content pipeline forks downstream; the creator stays single-voiced.

**Closing (30-40w):** These are openings, not solved problems. The question is which of them pays first.

### "When to leave Cowork" (~350w)

**Opening (40-50w):** Cowork is the entry point, not the destination. Code is the next surface. Most people never need it. The signals that say you might.

**Signal 1 — Repeated work on the same file (60-80w):** When three consecutive chats have been about one file, the chat interface stops helping. Code works off the file directly. No re-uploading. No "let me remind you what the function does."

**Signal 2 — External tooling beyond connectors (60-80w):** Build, deploy, CI, package managers, shell scripts. Cowork's connectors extend the chat; they don't extend the terminal. When the work is half-shell-commands, the shell is the better surface.

**Signal 3 — Project size exceeds context-window practical limit (60-80w):** When the project has more files than one chat can hold in mind, the constraint stops being "what you can say" and becomes "what Cowork can remember." Code treats the filesystem as the memory.

**Signal 4 — Comfort with terminal workflow (50-70w):** Or comfort building it. The terminal is a learnable surface. It's also optional. The earlier signals can push; this one has to pull.

**Closing (30-40w):** Most people never need to leave. If you do, the signals above will arrive naturally — and by then the question won't be "should I?" but "what's my first repo?"

## No-Gos

- No naming specific Jarda businesses (wedding photography, Slovenian tourism, specific client names)
- No pricing / plan recommendations ("this is worth the upgrade", "Pro tier includes...")
- No "try this" CTAs — appendix is author-notes, not a guide
- No SEO block (deferred to possible v2.5)
- No linking to any external writer beyond what's already in the Market Map
- No solo-builder AI stack economics numbers ($3K-$12K/yr, 80% admin reduction) — per Codex round-3 hedging, unsourced and out of register
- No real names in any patterns ("[Creator]" not "Jarda")

## Verification commands

```bash
# 1. Cluster 1 must be done first
grep -A1 'status:' /Users/profile_1/Coding/jarda/jarda-ai-start/docs/plans/2026-04-21-cluster-1-market-map-correction.md | head -5

# 2. Appendix block count increased from 3 to 5
grep -c 'research-block' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html

# 3. New block titles present
grep -E 'Where the time goes|When to leave Cowork' /Users/profile_1/Coding/jarda/jarda-ai-start/index.html

# 4. Voice grep clean (banned markers list)
bash /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/voice-check.sh

# 5. Privacy audit exits 0
bash /Users/profile_1/Coding/jarda/jarda-ai-start/scripts/privacy-audit.sh

# 6. Total appendix word count ≤2000
# (extract appendix region, wc -w; threshold 2000)
python3 -c "import re; html=open('/Users/profile_1/Coding/jarda/jarda-ai-start/index.html').read(); m=re.search(r'<section[^>]*class=\"[^\"]*appendix[^\"]*\"[^>]*>(.*?)</section>', html, re.DOTALL); text=re.sub(r'<[^>]+>', ' ', m.group(1)) if m else ''; print('appendix words:', len(text.split())); assert len(text.split()) <= 2000, 'FAIL: appendix exceeds 2000w'"
```
