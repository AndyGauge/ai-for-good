---
status: draft — compiled from training-knowledge cutoff Jan 2026 without live web access
verification: every URL below needs spot-checking before the talk
confidence_key: HIGH = well-documented; MED = widely reported, verify numbers; LOW = directional
---

# Research Brief: AI-Mediated Interviews at Scale — The Ethical Case

## 1. High-volume hiring reality

**Google** (HIGH): Laszlo Bock, former SVP People Ops, said Google received ~3 million applications/year against ~7,000 hires — ~0.23% acceptance rate, "harder than Harvard." Source: Bock's book *Work Rules!* (2015); repeated in Business Insider and CNBC coverage.
- https://www.businessinsider.com/google-hiring-statistics-2016-10 (verify)

**Meta/Facebook** (MED): Pre-2022 figures cited 2M+ applications/year. Post-2022–2023 layoffs and 2024–2025 hiring freezes compressed openings while applications rose.

**Amazon** (MED): Largest corporate recruiter in the US. For SDE roles, no clean public ratio — but internal leaks to Business Insider in 2023 indicated L4/L5 SDE postings routinely drew 1,000–10,000 applicants each.

**Stripe / Shopify** (LOW — directional): Stripe has publicly said individual engineering postings draw "thousands" of applicants (Patrick Collison tweets; verify).

**Rust-specific** (MED, mostly anecdotal):
- Rust Foundation is small (<20 employees as of 2025). Postings on https://foundation.rust-lang.org/jobs/ routinely draw hundreds of applicants.
- High-profile Rust roles at Oxide Computer, Fermyon, Astral, and Cloudflare anecdotally draw 500–2,000 applicants per posting.
- Oxide publishes hiring process transparency: https://oxide.computer/careers (unique "written materials" process, explicitly anti-resume-screen).

**What recruiters actually do with the 99%** (HIGH):
- ATS keyword filters (Workday, Greenhouse, Lever) near-universal. Harvard Business School's 2021 "Hidden Workers: Untapped Talent" report (Fuller, Raman et al.) found ATS systems screen out 88% of qualified candidates due to rigid keyword criteria. https://www.hbs.edu/managing-the-future-of-work/Documents/research/hiddenworkers09032021.pdf
- LinkedIn Economic Graph data (2023): median recruiter spends 6–7 seconds per resume.
- Jobvite's annual Recruiter Nation Report consistently shows ~40% of hires come from referrals despite referrals being ~7% of applications. https://www.jobvite.com/lp/recruiter-nation-report/

## 2. AI interview tools — what they do, fairness claims, failure modes

**HireVue** (HIGH): Video interviews scored by ML. Originally used facial-expression analysis. **Retired facial analysis January 2021** after EPIC's 2019 FTC complaint and an ORCAA audit.
- EPIC complaint: https://epic.org/documents/in-re-hirevue/
- Washington Post coverage by Drew Harwell (Oct 2019, Jan 2021): https://www.washingtonpost.com/technology/2019/10/22/ai-hiring-face-scanning-algorithm-increasingly-decides-whether-you-deserve-job/

**Karat** (MED): Human-in-the-loop technical interviews. https://karat.com

**CodeSignal** (HIGH): Automated coding assessments + proctored "Certified Evaluations." 2024 launched "Conversation Practice" with generative AI interviewer. https://codesignal.com

**Sapia.ai** (MED): Chat-based structured interviews (no video, no voice). Claim: removes demographic signals. Publishes fairness audits annually. https://sapia.ai/resources/

**Documented failure modes:**
- MIT Technology Review (Hao, 2021): HireVue's accent and facial-feature handling flagged for disparate impact. https://www.technologyreview.com/2021/07/21/1029860/disability-rights-employment-discrimination-ai-hiring/
- Cambridge study (Rhea et al., 2022): "An External Stability Audit Framework to Test the Validity of Personality Prediction in AI Hiring" — found Humantic AI and Crystal gave different personality scores depending on file format. https://arxiv.org/abs/2201.09151
- ACLU complaint against HireVue (2023): deaf and autistic complainant.

**Regulation:**
- **NYC Local Law 144 (AEDT)**: Effective July 5, 2023. Annual independent bias audit, public audit summary, 10-day candidate notice. https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page
- **EEOC** May 2023 technical assistance: "Select Issues: Assessing Adverse Impact in Software, Algorithms, and AI Used in Employment Selection." Four-fifths rule still applies. https://www.eeoc.gov/laws/guidance/select-issues-assessing-adverse-impact-software-algorithms-and-artificial
- **EU AI Act** (Reg 2024/1689, in force Aug 2024, employment provisions Aug 2026): Annex III §4 classifies hiring AI as **high-risk**. https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- **Illinois AI Video Interview Act** (2020) and **Illinois HB 3773** (2026).
- **Colorado AI Act (SB 24-205)**: effective Feb 2026.

