# Feature creep

## Summary

Feature creep is the excessive, ongoing addition of new features to a product beyond its basic function. It leads to software bloat, over-complication and missed deadlines. It is controlled by focusing on core features, following a roadmap with a clear change protocol, avoiding gold plating and validating features with real users before building them.

## Prerequisites

TODO: link the notes a reader should know first (requirements prioritization, change management).

## Core concepts

TODO: add a diagram, for example an impact versus effort quadrant chart for incoming feature requests (see GUIDELINE section 6.2).

### Definition

Feature creep is the excessive ongoing expansion or addition of new [features](https://en.wikipedia.org/wiki/Software_feature) in a product, especially in computer software, video games and consumer and business electronics. These extra features go beyond the basic function of the product and can result in [software bloat](https://en.wikipedia.org/wiki/Software_bloat) and over-complication, rather than simple design.

What counts as feature creep varies among end users: what some users perceive as creep, others consider practical functionality.

### Causes

The most common cause of feature creep is the desire to give the consumer a more useful or desirable product, in order to increase sales or distribution. Once the product does everything it was designed to do, the manufacturer must choose between adding functions some users might consider unneeded (sometimes at the cost of efficiency) and keeping the old version (at the cost of a perceived lack of improvement).

Another major cause is a [compromise from a committee](https://en.wikipedia.org/wiki/Design_by_committee) that decides to implement several different viewpoints or use cases in the same product. As more features are added to support each approach, cross-conversion features between the approaches may become necessary, which complicates the product further.

### Control

There are several methods to control feature creep: strict limits on allowable features, multiple variations of the product, and pruning excess features.

#### Separation

The temptation of later feature creep can be reduced by basing the initial design on strong software fundamentals, such as logical separation of functionality and data access, for example submenus that power users can open when they want more functionality and more detailed information. Creep can be actively controlled with rigorous [change management](https://en.wikipedia.org/wiki/Change_management) and by moving changes to later delivery phases of a project.

#### Variations and options

Another method is to maintain several variations of a product, with features kept limited in the more basic variations (for example the editions of Microsoft Windows). For software user interfaces, viewing or operation modes (such as a basic mode and an expert mode) let users choose what matches their needs.

#### Modularity

Power users who need more functionality can add it themselves through modules, plug-ins, add-ons and themes, so the core product stays small.

#### Pruning

At some point the cost of maintaining a subset of features becomes prohibitive and the features can be pruned. A new version can omit them, possibly after a transition period in which they are [deprecated](https://en.wikipedia.org/wiki/Deprecation). When several variations of a product exist, some of them can be phased out.

### Avoiding feature creep

#### Focus on the core features

The rule of product design is simple to state: ship the right features to the right people. It is hard to apply, because it requires identifying the parts of the product (the core features) that give the most value to the target audience. To keep a project focused on core features:

- **Start with user and market research.** Identify the target audience, their needs and their wants. Know which problem you are solving, and for which user.
- **Prioritize all features according to the needs of users.** Have a clear rationale for every feature. The [jobs-to-be-done framework](https://hbr.org/2016/09/know-your-customers-jobs-to-be-done) helps identify the features that give the most value.
- **Check that the target audience is willing to pay for the solution.** If potential customers will not buy the product, the work may be wasted, so research this before building.

#### Create a roadmap and follow it

Feature creep is hard to prevent when the team does not notice it happening. It is much more likely when a team has no clear roadmap, because then every problem is solved reactively rather than proactively. To create a roadmap:

- **Formalize the scope.** Before work starts, the team has a written scope of work approved by the stakeholders.
- **Identify the major and minor milestones and put them on a timeline.** Review the milestones whenever a scope change is requested, so the project does not slip.
- **Introduce a clear protocol for changes.** Define how changes are reviewed, approved or rejected.
- **Treat incoming feature requests as a zero-sum game.** When stakeholders ask for a new feature, another feature leaves the scope so that the deadline still holds. This makes stakeholders reconsider the value of the request, or it gives the team more time and budget.
- **Create an impact versus effort matrix.** The matrix maps features against their potential value and the effort needed to build them. It also records the history of product decisions and their rationale.

#### Stay away from gold plating

Gold plating is the tendency of a team to over-deliver on the scope and add features that stakeholders did not ask for, in the hope of making them happier.

#### Learn to say no to feature requests

The ability to say no is one of the most important skills of a project or product manager, because it prevents scope creep.

#### Establish a quick build-measure-learn cycle

Validate ideas before investing time and effort in building them. When adding features, test them with real users, and make sure each feature is linked to a user need and delivers value to the target audience.

## Worked example

TODO: add a concrete example, such as a backlog of ten feature requests scored on impact and effort, with the decision for each.

## Trade offs and when to use it

TODO: describe when adding features is the right call and how to tell healthy growth from creep.

## Common mistakes

TODO: list frequent mistakes, such as accepting requests without removing anything from the scope.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

TODO: add primary sources (specification, original paper or official documentation), with one sentence on why each is worth reading.
