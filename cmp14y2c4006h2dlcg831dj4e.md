---
title: "When AI Runs the Tests, What Is the Quality Engineer For?"
seoTitle: "When AI runs the test what is the quality engineer for"
seoDescription: "If AI is going to execute most of what quality engineering used to execute, what does the QE space actually look like on the other side of that shift?"
datePublished: 2026-05-11T11:45:42.486Z
cuid: cmp14y2c4006h2dlcg831dj4e
slug: when-ai-runs-the-tests-what-is-the-quality-engineer-for
cover: https://cdn.hashnode.com/uploads/covers/69c55e5f10e664c5daf8a077/1f635dd8-58fd-4876-8b4b-8124aaee1509.jpg
tags: ai, quality-assurance, quality-engineering

---

The question that started this, and has been quietly bothering me for months, is simple. If AI is going to execute most of what quality engineering used to execute, and the engineer's job is going to be judgment, what does the QE space actually look like on the other side of that shift?

The honest answer is that nobody knows yet, but the shape of the answer is becoming visible, and it is more interesting than the current discourse suggests. Most of what gets written about AI and testing right now is essentially a story about automation: faster test generation, better self-healing, smarter triage, with roughly the same function doing roughly the same work at higher throughput. I think that story is wrong, or at least shallow. The deeper change is not that the function speeds up. It is that the function gets rebuilt around the part of the work that the tools never optimised for in the first place.

It is worth being precise about what the tools were optimised for, because the standard version of this argument tends to claim that "test artefacts were scarce" and that AI now makes them cheap. That is not quite right. Test artefacts have not been scarce for years.

