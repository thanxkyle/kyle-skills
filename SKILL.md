---
name: outbound-sequence
description: >
  Build a 6-email cold outbound sequence for any named restaurant/hospitality account.
  Use this skill whenever Kyle says things like "build me a sequence for [brand]", "write a sequence for [role] at [brand]",
  "make outreach for [brand]", "write emails for [concept] brand", or any variation of wanting a multi-email cold outreach
  sequence for a prospect. Kyle will provide: (1) brand name, (2) concept type (coffee/burger/pizza/chicken/drink/juice/fast casual/casual dining/other),
  (3) contact role (CMO/CEO/CFO/VP Marketing/VP Operations). The skill researches the brand, selects a signal-matched framework,
  maps the concept and role to the right angle, and prints all 6 emails to chat for Kyle to copy into Apollo.
  Always use this skill — do not try to write sequences manually without it.
---

# Outbound Sequence Skill

You are writing a 6-email cold outbound sequence on behalf of Kyle Bartholomew, an Account Executive at Thanx.
Thanx is a loyalty and guest data platform built for multi-unit restaurant brands — helping them grow revenue by understanding
and engaging their best guests. Kyle sells into restaurant/hospitality brands typically with 20+ locations.

---

## Step 1: Gather Inputs

You need three things from Kyle before starting:
1. **Brand name** (e.g., "Ziggi's Coffee")
2. **Concept type** (coffee / burger / pizza / chicken / drink or juice / fast casual / casual dining / other)
3. **Contact role** (CMO / CEO / CFO / VP Marketing / VP Operations / other)

If Kyle hasn't provided all three, ask. Then proceed.

---

## Step 2: Research the Brand

Run all of these in parallel — don't wait for one to finish before starting the others.

**A. Salesforce lookup** — query for the account using `mcp__Keystone__salesforce_query`:
```sql
SELECT Id, Name, NumberOfEmployees, Website, OwnerId, LastActivityDate, Description
FROM Account
WHERE Name LIKE '%[BrandName]%'
LIMIT 5
```
Look for the most recent activity, any open opportunities, owner, and any notes in Description.

**B. Web search for signals** — use `WebSearch` to find news from the last 90 days:
- Search: `"[BrandName]" loyalty app OR rewards OR expansion OR funding OR new locations 2025 OR 2026`
- Search: `"[BrandName]" restaurant news 2026`
- Look for: new menu launches, LTOs, expansion announcements, new hires (especially marketing/tech leadership), rebrands, franchise growth, app launches, tech stack changes

**C. Tech stack lookup** — query Nucleus DB using `mcp__Keystone__replica_query`:
```sql
SELECT p.name as partner_name, pa.partner_id
FROM partner_accounts pa
JOIN partners p ON pa.partner_id = p.id
JOIN accounts a ON pa.account_id = a.id
WHERE a.name LIKE '%[BrandName]%'
```
Note any POS, marketing, or loyalty platform connections. If Dreambox (partner_id=12) appears, that's a shared integration angle.

**D. Notion case studies** — check the Content Library for approved external case studies:
Use `mcp__Keystone__notion_query_database` or `mcp__52e1e905-a589-4bcf-9f68-84703ee7465c__notion-search`
to find case studies tagged as "Sales Status: Green". Then select the best match for this brand's concept.

After research, briefly summarize what you found (2-3 bullet points) before moving to the next step.

---

## Step 3: Select the Best Signal

Based on your research, identify the single strongest signal. Rank in this order:

1. **News trigger (last 90 days)**: menu launch, LTO, new hire, funding, expansion, tech change
2. **Operational observation**: franchise complexity, digital ordering gap, loyalty platform mismatch for their scale
3. **Persona-only**: no strong trigger found — lean on their role and what keeps that role up at night

This determines your framework (next step).

---

## Step 4: Select the Email Framework

| Signal type | Framework | When to use |
|---|---|---|
| Strong recent trigger (news/hire/launch/funding) | **TIA** — Trigger, Insight, Ask | Time-sensitive event gives you a natural in |
| Mix of observation + some context | **OPPA** — Observation, Problem, Proof, Ask | Default. Most versatile. |
| No clear trigger, persona understanding only | **QVA** — Question, Value, Ask | When you understand their role but have no hook |

**TIA structure:**
- Trigger: reference the specific event (launch, hire, news)
- Insight: one thing that gets interesting/complex as a result
- Ask: a peer-level question, not a pitch

**OPPA structure:**
- Observation: something you noticed about their brand/category
- Problem: what gets tricky at their stage/scale (framed as a question)
- Proof: a brand that faced the same and what happened (FOMO, not similarity)
- Ask: soft permission to share more or set a call

