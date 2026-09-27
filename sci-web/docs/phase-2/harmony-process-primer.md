# What Is a Harmony Assembly?

## tl;dr

A Harmony assembly is a structured conversation that happens over email. A small group of people respond to questions, and AI synthesises everyone's input into shared positions that the group then refines and votes on. The whole process is designed so that no one gets left behind, and the process is provably fair. The system starts by specifically seeking solutions that the least-satisfied person can live with.

You don't need to install anything. You just reply to emails.


## How It Works

An assembly moves through three phases. Each phase involves one or more rounds where you receive an email, reply to it, and then receive a synthesis of what everyone said.

### Phase 1: DISCOVER -- "What does everyone think?"

You'll receive an email with an open-ended question about the topic. Reply with your honest thoughts in your own words - freeform text is fine, bullet points are fine, voice-to-text is fine. Nobody is grading your prose.

After everyone responds (or the deadline passes), AI reads all the responses and produces an anonymous synthesis: a summary of themes, areas of agreement, and areas of disagreement. No names are attached. You'll receive this synthesis by email.

There may be follow-up rounds if the facilitator wants to explore disagreements or uncertainties further. Each round builds on the last.

### Phase 2: DELIBERATE -- "Which approach works best?"

Based on what the group said in DISCOVER, the system generates candidate content - concrete proposals for additions to the spec that try to capture different ways of balancing everyone's concerns. You'll typically see three candidates - one prioritising the satisfaction of the least agreeable person, one aiming for the highest mean satisfaction across the group and one 'anti-consensus' proposal that aims to provoke discussion. 

*Your job is to rate each candidate from 0 to 10* and explain your reasoning. The system computes fairness metrics, paying particular attention to the lowest rating any candidate received. A candidate isn't considered viable until even the least enthusiastic participant rates it at least 5 out of 10 (this is the default - the thresholds are configurable).

If no candidate clears that bar, the system drafts a revised candidate incorporating feedback and you rate again,until at least one candidate is viable. If multiple candidates are viable, the highest rated one wins.


### Phase 3: DECIDE -- "All aboard?"

The strongest candidate from DELIBERATE is put to a final vote. You have three options:

**ENDORSE** -- "I actively support this."
**CONSENT** -- "This isn't my first choice, but I can live with it."
**OBJECT** -- "I cannot accept this."

Any single OBJECT blocks consensus. If you object, you'll be asked to explain what specific change would upgrade your vote to at least CONSENT. The group may then run another DELIBERATE round to address your concerns.

This means the process cannot simply outvote you. Your concerns have to be addressed - but the converse is also true; if you onbject you have to state what specific changes ould upgrade your vote to aty least CONSENT.

## What's Expected of You

- Reply to the emails. That's the main thing. The process works best with high participation.
- Be honest. The synthesis is only as good as the input. If you have concerns, raise them.
- Meet the deadlines. Each round has a response window (typically 48 hours). You'll get a reminder if you haven't responded. If you really struggle for time, a numeric score alone can be a sufficient minimum viable response!


## Why Use AI for This?

**It reveals hidden preferences.** 

In a meeting or group chat, social dynamics shape what people say. Louder voices dominate. People self-censor to avoid conflict. AI-synthesised deliberation sidesteps this: everyone responds privately, and the synthesis surfaces patterns that might never emerge in a room -- including minority concerns that would otherwise be drowned out.

**It works across time zones and languages**

You respond when it suits you, from wherever you are. Because the AI works with the meaning of what you wrote rather than the exact words, participants can write in the style and tone they're most comfortable with and the synthesis still captures their position.

**It's more sustainable**
A multi-round deliberation that might otherwise require several video calls instead happens asynchronously over email. Fewer calls means lower energy consumption and less screen fatigue.

**It incorporates information from outside the process**
If relevant discussions happen elsewhere, like a call, meeting notes, out-of-band discussions, etc. the facilitator can fold that material into the synthesis as supplemental data. The process doesn't have to be the only channel for the conversation to benefit from those inputs.
There are options for synthetic participation. In some configurations, AI-generated perspectives can be included alongside human responses, for example, to represent a stakeholder group that couldn't participate directly, or to stress-test a position. These are always flagged as AI-generated in the system's records.


## How Do You Know the Process Is Fair?

**Your response is cryptographically committed**

Every response is hashed and included in a Merkle tree -- a data structure used to prove that a piece of data was included in a set without revealing the rest of the set. After each round, you can receive an inclusion proof: a short piece of data that mathematically proves your response was part of the synthesis input. It would be computationally infeasible to produce this proof if your response had been altered or excluded. You can view what was submitted to the model in human-readable plaintext, and then drop it into our public web app to verify that the precise text you reviewed was really included in the synthesis.

**The synthesis is anonymous by design**
The AI is specifically instructed never to attribute views to individuals. The synthesis describes themes, patterns, and tensions -- not who said what. This is enforced by automated validation that checks the output for leaked names or email addresses before it reaches you.

**The minimax metric protects minority positions**
The system doesn't just optimise for the average. It specifically tracks the lowest rating any participant gives a candidate. A proposal that delights nine people but is unacceptable to one person is not considered viable. The process keeps iterating until the least-satisfied person's concerns are addressed. This is later reinforced by our final voting round, where all objections have to be resolved.

**Veto power in the final vote**
The DECIDE phase gives every participant the ability to block consensus. This is not majority rule. A single OBJECT vote prevents adoption and forces the group to address the objection. This structural guarantee exists regardless of what the AI does.

**Inputs are validated for manipulation**
The system screens responses for prompt injection attempts (where someone tries to manipulate the AI by embedding instructions in their response). Suspicious inputs are flagged for the facilitator to review before synthesis.

**PII is automatically redacted**
If you accidentally include sensitive information like phone numbers or email addresses in your response, the system redacts it before the text reaches the AI. This is a safety net, not a replacement for being mindful about what you share.

**There is a full audit trail**
Every action - responses received, syntheses generated, emails sent, operator decisions - is logged with timestamps. The facilitator can produce a complete record of the process on request.


## Frequently Asked Questions

**Can other participants see my response? **
No. All emails are sent using BCC. Participants see only the anonymous synthesis, never each other's raw responses.

**What if I miss a deadline? **
Your response won't be included in that round's synthesis, but you can still participate in future rounds. If you're slightly late, the facilitator may extend the deadline.

**Can I change my mind between rounds?** 
Yes. Each round is a fresh opportunity to express your current thinking. The process expects views to evolve.

**How many rounds will there be?** 
It depends on how quickly the group converges. A simple topic might need one DISCOVER round, one DELIBERATE round, and one DECIDE round. A contentious topic might need several rounds of DISCOVER and DELIBERATE before reaching DECIDE.

**What happens if consensus isn't reached?** 
The facilitator may run additional rounds, introduce revised candidates, or conclude the assembly without consensus. The process doesn't force agreement -- it just makes genuine agreement easier to find.

**Who is the "facilitator" or "operator"?** 
The person who set up the assembly. They control when rounds start and end, can extend deadlines, and review flagged responses. They don't control the AI synthesis itself, but they confirm the progression of the assembly from round to round, and they can trigger generating reports and metrics.

**How energy/carbon-hungry is this process?** 
We track all token usage throughout the assembly life-cycle, meaning we can generate consumption and emission estimates for specific assemblies. We expect that most assemblies run using Harmony will be less energy-hungry than most "traditional" assemblies because the AI usage displaces travel to a meeting location or multi-participant Zoom calls. The actual usage depends on the assembly length, configuration and number of participants.
