# The Utility

In 2020, China's State Council added a phrase to its official development lexicon: 新基建, *new infrastructure*.

The old infrastructure was roads, bridges, ports. The new infrastructure was compute, data, and AI. The State Council declared them equivalent — things the country would build, subsidize, and make available at scale, the way earlier generations built the national grid.

That is the premise this chapter is about. China decided AI is a utility.

## The voucher

The core mechanism is 算力券 — the compute voucher. A municipality issues vouchers worth a fixed amount, good against AI compute at specified data centers. Small and medium enterprises redeem them. Startups, research labs, university teams redeem them. The subsidy pays down the rental cost of GPU time.

As of 2024 and 2025:

- Shanghai: about 600 million RMB ($84M) in vouchers, covering up to 80% of AI rental fees, plus 100 million RMB for data and model training.
- Shenzhen: 500 million RMB annual program. 50% subsidy for general applicants, 60% for startups.
- Chengdu: 100 million RMB, expanded from an earlier pilot.
- Shandong: 30 million RMB initial, another 1 billion queued.
- Beijing: a parallel program in the Economic-Technological Development Area.

Together they create a second market beneath the commercial AI market — where access is subsidized the way public transit is subsidized alongside private cars.

## The open weights

The utility framing runs deeper than vouchers. The major Chinese labs — DeepSeek, Alibaba's Qwen, Zhipu's GLM, ByteDance's Doubao, Baidu's Ernie, 01.AI's Yi — have made open weights the norm. Not open in the sense of *we wrote a paper*. Open in the sense of *the weights are on Hugging Face, under a permissive license, anyone can download them*.

Qwen 3.5's 397-billion-parameter mixture-of-experts model ships under Apache 2.0, with 256,000-token context and 201-language support. DeepSeek V4, released in early 2026, runs inference at about thirty cents per million input tokens. Claude Sonnet at the same moment was three dollars. GPT-5 was a dollar and a quarter.

The pricing gap is not a discount. It is a different theory of what the model is for.

A closed-weight frontier lab is a company. A company sells a product.

An open-weight model under Apache 2.0 is closer to a public-works project. You do not sell Apache 2.0. You subsidize it, deploy it, and measure the economic activity it enables. DeepSeek and Qwen together went from about one percent of global AI usage in early 2025 to roughly fifteen percent a year later. The strategy worked.

## What utility means

A utility has three properties.

- It is ubiquitous. Everyone has access, at prices calibrated to public good, not to market optimization.
- It is metered. You pay for what you use, at regulated rates, with defined tiers for low-income users.
- It is accountable to the public. Not a private monopoly.

China is working the ubiquity problem. The vouchers extend access to the populations private pricing would exclude. The open weights let small firms self-host without paying rent to a US provider.

The metering is real but state-bound. Chinese models file with the Cyberspace Administration — 346 generative-AI services as of April 2025 — and content moderation is enforced by law.

Accountability is the hardest word. A utility accountable to the public is accountable to the public. A utility accountable to the state is accountable to the state. Those are not the same condition.

## The honest part

Every chapter has the honest part. This one's is larger.

The utility framing is not clean. The same state that subsidizes the compute also operates Hikvision and Dahua. The Cyberspace Administration's Interim Measures for Generative AI Services, effective August 2023, require providers to prevent content that "endangers national security" or "undermines social stability." Those phrases are not neutral.

Export controls matter too. US restrictions on HBM memory and advanced lithography mean that the Chinese AI stack is built under asymmetric constraints. Some of the efficiency in DeepSeek and Qwen is real engineering, and some of it is a forced response to a hardware gap.

None of this disqualifies the utility framing. All of it complicates it. *China treats AI as a utility* and leaving it there is not honest. *Therefore it cannot be a model for anything* is not honest either. The utility framing is a useful idea that arrived wrapped in a governance model the US would not adopt.

The question for the reader of this book is whether the idea can be separated from the wrapper.

## The Rust part

A note for the audience of this book.

Some of the most important database and infrastructure software of the last five years came out of China, in Rust. TiKV and TiDB from PingCAP. GreptimeDB. RisingWave. The ByteDance teams behind Feishu were early Rust adopters. RustChinaConf has run in Shenzhen, Shanghai, and Hangzhou. The Rust community in China is large, active, and shipping at major scale.

If AI becomes a utility, the infrastructure underneath it has to be fast, cheap, and memory-safe. That is a Rust problem. The Chinese teams were early. They were not the only ones, but they were early, and the work is genuinely impressive. The Rust audience for this book should know.

## The pattern

Every chapter of this book is the same move at a different scale.

AlphaFold made a tool available to two million scientists for free. The address chapter handed one generic transform to one domain owner. The interview chapter gave every applicant a real shot. Cue put a pair of hands in the manager's thread. Oregon proposed a public-good alternative to Tyler, built locally.

China's bet is bigger than any of those. The bet is that AI is more like electricity than like software — that the right governing layer is a utility regulator, not a market.

That bet may or may not be the right bet. It is the bet most directly aimed at the access gap named in the introduction to this book. The US has not made any equivalent bet. The American frontier labs are private, closed, and priced by the market. The public has no voucher. The student, the non-profit, the rural school district, the immigrant worker at the address the payroll system could not fit — they pay the market rate or they do without.

That is a choice. It is worth calling a choice.

The utility framing is the alternative. The rest of this book is what a person with access to the utility can do.
