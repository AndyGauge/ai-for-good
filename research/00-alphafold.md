---
status: sourced; facts verified against primary sources April 2026
verification: URLs spot-checked during research session
confidence_key: HIGH = primary source confirmed; MED = from secondary summary; LOW = flagged inline
---

# Research Brief: AlphaFold — the unimpeachable opener

## 1. The science (HIGH)

**The problem.** Proteins fold into specific 3D shapes that determine their function. Predicting that shape from amino-acid sequence alone — the "protein folding problem" — was a 50-year grand challenge. Levinthal's paradox (1969): a protein could theoretically sample 10^300 configurations, yet folds in milliseconds, so there must be funneling principles we don't fully understand.

**CASP.** The Critical Assessment of Structure Prediction, run biennially since 1994, is the field's blind test. Organizers give teams amino-acid sequences of proteins whose experimental structures exist but are unpublished; teams predict; predictions are scored against truth.

**AlphaFold 1 (CASP13, 2018).** DeepMind's first entry placed first but still gave coarse predictions.

**AlphaFold 2 (CASP14, 2020).** The breakthrough. In the assessors' ranking by summed z-scores (>2.0), **AF2 scored 244.0 vs 90.8 for the next-best group** — a margin unprecedented in CASP history. AF2 produced high-accuracy structures (GDT_TS > 70) for 87 of 92 domains and structures on par with experimental accuracy (GDT_TS > 90) for 58 domains, with a median GDT_TS of 92.4. Published: Jumper et al., "Highly accurate protein structure prediction with AlphaFold," *Nature* 596, 583–589 (2021). https://www.nature.com/articles/s41586-021-03819-2 and companion CASP14 paper in *Proteins* https://pubmed.ncbi.nlm.nih.gov/34599769/

**AlphaFold 3 (2024).** Extended to protein complexes, nucleic acids, ligands, and post-translational modifications. Publication: Abramson et al., *Nature* 630 (May 2024). Raised concerns about closed weights (initially server-only) — relevant to the open-vs-closed-access thread running through the book.

## 2. The public-good delivery (HIGH)

**AlphaFold Protein Structure Database (AFDB).** Partnership between **Google DeepMind and EMBL-EBI** (European Bioinformatics Institute, Hinxton, UK). https://alphafold.ebi.ac.uk/

- **Over 200 million protein structure predictions** — essentially all proteins in UniProt.
- **License: CC-BY-4.0** — free for academic AND commercial use. This is the ethically load-bearing choice: DeepMind could have paywalled it.
- March 2026 expansion added NVIDIA and Seoul National University for protein-complex predictions.
- DeepMind's stated reach: **over 2 million researchers from 190 countries** have used AFDB (cited in ACS C&EN coverage of the Nobel): https://cen.acs.org/people/nobel-prize/Baker-Hassabis-and-Jumper-win-2024-Nobel-Prize-in-Chemistry/102/web/2024/10

## 3. Impact stories (MED — general verified, specific drug candidates need case-by-case verification)

**Neglected tropical diseases.** DNDi (Drugs for Neglected Diseases initiative) publicly credits AlphaFold with accelerating target identification for leishmaniasis, sleeping sickness, Chagas disease, mycetoma. https://dndi.org/news/2024/nobel-prize-chemistry-awarded-for-alphafold-an-ai-model-used-dndi-for-neglected-diseases/

**Survey of applications** (Drug Discovery Trends, 7 case studies): https://www.drugdiscoverytrends.com/7-ways-deepmind-alphafold-used-life-sciences/ — malaria vaccine candidate design, PETase / plastic-degrading enzyme variants, antibiotic resistance mechanism analysis.

**Caveat:** specific "AlphaFold cured X" claims are usually overstated. AlphaFold accelerates the *target identification* and *rational design* phases; it does not replace wet-lab validation, clinical trials, or regulatory approval. For a Rust conference, framing it as "the fastest you-can't-do-that-by-hand transformation" is more defensible than miracle-cure narratives.

## 4. The 2024 Nobel (HIGH)

**Chemistry**, announced October 2024. https://www.nobelprize.org/prizes/chemistry/2024/press-release/

