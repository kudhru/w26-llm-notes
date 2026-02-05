# Guidelines for Projects involving Evaluation/Benchmarking of LLM and AI Agents for Different Games

## Overview

This document provides comprehensive guidelines for students undertaking projects that evaluate and benchmark Large Language Models (LLMs) and AI agents across different game environments. Following these guidelines will help ensure your work meets the standards required for publication at reputable conferences.

The key principle is to present your work as a **benchmark paper**—similar to established benchmarks for poker, chess, and sudoku—rather than simply reporting that you tested some models on a game.

---

## 1. Dataset Creation

### 1.1 What Constitutes a Dataset in This Context

A dataset for game benchmarking consists of:

- A **comprehensive list of scenarios or situations** in which the LLM or AI agent must make decisions
- **Corresponding evaluation criteria** for each scenario to assess decision quality (good, bad, optimal, suboptimal, etc.)

### 1.2 Determining Dataset Size

Different benchmark papers present varying dataset sizes:

| Scale | Sample Size |
|-------|-------------|
| Small | 250–500 samples |
| Medium | 1,000–5,000 samples |
| Large | 10,000–20,000 samples |
| Very Large | 50,000+ samples |

Your target size depends on available resources including time, energy, and API credits. However, generating large datasets is achievable through systematic dimension variation.

### 1.3 Generating Scenarios Through Dimensional Analysis

Identify all **dimensions or attributes** (knobs) in your game environment and systematically vary them.

> **⚠️ Important Note for Students:**
> 
> The dimensions listed below are **illustrative examples only**. The actual dimensions will vary significantly from game to game depending on the specific game mechanics, rules, and environment. The high-level idea is simple: identify the different knobs in your game environment that you can systematically vary to generate a large number of scenarios.
> 
> **If you have any doubts about identifying the right dimensions for your specific game, please discuss with the instructor before proceeding.**

**Example Dimensions (for illustration purposes):**

1. **Number of players** (1, 2, 3, 4, 5, ...)
2. **Game state complexity** (early game, mid game, late game)
3. **Resource availability** (low, medium, high)
4. **Information visibility** (full information, partial information, hidden information)
5. **Player positions/roles** (first mover, last mover, specific roles)
6. **Difficulty level** (easy, medium, hard, expert)

**Calculating Scenario Count:**

If you have 6 dimensions with 5 possible values each:
```
5^6 = 15,625 possible scenarios
```

This combinatorial approach easily generates thousands or lakhs of scenarios.

### 1.4 Scenario Documentation Requirements

For each scenario, document:

- Initial game state
- Available actions/decisions
- Context and constraints
- Expected optimal action(s)
- Evaluation rubric

---

## 2. Game Simulator Development

### 2.1 Core Requirements

Build a simulator that can:

- **Simulate the game end-to-end** from beginning to termination
- **Handle multiple turns** throughout the game
- **Support multiplayer interactions** (multiple LLM agents playing against each other)
- **Support single-player mode** where applicable
- **Prompt the LLM/AI agent** at each decision point
- **Record all actions and game states** for analysis

