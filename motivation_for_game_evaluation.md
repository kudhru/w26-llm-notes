# Motivating Your Benchmark Paper: A Narrative Framework

## The Core Story You Need to Tell

Your paper needs to answer one fundamental question a reviewer will ask in the first 30 seconds: **"Why should I care about this game, and why now?"** The seven points below, used together, build a compelling and layered answer to that question.

---

## The Seven-Part Motivation Argument

### Point 1: Establish the Gap — "No One Has Done This Before"

Open with a direct, confident claim of novelty:

> "Despite the rich and growing body of work evaluating LLMs on game environments, **no prior work has benchmarked LLM or AI agent performance on [Game X]**. To the best of our knowledge, this paper is the first systematic evaluation of LLMs on this game."

This is your strongest hook. Use it early — ideally in the abstract and the first paragraph of the introduction. Reviewers respond well to clear, verifiable first-mover claims.

---

### Point 2: Situate Yourself in a Legitimate and Active Research Tradition

Don't let your work look isolated. Anchor it in the broader movement:

> "Benchmarking LLMs and AI agents on games has emerged as a vibrant and well-established research direction. Dedicated benchmarks exist for Chess, Sudoku, Poker, Mafia, and several other games, each of which has produced valuable insights into model capabilities and limitations. This body of work reflects a broad community consensus that **games provide controlled, structured, and reproducible environments** for probing LLM reasoning, strategy, deception, cooperation, and decision-making. Our work contributes a new and previously unexplored game to this growing ecosystem."

This does two things: it validates the research direction itself, and it signals that you are building on solid foundations rather than working in a vacuum.

---

### Point 3: Establish the Game's Cultural and Global Significance

Make the case that the game itself is worth studying:

> "[Game X] is one of the oldest and most widely played games in the world, with a player base spanning dozens of countries and cultures. Its longevity and popularity are not accidental — the game encodes rich strategic, social, and cognitive challenges that have captivated players for generations. **A game that has engaged millions of human minds over centuries is a natural and meaningful testbed for evaluating artificial intelligence.**"

This argument is simple but important. Reviewers are less likely to question the relevance of a game that has demonstrated real-world traction at scale. Ground this with any numbers you can find — estimated player counts, countries played in, cultural presence, and so on.

---

### Point 4: Map Game Behaviors to Real-World Relevance

This is where you do the intellectual heavy lifting. Be specific and deliberate:

> "Beyond its entertainment value, [Game X] operationalizes a set of cognitive and strategic behaviors that are directly relevant to real-world decision-making contexts. Specifically, our benchmark evaluates LLMs on [Behavior 1, e.g., negotiation under incomplete information], [Behavior 2, e.g., risk assessment with asymmetric stakes], and [Behavior 3, e.g., multi-party coalition formation]. These behaviors are not merely academic — they mirror challenges that arise in [real-world domain 1, e.g., automated negotiation systems], [real-world domain 2, e.g., financial decision-making], and [real-world domain 3, e.g., multi-agent coordination]. Understanding how well LLMs handle these behaviors in a controlled game setting has direct implications for how we deploy and trust these models in higher-stakes applications."

Students should fill in this section carefully and specifically for their game. Generic claims weaken the argument. The more precisely you can draw the line from a game mechanic to a real-world scenario, the more compelling this becomes.

---

### Point 5: Acknowledge Overlap with Existing Work — and Reframe It as a Strength

Students often get defensive about this. Flip the framing:

> "We acknowledge that some of the behaviors evaluated in our benchmark — such as [bluffing, strategic deception, cooperative reasoning] — have been studied in prior game benchmarks. However, **having multiple independent benchmarks for evaluating the same behavior is a feature, not a limitation.** In empirical AI research, replication and cross-environment validation are cornerstones of scientific rigor. If our findings on [Behavior X] align with those from [Poker/Mafia/other benchmark], this strengthens the claim that the behavior is a robust and generalizable characteristic of current LLMs. If our findings diverge, this is equally valuable — it reveals that LLM behavior is sensitive to game context and does not transfer uniformly across environments. Either outcome is a meaningful scientific contribution."

This argument directly preempts common reviewer criticisms about incremental work. Use it proactively in your paper rather than waiting to deploy it in a rebuttal.

---

### Point 6: Highlight What Only Your Game Can Offer

End the motivation section on your strongest unique claim:

> "Critically, [Game X] also enables the evaluation of behaviors that have received little or no attention in existing game benchmarks. In particular, [Unique Behavior 1] and [Unique Behavior 2] are mechanics that are either absent from or peripheral to existing benchmarks such as Chess, Poker, and Sudoku. **These dimensions represent a genuine gap in the current LLM evaluation landscape, and this benchmark directly addresses that gap.** To the extent that these behaviors matter for real-world applications — and we argue above that they do — our work adds evaluation coverage that the community currently lacks."

