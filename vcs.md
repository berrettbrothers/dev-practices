Software Version Control
===============

### Branching

###### Basic Rules

* Only create new branches from `quality`
* Start new features in branches named `feature/[feature name]`
* Merge features into `episode/[release name]` for integration/review
* Make pre-deploy bug fixes or hot fixes in branches named `fix/[issue #]`
* Only merge accepted code to `quality` via Pull Request
* Pull Requests to `quality` must be reviewed by someone other than the requester
* Only merge to `master` via Pull Request from `quality`

###### Workflow

The `master` branch is always in a deployable state. Code has to pass QA before being merged here. You may never branch from `master` and pull requests may only be made from the `quality` branch. 

The `quality` branch is used for quality testing before sending code to the master branch. 
It is also the sole starting point for any new feature branches to be forked from. No major work should happen in this branch only minor bug fixes, these fixes will typically be related to fixing issues in preperation for deployment. 

The `integration` branch is used as our integration and presentation branch. Used when preparing to present features, bug fixes and code changes. This branches main purpose is to integrate features together, to verify that the various features intergrate properly with one another. Also presenting can happen from these branch(es). If features do not integrate together, branches can be created to integrate features together. This branch is not long running, it will be destroyed after commits get merged to `quality`. 


The `feature/feature-name` branches are used for feature development, these should only be forked from the `quality` branch. No other feature branches should be merged into a specific feature branch. (e.g. `feature/a` and `feature/b` should only be merged together when moving to `integration`) 

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


#### Committing Your Work

Be concise and clear about what you are committing and why. Follow [these guidelines](http://robots.thoughtbot.com/post/48933156625/5-useful-tips-for-a-better-commit-message) for better commit messages.
