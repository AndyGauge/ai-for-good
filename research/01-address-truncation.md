---
status: sourced; facts verified against primary sources April 2026
verification: URLs spot-checked during research session
confidence_key: HIGH = primary source confirmed; MED = from secondary summary; LOW = flagged inline
framing_reference: see 01-address-truncation-angle.md for the chapter's thesis
---

# Research Brief: Address Truncation — the generic-transform chapter

## 1. The USPS standard (HIGH)

**USPS Publication 28, Postal Addressing Standards** — the canonical reference. https://pe.usps.com/text/pub28/welcome.htm — October 2024 edition PDF: https://pe.usps.com/cpim/ftp/pubs/pub28/pub28.pdf

Key tables:
- **Street Suffix Abbreviations** (Appendix C1): https://pe.usps.com/text/pub28/28apc_002.htm
- **Secondary Address Unit Designators**: https://pe.usps.com/text/pub28/28c2_003.htm
- **Delivery Address Line**: https://pe.usps.com/text/pub28/28c2_012.htm

Representative suffix abbreviations:

| Full | USPS Standard |
|---|---|
| AVENUE | AVE |
| BOULEVARD | BLVD |
| STREET | ST |
| DRIVE | DR |
| ROAD | RD |
| LANE | LN |
| COURT | CT |
| CIRCLE | CIR |
| PLACE | PL |
| TERRACE | TER |
| PARKWAY | PKWY |
| EXTENSION | EXT |

The USPS publishes hundreds more. Pub 28 is the *rules*, and the rules alone do not solve the problem — see section 3.

## 2. Field-length constraints in HR/ATS systems (MED)

Workday and similar HCM systems do not document a strict 29- or 30-character limit at the application layer, but **downstream integrations enforce limits**. Sources:

- Texas A&M's official Workday guidance: https://uas.tamu.edu/tax/_media/instruction-address-entry.pdf — explicit instructions for employees on handling long addresses.
- General address-field analysis (Service Objects): https://www.serviceobjects.com/blog/character-limits-in-address-lines-for-usps-ups-and-fedex/ — USPS, UPS, FedEx all have different address-line limits; 30 characters is a common lower bound.
- BigCommerce community thread on 30-char limits: https://support.bigcommerce.com/s/question/0D54O000077uOZJSA2/limiting-address-lines-to-30-characters?language=en_US
- About-Workday field-lengths blog: https://aboutworkday.blogspot.com/2013/04/workday-field-lengths.html

**The important point for the chapter:** the 29-character limit isn't imposed by Workday being stupid. It's imposed by the downstream payroll, mailing, or carrier integration — and the HR system inherits it so that records don't round-trip corrupted. This is a *real constraint in the world*, not an artifact of bad engineering. Which is why "just change the field to 120 characters" doesn't work. The limit comes from a printer, a label format, or a batch file spec that has outlasted three CIOs.

## 3. libpostal — the ten-year deterministic version of the problem (HIGH)

**libpostal** is the best deterministic attempt at global address parsing. https://github.com/openvenues/libpostal — a C library using Conditional Random Fields (statistical NLP), trained on **over 1 billion address records** from OpenStreetMap and OpenAddresses.

Scale:
- **27 GB** of OSM training addresses
- **30 GB** of OpenAddresses training data
- **11 GB** of GeoPlanet postal codes
- Senzing's updated model (2024) added 40% more — **1.2 billion training records**: https://senzing.com/what-is-libpostal/
- Claimed accuracy: **99.45% full-parse on held-out examples**.

**This is the ethical turning point of the chapter.** A decade of engineering. A billion training examples. State-of-the-art statistical NLP. 99.45% accuracy. And it still cannot tell a payroll vendor how to fit `1234 Northwest Martin Luther King Jr Boulevard Apt 5B` into 29 characters in a way that preserves deliverability — because *accuracy on held-out addresses* is not the same as *make this deliverable in 29 characters*. libpostal *parses*; it does not *summarize with preserved intent*. Those are different jobs.

The author's counter-move: stop building libpostal. Write one `transform(input, instruction: "fit to 29 chars, preserve USPS deliverability, use Pub 28 abbreviations")` and let the natural-language instruction *be* the program. If the rule changes — Puerto Rico urbanizations, new APO format, different carrier — you edit the English, not the C code.

## 4. Aimbridge Hospitality — the specific case (HIGH)

- **World's largest third-party hotel management company.** https://www.aimbridgehospitality.com/
- **~45,000 associates** (Wikipedia, PRNewswire 2024 announcement): https://www.prnewswire.com/news-releases/aimbridge-hospitality-named-among-us-news--world-reports-2024-2025-best-companies-to-work-for-302252448.html
- **1,500+ properties in 50 states and 23 countries.**
- Shift-scheduling platform with 12,000+ workers trading shifts — suggests a modern HR stack (likely Workday or UKG) but specific vendor not publicly confirmed.
- Hospitality Net profile: https://www.hospitalitynet.org/organization/17011870/aimbridge-hospitality

For the chapter: 45,000 employees × hospitality turnover rate (see §5) = tens of thousands of onboarding events per year. Every one requires an address in the HR system. Every one is at risk of the 29-char truncation failure.