### 2.2 Simulator Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Game Simulator                        │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐  │
│  │ Game State  │───▶│   Prompt    │───▶│  LLM/Agent  │  │
│  │  Manager    │    │  Generator  │    │  Interface  │  │
│  └─────────────┘    └─────────────┘    └─────────────┘  │
│         │                                     │          │
│         │          ┌─────────────┐            │          │
│         └──────────│   Action    │◀───────────┘          │
│                    │  Validator  │                       │
│                    └─────────────┘                       │
│                           │                              │
│                    ┌─────────────┐                       │
│                    │   Logger/   │                       │
│                    │  Recorder   │                       │
│                    └─────────────┘                       │
└─────────────────────────────────────────────────────────┘
```

### 2.3 Key Components

1. **Game State Manager**: Tracks current state, enforces rules, determines valid moves
2. **Prompt Generator**: Converts game state into appropriate prompts for LLMs
3. **LLM/Agent Interface**: Handles API calls to different models
4. **Action Validator**: Ensures LLM responses are valid game actions
5. **Logger/Recorder**: Records all decisions, states, and outcomes for analysis

---

## 3. Evaluation Metrics

### 3.1 Two-Level Evaluation Framework

You need **two distinct sets of metrics**:

#### Level 1: Single-Turn Decision Evaluation

Metrics for evaluating individual decisions within scenarios:

| Metric | Description |
|--------|-------------|
| **Decision Accuracy** | Did the LLM make the optimal/correct decision? |
| **Decision Quality Score** | Graded quality (e.g., 1-5 scale) |
| **Response Validity** | Was the response a valid game action? |
| **Reasoning Quality** | Quality of explanation/justification provided |
| **Response Time** | Latency of decision-making |
| **Consistency** | Same decision when presented same scenario multiple times |

#### Level 2: End-to-End Game Performance

Metrics for evaluating overall game-playing ability:

| Metric | Description |
|--------|-------------|
| **Win Rate** | Percentage of games won |
| **Average Score/Points** | Mean performance across games |
| **Survival Rate** | How long the agent stays in the game |
| **Strategic Depth** | Evidence of long-term planning |
| **Adaptability** | Performance against different opponents |
| **Error Recovery** | Ability to recover from suboptimal positions |

### 3.2 Game-Specific Behavioral Metrics

Depending on your game, include metrics for specific behaviors:

- **Bluffing Tendency/Quality**: How often and how effectively the agent bluffs
- **Cooperation vs. Defection Rate**: In games with cooperative elements
- **Risk-Taking Behavior**: Conservative vs. aggressive play styles
- **Cheating Tendency**: Attempts to make invalid moves or exploit rules
- **Deception Detection**: Ability to identify when opponents are bluffing

> **📝 Critical Note on Developing Novel Metrics:**
> 
> The metrics listed above are merely examples. As a student, you should invest **conscious and deliberate effort** in developing **novel metric names and definitions** that are specific to your game.
> 
> **Why is this important?**
> 
> 1. **Justification for Novelty**: When reviewers evaluate your paper, one key question will be: "What new behaviors or dimensions are you evaluating that haven't been explored before?" Having well-defined, novel metrics unique to your game helps answer this question convincingly.
> 
> 2. **Contribution to the Field**: A good benchmark paper doesn't just apply existing metrics—it introduces new ways of measuring LLM behavior that are relevant to the specific game context.
> 
> 3. **Differentiation from Existing Work**: If you only use generic metrics that have been used in poker, chess, or sudoku benchmarks, reviewers may question the need for your benchmark.
> 
> **Action Required**: Brainstorm and document at least 3-5 game-specific metrics that capture unique behavioral aspects of your game. Give them clear, descriptive names and provide formal definitions for each.

---

## 4. Model Selection and Evaluation Strategy

### 4.1 Recommended Model Categories

Given budget constraints, structure your evaluation in **two phases**:

#### Phase 1: Initial Submission (Open-Source Models Only)

Use open-source and locally-runnable models for your initial experiments and first submission:

**Large Open-Source Models (2-3 models):**
- DeepSeek-V2/V3
- Qwen-72B or larger variants

**Small/Medium Open-Source Models (3-4 models):**
- DeepSeek-7B/8B
- Qwen-7B/14B
- Llama-3-8B/70B
- Mistral-7B/Mixtral

#### Phase 2: Post-Review (Closed-Source Models)

> **⚠️ Important Budget Strategy:**
> 
> **Do NOT spend any credits or resources on closed-source model evaluation initially.** Evaluating models like GPT-4, Claude, and Gemini is very costly, and we cannot afford to spend these resources on every project.
> 
> **The closed-source evaluation will only be conducted after the first round of conference reviews.** Once you submit to a conference and receive reviewer feedback, we will be able to judge:
> - Whether the project has potential for acceptance
> - Whether investing additional resources is worthwhile
> - What specific experiments reviewers are asking for
> 
> Based on the reviews, we will selectively allocate API credits for closed-source model evaluation on promising projects.

**Closed-Source Models (to be evaluated post-review, 1-2 models):**
- OpenAI GPT-4/GPT-4o
- Anthropic Claude
- Google Gemini

### 4.2 Budget Allocation Strategy

```
Phase 1 (Initial Submission):
└── 100%: Open-source model inference

