# Git Flow Explained

**Disclaimer**

- Last modified(yy/mm/dd): 24/06/03
- Written By: @glenn-syj

## Expalanation

### Start Point

In the last project, my team decided git flow to be a branching strategy. In the ongoing project, we also chose to apply git flow for the cooperation process. I had to run a seminar for our team mates who were not familiar to the git flow.

### Tackling Curioisity

Git flow is a git branching model of which workflow uses branches for features, a current version, a next version, and bug fixes. Then, how can we use the git flow and find out what means what? 

**Why GitFlow**

**Using GitFlow**

The git program provides commands for git flow. The initial step is initializing the git flow on the local repository created or cloned. `git flow init` would be the command. 

```
$ git flow init


Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [main]
Branch name for "next release" development: [develop]


How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix brancehs? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []


$ git branch
* develop
 main
```

Let's see what happened after the command.

```
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
```

These lines tell that, as no git repostiroy is found in the path, the repository and the base branches for productions and releases has been created.

```
How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix brancehs? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
```

Naming the supporting branches follows. The lines above show a process of deciding each branch name to be set as the default name.

`git flow {prefix} start {branch-name}` creates the branch in the local repository. Adding, committing, and pushing the changes into the repository is just same as before.

As my team decided to delete the merged branch in the github website, the local branch needs to be removed too.

### Conclusion

### References

https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow#:~:text=Gitflow%20is%20an%20alternative%20Git,by%20Vincent%20Driessen%20at%20nvie.