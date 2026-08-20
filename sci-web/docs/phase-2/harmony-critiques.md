# Common Criticisms of LLM-Assisted Assemblies

## Who this document is for

If you're evaluating Harmony and have concerns about using AI in a deliberative process, or if you're anticipating those concerns from others, this document lays out the most common objections and how Harmony addresses them. We've tried to be honest about where trade-offs exist rather than pretending there are none.


## "It removes the human connection"
This is the most intuitive objection, and it deserves a careful answer.

### What's actually being replaced
Harmony doesn't replace human deliberation. It replaces the logistics of deliberation: scheduling meetings, managing turn-taking, taking minutes, circulating summaries. The humans still do all the thinking, writing, evaluating, and deciding. The AI reads what people wrote and identifies patterns. The humans judge whether those patterns are right.

### What's gained by removing the room
The face-to-face meeting is often held up as the gold standard for deliberation. But research on group dynamics consistently shows that in-person discussions amplify certain biases:

- Dominance effects. A small number of speakers consume the majority of airtime. Quieter participants -- who may hold important minority views -- self-censor or never get the floor.
- Conformity pressure. People anchor to the first opinion expressed and adjust toward the perceived group consensus, even when they privately disagree (Asch conformity, groupthink).
- Status effects. Seniority, confidence, and fluency are mistaken for correctness. The most articulate speaker wins, not the best idea.
- Availability bias. Whatever was said most recently or most vividly dominates the group's memory of the discussion.

An asynchronous, anonymised process neutralises all of these. Every participant gets equal space. Nobody knows who said what. The synthesis is based on all responses equally, not on who spoke last or loudest.

## The connection that matters

The purpose of a deliberative assembly is collective decision-making. The "connection" that matters is that each participant's concerns are heard, considered, and addressed. Harmony makes this verifiable: you can mathematically prove your response was included in the synthesis, and the minimax metric guarantees the process cannot ignore anyone's dissatisfaction.

If your group also needs social connection, that's valuable, but it's a separate need that can be served with semi-regular drop-in calls. Conflating the two is how you end up with long meetings that are neither good socialising nor good decision-making.

## Harmony can complement face-to-face processes

Nothing prevents using Harmony alongside in-person discussion. The supplemental data feature lets facilitators incorporate meeting notes, Slack conversations, or phone call summaries into the assembly. An organisation might hold a workshop to surface initial views, then use Harmony to structure the convergence process across a distributed team. Or vice versa: run the assembly first to establish where people actually stand, then meet in person to discuss the remaining disagreements. Used this way, Harmony doesn't compete with human connection - it provides a substrate of structured, verifiable input that makes in-person time more productive.


## "I don't trust AI to represent my views"
This concern has several layers, and each one has a concrete answer.

### The AI doesn't decide anything
This is worth stating plainly. The AI synthesises -- it produces a summary of what the group said. It does not make decisions, cast votes, or determine outcomes. Every substantive decision (rating candidates, casting the final vote, objecting) is made by human participants. The AI is a lens, not a judge.

### You can verify your inclusion
Every response is cryptographically hashed and committed to a Merkle tree. After synthesis, you can receive an inclusion proof -- a short piece of data that mathematically proves your exact response was part of the input set. If your response had been altered or excluded, the proof would not validate. You can inspect the human-readable plaintext that was submitted to the model and verify it through a public web app.

### The synthesis is checked before you see it
Before any synthesis reaches participants, it passes through automated validation that checks for leaked participant identities, PII, and attribution. The facilitator reviews each synthesis before distribution. And every participant gets to respond to what the synthesis says - if it misrepresents the group's views, that will surface in the next round.

### The minimax metric is a structural safeguard
Even if the synthesis were imperfect, the decision process has a safety net: the minimax metric. A candidate position is not viable until even the least satisfied participant rates it at least 5/10. This means a biased synthesis that ignored someone's concerns would produce a candidate that person rates poorly, which the system would flag as non-viable. Bias in synthesis gets corrected by the rating mechanism.

### The final vote is human, and it's a veto
The DECIDE phase gives every participant the power to OBJECT, which blocks consensus entirely. This is not majority rule. If you feel the process has misrepresented you at any point, you can block the outcome and explain what needs to change. This structural guarantee works regardless of what the AI does.

## "What about energy use and carbon emissions?"
This is a legitimate concern, and we take it seriously. But we think the numbers will favour Harmony.

### What Harmony displaces
Consider what a traditional multi-round deliberation looks like: multiple video calls with all participants present, each lasting 60-90 minutes, requiring synchronous availability, and potentially requiring travel for hybrid or in-person formats.

A typical 1-hour Zoom call with 10 participants uses roughly 0.3-1.5 kWh depending on video quality and hardware. A 3-round deliberation with 2 calls per round uses 6 calls, or roughly 2-9 kWh -- not counting travel, heating/cooling meeting rooms, or the embodied energy of maintaining office space.

### What Harmony consumes
A Harmony assembly makes approximately 5-15 LLM API calls depending on the number of rounds and participants. Each call processes a few thousand tokens. The total energy consumption for the LLM inference is on the order of 0.01-0.1 kWh for a complete assembly -- one to two orders of magnitude less than the video calls it replaces.

