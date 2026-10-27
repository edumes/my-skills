---
name: style
description: Write and change code the way Kent Beck's Tidy First? describes. Keep structure changes (tidyings) apart from behavior changes, tidy only where it makes the current change easier, and name tidyings in reviews. Use when writing, changing, reviewing, or refactoring code.
---

# Style

Write for the next person who has to change the code. Most of the cost of software is the cost of changing it, and big changes are expensive because of coupling: changing one element forces changes to others. Keep elements that change together close, and elements that change apart separate.

Every edit is one of two kinds:

- A behavior change alters what the program does.
- A structure change alters only how the code is organized. A tidying is a small structure change: minutes of work, easy to reverse, behavior identical.

Keep the two apart, and use structure to serve behavior: make the change easy (this may be hard), then make the easy change.

## Before each change

1. Read the code the task touches and ask what makes the change hard to make or to read.
2. If a few tidyings would make it easy and you know exactly which, tidy first, then make the behavior change.
3. If making the change easy needs more than a small batch of tidyings, stop and propose the tidying as its own step before doing it.
4. Write your own new code tidy from the start. Cleaning up code you just wrote is part of the change, not a separate tidying.

## When to tidy

Beck's question is first, after, later, or never. Here:

- First: in code the task touches, when it makes the change easier now. Do it.
- Later: anything else worth tidying that you notice on the way. Name it in one line of your reply and leave the code alone.
- Never: code nobody is about to change. Don't tidy it and don't mention it.

## Keeping structure and behavior apart

- A tidying keeps behavior identical: tests pass without changes. If a test has to change, it was a behavior change.
- When you commit (only when asked), tidyings and behavior changes never share a commit. Tidyings go first as `refactor` commits, the behavior change after as `feat` or `fix`.
- When you don't commit, the reply says which edits were structure only.
- If you tangled them, untangle before handing over: split the work into separate commits, or set it aside, tidy first, and redo the behavior change.
- Keep tidying batches small. A large tidying diff is hard to review and no longer cheap to reverse.

## Tidyings

Use these names when you mention a tidying.

- Guard clauses: return early on preconditions instead of nesting the main path. Keep them few.
- Dead code: delete it. Version control remembers.
- Normalize symmetries: when the same thing is done in different ways, convert to the way the codebase already prefers.
- New interface, old implementation: when the routine you need to call is awkward, write the interface you wish you had and have it call the old one.
- Reading order: reorder a file so the reader meets elements in the order they need them.
- Cohesion order: move elements that change together next to each other, in a file or in a directory.
- Move declaration and initialization together: declare a variable where it gets its value.
- Explaining variables: extract a hard-to-read subexpression into a variable named after its intent.
- Explaining constants: name a literal when its meaning is not plain where it sits. A literal that is already clear in context stays.
- Explicit parameters: pass what a routine uses as parameters, instead of a bag of options or values read from the environment deep inside.
- Chunk statements: put a blank line between the parts of a block that do different things.
- Extract helper: move a block with a clear purpose and few ties to the rest into a named routine.
- One pile: when code is split into pieces so small they hide what it does, inline them into one place first, then tidy back out.
- Explaining comments: write down the why the code cannot show, the thing you had to work out yourself.
- Delete redundant comments: remove comments that repeat what the code says.

One tidying often reveals the next. Follow the chain only while it makes the current change easier.

## Reviewing

Report findings as a short list, most useful first. Each one gives `file:line`, the tidying it calls for by name, and why it matters in one line. Flag any diff that mixes structure and behavior changes, and say how to split it. "Nothing to tidy" is a valid result.

## Other skills

- `ponytail` decides how much new code to write. A tidying earns its place by making the change easier; never add abstraction, indirection or options that ponytail would cut.
- `generalize` decides when repetition becomes a generic. Leave duplication to its rule of three.
- `simplify-code` runs a dedicated simplification pass over working code when asked.
- When they disagree, this skill yields. The codebase's own conventions beat every rule here.

## Sources

- Kent Beck, *Tidy First?: A Personal Exercise in Empirical Software Design* (O'Reilly, 2023)
- Kent Beck, [Software Design: Tidy First?](https://tidyfirst.substack.com/) newsletter