![](https://cdn.hashnode.com/uploads/covers/69c55e5f10e664c5daf8a077/5e9966a0-0ba3-4d67-9640-b1f76676ffcd.png align="center")

Large organisations routinely sit on suites with tens of thousands of tests, often more than they can run, often more than they should have written. What has been scarce, and what every major tool quietly optimised for, is human labour around those artefacts. Writing them, maintaining them, running cycles, investigating failures, triaging flake. From Selenium and TestRail through to the modern AI test generators, the whole stack has been built on the same implicit theory: that the rate-limit on quality is the engineer's hours spent on artefact work.

AI compresses that labour to something close to zero. What it exposes, by stripping out the noise, is that the labour was never really the rate-limiting. The actual rate limit on quality has always been judgment, and the labour was just the visible part of the work, the part you could put on a sprint board. The judgment was happening underneath, in the heads of senior engineers, in informal hallway conversations, in the daily decisions about what to test and what to leave alone. It was real work, but it was invisible work, and most QE organisations have never been structured to value it, develop it, or pay for it explicitly.

That is the shift worth paying attention to. Not "execution gets faster", and not "tests become cheap". It is that the work which was always doing the real lifting becomes the visible work, and the function has to reorganise around it. Three things follow, and most of the discipline has barely begun to sit with them.

![](https://cdn.hashnode.com/uploads/covers/69c55e5f10e664c5daf8a077/afa7ee44-b447-41d7-80c9-62e434539fe6.png align="center")

## **1 - Risk articulation has to become an explicit craft**

When labour around test artefacts is what rate-limits you, prioritisation happens by default. You write the tests you have time for, which tend to be the obvious ones, and the act of writing them serves as a rough proxy for declaring that they matter. The proxy was always crude, but it worked because the labour was real and finite.

When AI generates and runs everything, that proxy disappears. You can no longer let "what got tested" stand in for "what matters". You have to say, in writing, which failure modes are actually consequential, at what cost, with what blast radius, and whose problem they become when they hit. Most organisations are not set up for this. They have severity scales and escalation flowcharts, but those are categorisation tools, not risk models. A senior engineer who has lived through a release-day outage knows things about where the system actually breaks that no dashboard captures, and that knowledge is going to become more valuable, not less, because no tool can generate it on its own. A 50ms regression on a hot path is a different category of risk from a UI bug, and nothing in the AI stack will make that distinction unless someone has put the risk model in writing first.

## **2 - Correctness has to become a first-class artefact**

The thing that has actually been scarce in QE, and underinvested in for the last twenty years, is a clear definition of what good looks like for a given system. Schemas, contracts, invariants, service-level objectives, policies-as-code, evals with rubrics. These have always existed at the edges of the work, usually as informal side documents, often as tribal knowledge in the heads of two or three senior people who happened to be in the room when a decision got made. They are not tests, they are specifications of correctness, and historically the discipline has smuggled them into the system through assertions and setup scripts rather than treating them as the central artefact.

Once AI is the thing doing the executing, the implicit version stops working. The AI needs something concrete to execute against, and "behave correctly" is not a specification it can act on. The teams that get ahead over the next few years will be the ones that treat their correctness definitions as their most important intellectual asset, more important than the test suite itself. Tests can be regenerated against a clear specification, but a clear specification cannot be reverse-engineered out of a million regenerated tests. It is closer to the difference between owning a recipe and owning a freezer full of pre-made meals.

## **3 - Governing the AI itself becomes part of the job**

This is the implication most teams have not yet internalised. The moment AI is generating your tests, producing your synthetic data, and triaging your failures, it stops being a tool you use and becomes a component in your quality system. It deserves the same scrutiny you would apply to any other piece of production infrastructure, which means evals on the quality of its outputs, drift detection on its triage decisions, audit trails so a reviewer can trace how a release decision was reached, and red-teaming the parts of the pipeline that can actually move production.

This is genuinely new work, and it maps cleanly onto the responsible-AI and evaluation discipline that has been building up across the industry over the last two years. In regulated environments, it is not optional. If an AI agent contributed to a release sign-off, somebody will eventually need to answer for how that agent was qualified, what its known failure modes are, and who is accountable when it gets something wrong. That answer has to live somewhere, and the function best positioned to own it is QE.

## **Where I would push back on my own framing**

Two honest caveats before this gets too neat. The first is that the displacement is easy to overstate, because AI execution is still aspirational across most of the stack. Today's models are reliable at generating unit tests, passable at maintaining UI tests, weak at designing meaningful integration tests, and genuinely poor at exploratory testing in unfamiliar domains. For the next two to three years, the role is going to stay hybrid, still doing the execution work in the parts of the stack that resist automation while learning to govern and judge in the parts that are getting easier. The clean reframing is the destination, not the current state, and tooling has to support both modes at once.

The second caveat is that "judgment" is doing a lot of rhetorical work in the framing. Some of what we currently call judgment is just pattern recognition, and AI will absorb most of it eventually. Recognising a flaky test, spotting an obvious regression, and classifying a triage signal, all of that will commoditise. The judgment that compounds with experience and does not get cheaper is the strategic kind, knowing what the product is actually for, what a failure would mean for the business, what reviewers or regulators genuinely care about as opposed to what they happened to write down. That is the part worth investing in deliberately, and it is also the part that nobody is currently being trained for.

## **The senior QE role bifurcates**

The practical consequence of all this is that the senior QE role splits into two paths over the next few years, and people will end up on one or the other, whether they planned it or not.

One path stays close to execution. Deeply tool-fluent, comfortable inside AI test generation systems, owns the pipeline, and in practice becomes an SRE for test infrastructure. The work is portable and in demand, and it increasingly competes for the same talent and compensation bands as platform engineering. The other path moves toward something that looks more like a principal engineer or a quality architect, defining correctness, owning risk models, governing AI use, and interfacing with reviewers and product leadership. It is harder to measure in throughput metrics, far more leveraged in outcome, and considerably harder to hire from outside the organisation, because the relevant experience accumulates slowly inside companies rather than showing up on a CV.

![](https://cdn.hashnode.com/uploads/covers/69c55e5f10e664c5daf8a077/6ce3a0bb-9fd3-4d66-818a-fd8ede837bcc.png align="center")

The interesting question is whether the industry will build titles and career ladders for the second path quickly enough, or whether the people doing that work will keep being called "senior QE" while the actual substance of the role changes underneath them. My guess is the latter for a while, until a handful of high-profile organisations put a clearer label on it and everyone else follows. Quality architect, AI assurance lead, principal QE, something in that family.

## **The question I keep coming back to**

Of the three (risk articulation, correctness as artefact, governing AI), which is the hardest to build real organisational muscle for?

My instinct is correctness, and not because the others are simple. Risk articulation can be carried by a strong individual who has been around long enough to see how systems actually break, and governing AI can be set up as a programme with the right hires and the right budget. Correctness, by contrast, demands a cross-functional conversation that most organisations have spent years avoiding, where engineering, product, compliance, and operations all have to agree, in writing, on what good means in a way that survives an external review. The team that learns to hold that conversation well will compound an advantage that is genuinely hard to copy, because the advantage is mostly the muscle of having held the conversation in the first place.

Curious which one you would bet on.