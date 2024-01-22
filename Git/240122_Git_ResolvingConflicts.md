## Resolving Conflicts After the Pull Request

### Explanation

**Start Point**

In the project, my colleague and I worked in the same branch for the login feature. To avoid getting the code overwritten, I decided to make a new branch based on the branch for a login feature. (I know, we should have let the files parted more structurally independent.) After making the branch and the casual add-commit-push, I've faced few conflicts.

**Tackling the Problem**

There were three lines to annotate the conflicting lines.

- `<<<<<<<` `feature-new` </br>

    It means that below this would be the conflicting code from the branch which needs merging.  

- `=======`

    It divides the space into two sections, the merging branch codes and the branch you want to merge into. 

- `>>>>>>>` `main` </br>

    It means that above this would be the conflicting code from the branch / main which you are trying to merge into.

Resolving the conflicts needs manual code modification. Furthermore, the modification needs to be cautious. The flow and the original intention of codes should be highly considered.