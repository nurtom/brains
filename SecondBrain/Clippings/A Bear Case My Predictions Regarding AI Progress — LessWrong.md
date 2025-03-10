---
title: "A Bear Case: My Predictions Regarding AI Progress — LessWrong"
source: "https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/a-bear-case-my-predictions-regarding-ai-progress"
author:
  - "[[Thane Ruthenis]]"
published: 2025-03-05
created: 2025-03-10
description: "This isn't really a \"timeline\", as such – I don't know the timings – but this is my current, fairly optimistic take on where we're heading. …"
tags:
  - "clippings"
---
## 275

## 275

This isn't really a "timeline", as such – I don't know the timings – but this is my current, fairly optimistic take on where we're heading.

I'm not *fully* committed to this model yet: I'm still on the lookout for more agents and inference-time scaling later this year. But Deep Research, Claude 3.7, Claude Code, Grok 3, and GPT-4.5 have turned out largely in line with these expectations<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fn71wj581psb4" class=""><span>[1]</span></a></span></span></sup>, and this is my current baseline prediction.

---

## The Current Paradigm: I'm Tucking In to Sleep

I expect that none of the currently known avenues of capability advancement are sufficient to get us to AGI<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnznbex4dkqfh" class=""><span>[2]</span></a></span></span></sup>.

