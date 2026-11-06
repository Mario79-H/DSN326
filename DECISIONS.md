# Decisions

*Every decision you make this term, with a date and a reason. Your AI log lives here too.*

Replace this placeholder in Week 1. Put something real in it — your backlog item and why you picked it is a decision like any other.

**What goes in:** decisions, the gaps you closed and how, what you declined to do, what you cut, system decisions, anything you re-framed later, and your AI log. **What doesn't:** raw findings. Those go in [EVIDENCE.md](EVIDENCE.md).

Write it as you go. Reconstructing this in Week 7 produces a file that reads like a case study rather than a record, and the design walkthrough will find the difference.

Full structure is in the **Decision Record** template. The short version:

```markdown
## 2026-09-14 — Chose Option B over A

**What I decided:** [one line]
**Why:** [the evidence, named]
**What I gave up:** [the cost]
**What would change this:** [what evidence would flip it]
```

For an AI entry, same shape: which tool, what for, what you kept, what you changed. Directing a tool is a decision.

---

## 2026-11-4 — Chose Backlog item HEARD-219 

**What I decided:**
  To choose backlog item HEARD-219 - Group order falls apart
**Why:**
  Because its an interesting ticket and has a lot of moving parts that could affect it.
**What I gave up:**
Nothing.
**What would change this:**
N/A

AI Entry
**Which tool**
Bolt
**What For**
Getting the tokens for each group
**What I Kept**
The tokens and the values it gave me
**What I Changed**
Nothing

## Week 2 
2026-11-5
**Missing Number**
The gap: The ticket says orders over $80 have a higher error rate and a higher refund rate, but does not give me the rate values or the number of orders. 
What I found: In the last quarter, 34,000 group orders were started and 21,000 of them were completed. This is inferred by carts with 6+ items and 3+ names in the instructions.
Source: PM pack metrics table and summarized with Dev
What it changes: Around 38% of group orders are not being completed, and there is a significant amount of errors and refunds. Both problems probably have the same source, but not knowing what the source is, I will have to take a deeper look during the sessions to see if I find something.

**Solution disguised as a problem**
What the ticket asks for: The ticket says the solution is when the person placing a large order can keep track of what they're ordering and for whom, and fix a mistake without starting over.
The problem underneath it: Knowing who they order for is assuming the person adds it to the instructions of an item. Only 22% of guest orders have a special instruction, which includes normal orders.
Source: PM pack metrics table
Does the proposed solution address the real problem?: We cannot assume the person ordering is always including a name in the instructions under an item in their group order. Consider this and watch if this situation happens in the sessions.

**The unstated constraint**
The constraint: A new backend service
Where I found it: PM pack
Why the ticket doesn't mention it: The ticket is implying a front-end solution is needed rather than a back-end solution
What it rules out: Adding a 'Name' field to each item, or grouping items within the order by name

AI Entry
**Which tool**
Claude
**What For**
Asking Dev about the missing number gap and getting information from it
**What I Kept**
The information
**What I Changed**
Nothing

