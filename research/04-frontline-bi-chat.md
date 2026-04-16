---
status: draft — compiled from training-knowledge cutoff Jan 2026 without live web access
verification: every URL and specific number needs spot-checking before the talk
confidence_key: flagged inline; [SPEC] = author's extrapolation, not citation-backed
---

# Research Brief: AI-mediated operational BI for frontline managers at scale

## 1. Span of control reality

Classical management theory put the limit low. V.A. Graicunas (1933) argued relationships grow combinatorially — 6 reports produce 222 possible interaction pairings. Lyndall Urwick popularized "no more than 5 or 6 direct reports" for complex work. US Army doctrinal span is 3–7 (FM 6-0). Background: https://en.wikipedia.org/wiki/Span_of_control

**Gallup** *State of the American Manager* (2015) — still the most-cited modern reference — found managers account for ~70% of the variance in employee engagement; only ~1 in 10 people have natural talent to manage.
- https://www.gallup.com/workplace/236570/employees-lot-managers.aspx
- https://www.gallup.com/workplace/231593/why-great-managers-rare.aspx

Gallup *State of the Global Workplace* (annual, most recent 2024): engaged employee share ~23% globally, ~33% US. [SPEC on 2025/2026 — verify.]

**Deloitte / McKinsey** on "delayering": McKinsey's "Span of control: The key to managing in flat organizations" pushes wider spans (10–15) in knowledge work. https://www.mckinsey.com/capabilities/people-and-organizational-performance/our-insights

**Observed spans at the high end:**
- **Retail** — Walmart store managers supervise 200–350 associates per supercenter; department managers 10–40.
- **Fast food** — McDonald's GM typically oversees 50–80 crew across shifts.
- **Call centers** — SHRM/ICMI guidance clusters around 12–15 agents per team lead; ops managers over multiple teams routinely sit above 100. https://www.icmi.com
- **Gig platforms** — Uber/Lyft driver ops specialists historically cover thousands-to-tens-of-thousands of drivers per city-ops headcount. [SPEC — verify against Uber Driver Ops talks at QCon/Data Council.]
- **Hospitality** — Marriott/Hilton property GMs typically 100–300 associates; regional directors many thousands.
- **Warehouse/logistics** — Amazon Area Managers publicly described as owning 50–100 associates per shift.

**Academic**: Hechanova-Alampay & Beehr (2001); Meier & Bohte (2000, 2003) on public-sector span; Gittell (2001) "Supervisory span, relational coordination and flight departure performance" in *Organization Science* — wider spans hurt coordination unless relational practices compensate. https://pubsonline.informs.org/journal/orsc

## 2. Current state of operational BI

**Adoption gap** — Gartner has published "BI adoption stuck at ~30%" repeatedly since 2015 (analyst Rita Sallam). https://www.gartner.com/en/research/magic-quadrant

Salesforce/Tableau 2022 "Data Culture" survey: only 39% of employees trust the data they're given. [SPEC — verify.]

**Dashboard fatigue** — well-documented in practitioner writing, weak in peer-reviewed literature. Good secondary sources:
- Benn Stancil's Mode/Substack essays
- Tristan Handy at https://roundup.getdbt.com
- Cassie Kozyrkov (formerly Google Chief Decision Scientist): "decision-makers don't read dashboards, they ask questions." https://medium.com/@kozyrkov

**Frontline-specific**: HBR "Why Your Data Strategy Won't Work" (Redman); NewVantage Partners' annual *Data and AI Leadership Executive Survey* — "data-driven organization" self-identification below 25% despite decades of investment. https://www.newvantage.com

## 3. Text-to-SQL and conversational BI

**Benchmarks:**
- **Spider** (Yale, Yu et al. 2018): https://yale-lily.github.io/spider — top systems now >90% execution accuracy, effectively saturated.
- **Spider 2.0** (2024): https://spider2-sql.github.io — deliberately harder, enterprise-grade warehouses. Top results sit ~20–30% as of late 2024. [Verify current numbers.]
- **BIRD** (Li et al. 2023): https://bird-bench.github.io — introduces external knowledge and dirty data. Human ~92%; best models 60s → 70s through 2024.

**Production systems:**
- Snowflake **Cortex Analyst** — https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst — semantic-model-based text-to-SQL, GA 2024.
- Databricks **AI/BI Genie** — https://www.databricks.com/product/ai-bi
- Google **Gemini in Looker** — https://cloud.google.com/looker/docs/studio/gemini-in-looker — uses LookML as semantic grounding.
- Microsoft **Copilot in Power BI** — https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-introduction
- **Hex Magic** — https://hex.tech/product/magic-ai
- **Vanna.ai** (OSS) — https://vanna.ai
- **Dataherald** — https://github.com/Dataherald/dataherald
- **WrenAI** — https://github.com/Canner/WrenAI

