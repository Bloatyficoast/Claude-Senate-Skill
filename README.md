# /senate
A Claude skill that stress-tests any decision by running it through a simulated 100-seat Senate: committee review, floor debate, amendments, a substitute, cloture (filibuster), and a final roll call. The Senate both debates and votes, and it can change what you asked for.
You say you want fast food. The Senate may pass a salad instead.
You say you want a new car. The Senate may pass a cheaper new car.
The Senate keeps your underlying goal and may change the means. If the final bill passes, you play the President and decide whether to approve or veto it.
All 100 seats are the same Claude reasoning from different starting positions, not separate instances, and the whole run happens in a single response.
> **What this is, and isn't.** `/senate` is a structured way to hear the best case for and against a decision, and for a better alternative, before you make it. It is not a poll of real people and it does not predict real votes.
Install
Claude Code
```bash
mkdir -p ~/.claude/skills/senate
cp senate/SKILL.md ~/.claude/skills/senate/SKILL.md
```
Claude app (claude.ai / desktop)
Zip the `senate` folder (the one that contains `SKILL.md`) and upload it under Settings, Capabilities, Skills.
Repo layout
```
senate/SKILL.md   the skill
README.md
LICENSE
```
Use
```
/senate I want to buy a new car.
```
Optional modifiers, added to the same message:
Modifier	Effect
`brief`	Shorter run: 1-line committee findings, 2 speakers per side, 1 amendment per side.
`as is`	The Senate may not rewrite your request. It only debates and votes on your original wording.
`simple cloture` / `no filibuster`	Ends debate with a simple majority instead of 60 votes.
`override`	After a veto, tries to override it (needs 67 of 100).
How it works
#	Phase	What happens
1	Committee review	3 to 4 committees review a neutrally worded bill. The Senate also writes down your goal.
2	Floor debate	Mirrored speeches from both caucuses, plus a swing voter. Alternatives are put on the table.
3	Amendments and Substitute	Fixes for real objections, then a head-to-head vote: your original versus the Senate's best alternative.
4	Cloture	A filibuster only if a real bloc is still opposed. Ending debate needs 60 of 100.
5	Roll call	Yea / Nay / Abstain on the bill as it now stands, always totalling 100.
6	Outcome	More than 50 Yeas passes it to you, with a "what changed from your request" line, to approve or veto. 50 or fewer is disapproved.
Built to be fair to the proposal
The skill has explicit rules so the result doesn't just tell you what you want to hear, and doesn't push its own taste either:
Judge the idea, not the person. Your wording and enthusiasm don't move any seat.
Neutral bill text. Your proposal is restated without loaded words.
Mirrored, equal treatment. Both sides get the same number of speakers and the same space, and both are steelmanned.
No made-up evidence. No invented statistics, laws, or citations. Unverified claims are flagged.
Changes must serve your goal. The Senate keeps what you are trying to achieve and may only change how. Personal choices start with a presumption in your favor, and any change needs a concrete reason and is never a lecture.
Substitutes go both ways. The Senate may suggest cheaper or pricier, safer or bolder, healthier or more indulgent, whatever fits the goal best, and it checks that it isn't always nudging one direction.
The original gets a real contest. If your request wins the substitute vote, the Senate says why.
Tallies follow the reasoning. The numbers always sum to 100 and are explained.
Mirror check. Before the final vote, the Senate asks whether it would treat the opposite bill the same way.
The President can't change the vote. Your approve or veto comes after the roll call.
Example (illustrative, not a real poll)
```
/senate I want to buy a new car.
```
```
Bill: The user shall buy a new car.
Goal (inferred): reliable transportation they feel good about owning.

Committees
- Feasibility: favorably. New cars come with warranties and fewer surprise repairs.
- Cost and Resources: with amendments. A new car loses value quickly and monthly payments are the main risk.
- Risk: with amendments. Insurance and fees add to the real cost.

Debate: 50 firm Yea / 28 firm Nay / 22 undecided. Swing voter would back it with a price cap.

Amendments
- A1 Set a total budget before shopping: Yea 86 / Nay 8 / Abstain 6. Adopted.
- A2 Compare insurance cost before signing: Yea 79 / Nay 14 / Abstain 7. Adopted.

Substitute
Original -> Senate Version: "a new car" -> "a lower-priced new car".
Why: it meets the same goal (reliable, covered by warranty) with a smaller payment.
Substitute check: had the request been a budget car, the Senate would have weighed a step-up model just as seriously.
Vote: Yea 63 / Nay 31 / Abstain 6. Substitute adopted.

Cloture: no filibuster; no large bloc held an unresolved objection.
Mirror check: the same reasoning applied to "never buy a new car" produces a similar split.

Final roll call: Yea 69 / Nay 24 / Abstain 7 (100)
Result: PASSED
What changed from your request: new car -> lower-priced new car.
Dissent and concurrence: the Nay side's strongest point was that a used car would cost even less.

President: Approve / Veto / Send back with changes?
```
Limitations
Every seat is the same model, so disagreement is simulated reasoning, not independent opinion.
The skill can't verify facts unless a search tool is available. Unverified claims are marked as such.
It is meant for decision-making practice. For medical, legal, or financial decisions it is not professional advice.
Changelog
1.1.0: The Senate can now rewrite the request. Added the Goal line, the Substitute vote, the `as is` modifier, and neutrality rules 13 and 14.
1.0.0: Committee, debate, amendments, cloture, roll call, and presidential approve or veto, with 12 neutrality rules.
Contributing
Issues and pull requests are welcome, especially ones that make the neutrality rules stricter or the output shorter.
License
