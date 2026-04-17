# Introduction

I used Claude Opus 4.7 to write this book.

Claude is a large language model. A large language model is a trained reader that writes back. I asked, it drafted, I edited. Every word. I read every word. I kept what was mine. I cut what wasn't. The sentences here are sentences I approve of. Not because I typed them first. Because I agree with them enough to put my name on the cover.

That is the strongest honest claim I can make. It is not a strong enough claim.

A mechanical typewriter hammers the key into the ribbon and the ribbon into the paper. On the back of the page there is an indentation. A mark. A dent. You can run your finger across it. You can feel that a person was here, at a specific moment, at a specific pressure. The paper remembers.

Digital text does not have a back side. Pixels change color. Electrons rearrange. The computer's filing cabinet — what engineers call a version-control system — rolls the rearrangement forward or back and leaves no mark. No dent. I can replace this sentence with a better one in a second. I can replace it again in the next second. There is no indentation. The screen does not remember anything.

So when I tell you I read every word, understand what I am and am not claiming. I am claiming intent. I am not claiming the kind of physical, slow-hand accountability a typewriter once extracted from every writer by the friction of the medium. The friction is gone. The accountability is now something I supply on purpose or it does not exist.

---

There is a newer physics problem here, and it worries me more than the missing indentation.

A person reads at about two hundred and fifty words a minute. A person types at about forty. A person handwrites at about twenty-five. Reading has always been several times faster than writing. The gap is not a coincidence. The gap is the human body. The muscles that move the hand are slower than the eye, and the slower thing is the filter. Writing is the place where thought was forced to pass through the hand, and in that passage, most of what would have been said got rejected before it became a sentence.

That filter is being dismantled.

Brain-computer interfaces decode imagined sentences now. BrainGate types at twenty-two words a minute from hand-motor signals. Stanford's inner-speech prototype decodes attempted speech at sixty-two. Meta's non-invasive system sits at forty. The interface is moving from the fingers to the cortex. Every year, the scientists push the sensor closer to the brain.

The muscle delay was not just a bottleneck. It was a jury. For as long as humans have written, the slower thing — the hand — has been where the brain's drafts were corrected, revised, or quietly dropped. When that goes, anything anyone imagines becomes publishable at the speed of thought. I am not ready for that. I do not think most writers are. I am afraid of what we lose when authorship stops being a physical act.

This book is about that choice.

There is another admission. I had this tool because I could afford it, and because the company I worked for granted me the rest. The subscription costs real money. The account at the tier I used — what engineers call an API key, what a business person calls a paid seat — costs more. And the setup that lets me run not one question at a time but many — what engineers call an agentic workflow, what a manager would recognize as running a small office of specialists handing work to each other — costs most of all. For most of the people who might benefit most from what this book argues, that setup is out of reach.

I cannot fix that in these pages. I can name it. When I tell you *an engineer wrote a generic interface and handed it to the business owner*, I am describing a workflow that presupposes the engineer had the technical account, the business owner had the browser tab the company paid for, and the company had enough budget to let them both experiment for a week without producing anything shippable. Most organizations do not have that. Most individuals do not either.

The second cost is time. Nobody talks about this one honestly. You do not sit down at an agentic workflow — at your small office of specialists — and produce the book you are reading. You sit down at one question. You type. You get an answer. You feel clever. You get the satisfaction of publishing your thoughts the same day you have them.

And then you start to notice that one question is not enough for the actual work. The good stuff happens when the first answer hands off to a second. The second hands to a third. The third writes a note that a fourth reads and critiques. Engineers call this *agentic*. A receptionist calls it *a team with a good routing process*. They are the same thing.

The transition is awkward. You go from *asking the chatbot* to *running the small office*. It feels like learning stick after years of automatic. You produce worse output for a while. You feel slower. You want to close the laptop and write the next paragraph by hand just to feel competent again.

That discomfort is the tax you pay to move from tourist to operator. Like any tax on learning, it falls hardest on people who don't have slack in their schedule to pay it.

