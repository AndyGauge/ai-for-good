# AlphaFold

Count every token every AI has ever processed. Every ChatGPT query. Every Claude call. Every code suggestion, every agent request, every training pass, every inference request at every lab since the first GPT shipped.

Multiply that number by itself. Twenty times.

That is the number of ways a single protein can fold.

One protein. In your body. Right now.

A biochemist named Cyrus Levinthal worked it out in 1969. He was making a point. A protein cannot actually search that many configurations. If it did, folding would take longer than the age of the universe, and proteins fold in milliseconds. So either the universe is lying or the search is not what we think it is.

That is the problem. For fifty years, that was *the* problem. The grand challenge. The one biochemists would shake their heads about at conferences and say *this one will take another hundred years*. Because how do you search a space you cannot even represent?

The answer, before 2020, was that you didn't.

You grew a crystal. You put it in an X-ray beam. You stared at the diffraction pattern for months. You guessed. Or you froze the protein at cryogenic temperatures and shot it with electrons — what scientists call cryo-EM, what a funder calls *a five-million-dollar microscope on the second floor that needs its own power feed*. Either way, one structure. Sometimes two. Over a career.

The Protein Data Bank is the global archive of everything we ever solved by those methods. The PDB. Every crystallographer, every electron microscopist, every NMR spectroscopist — what a chemist calls *their life's work*, what an accountant calls *the depreciation schedule on that microscope* — each one submitting their structures to the same shared library, year after year.

In 2020, fifty years after Levinthal posed the paradox, the PDB had about two hundred thousand structures.

Two hundred thousand sounds small. It isn't.

Each structure is a PhD. A microscope running six months at a stretch. A graduate student growing a crystal at three in the morning because the temperature was finally right. A paper with seven authors and two years of peer review. A career.

Two hundred thousand careers in a shared archive.

Microsoft has that many employees. Apple has fewer. IBM once had more. Imagine an entire Fortune 100 company where every single person has a PhD in protein chemistry. Imagine none of them ever leaving. Imagine all of them, for fifty years, growing crystals and shooting them with X-rays.

That is the PDB.

Then AlphaFold 2 showed up.

## CASP

The way the field tested itself was called CASP. The Critical Assessment of Structure Prediction. A biennial blind test. The organizers took proteins whose experimental structures had been solved but not yet published, gave teams only the amino-acid sequence, and asked the teams to predict the shape. Then they scored the predictions against the truth.

CASP is where ambition went to die. You thought your algorithm was good. Then you ran it against a target the organizers had kept secret, and the target would fall somewhere between garbage and gesture. The scores hovered in the region that scientists call *encouraging* and everybody else calls *not working*.

AlphaFold 1 entered CASP13 in 2018. Placed first. Still produced coarse predictions.

AlphaFold 2 entered CASP14 in 2020.

In the assessors' summed z-score ranking — a statistician's way of saying *how many standard deviations above the field* — AlphaFold 2 scored 244.0. The next best group scored 90.8. On 87 of 92 domains, it produced structures accurate enough to publish. On 58 of those, the predictions were *as good as the experimental structures were*. Median accuracy: 92.4 out of 100.

The old way surrendered.

John Moult, the organizer of CASP, who had been running this competition for twenty-six years watching incremental improvement, said the problem had been solved. Not *solved enough*. Solved. The community agreed. There were still edge cases. There would always be edge cases. But the thing that had been a fifty-year grand challenge was, in some working sense, finished.