Phase 2 (Post-Review, if approved):
├── Additional budget allocated based on reviewer feedback
└── Focused closed-source experiments on specific scenarios
```

### 4.3 Evaluation Protocol

**For Initial Submission:**
1. Run all open-source models on the **complete scenario dataset**
2. Conduct **head-to-head games** between different open-source models
3. Run multiple trials to ensure **statistical significance**

**For Post-Review Revision (if applicable):**
4. Select a **stratified sample** (covering all dimensions) for closed-source models
5. Address specific reviewer concerns with targeted experiments

---

## 5. Real-Life Relevance and Transferability

### 5.1 Mandatory Discussion Section

Your paper must include a dedicated section discussing:

- **Real-world applications** of the behaviors observed
- **Transferability** of findings to practical scenarios
- **Implications** for AI deployment in similar decision-making contexts

### 5.2 Connecting Game Behaviors to Real-World Traits

> **Note:** The table below is a **suggestive list for illustration purposes only**. The actual mapping between game behaviors and real-world relevance will be highly specific to your game and will vary significantly from game to game. You should develop your own mapping based on the unique mechanics and behaviors present in your chosen game.

| Game Behavior | Real-World Relevance |
|---------------|---------------------|
| Bluffing/Deception | Negotiation, sales, diplomacy |
| Risk Assessment | Financial decisions, medical diagnosis |
| Cooperation | Team coordination, multi-agent systems |
| Strategic Planning | Business strategy, resource allocation |
| Adversarial Reasoning | Security, fraud detection |
| Information Asymmetry Handling | Market dynamics, intelligence analysis |

### 5.3 Example Framing

> "The negotiation patterns observed in [Game X] directly mirror real-world business negotiations where parties have asymmetric information. Our finding that Model Y consistently overestimates opponent cooperation suggests potential risks when deploying such models in automated negotiation systems."

---

## 6. Multilingual Exploration

### 6.1 Language Variation Experiments

Conduct experiments varying the language of interaction. **For our projects, we will focus primarily on Indic languages** to explore how LLM performance varies across languages commonly spoken in India.

**Experiment Types:**

1. **Single-Language Games**: Same game played entirely in different languages

   **Priority Languages (Indic Focus):**
   - English (baseline)
   - Hindi
   - Bengali
   - Telugu
   - Tamil
   - Marathi
   - Punjabi
   - Bhojpuri
   - Marwari
   - Other regional Indic languages as relevant

2. **Mixed-Language Games**: Players communicate in different Indic languages within the same game (e.g., one player in Hindi, another in Tamil)

3. **Code-Switching Scenarios**: Players switch between languages mid-game (common in Indian multilingual contexts, e.g., Hindi-English code-mixing)

> **Why Indic Languages?**
> 
> - Most existing LLM benchmarks focus on English or major European/Asian languages
> - Indic languages are underrepresented in LLM evaluation research
> - India's multilingual context provides a rich testbed for cross-lingual LLM behavior
> - This focus can be a unique contribution differentiating your benchmark from existing work

### 6.2 Metrics for Multilingual Analysis

- Performance delta across languages
- Consistency of strategy across languages
- Language-specific behavioral patterns
- Impact of language on cooperation/competition dynamics

### 6.3 Documentation Requirements

For each language tested, document:
- Translation/localization methodology
- Native speaker validation (if applicable)
- Language-specific prompt adaptations

---

## 7. Persona-Based Experiments

### 7.1 Assigning Personas to Players

For games with distinct roles, assign personas to examine behavioral variations:

**Persona Dimensions:**

| Dimension | Example Values |
|-----------|----------------|
| **Personality Traits** | Cunning, humble, aggressive, cautious, friendly |
| **Demographic Attributes** | Age, profession, background |
| **Cultural Background** | Different nationalities, cultural contexts |
| **Expertise Level** | Novice, intermediate, expert |
| **Moral Alignment** | Ethical, neutral, unethical |

### 7.2 Example: Thief-Sheriff Game

```
Thief Personas:
├── Cunning Thief: "You are a clever, strategic thief who plans carefully"
├── Aggressive Thief: "You are bold and take risks without hesitation"
├── Humble Thief: "You are cautious and avoid confrontation"
└── Desperate Thief: "You are in dire circumstances and must succeed"

