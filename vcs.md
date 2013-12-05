Software Version Control
===============

### Branching Model

###### Basic Rules

* Only create new branches by branching `quality`
* Start new features in branches named `feature/[feature name]`
* Merge features into `episode/[episode name]` for integration/review
* Make pre-deploy bug fixes or hot fixes in branches named `fix/[issue #]`
* Only merge accepted code to `quality` via Pull Request
* Pull Requests to `quality` must be reviewed by someone other than the requester
* Only merge to `master` via Pull Request from `quality`


###### Workflow

The `quality` branch is a long-running branch that contains the latest stable (but not necessarily deployable), canonical version of our code. It is _always_ the starting point for creating new branches and is also used for final quality testing when preparing our code for deployment to production. No work should ever be done on this branch. Ever. Seriously, you guys.

At the beginning of a new development cycle, create an integration branch from `quality` following the naming scheme `episode/[episode name]`. You shouldn't be committing any changes to this branch until the end of the cycle when all work is being merged for integration/review. This branch, or a similar one with a subset of features (more on this later), will serve as the basis of the review process with stakeholders. These integration branches are temporary and only survive through the end of the current development cycle.

Begin work on new features by branching from `quality` and creating a new branch following the naming scheme `feature/[feature name]`. A new, separate feature branch should be created for each feature concept in the current development cycle. You may locally branch off from your primrary feature for related sub-features, but you must merge that work back into your primary feature branch before pushing your code upstream. Do your primrary development work on these feature branches and _only_ merge changes from the upstream `quality` branch if you ever need to get your branch in sync with other features being prepared for deployment. _The version of a file in the_ `quality` _branch supercedes all others whenever merge conflicts arise_. If you are intentionally modifying code in your current branch that conflicts with the upstream `quality` version, be cautious and deliberate about your merge resolution and make detailed, useful comments in the commit message.

For features requiring the work of more than one developer, create a canonical feature branch at the upstream repo and push to/pull from it to synchronize work between one another. Naturally, you would create a local version of that branch to do your work and follow the Pull Request procedures for mixing work into the canonical branch.

At the end of a development cycle, all individual features branches are merged into the integration branch. This is where the nitty-gritty testing and code review takes place to determine if all the code plays nicely together. If serious code conflicts and/or integration issues occur, you may create alternate integration branches (using `quality` as the source) to test different features in combination. This may be desireable to prove that certain features are stable enough together to move further upstream to `quality` in preparation for deployment, whereas another feature might not be quite ready for the limelight. These alternate versions should be named like `episode/[episode name]-[version]`. Presentation of features to stakeholders may be done from multiple integration and/or feature branches depending on the varying levels of code stability.

Once features have been accepted by stakeholders during the review process, a stable integration branch may be merged into `quality` to prepare for code deployment to production. This should be done with a Pull Request from the candidate integration branch to `quality`. Someone other than the requester must review the code and accept the request. The `quality` branch should then be deployed to a QA/staging server for final review. If last minute bugs or minor oversights appear during this final quality assurance stage, issues should be logged appropriately and fix branches should be created from `quality` to restore the branch to a stable state. These branches should be named `fix/[issue #]` and should merged back into the `quality` branch when the issue is confirmed resolved.

Finally, the stable `quality` branch can be merged into the `master` branch for imminent deployment. This is also accomplished by way of a Pull Request from the `quality` to `master` branch in the canonical repo. The `master` branch is long-running and always considered to be in a deployable state. Below is a sample diagram of how the process might look. 


<pre>
(master) ---------------------------------------------------------------------------------------- *
                                                                                                 /
(quality) --------- * ---------------------------------------------------- * ------------------ *
                    \\\                                                   / \                  /
         (episode/1) \\* --------------------------------- * ----------- *   \                /
                      \\                                  /             /     \              /
          (feature/A)  \* -------- * -------- * -------- *             /       \            /
                        \                                             / (fix/1) * -------- *
             (feature/B) * -------- * -------- * -------- * -------- *
</pre>


### Committing Your Work

Be concise and clear about what you are committing and why. Follow [these guidelines](http://robots.thoughtbot.com/post/48933156625/5-useful-tips-for-a-better-commit-message) for better commit messages.
