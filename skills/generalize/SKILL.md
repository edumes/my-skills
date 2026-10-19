---
name: generalize
description: Turn code that keeps being written again into one generic implementation that each case declares instead of rewriting. Use when writing code that mirrors existing code (another resource, report, screen or test suite with the same shape), when starting a new instance of a category the system will have many of, or when the user asks to find duplication, generalize, or audit a codebase for repetition.
argument-hint: "[audit [path]]"
---

# Generalize

When the same shape keeps being written, write it once. Shared behavior lives in one generic implementation, and each case shrinks to a declaration of what makes it different. Adding the next case should mean declaring it, not copying the last one.

Two modes:

- While coding (default): runs alongside any coding task.
- Audit (`/generalize audit [path]`): scans for repetition and reports what to generalize.

## When repetition justifies a generic

- A category starts generic. If the new thing is one of a kind the system has or will have many of, each a variation of the same lifecycle (resources, reports, screens and forms, integrations, jobs, notifications), build it as generic + declaration from the first case. Check the codebase and the request to confirm it is a category; if unsure, ask in the proposal.
- Everything else follows the rule of three. On the second occurrence, write it and point out the similarity in one line of your reply. On the third, generalize.
- Count shape, not text. Two blocks with different names and types but the same steps are the same pattern. Two identical blocks that change for different reasons are not: merging them couples things that will drift apart, so leave them alone.

Repetition counts in production code, tests (setup, fixtures, suites repeated per resource), and schemas and config (validation, route definitions, JSON schemas, migrations).

## The shape scales with the pattern

A repeated snippet becomes a function, component or generic type.

A repeated structure, such as every layer of a resource (model, service, controller, routes, tests), becomes an engine plus a declaration:

- The engine owns the shared lifecycle once.
- Each case declares only what differs, preferably as data or metadata (a config object, decorators on the model) rather than code.
- Variation goes through extension points: options on the declaration, hooks the engine calls, a subclass override for a real exception, and a way to add case-specific pieces (extra routes, extra fields) without forking the engine.
- Tests follow the same split: one contract suite that runs against every declaration, plus tests for each case's own extensions only.

Name the generic after the category (`ResourceService`, `reportRoutes`), never after the first case.

## While coding

1. Before writing, look for a generic that already covers the task: an engine, a factory, a helper, a shared test suite. If one exists, declare the new case through it the way the surrounding cases do. Reimplementing what it already does is a bug.
2. If the generic almost covers the task, the missing piece is an extension point. Add it to the generic only when it is a behavior of the category; a one-off belongs in the case, through the extension points that already exist.
3. If what you are about to write mirrors existing code and the threshold above is met, stop and propose before building. Using an existing generic needs no approval; creating one, or changing an existing generic's contract, does.

## Audit

Scan production code, tests, and schemas and config under the given path (default: the whole repository). Look for files that share a naming pattern and the same set of methods, copy-pasted blocks, repeated route and schema definitions, and test files with the same setup. Use a duplicate detector the project already has, if any; do not add one.

Rank findings by number of occurrences, size, and how likely more cases are to come. Report each in the proposal format, condensed, and recommend where to start. "Nothing worth generalizing" is a valid result. Change nothing until the user picks.

## Proposal

Before building any new generic, show:

1. Occurrences: every place the pattern appears, as `file:line`.
2. Fixed and varying: what is identical across them, and what differs.
3. Shape: function, component, generic type, or engine + declaration, with its extension points.
4. The next case: the actual declaration a new case would need afterwards. This is the payoff, so show it.
5. Migration: every existing occurrence moves to the generic, in small steps that each keep tests green. Do not leave two ways of doing the same thing.
6. Left out: look-alikes that stay separate, and why.

Then wait for approval.

## Building it

- Derive the generic from the cases you have. The engine covers what they share, and every extension point exists because a known case needs it. No options for cases nobody has.
- Build the engine with the first case migrated onto it, then migrate the rest one at a time.
- Code you move into the generic keeps each case's validation and error handling.
- Signs the generic is wrong: a flag per caller, a branch on the case's name inside the engine, callers working around it. Move that variation to an extension point, or take the case out of the generic.

`ponytail` and `style` still govern the generic's own code. This skill decides when a generic is justified, and a justified generic is not "abstraction nobody asked for".

## Example

A backend where every resource repeated its service, controller and routes:

```ts
// Before: every resource repeats every layer
class CustomerService {
  list(ctx) { /* scope, filter, paginate */ }
  create(data, ctx) { /* validate, persist, audit, notify */ }
  // update, delete, export...
}
class SupplierService { /* the same, with Supplier */ }

// After: the engine owns the lifecycle once
class ResourceService<T> {
  list(ctx) { /* scope, filter, paginate */ }
  create(data, ctx) { /* validate, beforeCreate, persist, audit, notify */ }
  protected beforeCreate(data: T, ctx) {} // exists because invoices need it
}

function defineResource<T>(options: {
  entity: Entity<T>; // fields and rules live as metadata on the model
  service?: ResourceService<T>;
  extraRoutes?: Route[];
}) { /* builds service, controller and routes */ }

// Each case declares only what differs
export const customers = defineResource({ entity: Customer });

export const invoices = defineResource({
  entity: Invoice,
  service: new InvoiceService(), // overrides beforeCreate to assign the number
  extraRoutes: [issueInvoiceRoute],
});

// One line gives a case the whole test suite
runResourceContract(customers);
```

The engine grows large while each declaration stays a few lines, and that is the intended trade.