### We track it
Harmony records token usage for every API call throughout the assembly lifecycle. This means you can calculate actual energy consumption and carbon emissions for any specific assembly, rather than relying on estimates. The token-usage data is available per-assembly as a JSON file and is reported at conclusion.

### The real emissions story
The most carbon-intensive thing about traditional deliberation is travel. Even a single return flight for one participant to attend an in-person meeting dwarfs the energy cost of thousands of LLM API calls. But even for fully-remote teams, the cumulative energy cost of synchronous video calls - plus the infrastructure to support them (data centres for video streaming, always-on endpoints) - likely exceeds the burst compute cost of a handful of LLM inference calls.

The honest framing is: LLM inference is not free, but it is dramatically cheaper than the activities it displaces.

## "Isn't this just replacing human judgement with AI?"

No. It's replacing human logistics with AI and keeping human judgement at every decision point.

Here is what the AI does:

- Read responses and identify themes, agreements, and disagreements
- Draft candidate positions that attempt to balance competing concerns
- Compute fairness metrics on participant ratings

Here is what humans do:

- Write their actual views
- Rate candidate positions
- Provide feedback on what's missing or wrong
- Cast the final ENDORSE / CONSENT / OBJECT vote
- Block consensus if their concerns aren't addressed

The AI accelerates the boring parts (reading 20 responses and writing a summary) so that humans can focus on the hard parts (evaluating proposals and making judgement calls). This is augmentation, not replacement.


## "What if someone games the system?"

### Strategic voting in DELIBERATE
A participant could dishonestly rate candidates to try to steer the outcome - for example, rating a strong candidate low to prevent it from clearing the viability threshold. This is a real concern, and it's not unique to AI-assisted processes (it affects any voting system).

Harmony's mitigation is structural: the minimax metric means that gaming requires coordination among multiple participants to suppress a candidate. A single strategic voter can lower the minimax score, but the facilitator can see individual ratings and identify outlier behaviour. And the final DECIDE vote requires explicit ENDORSE/CONSENT/OBJECT rather than numeric scores, making strategic misrepresentation harder to sustain.

### Adversarial framing in responses
A more subtle attack: crafting responses that exploit how the LLM weighs input. For example, making false consensus claims ("everyone I've spoken to agrees that...") or using authority signalling ("industry best practice requires...") to anchor the synthesis toward a preferred outcome.

We are transparent that this is a fundamental limitation of LLM-based synthesis. The system cannot distinguish legitimate persuasion from adversarial framing. The mitigations are:

- The facilitator reviews each synthesis before distribution and can regenerate it
- Every other participant gets to respond to the synthesis -- misleading framings will be challenged in subsequent rounds
- The minimax metric catches outcomes that leave people dissatisfied, regardless of how the synthesis was steered
- The veto in DECIDE is the final backstop

No deliberative process is immune to rhetorical manipulation. The question is whether an LLM-mediated process is more vulnerable than a meeting. In a meeting, a skilled rhetorician can dominate the room in real time with no written record. In Harmony, every input is recorded, every synthesis is reviewable, and every participant gets equal space regardless of charisma.


## "Who controls the prompts?"
The prompts that instruct the AI are part of the codebase and are inspectable. The facilitator does not secretly control what the AI is told to do. The system prompts include explicit instructions to:

- Not attribute statements to individuals
- Not include participant identifiers
- Focus on themes and collective insights
- Produce structured output with consensus areas, disagreement areas, and uncertainty areas

Organisations can customise prompts for their specific context, but the security constraints (anonymisation, PII redaction, output validation) are enforced at the code level and cannot be overridden by prompt customisation.

## "What about LLM bias?"
All LLMs carry biases from their training data. In the context of synthesis, this could manifest as the model giving more weight to perspectives that align with mainstream views, or framing issues through a particular cultural lens.

Harmony's design limits the impact of model bias in several ways:

- The model summarises; it doesn't originate. The synthesis is constrained by what participants actually wrote. The model cannot introduce positions that no participant holds.
- Bias is surfaced by the rating mechanism. If the synthesis skews in a direction that doesn't represent the group, participants will rate the resulting candidates poorly. The minimax metric catches this.
- The facilitator can regenerate. If a synthesis appears biased, the facilitator can regenerate it, edit it, or supplement it before distribution.
- Multiple rounds correct for drift. Each round of participant feedback anchors the process back to what the group actually thinks, limiting how far model bias can push the outcome.

The honest answer is that LLM bias is real and cannot be fully eliminated. But in a multi-round process with human ratings and veto power, its practical impact on outcomes is limited. The bigger risk in traditional deliberation is human bias (status effects, conformity pressure), which Harmony structurally eliminates.


## "This is a solution looking for a problem"
Some groups don't need structured deliberation. If your team is small, co-located, aligned, and has no history of meetings dominated by a few voices, a conversation around a table may be perfectly adequate.

Harmony is designed for situations where the simpler approach breaks down:

- Distributed teams that can't easily get in a room together
- Cross-timezone groups where synchronous meetings always disadvantage someone
- Sensitive topics where social pressure distorts what people say
- Recurring disagreements where the same voices win every time and the same concerns go unaddressed
- Regulatory or governance contexts where you need a verifiable audit trail of how a decision was reached
- Large groups (15+) where round-table discussion becomes unwieldy
- Multi-language groups where some participants are disadvantaged by meetings held in a single language

If none of these apply to your situation, you may not need Harmony.
