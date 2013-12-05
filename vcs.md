Software Version Control
===============

#### Branching
The `master` branch is always in a deployable state. Code has to pass QA before being merged here. 

The `quality` branch is used for quality testing before sending code to the master branch. 
It is also the sole starting point for any new feature branches to be forked from. No major work should happen in this branch only minor bug fixes, these fixes will typically be related to fixing issues in preperation for deployment. 

The `integration` branch is used as our integration and presentation branch. Used when preparing to present features, bug fixes and code changes. This branches main purpose is to integrate features together, to verify that the various features intergrate properly with one another. Also presenting can happen from these branch(es). If features do not integrate together, branches can be created to integrate features together. This branch is not long running, it will be destroyed after commits get merged to `quality`. 


The `feature/feature-name` branches are used for feature development, these should only be forked from the `quality` branch. No other feature branches should be merged into a specific feature branch. (e.g. `feature/a` and `feature/b` should only be merged together when moving to `integration`) 


#### Committing Your Work

Be concise and clear about what you are committing and why. Follow [these guidelines](http://robots.thoughtbot.com/post/48933156625/5-useful-tips-for-a-better-commit-message) for better commit messages.