Here is a concrete example of what the small office does not do for you.

Early in this book is a chapter about AlphaFold. The model I worked with wanted to open that chapter with the statement that a single protein can fold into ten to the three hundredth power configurations. That is the correct number. It is also a useless number. Nobody can feel ten to the three hundredth power.

Turning that number into a sentence a reader can feel is architecting — what an engineer calls *system design*, what an editor calls *making it land*. I did it by reaching for *Making Numbers Count* by Chip Heath and Karla Starr, a book on how to communicate statistics in a way human beings can actually hold. The version that ended up in the chapter: take every token every AI has ever processed — roughly a quadrillion — and multiply it by itself twenty times. That is one protein.

The model wrote *ten to the three hundredth*. The human who read books on how numbers land wrote *multiply every AI token ever by itself twenty times*.

That is the part of authorship the model does not do. You can automate a draft. You cannot automate the translation from a fact that is technically true to a sentence that carries the weight of the fact into a reader who does not come to the page with a PhD.

So when an autodidactic, hypergraphia-induced writer finds a utility, they write.

So I am starting from privilege. Money. Access. Time. Every argument that follows has to be read against that. The claim is not that everyone can do what I did tomorrow. The claim is that the pattern is ethically preferable to the old way *if* the access gap closes. And that closing the access gap is one of the more important "AI for good" projects any of us could take on.

---

There is one more admission. The one I least want to write.

Some of my best friends are authors in active litigation against AI companies. I cannot share the details. The cases are ongoing. The filings are not mine to discuss. The people involved are not characters for me to use to make a point. But I will not pretend they aren't there.

Their harm is personal. It is not abstract. These are people I love. Their books — the books we talked about when I came over to hang out with their son, the books that influenced me to join the Rust project and write technical documentation — were used without their consent to train the systems that now compete with them in their own markets.

> What engineers call *pretraining*. What an author calls *my life's work, scraped*. Same act. Two names. Two grief registers.

The company whose model wrote paragraphs of this book alongside me is not, in every respect, on the same side of this fight as my friends are.

I do not know how to reconcile that. I am suspicious of anyone who says they do.

---

What I can say is this. The ethical case this book makes is not a defense of how the training data was acquired. It is a case about what specific *uses* of these systems are better than the alternatives humans were forced to ship before. Two different arguments. They have to stay separate if we are going to think clearly. The author whose book was scraped is owed something. Real money. Real acknowledgment. Real say over future training. That debt does not go away because I describe an address-shortening function that the tool happens to be good at. Both things can be true. The harm to the writers is real. The uses in this book are still, in my judgment, ethically preferable to the old way. I will argue the second at length. I will not pretend the first does not exist.

Here is the pattern the book is about.

An engineer who refused to write the combinatorial hell of an address-shortener — what engineers call a *normalizer*, what an HR clerk calls *a thing that won't break my payroll file* — and instead wrote a generic interface and handed the specification to the person who owned the problem. A hiring manager facing a hundred thousand applications and twelve openings, deciding whether it is more ethical to ghost ninety-nine percent of them or to give every one of them twenty minutes with a machine. A district manager responsible for four hundred people who cannot read four hundred dashboards. A state employee trying to query their own government's data without paying a vendor for a custom report. A billion people in China being offered AI as a utility, like water, like electricity. A Nobel Prize for folding proteins no human could fold by hand in a hundred lifetimes.

Every case is the same shape. The old way required a person to pretend they could brute-force something that cannot be brute-forced. The new way requires a person to write down, in plain language, what they actually want.

Engineers call this *specification*. A manager calls it *knowing what you're asking for*. The tool just collapses the distance between the two.

From writing the rules to writing the intent.

That is the shift. The tool that makes the shift possible is the one that wrote these paragraphs with me. I would be dishonest not to say so. I would be naive to pretend that saying so is enough.

I used Claude Opus 4.7. I read every word. I approve the message. I know it is not enough.

The rest of the book is my attempt to make it enough.
