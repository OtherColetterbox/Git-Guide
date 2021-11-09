# Guide to using Git/GitHub

----

## I wrote this a couple of years ago - I can go through and remove any irrelevant parts (e.g. references to a specific IDE we don't use, problems that are really specific to another group of people...) if there's any interest in using it.

![](https://media.giphy.com/media/kswZdQQQV7pAc/giphy.gif)

----

### Contents
#### [Section 1: Cloning and pushing to an existing repo](#section-1-cloning-and-pushing-to-an-existing-repo-1)
#### [Section 2: Creating a project in IntelliJ (or other) and pushing it to GitHub](#section-2-creating-a-project-in-intellij-or-other-and-pushing-it-to-github-1)
#### [Section 3: Help! :'( (And FAQ)](#section-3-help--and-faq-1)
#### [Section 4: Common problems people have encountered on this project so far](#section-4-common-problems-people-have-encountered-on-the-projects-so-far)

----

### Section 1: Cloning and pushing to an existing repo
#### From cloning the repo to pushing changes...

1. Open Command Prompt.
2. Navigate to where you want your project to be.
3. Clone the existing repository.
  ```
  git clone [link to repo - this will end in ".git"]
  ```
4. CD into the project folder.
  ```
  cd [name of project folder]
  ```
5. If you want to see the local branches:
  ```
  git branch
  ```
Or if you want to see all branches, including remote:
  ```
  git branch -a
  ```
6. If the branch you want to work on already exists, switch to it.
  ```
  git checkout [branch name]
  ```
Or create a new branch and switch to it.
  ```
  git checkout -b [branch name]
  ```
7. Work on your code! :)
8. Check the status if you want to see which files have been changed.
  ```
  git status
  ```
9. Add the files you've changed to the staging area.
  ```
  git add [file name]
  ```
10. Commit your changes (don't forget to add a commit message)!
  ```
  git commit -m "[commit message]"
  ```
If you forget to add a commit message, you can exit Vim by typing ":wq" at the bottom and pressing enter.

11. Make sure that your version of the project is up to date (i.e. that no one has pushed any changes between when you last pulled and now) by pulling again.
  ```
  git pull
  ```
Note: Use "git pull" on the master branch. A common problem that people have run into during the projects is that they've typed "git pull" on a specific branch, and then when it's asked for more information they've typed "git pull origin \[current branch name\]" and only pulled the current branch. You want to pull the whole project.

12. (Switch back to the relevant branch if you moved to master in the last step.) Push your changes.
  ```
  git push origin [branch name]
  ```

![Final Space was only okay.](https://media.giphy.com/media/47D5dzXraWsldmlx9F/giphy.gif)

----

### Section 2: Creating a project in IntelliJ (or other) and pushing it to GitHub
#### Sometimes you'll want to create the project in IntelliJ and set up Maven etc. instead of starting from something that's cloned from GitHub. This also applies to situations where you've started on a project and only decide to push it to GitHub later (no judgement, I promise).

1. Create a project in IntelliJ; set up Maven, etc.
2. Create the repo on GitHub. If it's your first time linking an existing project with a GitHub repo, I recommend initialising the project without a readme, gitignore or license (so that the version on GitHub is empty) to avoid extra steps.
3. Navigate to the project folder in the terminal.
4. The following command initialises the local version of your project as a GitHub repository:
  ```
  git init
  ```
5. Now you need to link your local repository to the remote repository. Find the link to the GitHub repo; it's the same link as if you were cloning it. The following command will set your local repo up to push to your GitHub repo:
  ```
  git remote add origin [link to remote repo]
  ```
If you set up an empty GitHub repo, you're now ready to add/commit/push changes as normal! If the GitHub repo has files that you need to pull (README.md, .gitignore, LICENSE.md etc.), you'll need to do a little more.

6. Set your local master branch to track its remote counterpart.
  ```
  git branch --set-upstream-to=origin/master master
  ```
7. Typing "git pull" on its own may cause it to say "fatal: refusing to merge unrelated histories." If it does, type the following:
  ```
  git pull origin master --allow-unrelated-histories
  ```
The default commit message to merge the changes is fine. Use the arrows to get to the bottom of the window; type the following and press enter:
  ```
  :wq
  ```
8. You can now push your changes.
  ```
  git push origin master
  ```
  
![](https://media.giphy.com/media/wtlo7Hr4YIbQs/giphy.gif)

----

### Section 3: Help! :'( (And FAQ)

* "It's saying I've changed files that I haven't."
  * Try "git diff" to see the changes. That will shed some light on whether it's just your linter (if you have one), or if maybe you didn't merge some changes that you thought you did, etc.
  ```
  git diff
  ```
  * To see changes in files you've already staged:
  ```
  git diff --staged
  ```
* "Why can't I see the branches I expect to see?"
  * You may be looking at local branches specifically. This is the command to also see remote branches:
  ```
  git branch -a
  ```
  * You may have an old version of the repo that doesn't have the branch. Pull the most recent version.
  ```
  git pull
  ```
* "What if I have changes that I don't want to commit, but I want a clean working tree?"
  * You can stash changes, and an upside of this is that it doesn't actually delete them.
  ```
  git stash
  ```
* "I accidentally staged a file that I didn't mean to."
  * To remove a file from the staging area:
  ```
  git reset [file name]
  ```
* "I've started a project on IntelliJ, created a repo on GitHub, remembered to add the origin, set the branch to track the correct branch... anyway, it says "fatal: refusing to merge unrelated histories" when I try to merge."
  * Git doesn't like that the two repos have different commit histories. If you're sure that it's basically just that your local version has the project while the remote repo just has the files you initialised it with (a .gitignore, a README.md, a license etc.), then you can reassure it (i.e. tell it to shut up) with the following:
  ```
  git pull origin master --allow-unrelated-histories
  ```

![It's okay, friend. <3](https://media.giphy.com/media/gl8ymnpv4Sqha/giphy.gif)

----

### Section 4: Common problems people have encountered on the projects so far
#### This is kind of like the above section, but more specific to our experiences...

* Sometimes it's really easy to miss that the command line is telling you that it has run into a problem. The text will be calm and white, but it will (for example) be telling you that the merge you just attempted actually failed, so when you next start the process of adding and committing, it will tell you that a whole bunch of files have changed, and you won't know why. Or you'll end up in a situation where you'll be very convinced that you have the latest version of the project, when you actually don't. That's why we have to be super careful about reading what the terminal says! :)
* Regarding .iml files, we just need to decide (at the beginning) whether or not they go in the .gitignore and be consistent about it. In general, if it says you've made changes to a file (and the terminal's complaining about potentially overwriting it) but you don't see any (using git diff) and you're sure you didn't actually change it, just stash the changes or something; no one cares. It'll be fine.
* Sometimes people have been very confused about why they don't seem to have the whole project, when they've only pulled one branch. "git pull origin \[branch name\]" will only pull the specified branch.

![](https://github.com/Coletterbox/Git-Guide/blob/master/git%20doesn't%20break%20things.jpg?raw=true)
