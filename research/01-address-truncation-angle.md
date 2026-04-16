---
type: author framing note
chapter: address truncation
status: author-provided, verbatim intent
---

# The chapter's actual thesis

Not "LLM beats truncation." The thesis is:

> If I had to write the code that managed every address in the world for this stupid 29-char function, I'd go crazy. Instead I wrote a generic interface that receives any param, outputs to any data key, and runs an LLM transformation — using natural language to describe the function.

## What the chapter is really about

The combinatorial hell of edge cases a deterministic 29-char address fitter has to handle:

- USPS standard abbreviations (AVE, BLVD, APT, NE/NW) — covered by USPS Pub 28, but…
- Apartment/unit positions ("Apt 5B" vs "#5B" vs "Unit 5B" vs trailing)
- PO Boxes vs street addresses
- Military APO/FPO/DPO
- International (Canada postal codes, UK postcodes, German "str." endings, Japanese reverse order)
- Rural route, highway contract, general delivery
- Puerto Rico urbanizations
- Directionals before/after street name
- "Saint" vs "St" vs "St." collisions (is "St Paul St" a saint or a street?)
- Diacritics and Unicode normalization
- Honorifics embedded in street names ("Dr Martin Luther King Jr Blvd")
- Suite/Floor/Building/Room combinations
- Company names + street on same line
- Care-of lines (c/o)
- Left-aligned vs right-aligned abbreviation preferences

No finite set of rules captures this. Every real-world edge case is someone's actual address.

## The generalization move

The author's abstraction isn't "address-summarizer." It's:

```
fn generic_llm_transform<I, O>(input: I, instruction: &str) -> O
```

A function whose *body* is natural language. You describe the transformation in English; the LLM is the implementation. Address truncation is one use. Recipe parsing is another. Log normalization is another.

This is the Rust-audience hook: Rust programmers have spent careers writing carefully-typed adapter code for every specific transformation. The LLM-as-function pattern inverts it. The type signature is concrete; the body is prose.

## Why this is the "ethical" case

The deterministic version fails humans — truncates `1234 Northwest Martin Luther King Jr Boulevard Apt 5B` to `1234 Northwest Martin Luther` and the paycheck never arrives. The LLM version, prompted with "fit to 29 chars, preserve USPS deliverability," outputs `1234 NW MLK Jr Blvd Apt 5B`. Deliverable. Recognizable. Dignified.

But the *ethics* isn't just "LLM got it right." The ethics is: a human being tried to write this function the hard way, and the human either gives up (and candidates get truncated addresses) or goes insane trying to handle every edge case (and ships late, buggy, and still wrong for the 10,000th edge case nobody thought of).

Choosing the LLM here is choosing not to torture a developer with an impossible spec. That's the ethical frame.

## The handoff — the actual ending of the story

The author wrote the generic interface **once**, and then handed the automation to the business person who owned the requirement. That person maintains the natural-language spec going forward.

It no longer takes the author's time.

This is the load-bearing move for the book's wider thesis:

- **Engineer writes the tool once.** Generic `transform(input, instruction)` — boring, cheap, reusable.
- **Business owner writes the spec forever.** The HR ops person, the DM, the policy analyst — whoever actually owns the domain — writes and edits the natural-language prompt.
- **Maintenance cost for the engineer goes to zero.** No Jira tickets for "address truncation broke on PR addresses." The person who understands the problem also owns the fix.

This is *democratizing implementation*. Prompts become the code; prompts are readable (and editable) by non-engineers. The engineer stops being a translator between business intent and silicon.

This thread runs through every case study in the book:
- **Oregon × Tyler:** state employees write their own queries in English instead of waiting on Tyler consultants
- **Frontline BI chat:** DMs ask questions of their data without a BI analyst in the loop
- **100k applicants:** hiring managers define the rubric in English; every applicant gets engaged with by that rubric
- **China-as-utility:** the utility isn't "a chatbot"; it's the power to describe a function and have it run

The address chapter is where the author introduces the pattern concretely — small problem, big implication.

## Code to show on the slide

- **Bad:** `let s = address.chars().take(29).collect::<String>();`
- **Worse:** 400 lines of pattern-match rules that still miss Puerto Rico urbanizations
- **The author's approach:** a generic `transform(input, instruction: "fit this address into 29 chars, preserving USPS deliverability; use standard abbreviations from Pub 28")` — one line, one natural-language spec, handles the long tail.

The talk argument: when the problem is "every edge case in the world," the ethical move is to stop pretending deterministic code can do it, and delegate to a system whose native representation is natural language.