Students should identify at least two or three behaviors or dimensions that are unique to their game and lean into them hard. These are the most defensible claims of novelty and the ones most likely to satisfy a skeptical reviewer.

---

### Point 7: Defend Depth Over Breadth — One Game, Done Rigorously

A common reviewer pushback is: *"Why study just one game? Why not evaluate across a family of games?"* Address this head-on rather than leaving it as a vulnerability:

> "A natural question is whether it would be more valuable to benchmark LLMs across multiple games simultaneously. We argue the opposite: **the scientific value of a benchmark lies in its depth and rigor, not in the number of games it covers.** Evaluating a single game comprehensively — with carefully constructed scenario dimensions, multiple evaluation metrics, multilingual experiments, persona-based analyses, and ablation studies — yields far richer and more actionable insights than a surface-level evaluation spread thinly across many games. This approach is well-precedented in the literature: dedicated benchmark papers for Chess, Poker, and Sudoku have each made lasting contributions precisely because they go deep on a single environment. A shallow multi-game evaluation would force uncomfortable trade-offs: fewer scenarios per game, less systematic dimensional coverage, reduced statistical power, and diminished ability to study game-specific behaviors in the nuanced detail they deserve. Our goal is not to survey the landscape of games broadly, but to establish a rigorous, replicable, and comprehensive benchmark for [Game X] that the community can build on."

This reframe is important: breadth is not inherently better than depth. Make the case clearly that your methodological choice is a deliberate and principled one, not a limitation born of convenience.

---

## Putting It All Together: A Suggested Narrative Flow

When writing the introduction, weave these seven points into a single flowing argument rather than presenting them as a numbered list. A natural order is:

**Broad hook** (games are great testbeds) → **Specific gap** (this game has never been studied) → **Why the game matters** (popular, culturally significant) → **What behaviors it lets us study** (specific and real-world relevant) → **How it fits with existing work** (reinforces and extends) → **What only it can offer** (unique contribution) → **Why depth beats breadth** (one game, done rigorously).

This arc takes the reader from the general to the specific, from motivation to contribution, and from humility to confidence — which is exactly the tone a strong benchmark paper should strike.

---

## Combined Paragraph for Introduction and Related Work Sections

The following paragraph synthesizes all seven points into a single cohesive narrative. Students should adapt it to their specific game, filling in the bracketed placeholders:

> "Games have long served as controlled and reproducible environments for evaluating AI capabilities, and dedicated benchmarks for Chess, Poker, Sudoku, Mafia, and related games have each made lasting contributions to our understanding of LLM reasoning, strategy, and decision-making — reflecting a broad and active community interest in game-based AI evaluation. Despite this rich landscape, **[Game X] has received no attention in the LLM benchmarking literature; to the best of our knowledge, this paper presents the first systematic evaluation of LLMs on this game.** This gap is notable: [Game X] is one of the oldest and most widely played games in the world, with a global player base and centuries of strategic depth, making it a natural and compelling testbed for AI evaluation. The game operationalizes behaviors — including [Behavior 1], [Behavior 2], and [Behavior 3] — that map directly to real-world challenges in [Domain 1], [Domain 2], and [Domain 3], underscoring the practical relevance of this benchmark beyond the game itself. While some of these behaviors have been explored in prior benchmarks, having multiple independent environments for studying the same capability is a scientific strength, not a redundancy: converging findings across games build confidence in generalizability, while diverging findings reveal the context-sensitivity of LLM behavior, and both outcomes advance the field. More importantly, [Game X] uniquely enables the study of [Unique Behavior 1] and [Unique Behavior 2], which existing benchmarks do not capture — representing a genuine and previously unaddressed gap in the evaluation landscape. Finally, rather than pursuing a broad but shallow evaluation across multiple games, this paper deliberately takes a depth-first approach: by investing in comprehensive scenario construction, multi-dimensional analysis, multilingual experiments, and persona-based studies within a single game, we are able to surface nuanced behavioral insights that a multi-game survey could not achieve. This is consistent with the methodological tradition of the benchmark papers that have had the most lasting impact on the field."

---

## A Note on Tone

One common mistake is hedging too much. Phrases like *"we attempt to explore"* or *"we hope this may be useful"* undermine the case you are making. State your contributions directly: *"This paper presents the first benchmark for [Game X],"* *"We identify three behaviors unique to this setting,"* *"Our findings reveal..."* Confidence in your framing, backed by the structured argument above, will serve you well both with reviewers and readers.
