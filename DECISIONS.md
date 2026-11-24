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

# Week 3

**Three Options**
|  | A: Name on each item | B: Distinguishing group order vs big order | C: Group orders using names | 
|---|---|---|---|
| In one sentence | Each item on a order has an input labeled 'Name', where the user can enter the name the item belongs to | User can select from either a group order with multiple people, or a big order for one family | Reorganize flow to add a name, select food items for person, and then add new name with their food items, and so on  |
| Costs the user | Extra seconds entering a name for each item | Noticing the checkbox and understanding what each state means to their according to their order |  Go one by one for each person, trusting that they know what each person wants from the start |
| Costs the system, incl. build | Saving the value in the database. Visually, just add another label input field to the card with the same tokens | Adding the flag to the database. Frontend, just a single label and checkbox | Reformat flow of group orders, restructure database to accommodate grouping by name  |
| Assumes | User sees field within the item | User notices the single checkbox and knows what it means | User knows all the items for a person |
| What would kill it | Testers don't see the Name field | Testers don't see the checkbox | Testers find the new flow tedious or complicated |

# Week 4

Hey Marisol, I'm writing back to you about HEARD-219. I wanted clarification on one thing; does grouping items by names need implementation of a new backend service? I know Nate is committed through Q4. I would hope it doesn't need that, but since its a priority P2 I wanted to make sure first. In case of no response before Friday, I'll assume that it does and work around that.
My idea is to utilize option B, which is adding a checkbox at the top of the group order page that will flag the group order as either a group with multiple people, or just a large order, along with option C, which is grouping by name. If the order is an order for multiple people, a 'Add Person' button will appear that, when clicked, shows a popup that will have a field to enter their name and a dropdown with all the items in the order, and the user will select the items for that person. Once saved, the order list is updated with those items grouped under a person, and the rest of the items ungrouped as it is now. 
The tradeoff for this is that there are additional steps for the user to group their order by name, which some users might not like, but will serve to better organize the group order, both for the customer and food staff. This change is reversible, but would take time to change it back, just like it will take time to implement the change. 

**Studio B - Full Fidelity**

The primary device target is phone at comfortable, with desktop at compact being the secondary. In terms of system decisions, I did some extensions of existing components. The button to open the dialog, the checkbox to show the button, and the input field to add a name are all existing components within Rail. The dialog also exists, used when ordering an item. When creating the dialog, I did detach the instance to include the select component within the layout.