- **Half to David Baker** (University of Washington) — "for computational protein design"
- **Half shared by Demis Hassabis and John Jumper** (Google DeepMind, London) — "for protein structure prediction"
- 11 million Swedish kronor (~$1M USD), split 50/25/25.

The Nobel citation is careful: AlphaFold won for *prediction*, Baker won for *design* (Rosetta, RFdiffusion). Both halves together close the loop — predict any structure, then design a new one. Useful for a talk: the 2024 Nobel is the first to recognize AI-native scientific work at this level.

## 5. Before AlphaFold (MED — figures are order-of-magnitude)

Pre-2020, experimental structure determination was the only path:

- **X-ray crystallography**: requires growing well-diffracting crystals — months to years of trial-and-error per protein; membrane proteins often infeasible. https://febs.onlinelibrary.wiley.com/doi/10.1111/febs.15676
- **Cryo-EM**: requires ~$5M microscopes, specialized sample prep, substantial compute for reconstruction. https://pmc.ncbi.nlm.nih.gov/articles/PMC5192981/
- **NMR spectroscopy**: limited to small/medium proteins in solution.

Rough industry number (cite with caveat): **a single novel structure historically cost $50K–$500K and took 6–24 months**. The Protein Data Bank reached 200K experimental structures after 50+ years of global effort. AFDB produced 200M predictions in under three years.

**Order-of-magnitude comparison for the talk:** 1,000× more structures, generated by a model whose inference cost per prediction is pennies. This is the "AI as infrastructure" moment made concrete.

## 6. Rust-audience angle (HIGH — verified crates exist)

Rust has a real, growing structural-bioinformatics ecosystem:

- **pdbtbx** — pure-Rust PDB/mmCIF parser. Uses Rayon for multithreaded iteration and rstar for spatial lookup. https://crates.io/crates/pdbtbx — this is the canonical crate for parsing AlphaFold outputs.
- **rust-bio** — general bioinformatics algorithms. https://rust-bio.github.io/
- **bio-forge** — pure-Rust macromolecule prep (protonation, solvation, topology). https://github.com/TKanX/bio-forge
- **pdbrust** — alternative PDB parser. https://crates.io/crates/pdbrust
- **Athanor** — commercial Rust structural-bio libraries. https://www.athanorlab.com/rust-tools
- Broader biology crate listing: https://lib.rs/science/bio

**Talk hook:** AlphaFold itself is JAX/Python, but the *downstream* infrastructure — parsing millions of mmCIF files, indexing by residue, running spatial queries across 200M structures — is exactly the performance-critical territory Rust owns. The ethical frame: AlphaFold's *outputs* are a public good only if there is a public-good tooling layer that lets scientists query them without a supercomputer.

## 7. Honest critiques (HIGH — don't skip these on stage)

- **Intrinsically disordered proteins (IDPs).** AlphaFold's low-confidence regions (low pLDDT) correlate with disorder. It doesn't *predict* IDPs — it flags them. Recent arXiv work documents "hallucinations" in AF3 for disordered regions. https://arxiv.org/html/2510.15939v2
- **Conformational ensembles.** A protein in vivo samples multiple conformations; AlphaFold predicts *a* structure, not the ensemble. This matters for drug binding. https://www.annualreviews.org/content/journals/10.1146/annurev-biodatasci-102423-011435
- **Novel folds / de novo.** AF2 was trained on PDB; proteins with folds not in the training set are predicted less reliably.
- **Dynamics and allostery.** Static snapshots miss function-relevant motion.
- **Mohammed AlQuraishi** (Columbia) has been a prominent measured critic, arguing AF is a tool not a theory — it predicts, it doesn't *explain* folding. His end-to-end differentiable models (RGN, OpenFold) are the main open reimplementations.
- **AlphaFold 3's closed weights** at launch drew backlash from the open-science community.

## What to say on stage

AlphaFold is the *opener* because it is the one "AI for good" claim no one in the room will contest. What it shows is not that AI is magic but that **when a problem is truly combinatorial (10^300 folds), humans can't brute-force it — they can only describe what they want and let a system do the search**. Same pattern as the address case later in the book: stop writing the million rules, start describing the intent.
