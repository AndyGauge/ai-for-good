# The Address

An integration engineer's job, stripped of jargon: map every system in the world to ours.

Every customer already has an HR system. Sometimes five, from old acquisitions. Workday here, UKG there, ADP in the regional unit that has been on ADP since 1994. The product has to push data into and pull data out of all of them. Every field is a negotiation between two systems that never agreed on what the field was.

Here is the ticket.

> The hotel onboarding is failing for new hires whose addresses are longer than twenty-nine characters. Can we truncate?

The twenty-nine-character limit is one rule. There are thousands like it. None documented. All discovered in production. The payroll vendor uses a 1997 flat-file format with fixed-width byte columns, so UTF-8 accents silently shift the truncation point. The consultant knows the symptom. Not the rule.

A week of debugging. One fix. The fix breaks a different customer with the same limit for a different reason.

One ticket. Two new tickets. Always.

This is the integration engineer's job. The specification is infinite. The code is finite. You are paid to lose.

## The shift

Treat the LLM like a deterministic function. Pin the model. Supply the input. Validate the output. Inside that envelope, it behaves like any other function. Input goes in. Output comes out. Non-determinism under the hood is not your problem. The interface is your problem.

Write the instruction in the shape of a requirement.

> Given this input, summarize with preference for deliverability, and try to keep it under twenty-nine characters.

Email subject line under sixty? Same shape. Twitter post under two-eighty? Same shape. Copy. Paste. Edit. Deploy.

When a consultant surfaces a new rule, you do not rewrite code. You add a sentence.

> ...and for Puerto Rico urbanizations, keep the urbanization name before the house number.

One more clause. No dependency update. No release cycle. No rewrite of the state-abbreviation table.

Then hand the instruction to the person who actually knew what it should say. The HR operations lead who has been filing tickets like these for twenty-two years, against somebody else's product. Twenty-minute training. From then on, the tickets go to her. She maintains the sentence.

The engineer stops being the pipeline. The person who owns the problem owns the fix.

## The honest part

LLMs hallucinate. They will decide *Strt* is a fine abbreviation for *Street*. A human carrier will probably still deliver — they will just think your data-entry clerk needs glasses. But *Strt* is not USPS-recognized. It will not round-trip through CASS. The automated sort snags. The payroll integration rejects the record. You are back to a ticket.

So you validate. libpostal. A real address-standardization library. Ten years old, deterministic, boring. If the LLM's answer fails the check, you retry with a tightened prompt or escalate to a human.

The LLM generates. Deterministic code verifies. Both layers matter.

Not free. Every call costs. For a real-time form, affordable. For a batch of ten million records, you cache, pre-validate, only call the model when the cheap parser fails.

Auditable. You log prompt, input, output, validation. When the compliance officer asks *why did this address change*, you show the prompt. The prompt is in English. She can read it.

Auditability is what the pattern buys you that the 1997 flat-file format never did.

LLMs cannot count to twenty-nine. They cannot do dates at all. The guidance is more than enough anyway. You are not asking the model to count. You are asking it to try. The validator catches the rest.

## The arc

The function predated this ticket. I had built it for a hype-driven feature my company had rejected on ethical grounds. The code was reusable. The ethics, my company had to teach me.

I am not the hero of this chapter. I am the integration engineer who stopped writing rules and started writing intent.

You will not map every address in the world to every HRIS in the world by writing every rule.

You will map it by writing one deterministic function that takes an instruction, then maintaining the instruction.

Writing the rules is infinite. Writing the intent is a paragraph.

The paragraph is maintained by the person who already knew what it should say.