Jumper J, Evans R, Pritzel A, et al. *Nature* 596, 583–589 (2021). [https://www.nature.com/articles/s41586-021-03819-2](https://www.nature.com/articles/s41586-021-03819-2). The paper has been cited more than any AI paper in history by working biologists. Not theoreticians. Working biologists. The people with the microscopes on the second floor.

## The ethical move

Here is where most tech-hype stories end. Company wins. Stock goes up. Conference talks get louder.

DeepMind did something else.

They partnered with the European Molecular Biology Laboratory — what a researcher calls *EMBL-EBI*, what a taxpayer calls *a public-sector lab in Hinxton, UK that anyone can use*. Together they built the AlphaFold Protein Structure Database. AFDB.

Then they predicted two hundred million protein structures. Effectively every protein in UniProt. Every protein that anyone had ever named.

Then they released all of it. Free. Under a license called CC-BY-4.0, which is a legal document that says *use this however you want, commercially, academically, forever, just say where it came from*.

Two hundred million structures. Fifty years of global effort had produced two hundred thousand. AlphaFold produced two hundred million. One thousand times more. Free.

Two hundred million is more than every person with a job in the United States. Every factory, every farm, every office, every hospital. Every paycheck. That is about one hundred sixty million workers. AlphaFold made more predictions than that.

Still less than China's workforce. Seven hundred forty million. But bigger than America's.

A predicted protein for every working person in America. Then add the United Kingdom. Then Ireland. Then keep going down the list of smaller nations. You still have many workforces to spare.

As of the Nobel announcement, more than two million scientists from 190 countries had used it.

That is the claim. That is the unimpeachable part. That is why AlphaFold opens this book.

## The Nobel

October 2024. The Royal Swedish Academy of Sciences. Chemistry.

Half to David Baker, at the University of Washington, *for computational protein design*. Baker had spent twenty years using computers to build proteins that had never existed in nature. He designed pharmaceuticals. He designed vaccines. He designed tiny sensors and nanomaterials. He did it with a tool called Rosetta, an open-source codebase that has outlasted three university presidents.

Half to Demis Hassabis and John Jumper, at Google DeepMind, in London, *for protein structure prediction*.

Eleven million Swedish kronor. Split fifty-twenty-five-twenty-five. What a banker calls *liquidity*, what a grad student calls *never having to write another grant as long as I live*.

The citation was careful. Baker won for *design*. Hassabis and Jumper won for *prediction*. The two halves together close a loop. Predict any structure. Design a new one. Two halves of the same tool.

And the Royal Swedish Academy, which had spent a century handing the chemistry Nobel to people who did chemistry with their hands, gave half of it to a model.

## The honest part

This book is not going to pretend. Every chapter has this section. The honest part.

AlphaFold does not predict intrinsically disordered proteins. It flags them. It marks the region low-confidence and moves on. If your protein is a floppy signaling peptide with no stable structure at all, AlphaFold will tell you it doesn't know. Which is better than most tools do. But it is not *prediction*. It is *admission*.

AlphaFold does not predict conformational ensembles. A protein in a real cell samples many shapes. It breathes. It flexes. AlphaFold gives you one snapshot. For drug binding, that snapshot is often the wrong snapshot.

AlphaFold does not predict novel folds. It was trained on the PDB. Proteins whose shapes fall outside the distribution of what's already been solved — new folds, engineered proteins, proteins from life that never made it into the training set — are predicted worse than proteins the model has seen many times.

AlphaFold 3, released in 2024, extended the system to complexes and nucleic acids and ligands. The community cheered the science. Then looked at the license. The weights were closed. Server access only. The open-science community, which had built its entire scaffolding around AF2's openness, went public with the grievance. DeepMind eventually relented. Partly.

The honest part, every chapter: a tool this powerful, released this widely, will be misused. Papers will be published with AlphaFold structures as ground truth when the confidence scores did not warrant it. PhD committees will accept theses that depended on a prediction the author did not verify. Grants will be awarded on the strength of hallucinated drug targets.

That is not an argument against the tool. It is the cost of the tool. The cost is there. The benefit is larger. Both things are true. I will not pretend otherwise.

## The Rust part

AlphaFold itself is written in JAX. JAX is a Python library for machine learning. Python is the language of machine learning because Python is what the researchers know. Fine.

The question is what happens downstream.

Two hundred million structure predictions are two hundred million files in a format called mmCIF. If you want to query them — find all proteins with a particular fold, all binding sites near a particular residue, all structures where a particular motif shows up — you need infrastructure. Parsers that do not leak memory. Spatial indexes that do not stall. Iterators that actually use the cores the researcher paid for.

That is where Rust earns its keep.

**pdbtbx** is a pure-Rust parser for PDB and mmCIF files. It uses Rayon for multithreaded iteration. It uses rstar for spatial lookup. It does not surprise anyone. [https://crates.io/crates/pdbtbx](https://crates.io/crates/pdbtbx)

**rust-bio** is a general-purpose bioinformatics library. [https://rust-bio.github.io/](https://rust-bio.github.io/)

**BioForge** is a pure-Rust toolkit for preparing macromolecular systems for simulation. [https://github.com/TKanX/bio-forge](https://github.com/TKanX/bio-forge)

None of these are AlphaFold. All of them are the infrastructure that lets AlphaFold be useful. A model that predicts two hundred million structures is only a public good if there is a public-good *tooling layer* underneath it — what an engineer calls *the query layer*, what a scientist calls *the part that lets me actually find my protein in the database*.

The ethical argument runs both ways. DeepMind made the science free. It took the Rust community — and the Python community, and the C community, and everyone else — to make the science *reachable*. The infrastructure is where the generosity becomes usable.

## The pattern

Every chapter of this book is the same shape. AlphaFold is its biggest version.

A combinatorial problem. A human who had been told to brute-force it. A tool that swaps rules for intent.

The rest is smaller. An address field. A hiring funnel. A district manager. A state employee. A billion citizens handed AI as a utility.

AlphaFold is the proof of concept.

The rest is the receipts.