**QVA structure:**
- Question: the question they're already asking themselves in their role
- Value: what brands using Thanx are doing differently
- Ask: one soft question back to them

---

## Step 5: Map Role to Angle

Use this to know what pain point to anchor on for the contact's role:

| Role | What keeps them up at night | Angle |
|---|---|---|
| CMO / VP Marketing | Personalization at scale, loyalty ROI, retention vs. acquisition spend, proving marketing impact | Guest data, segmentation, knowing who your top 10% are and keeping them |
| CEO / Founder | Unit economics, digital vs. in-store split, competition from QSR/big chains, scalable growth | Revenue per guest, not just loyalty points — building a moat with data |
| CFO | ROI justification, cost per acquisition, discount efficiency, proving program pays back | Thanx helps brands reduce blanket discounting and direct spend to guests who would have churned |
| VP Operations / COO | Franchise consistency, tech stack complexity, guest experience at scale | Simplifying the loyalty/marketing stack, one source of truth for guest data |
| VP Marketing | Channel mix, email performance, app vs. web, retention tactics | More targeted campaigns, less spray-and-pray discounting |

---

## Step 6: Map Concept to Angle

Use this to ground your emails in the specific dynamics of their concept type:

| Concept | What matters most | Natural Thanx angle |
|---|---|---|
| Coffee | Daypart loyalty (morning habit is gold), frequency, reward redemption timing, LTO conversion | Understanding which regulars are converting to new items vs. which are at risk of lapsing |
| Burger / QSR | Digital ordering mix, app adoption, third-party dependency (Uber/DoorDash margin bleed), combo optimization | Owning first-party data, reducing delivery margin bleed, identifying high-value dine-in guests |
| Pizza | Delivery-heavy, franchise complexity, frequency + occasion (Friday night), digital loyalty | Franchise-consistent loyalty without franchisee tech chaos |
| Chicken | Fast growth category, lots of new competition, occasion-based (family meal), new market entry | Identifying which new market guests become regulars, not just trial |
| Drink / Juice / Smoothie | High frequency, subscription opportunity, daypart (morning/afternoon), health-conscious guest | Frequency programs, daypart targeting, guest lifetime value |
| Fast Casual | Lunch-heavy, lunchtime frequency, competition from delivery, digital engagement | Understanding your lunch regulars and keeping them |
| Casual Dining | Lower visit frequency, occasion-based, alcohol/bar revenue, group dining | Occasion-triggered outreach (birthdays, anniversaries), revenue per visit |

---

## Step 7: Select the Best Case Study

Pick the case study that best matches the brand's concept type and the pain point you're referencing. Use these thanx.com URLs (never share Google Drive links — these are for external use only):

| Brand | Concept | Best for | URL |
|---|---|---|---|
| Hopdoddy Burger Bar | Better Burger | Paytronix migration, A/B testing, enrollment | https://www.thanx.com/customers/hopdoddy-burger-bar/ |
| Pokeworks | Fast Casual / Poke | Enrollment, reduced discounting, SSS growth | https://www.thanx.com/customers/pokeworks/ |
| PINCHO | Burger/Kebab Fast Casual | -7% to +7% SSS, 14% SSS growth, franchise | https://www.thanx.com/customers/savory-funds-pincho-burgers-and-kebabs/ |
| Oakberry | Acai / Health | 1PD revenue, loyalty launch, new concept | https://www.thanx.com/customers/oakberry/ |
| Honest Mary's | Better-For-You Fast Casual | Small brand growth, enrollment, NPS | https://www.thanx.com/wp-content/uploads/2025/07/Thanx_CaseStudy_Speakscale_HonestMarys.pdf |
| Sonny's BBQ | BBQ Casual Dining | Regional chain, occasion-based, loyalty relaunch | https://www.thanx.com/wp-content/uploads/2025/07/Thanx-Sonnys-Case-Study.pdf |

If none match perfectly, pick the one whose story maps best to the problem you're surfacing.
Do not reference Mo'Bettahs or Big Chicken externally (Google Drive only, not for prospect emails).

---

## Step 8: Write the 6-Email Sequence

**Cadence:** Day 1 / Day 4 / Day 9 / Day 16 / Day 25 / Day 35

**Email roles:**
- **Email 1 (Day 1)**: Lead with the signal. TIA or OPPA opening. No mention of Thanx. One question.
- **Email 2 (Day 4)**: Deepen the problem. Introduce a brand using Thanx (FOMO framing). Still no name-drop of Thanx — "brands we work with" or "a [concept] brand we work with."
- **Email 3 (Day 9)**: Direct proof. Now you can mention Thanx by name. Share a case study stat. One ask.
- **Email 4 (Day 16)**: Reframe. Try a different angle (different pain point, or a question from a different direction).
- **Email 5 (Day 25)**: Value drop. Share something genuinely useful — a trend, insight, or observation — with zero ask. Show you're a peer, not a vendor.
- **Email 6 (Day 35)**: Breakup email. Graceful, confident, zero desperation. Leave the door open.