**Known failure modes** (Rajkumar et al. 2022 https://arxiv.org/abs/2204.00498; Pourreza & Rafiei DIN-SQL https://arxiv.org/abs/2304.11015):
- Hallucinated joins across unrelated keys
- Wrong aggregation grain (SUM over pre-aggregated rows, fanout double-counting)
- Ambiguous entity resolution ("revenue" — gross, net, booked?)
- Date-boundary errors (timezone, fiscal vs calendar)
- Silent wrong answers — SQL executes, returns plausible number, nobody catches it

**Mitigation consensus**: semantic layer grounding. dbt Semantic Layer, Cube, LookML, Malloy.
- https://cube.dev
- https://docs.getdbt.com/docs/use-dbt-semantic-layer/dbt-sl

## 4. The ethical / "AI for Good" angle

**Empirical core:**
- Gallup's manager-explains-70%-of-engagement is the load-bearing claim.
- Gallup Q12 meta-analysis (Harter et al., most recent 2020): https://www.gallup.com/workplace/321725/gallup-q12-meta-analysis-report.aspx — top-quartile engagement units show 81% lower absenteeism, 58% fewer patient safety incidents, 64% fewer safety incidents, 43% lower turnover. Verify exact numbers.
- Dube, Freeman, Reich — "The Stable Scheduling Study" — frontline manager discretion informed by better information produces large wellbeing gains for hourly workers. https://irle.berkeley.edu/stable-scheduling-study/
- Callen, Gulzar, Hasanain, Khan — "Political Economy of Public Employee Absence" — information asymmetries to frontline supervisors cause measurable harm.

**The moral frame for the talk:** decisions made by a District Manager over 400 workers *are* labor conditions. Shift swaps, discipline, PTO approval, safety escalation. If the DM is operating on stale PDFs and vibes, workers absorb the error. Information access for the supervisor is a working-condition issue for the supervised.

## 5. At-scale examples

- **Uber QueryGPT** — cleanest public case study for this talk. https://www.uber.com/blog/query-gpt/
- **Uber Michelangelo** (ML platform, public since 2017) — https://www.uber.com/blog/michelangelo-machine-learning-platform/
- **Walmart** — "Me@Walmart" and "Ask Sam" manager apps; 2024 CES keynote mentioned internal associate AI assistant. https://corporate.walmart.com/news
- **Pinterest** — "Text-to-SQL on Pinterest" engineering blog, 2024. https://medium.com/pinterest-engineering
- **LinkedIn** — "SQL-GPT" internal tool discussed at Data+AI Summit 2024.
- **Shopify** — Sidekick merchant assistant. https://shopify.engineering
- **Amazon Q for Business** — https://aws.amazon.com/q/business/
- **McDonald's** ended IBM drive-thru AI pilot in 2024; no verified manager-BI LLM case study.

## 6. Rust relevance for the rust-lang audience

Genuine Rust infrastructure in this stack:
- **Apache DataFusion** — Rust query engine, Arrow-native. https://datafusion.apache.org
- **arrow-rs** — https://github.com/apache/arrow-rs
- **Polars** — Rust-native DataFrame. https://pola.rs
- **LanceDB** — Rust vector DB, columnar Lance format. https://lancedb.com
- **Qdrant** — Rust vector DB. https://qdrant.tech
- **SurrealDB** — https://surrealdb.com
- **Meilisearch** — https://www.meilisearch.com
- **sqlparser-rs** — https://github.com/apache/datafusion-sqlparser-rs — parser used across the ecosystem for validating LLM-generated SQL
- **GlueSQL**, **GreptimeDB**, **RisingWave** — Rust OLAP/streaming
- **candle** (Hugging Face) — Rust ML framework. https://github.com/huggingface/candle
- **mistral.rs** — https://github.com/EricLBuehler/mistral.rs
- **rig** — Rust LLM application framework. https://github.com/0xPlaygrounds/rig

**Talk through-line:** the *validator* (does this SQL do what the semantic layer says it should?) is exactly where Rust earns its keep. DataFusion + sqlparser-rs can parse, type-check, and cost-estimate an LLM's proposed query in single-digit milliseconds before it ever hits Snowflake. The "AI for Good" claim with teeth: the safety layer that catches "SUM over a fanout join" is deterministic, auditable Rust, not another LLM.

---

**Flags and gaps:**
- Every URL and number needs verification before the talk.
- Strongest, most falsifiable claims — build the chapter around these: Gallup's 70%-of-variance, BIRD/Spider 2.0 benchmark gaps, Uber QueryGPT as named case study.
- Weakest claims to verify-or-cut: specific 2026 engagement percentages, specific PowerBI/Tableau adoption rates, McDonald's/Amazon internal tooling specifics.