## 5. Why address accuracy matters downstream (HIGH)

Hospitality turnover is the industry's defining HR statistic:

- **70–80% annual turnover**, among the highest of any US sector. BLS Leisure and Hospitality: https://www.bls.gov/iag/tgs/iag70.htm
- **5.8% monthly separations** (mid-2024 JOLTS): https://www.bls.gov/news.release/jolts.htm
- BLS average nonsupervisory hospitality wage: **$19.61/hour** (2024) vs. $28/hour across all private industries.
- SHRM replacement cost: **~$4,700 per lost hire** — recruitment, onboarding, training.
- HR Dive on hospitality leading quit rates: https://www.hrdive.com/news/industries-with-highest-quit-rates/721216/

**What breaks when the address is truncated:**
- **Form W-2** mailed to wrong address → IRS problem, back-and-forth at tax time
- **First paycheck** mailed/deposited based on address-verified direct-deposit form → delay, candidate quits before the fix
- **Uniform shipment** to new hire → can't report on day one
- **Benefits enrollment documents** → missed enrollment window, health coverage denied
- **I-9 verification follow-up** → termination for unverifiable status

For a low-wage hourly worker, any of these individually can be the reason they quit before week two. A broken address field doesn't just cost the $4,700 SHRM replacement number — it silently inflates the 70% industry turnover statistic.

**The ethical frame for the talk:** the engineer who decides "29 characters, hard truncate" is not just writing bad code. They are, indirectly, deciding which candidates get their first paycheck. The person whose street is `1234 N Martin Luther King Jr Blvd` gets paid. The person whose street is `1234 Northwest Martin Luther King Jr Boulevard` gets mailed to nowhere. Both are real addresses for the same real street, a block apart. The difference is whether the HR input clerk happened to key the short form.

## 6. The prior-art landscape for LLM address work (MED)

- **libpostal** — already covered; the state-of-the-art deterministic baseline.
- **Google Address Validation API** — commercial, opaque, expensive at scale.
- **SmartyStreets / Melissa / Loqate** — commercial CASS-certified vendors, expensive, per-record pricing.
- **OpenCage templates** (used by libpostal): https://github.com/OpenCageData/address-formatting
- **LLM-based approaches** — not yet a named product category as of April 2026, but the pattern is:
  - give the LLM the address + USPS Pub 28 + field constraint
  - ask for the best deliverable form at ≤N chars
  - validate the result with libpostal or CASS before persisting

**This is where the chapter's thesis lives:** the *validation* stays deterministic (libpostal, CASS) but the *generation* becomes natural-language-driven. Rust infrastructure matters here — `libpostal` has Rust bindings (`libpostal-rs`), and a `transform(input, instruction)` wrapper in Rust is a clean, auditable layer around whatever LLM provider you use.

## 7. The handoff — the payoff line (HIGH — author's own report)

The author wrote the generic `transform(input, instruction)` once. Then handed the *English instruction* to the HR operations person who understood the downstream constraint.

- HR ops no longer files Jira tickets for "PO boxes break the truncator"
- Engineer no longer rebuilds the rule table for Puerto Rico urbanizations
- When USPS updates Pub 28, HR ops edits one sentence in the prompt
- When a new international market opens, HR ops adds a sentence
- The engineer's calendar stops being a queue of one-line rule changes

**The chapter's load-bearing claim:** this is not just operational efficiency. It is a *return of authorship* to the person who owns the domain. For 40 years we have asked engineers to translate business intent into code; the LLM collapses the translation step. The business owner writes the spec in the language they already think in. The engineer builds the rails. The rails are generic.

## What to show on stage (Rust)

```rust
// The bad version — what they wrote in 1997 and still ship in 2026
fn truncate_address(addr: &str) -> String {
    addr.chars().take(29).collect()
}

// The deterministic "correct" version — 10,000 lines, still wrong
// (see libpostal — 1B training records, 99.45% accuracy, does not
// summarize, only parses)

// The generic version — the chapter's thesis
async fn transform<T: Serialize, R: DeserializeOwned>(
    input: T,
    instruction: &str,
    client: &AnthropicClient,
) -> Result<R> {
    // LLM call + validation. Implementation is boring.
    // The *specification* is the business owner's sentence:
    //
    //   "Fit this street address into 29 characters or fewer.
    //    Preserve USPS deliverability. Use Pub 28 abbreviations.
    //    Keep the apartment/unit number. If you have to drop something,
    //    drop the directional before dropping the street name."
    //
    // When the rule changes, the HR ops person edits the sentence.
    // The Rust code never changes.
}
```

## Honest caveats for the stage

- **LLMs can hallucinate.** Validate every output against libpostal or CASS before persisting. The LLM generates; deterministic code verifies. Both layers matter.
- **Latency and cost.** A CRM-style address form doesn't need sub-10ms response. An onboarding flow can afford 500ms per address. A batch payroll run is fine with a cache.
- **Auditability.** Log the prompt, the input, the output, and the validation result. Regulators (and your own HR ops person) will thank you.
- **Don't hand the prompt to someone who can't read USPS Pub 28.** The chapter argues the business owner maintains the spec — not a random person. "Business owner" here means *the HR operations lead who already knew what the deliverability constraint was*.