---

## Voice Rules — Non-Negotiable

These rules apply to every email in every sequence, no exceptions.

### The Core Posture
Write as an **expert partner, not a vendor.** The posture is: *I know your industry and I'm bringing you something worth knowing* — not *please consider our product.* Every email should feel like a smart peer sharing intelligence, not a salesperson asking for time.

One-sentence test: **Expert enough to command credibility, informal enough to signal belonging, concise enough to signal confidence.**

### Structure Rules
1. **Open with something specific.** A named fact about their brand, a specific data point, or a sharp observation about their category. Never a generic opener ("In today's competitive restaurant landscape..."). Never a compliment.
2. **One bold claim per email — max.** Make one strong, specific assertion. Not three features. Not a feature list. One claim, defensible and anchored in data or a named example.
3. **The "this, not that" contrast.** Frame the insight as a contrast: what most assume vs. what the data shows. "Higher discounts are not correlated with higher retention. You know what is? Segmentation."
4. **Close with access, not pressure.** Not "let me know if you'd like a demo." Instead: a soft question back to them, or personal availability as a signal of seriousness. "Happy to jump on a 20-minute call this week."
5. **Each email must stand alone.** Don't reference previous emails. Each one should be readable cold.

### Sentence-Level Rules
6. **No em dashes. Ever.** Not even one. Kyle's rule, non-negotiable. Use a colon, period, or rewrite.
7. **Contractions always.** "it's", "won't", "don't", "can't" — never write out the full form when a contraction works.
8. **Drop sentences.** End paragraphs with a short, punchy declarative. "That's the only reason I'm following up." "The math is pretty simple."
9. **Strong verbs over weak ones.** Prefer direct, active verbs. Avoid "impact", "leverage", "utilize", "drive value."
10. **"In order to" is always just "to."** Cut it every time.

### Tone Rules
11. **Frame insights as questions, not statements.** Don't tell them what they're doing wrong. Ask what they're seeing. "Curious how you're thinking about X" not "The tricky part is X."
12. **Never mention Thanx in Email 1 or Email 2.** Say "brands we work with" or "a [concept] brand we partner with." Let them ask.
13. **One ask per email.** One question. One CTA. Never two.
14. **No "similar to" or comparisons between brands.** Use FOMO: "Do you have X problem? [Brand] had it. Here's what happened."
15. **Data earns the right to the opinion.** Every substantial claim needs a specific number or a named example. Not "most restaurants" — "Pokeworks saw 4x enrollment growth in 7 months." Unsourced claims get cut.

### Length Rules
16. **CMO/CEO = 3-5 sentences max.** VP/Director = 5-7 sentences. Never more than 8 for anyone.
17. **Short emails signal confidence.** A 5-sentence email that gets a reply beats a 400-word essay every time.

### Banned Words
Never use these in any email: industry-leading, robust, best-in-class, seamless, cutting-edge, game-changer, innovative, holistically, world-class, boasts, I'd love to, would you be open to, quick call, data-driven, synergy, leverage (as a verb), utilize.

### Subject Lines
2-4 words. Lowercase or sentence case. Internal-looking. No exclamation marks. No questions. No "loyalty" or "platform" in the subject. Think: what would an internal email from a smart colleague look like? Examples: "morning regulars", "loyalty on your list?", "one thing i noticed", "the tech overhaul", "franchise data gap"

### Sign-Off
No closing phrase ("Best," "Warmly," "Regards," "Thanks," "Cheers"). Just:
```
-Kyle
```
The hyphen is intentional. It's Zach's format and it signals confidence without ceremony.

---

## Output Format

Print all 6 emails to chat in this format so Kyle can copy them directly into Apollo:

---

**EMAIL 1 — Day 1**
Subject: [subject line]

[email body]

---

**EMAIL 2 — Day 4**
Subject: [subject line]

[email body]

---

...and so on through Email 6.

After all 6 emails, add a one-line note on the framework you chose and why, and which case study you selected.

---

## Notes

- If the brand is already a Thanx customer (found in Salesforce as a current customer), flag this to Kyle before writing anything.
- If you can't find a strong signal, default to OPPA with the role-based angle. Don't fabricate a trigger.
- If the contact's name is known (Kyle may provide it), address the email to them by first name. If not, write without a salutation or use "Hi [First Name]," as a placeholder.
- Never apologize for reaching out cold. Never say "I know you're busy." Never say "I'll keep this short." Just keep it short.