Sheriff Personas:
├── Strict Sheriff: "You follow the law precisely with no exceptions"
├── Corrupt Sheriff: "You can be persuaded to look the other way"
└── Compassionate Sheriff: "You consider circumstances before judgment"
```

### 7.3 Analysis Framework

- Compare performance across personas
- Identify persona-behavior correlations
- Detect potential biases in model responses to demographic personas
- Document stereotype reinforcement or avoidance

---

## 8. Justification and Positioning

### 8.1 Understanding the Review Process

> **Context for Students:**
> 
> When you submit a paper to a conference, it goes through a peer review process where 3-5 expert reviewers critically evaluate your work. Reviewers are often looking for reasons to reject papers (acceptance rates at top venues are typically 15-25%), so you must anticipate their criticisms and address them proactively in your paper.
> 
> **Common reviewer mindsets:**
> - "Why should I care about this work?"
> - "What's novel here that hasn't been done before?"
> - "Is this contribution significant enough?"
> - "Are the experiments comprehensive and convincing?"
> 
> Below, we outline common criticisms you may face and how to counter them effectively.

### 8.2 Anticipating and Countering Reviewer Criticisms

#### Criticism 1: "You only explored one game—why does this matter?"

**Why reviewers raise this:** They question whether findings from a single game are generalizable or significant enough for publication.

**Counter-arguments to include in your paper:**

1. **Established Precedent**: Point out that poker, chess, and sudoku each have dedicated benchmark papers accepted at top venues. Each game provides unique insights, justifying focused study.

2. **Depth Over Breadth**: Argue that thorough evaluation on one game provides deeper insights than shallow evaluation across many games. A benchmark's value lies in its comprehensiveness, not the number of games.

3. **Unique Behavioral Aspects**: Clearly articulate what behaviors your game allows you to study that existing game benchmarks cannot (see Section 8.3).

4. **Real-World Relevance**: Explain the specific real-world scenarios your game maps to (see Section 5).

#### Criticism 2: "This is incremental—similar benchmarks already exist"

**Why reviewers raise this:** They see your work as merely replicating existing benchmarks with a different game.

**Counter-arguments:**

1. **Novel Dimensions**: Highlight the specific behavioral dimensions you evaluate that are NOT present in existing benchmarks (create a comparison table).

2. **Different Findings**: If your results differ from existing benchmarks, emphasize this: "Our findings show that models behave differently in [your game] compared to [existing benchmark], demonstrating that LLM behaviors do not generalize across game types."

3. **Reinforcing Findings**: If your results align with existing work, frame it as: "Our findings reinforce and validate observations from [existing benchmark], providing additional evidence for [behavior X] as a fundamental characteristic of current LLMs."

#### Criticism 3: "The dataset/evaluation is too small or limited"

**Why reviewers raise this:** They question the statistical validity or comprehensiveness of your experiments.

**Counter-arguments:**

1. **Dimensional Coverage**: Explain your systematic approach to scenario generation (Section 1.3) and show that you cover all relevant dimensions.

2. **Statistical Significance**: Report confidence intervals, run multiple trials, and conduct appropriate statistical tests.

3. **Resource Constraints Acknowledgment**: Acknowledge limitations honestly while arguing that your dataset size is comparable to accepted benchmark papers.

#### Criticism 4: "You didn't evaluate on GPT-4/Claude/other SOTA models"

**Why reviewers raise this:** They want to see how state-of-the-art closed-source models perform.

**Counter-arguments (for initial submission):**

1. **Resource Constraints**: Honestly state that comprehensive closed-source evaluation was beyond the project's budget.

2. **Open-Source Focus**: Argue that evaluating open-source models is valuable for reproducibility and for the research community that cannot afford closed-source APIs.

3. **Future Work**: Indicate that closed-source evaluation is planned for the camera-ready version if the paper is accepted.

#### Criticism 5: "What's the practical impact of this work?"

**Why reviewers raise this:** They want to understand real-world applications.

**Counter-arguments:**

1. **Real-World Mapping**: Provide concrete examples of how game behaviors map to real-world scenarios (Section 5).

2. **Deployment Implications**: Discuss what your findings mean for deploying LLMs in related real-world tasks.

3. **Safety Considerations**: If applicable, highlight safety-relevant findings (e.g., deception tendencies, rule-breaking behavior).

### 8.3 Positioning Against Existing Benchmarks

Create a comparison table clearly showing what your game offers that others don't:

| Aspect/Behavior | Poker | Chess | Sudoku | **Your Game** |
|-----------------|-------|-------|--------|---------------|
| Bluffing | ✓ | ✗ | ✗ | ✓/✗ |
| Perfect Information | ✗ | ✓ | ✓ | ✓/✗ |
| Multiplayer (3+) | ✓ | ✗ | ✗ | ✓/✗ |
| Cooperation | ✗ | ✗ | ✗ | ✓/✗ |
| Negotiation | ✗ | ✗ | ✗ | ✓/✗ |
| [Unique Aspect 1] | ✗ | ✗ | ✗ | ✓ |
| [Unique Aspect 2] | ✗ | ✗ | ✗ | ✓ |

**Key Positioning Strategies:**

1. Identify at least 2-3 aspects that are **unique to your game**
2. Explain why these aspects are important to study
3. Reference existing literature that calls for evaluation of these aspects

### 8.4 Handling Similar vs. Different Results

**If your results align with existing benchmarks:**
> "Our findings reinforce previous observations from [Poker Benchmark], demonstrating that [behavior X] is consistent across game types. This suggests [behavior X] may be a fundamental characteristic of current LLMs, independent of game context."

**If your results differ from existing benchmarks:**
> "Interestingly, our results diverge from findings in [Chess Benchmark], where models showed [behavior Y]. This discrepancy highlights the critical importance of diverse game benchmarks—model behaviors do not generalize uniformly across different game contexts, and each game type reveals different aspects of LLM capabilities and limitations."

### 8.5 Writing Effective Rebuttals

If reviewers raise concerns after submission, you will have an opportunity to respond (rebuttal phase). Tips for effective rebuttals:

1. **Be Respectful**: Thank reviewers for their feedback, even if you disagree
2. **Be Specific**: Address each concern point-by-point with concrete evidence
3. **Offer Additions**: Propose specific experiments or revisions you will add in the camera-ready version
4. **Acknowledge Limitations**: Honest acknowledgment of valid criticisms builds credibility

---

## 9. Agent Architecture Ablation Studies

### 9.1 Component Variation Experiments

If your AI agent has multiple components, conduct ablation studies:

**Example Agent Architecture:**
```
AI Game Agent
├── Component A: Game State Analyzer
├── Component B: Strategy Planner
├── Component C: Opponent Modeler
├── Component D: Risk Evaluator
└── Component E: Action Selector
```

### 9.2 Ablation Experiment Design

| Experiment | Components Active | Purpose |
|------------|-------------------|---------|
| Full Agent | A, B, C, D, E | Baseline performance |
| No Opponent Model | A, B, D, E | Impact of opponent modeling |
| No Risk Evaluation | A, B, C, E | Impact of risk assessment |
| Minimal Agent | A, E | Core capability baseline |
| etc. | ... | ... |

### 9.3 Prompt Variation Studies

**Variables to Manipulate:**

1. **System Prompt Variations**
   - Minimal instructions
   - Detailed game rules
   - Strategic hints included
   - Persona-infused prompts

2. **Information Provision**
   - Full game history provided
   - Limited recent history
   - No history (stateless)
   - Opponent action summaries

3. **Output Format Requirements**
   - Free-form response
   - Structured JSON output
   - Chain-of-thought required
   - Direct action only

### 9.4 Reporting Requirements

For each variation, report:
- Performance delta from baseline
- Statistical significance
- Qualitative behavioral changes
- Computational cost implications

---

## 10. Paper Structure Template

### Recommended Section Organization

```
1. Abstract
2. Introduction
   - Motivation and real-world relevance
   - Gap in existing benchmarks
   - Contributions