- I don't want to say the pretraining will "plateau", as such, I do expect continued progress. But the dimensions along which the progress happens are going to decouple from the intuitive "getting generally smarter" metric, and will face steep diminishing returns.
- Grok 3 and GPT-4.5 seem to confirm this.
- Grok 3's main claim to fame was "pretty good: it managed to dethrone Claude Sonnet 3.5.1 for some people!". That was damning with faint praise.
- GPT-4.5 is subtly better than GPT-4, particularly at writing/EQ. That's likewise a faint-praise damnation: it's not *much* better. Indeed, it reportedly came out below expectations for OpenAI as well, and they certainly weren't in a rush to release it. (It [was intended](https://openai.com/index/openai-board-forms-safety-and-security-committee/) as a new flashy frontier model, not the delayed, half-embarrassed "here it is I guess, hope you'll find something you like here".)
- GPT-5 will be even less of an improvement on GPT-4.5 than GPT-4.5 was on GPT-4. The pattern will continue for GPT-5.5 and GPT-6, [the ~1000x and 10000x models](https://www.lesswrong.com/posts/RDG2dbg6cLNyo6MYT/thane-ruthenis-s-shortform?commentId=DMdFqA4ChTRczRLXs) they may train by 2029 (if they still have the money by then). Subtle quality-of-life improvements and meaningless benchmark jumps, but nothing paradigm-shifting.
- (Not to be a scaling-law denier. I believe in them, I do! But they measure *perplexity*, not general intelligence/real-world usefulness, and Goodhart's Law is no-one's ally.)
- OpenAI seem to expect this, what with them apparently [planning to slap the "GPT-5" label](https://x.com/sama/status/1889755723078443244) on the Frankenstein's monster made out of their current offerings instead of on, well, 100x'd GPT-4. They know they can't cause another hype moment without this kind of trickery.
- Test-time compute/RL on LLMs:
- It will not meaningfully generalize beyond domains with easy verification. Some trickery like RLAIF and longer CoTs might provide *some* benefits, but they would be a fixed-size improvement. It will not cause a hard-takeoff self-improvement loop in "soft" domains.
- RL will be good enough to turn LLMs into reliable tools for some fixed environments/tasks. They will reliably fall flat on their faces if moved outside those environments/tasks.
- Scaling CoTs to e. g. millions of tokens or effective-indefinite-size context windows (if that even works) may or may not lead to math being solved. I expect it won't.
- It may not work at all: the real-world returns on investment may end up linear while the costs of pretraining grow exponentially. I mostly expect FrontierMath to be beaten by EOY 2025 ([it's not that difficult](https://www.lesswrong.com/posts/puv8fRDCH9jx5yhbX/johnswentworth-s-shortform?commentId=tzjmsY827Biwh5TtF)), but maybe it won't be beaten for years.<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnysooye03bqe" class=""><span>[3]</span></a></span></span></sup>
- Even if it "technically" works to speed up conjecture verification, I'm [skeptical](https://www.lesswrong.com/posts/GADJFwHzNZKg2Ndti/have-llms-generated-novel-insights?commentId=LWmLexCxAmaR936MC) on this producing *paradigm shifts* even in "hard" domains. *That* task is not actually an easily verifiable one.
- (If math *is* solved, though, I don't know how to estimate the consequences, and it might invalidate the rest of my predictions.)
- "But the models *feel* increasingly smarter!":
- It seems to me that "vibe checks" for how smart a model feels are easily gameable by making it have a better personality.
- My guess is that it's most of the reason Sonnet 3.5.1 was so beloved. Its personality was made much more *appealing*, compared to e. g. OpenAI's corporate drones.
- [The recent upgrade to GPT-4o](https://www.lesswrong.com/posts/bozSPnkCzXBjDpbHj/ai-104-american-state-capacity-on-the-brink#Huh__Upgrades) seems to confirm this. They seem to have merely given it a better personality, and people were reporting that it "feels much smarter".
- Deep Research was this for me, at first. Some of its summaries were just *pleasant* to read, they felt so information-dense and intelligent! Not like typical AI slop at all! But then it turned out most of it was just AI slop underneath anyway, and now my slop-recognition function has adjusted and the effect is gone.
- What LLMs are good at: eisegesis-friendly problems and in-distribution problems.
- [Eisegesis](https://en.wikipedia.org/wiki/Eisegesis) is "the process of interpreting text in such a way as to introduce one's own presuppositions, agendas or biases". LLMs feel very smart when you do the work of making them sound smart on your own end: when the interpretation of their output has a free parameter which you can mentally set to some value which makes it sensible/useful to you.
- This includes e. g. philosophical babbling or brainstorming. *You* do the work of picking good interpretations/directions to explore, *you* impute the coherent personality to the LLM. And you inject very few bits of steering by doing so, but [those bits are load-bearing](https://www.lesswrong.com/posts/bxt7uCiHam4QXrQAA/cyborgism#Cyborg_cognition). If left to their own devices, LLMs won't pick those obviously correct ideas any more often than chance.
- See R1's CoTs, where it often does... [that](https://x.com/teortaxesTex/status/1887726953509069109?lang=en).
- This also covers [stuff like Deep Research's outputs](https://x.com/sayashk/status/1887275315824660584). They're great specifically as high-level overviews of a field, when you're not relying on them to be *comprehensive* or *precisely on-target* or for *any given detail* to be correct.
- It feels like this issue is easy to fix. LLMs already have ~all of the needed pieces, they just need to learn to recognize good ideas! Very few steering-bits to inject!
- This issue felt easy to fix since GPT-3.5, [or perhaps GPT-2](https://www.lesswrong.com/posts/pv7Qpu8WSge8NRbpB/larger-language-models-may-disappoint-you-or-an-eternally).
- This issue is not easy to fix.
- In-distribution problems:
- One of the core features of the current AIs is the "jagged frontier" of capabilities.
- This jaggedness is often defended by "ha, as if humans don't have domains in which they're laughably bad/as if humans don't have consistent cognitive errors!". I believe that counterargument is invalid.
- LLMs are not good in some domains and bad in others. Rather, they are incredibly good at some *specific tasks* and bad at *other* tasks. Even if both tasks are in the same domain, even if tasks A and B are very similar, even if any human that can do A will be able to do B.
- This is consistent with the constant complaints about LLMs and LLM-based agents being unreliable and their competencies being *impossible to predict* ([example](https://www.answer.ai/posts/2025-01-08-devin.html)).
- That is: It seems the space of LLM competence shouldn't be thought of as some short-description-length connected manifold or slice through the space of problems, whose shape we're simply too ignorant to understand yet. (In which case "LLMs are genuinely intelligent in a way orthogonal to how humans are genuinely intelligent" is valid.)
- Rather, it seems to be *a set of individual points* in the problem-space, plus these points' immediate neighbourhoods... Which is to say, the set of problems the solutions to which are present in their training data.<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnnfivgw93jpp" class=""><span>[4]</span></a></span></span></sup>
- The impression that they generalize outside it is based on us [having a very poor grasp](https://www.lesswrong.com/posts/RDG2dbg6cLNyo6MYT/thane-ruthenis-s-shortform?commentId=vxHcdFb3KLWEQbmRv) regarding the solutions to what problems are present in their training data.
- And yes, there's *some* generalization. But it's dramatically less than the impressions people have of it.
- Agency:
- Genuine agency, by contrast, requires remaining on-target across *long inferential distances*: even after your task's representation becomes very complex in terms of the templates which you had memorized at the start.
- LLMs still seem as terrible at this as they'd been in the GPT-3.5 age. Software agents break down once the codebase becomes complex enough, game-playing agents get stuck in loops out of which they break out only by accident, etc.
- They just have bigger sets of templates now, which lets them fool people for longer and makes them useful for marginally more tasks. But the scaling on that seems pretty bad, and this certainly won't suffice for autonomously crossing the *astronomical* inferential distances required to usher in the Singularity.
- "But the benchmarks!"
- I dunno, I think they're just not measuring what people think they're measuring. See the point about in-distribution problems above, plus the possibility of undetected [performance-gaming](https://x.com/miru_why/status/1892500715857473777), plus some [subtly but crucially unintentionally-misleading reporting](https://x.com/colin_fraser/status/1892721051299172641).
- Case study: Prior to looking at [METR's benchmark](https://metr.org/blog/2024-11-22-evaluating-r-d-capabilities-of-llms/), I'd expected that it's also (unintentionally!) doing some shenanigans that mean it's not actually measuring LLMs' real-world problem-solving skills. Maybe the problems were secretly in the training data, or there was a selection effect towards simplicity, or the prompts strongly hinted at what the models are supposed to do, or the environment was set up in an unrealistically "clean" way that minimizes room for error and makes solving the problem correctly the path of least resistance (in contrast to messy real-world realities), et cetera.

As it turned out, yes, it's that last one: see the "systematic differences from the real world" [here](https://metr.org/blog/2024-11-22-evaluating-r-d-capabilities-of-llms/). Consider what this means in the light of the previous discussion about inferential distances/complexity-from-messiness.

As I'd said, I'm not 100% sure of that model. Further advancements might surprise me, there's an explicit carve-out for ??? consequences if math is solved, etc.

But the above is my baseline prediction, at this point, and I expect the probability mass on other models to evaporate by this year's end.

---

## Real-World Predictions

- I dare not make the prediction that the LLM bubble will burst in 2025, or 2026, or in any given year in the near future. The AGI labs have a lot of money nowadays, they're managed by smart people, they have some real products, they're willing to produce propaganda, and they're buying their own propaganda (therefore it will appear authentic). They can keep the hype up for a very long time, if they want.
- And they do want to. They *need* it, so as to keep the investments going. Oceans of compute is the only way to collect on the LLM bet they've made, in the worlds where that bet can pay off, so they will keep maximizing for investment no matter how dubious the bet's odds start looking.
- Because what *else* are they to do? If they admit to themselves they're *not* closing their fingers around godhood after all, what will they have left?
- There will be news of various important-looking breakthroughs and advancements, at a glance looking very solid even to us/experts. Digging deeper, or waiting until the practical consequences of these breakthroughs materialize, will reveal that they're 80% hot air/hype-generation.<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnvl37irxzr4a" class=""><span>[5]</span></a></span></span></sup>
- At some point there might be massive layoffs due to ostensibly competent AI labor coming onto the scene, perhaps because OpenAI will start heavily propagandizing that these mass layoffs must happen. It will be an overreaction/mistake. The companies that act on that will crash and burn, and will be outcompeted by companies that didn't do the stupid.
- Inasmuch as LLMs boost productivity, it will mostly be as tools. There's a subtle but crucial difference between "junior dev = an AI model" and "senior dev + AI models = senior dev + team of junior devs". Both decrease the demand for junior devs (as they exist today, before they re-specialize into LLM whisperers or whatever). But the latter doesn't really require LLMs to be capable of end-to-end autonomous task execution, which is the property required for actual transformative consequences.
- (And even then, all the rumors about LLMs 10x'ing programmer productivity [seem greatly overstated](https://www.lesswrong.com/posts/tqmQTezvXGFmfSe7f/how-much-are-llms-actually-boosting-real-world-programmer).)
- Inasmuch as human-worker replacements will come, they will be surprisingly limited in scope. I dare not make a prediction regarding the exact scope and nature, only regarding the *directionality* compared to current expectations.
- There will be a ton of innovative applications of Deep Learning, perhaps chiefly in the field of biotech, see [GPT-4b](https://www.technologyreview.com/2025/01/17/1110086/openai-has-created-an-ai-model-for-longevity-science/) and [Evo 2](https://x.com/IterIntellectus/status/1892251343881937090). Those are, I must stress, *human-made innovative applications of the paradigm of automated continuous program search.* Not AI models autonomously producing innovations.
- There will be various disparate reports about AI models autonomously producing innovations, in the vein of [this](https://x.com/SakanaAILabs/status/1892385766510338559) or [that](https://www.biorxiv.org/content/10.1101/2025.02.19.639094v1) or [that](https://arxiv.org/abs/2502.13025). They will turn out to be misleading or cherry-picked. E. g., examining those examples:
- In the first case, most of the improvements [turned out to be reward-hacking](https://x.com/miru_why/status/1892500715857473777) (and not even intentional on the models' part).
- [In the second case](https://x.com/jimnasyum/status/1892757709461533062), the scientists have pre-selected the problem on which the LLM is supposed to produce the innovation on the basis of already knowing that there's a low-hanging fruit to be picked there. That's like 90% of the work. And then they *further* picked the correct hypothesis from the set it generated, i. e., did eisegesis. And *also* there might be [any amount of data contamination](https://www.lesswrong.com/posts/GADJFwHzNZKg2Ndti/have-llms-generated-novel-insights?commentId=YhbWT4JaXK3EHbcQK) from these scientists or different groups speaking about their research in public, in the years they spent working on it.
- In the third case, the AI produces useless slop with steps like "..., Step N: invent the Theory of Everything (left as an exercise for the reader), ...", lacking [the recognition function](https://colah.github.io/notes/taste/) for promising research. GPT-3-level stuff. (The whole setup can also likely be out-performed by taking the adjacency matrix of Wikipedia pages and randomly sampling paths from the corresponding graph, or [something like this](https://dl.acm.org/doi/10.1145/2623330.2623623).)
- I expect that by 2030s, LLMs will be heavily integrated into the economy and software, and will serve as very useful tools that found their niches. But just that: tools. Perhaps some narrow jobs will be greatly transformed or annihilated (by being folded into the job of an LLM nanny). But there will not be AGI or broad-scope agents arising from the current paradigm, nor autonomous 10x engineers.
- At some unknown point – probably in 2030s, possibly tomorrow (but likely not tomorrow) – someone will figure out a different approach to AI. Maybe a slight tweak to the LLM architecture, maybe a completely novel neurosymbolic approach. Maybe it will happen in a major AGI lab, maybe in some new startup. By default, everyone will die in <1 year after that.

---

## Closing Thoughts

This might seem like a ton of annoying nitpicking. Here's a simple generator of all of the above observations: **some people desperately,** ***desperately*** **want LLMs to be a bigger deal than what they are**.

They are not evaluating the empirical evidence in front of their eyes with proper precision*.*<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnlph4528t2" class=""><span>[6]</span></a></span></span></sup> Instead, they're vibing, and spending 24/7 inventing contrived ways to fool themselves and/or others.

They often succeed. They will continue doing this for a long time to come.

We, on the other hand, desperately *not* want LLMs to be AGI-complete. Since we try to avoid motivated thinking, to avoid deluding ourselves into believing into happier realities, we err on the side of pessimistic interpretations. In this hostile epistemic environment, that effectively leads to us being *overly gullible* and *prone to buying into hype*.

Indeed, this environment is essentially optimized for exploiting [the virtue of lightness](https://www.lesswrong.com/posts/7ZqGiPHTpiDMwqMN2/twelve-virtues-of-rationality). LLMs are masters at creating the *vibe* of being generally intelligent. Tons of people are cooperating, playing this vibe up, making tons of subtly-yet-crucially flawed demonstrations. Trying to see through this immense storm of bullshit very much *feels* like "fighting a rearguard retreat against the evidence".<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnc0fnmg1rwsj" class=""><span>[7]</span></a></span></span></sup>

But this isn't what's happening, in my opinion. On the contrary: it's the LLM believers who are sailing against the winds of evidence.

If LLMs were *actually* as powerful as they're hyped up to be, there wouldn't be the need for all of these attempts at *handholding*.

Ever more contrived agency scaffolds that yield ~no improvement. Increasingly more costly RL training procedures that fail to generalize. Hail-mary ideas regarding how to fix that generalization issue. Galaxy-brained ways to elicit knowledge out of LLMs that produce nothing of value. The need for all of this is strong evidence that *there's no seed of true autonomy/agency/generality within LLMs*. If there were, the most naïve AutoGPT setup circa early 2023 would've elicited it.

People are extending LLMs a hand, hoping to pull them up to our level. But there's nothing reaching back.

And none of the current incremental-scaling approaches will fix the issue. They will increasingly mask it, and some of this masking may be powerful enough to have real-world consequences. But any attempts at the Singularity based on LLMs will stumble well before takeoff.

Thus, I expect AGI Labs' AGI timelines have ~nothing to do with what will actually happen. On average, we likely have more time than the AGI labs say. Pretty likely that we have until 2030, maybe well into 2030s.

By default, we likely don't have *much* longer than that. Incremental scaling of known LLM-based stuff won't get us there, but I don't think the remaining qualitative insights are many. 5-15 years, at a rough guess.

1. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnref71wj581psb4"><span>^</span></a></span></strong></sup>

For prudency's sake: GPT-4.5 has slightly overshot these expectations.
2. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnrefznbex4dkqfh"><span>^</span></a></span></strong></sup>

If you are really insistent on calling the current crop of SOTA models "AGI", replace this with "autonomous AI" or "transformative AI" or "innovative AI" or "the transcendental trajectory" or something.
3. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnrefysooye03bqe"><span>^</span></a></span></strong></sup>

Will o4 really come out [on schedule](https://x.com/_jasonwei/status/1870184982007644614) in ~2 weeks, showcasing yet another dramatic jump in mathematical capabilities, just in time to rescue OpenAI from the GPT-4.5 semi-flop? I'll be waiting.
4. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnrefnfivgw93jpp"><span>^</span></a></span></strong></sup>
5. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnrefvl37irxzr4a"><span>^</span></a></span></strong></sup>

Pretty sure Deep Research could not in fact ["do a single-digit percentage of all economically valuable tasks in the world"](https://x.com/sama/status/1886220904088162729), except in the caveat-laden sense where you still have a human expert double-checking and rewriting its outputs. And in my personal experience, on the topics at which I *am* an expert, it would be easier to write the report from scratch than to rewrite DR's output.

It's a useful way to get a high-level overview of some topics, yes. It blows Google out of the water at being Google, and then some. But I don't think it's a 1-to-1 replacement for any extant form of human labor. Rather, it's a useful zero-to-one thing.
6. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnreflph4528t2"><span>^</span></a></span></strong></sup>
7. <sup><strong><span><a href="https://www.lesswrong.com/posts/oKAFFvaouKKEhbBPm/#fnrefc0fnmg1rwsj"><span>^</span></a></span></strong></sup>

Indeed, even now, having written all of this, I have nagging doubts that this might be what I'm actually doing here. I will probably keep having those doubts until this whole thing ends, one way or another. It's not pleasant.