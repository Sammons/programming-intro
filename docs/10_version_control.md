## Version Control

Programmers make mistakes, they also work together, this turns into a morbid combination of blending our mistakes together in difficult to untangle ways.

Imagine two people editing and essay and having to merge the changes before the due date? bad news, I bet some sentences end up broken.

Over time there have been many solutions to version control, but the super popular one everyone uses today is `git`.

Version Control Systems allow several things:
* Recovery of any past code state
    * imagine you deploy a bug that takes down a website, you use git to safely undo the mistake without doing it by hand.
* Accountability. VCSs know who made what changes and checked them in.
* Security. Stems from accountability.
* Reviews. Clean difference-calculation showing the changes to a code base allow peer-reviews of just what changed everytime it changes.

## Git

Why the name? Torvalds says he named it after himself (*shrug*).

`git` is primarily a command line tool which traces changes and captures all of them in individual *commits* which can be checked into a *repository*. Changes are not synonymous with *commits*. As a developer you have to micro-manage this process yourself:

* stage the changes you have locally with `git add`
* commit the changes you have staged with `git commit`
* push the commits you have locally with `git push`
* delete the last commit with `git reset HEAD~1`
  * this causes conflicts if you have already pushed the commit.
* create a separate branch of changes with `git checkout -B mybranch`
* merge branches with `git merge otherbranch`

This is a deep topic, all I can say is read the docs and get on github. Learning to be good at git is important.

github.com has good docs and is now owned by Microsoft for better or worse.