## 3. Fairness research

- **Amazon scrapped tool** (HIGH): Reuters, Jeffrey Dastin, Oct 10 2018. Tool trained on 10 years of resumes, learned to downgrade "women's" (as in "women's chess club captain"). Scrapped 2017. https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G
- **Raghavan, Barocas, Kleinberg, Levy — "Mitigating Bias in Algorithmic Hiring"** (FAT* 2020). Landmark audit. https://arxiv.org/abs/1906.09208
- **Chouldechova (2017)** — "Fair prediction with disparate impact." https://arxiv.org/abs/1703.00056
- **Barocas & Selbst (2016)**, "Big Data's Disparate Impact," *California Law Review*. https://www.californialawreview.org/print/2-big-datas-disparate-impact
- **Bogen & Rieke** (Upturn, 2018), "Help Wanted." https://www.upturn.org/reports/2018/hiring-algorithms/

**Defender perspectives:**
- Schumann et al. (2020) — argued audited AI outperforms unstructured human interviews on demographic fairness. https://arxiv.org/abs/1912.02260
- Structured interview literature (Schmidt & Hunter 1998 meta-analysis).

## 4. The "5 minutes each" math

100,000 applicants × 5 min = 500,000 min = **8,333.3 hours**.

- One FTE @ 2,080 hrs/year = **~4.0 years** of continuous work.
- At ~$75/hr fully loaded: ~$625,000 for first-pass screens alone.
- Ladders eye-tracking study (2018): recruiters average 6–7 seconds per resume. https://www.theladders.com/static/images/basicSite/pdfs/TheLadders-EyeTracking-StudyC2.pdf
- At 10 sec/resume × 100,000: still 278 hours / ~7 weeks of one human, with context-switching errors.

**Implication:** "Read every resume" is economically impossible at scale. The real choice is *keyword filter + 99% ghosting* vs *AI-mediated conversation for all*. The strawman to watch: pretending the alternative is careful human review.

## 5. Dignity / access / ghosting

- **Greenhouse "State of Job Hunting" 2024**: 75% of candidates report being ghosted after an interview.
- **Indeed 2023 survey**: 77% of job seekers ghosted since pandemic onset.
- **CareerPlug 2024 Candidate Experience Report**: only ~30% of applicants receive any response. https://www.careerplug.com/candidate-experience-report/
- **Talent Board CandE Research** (annual): https://www.thetalentboard.org/cande-research/
- **Virginia Eubanks**, *Automating Inequality* (2018) — automated non-response is itself a decision. https://us.macmillan.com/books/9781250074317/automatinginequality

**Thesis:** ghosting is the baseline. Any system that responds to everyone — even imperfectly — clears a very low ethical bar.

## 6. Rust community context

- **Rust Foundation 2024 Annual Report** (HIGH): talent supply cited as #1 concern by member companies. https://foundation.rust-lang.org/static/annual-reports/
- **Stack Overflow Developer Survey**: Rust "most admired" every year. https://survey.stackoverflow.co/2024/technology#admired-and-desired
- **JetBrains State of Developer Ecosystem** 2024: Rust usage growing ~2x faster than Go. https://www.jetbrains.com/lp/devecosystem-2024/rust/
- **Self-taught pipeline** (MED): Rustlings, TRPL (free online), /r/learnrust suggest heavy self-taught population. 2023 community survey: https://blog.rust-lang.org/2023/08/07/Rust-Survey-2023-Results.html
- **Oxide Computer's hiring process** (HIGH): every candidate writes long-form answers; every submission is read. https://oxide.computer/blog/forming-the-hard-parts — the only plausible competing ethic to AI-for-all at Rust-community scale.

## Skeptic-defense notes

1. **"AI interviews have documented bias."** So does every alternative. Honest comparison: *audited AI* vs *un-audited human skim + ghosting*.
2. **"Just do referrals like Oxide."** Referrals reproduce existing networks — single most-documented source of demographic lock-in (Rivera, *Pedigree*, 2015).
3. **"The AI will have disparate impact."** Measure it. Four-fifths rule, EEOC guidance. Publishing the audit beats the silent-keyword-filter status quo.
4. **"Candidates will game it with ChatGPT."** Same on take-homes. Structure for reasoning-in-motion, not artifacts.
5. **"This is surveillance capitalism."** Only if you keep the data. Build for deletion-by-default.