3. Related Work
   - Existing game benchmarks
   - LLM evaluation methodologies
4. Game Description and Formalization
5. Dataset and Scenario Generation
   - Dimensional analysis
   - Scenario statistics
6. Methodology
   - Simulator architecture
   - Evaluation metrics
   - Model selection
7. Experiments and Results
   - Main benchmark results
   - Multilingual experiments
   - Persona experiments
   - Ablation studies
8. Discussion
   - Real-world implications
   - Comparison with existing benchmarks
   - Limitations
9. Conclusion
10. Appendix
    - Full prompt templates
    - Extended results tables
    - Scenario examples
```

---

## 11. Checklist Before Submission

### Dataset
- [ ] Minimum 500+ diverse scenarios
- [ ] Clear dimensional coverage documented
- [ ] Evaluation criteria defined for all scenarios

### Simulator
- [ ] End-to-end game simulation working
- [ ] Multi-turn support implemented
- [ ] Multiplayer capability (if applicable)
- [ ] Comprehensive logging enabled

### Evaluation
- [ ] Single-turn metrics defined and computed
- [ ] End-to-end metrics defined and computed
- [ ] Statistical significance tests performed

### Model Coverage
- [ ] 2+ large open-source models evaluated
- [ ] 3+ small/medium open-source models evaluated
- [ ] Closed-source model evaluation planned for post-review phase

### Additional Experiments
- [ ] Multilingual experiments conducted
- [ ] Persona experiments conducted (if applicable)
- [ ] Ablation studies completed

### Paper Quality
- [ ] Real-world relevance discussed
- [ ] Comparison with existing benchmarks included
- [ ] Limitations acknowledged
- [ ] Unique contributions clearly articulated

---
