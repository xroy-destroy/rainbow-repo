
I'm following Ry's Git Tutorial, a guide I found while desperately searching Google.
My object is to establish a procedure to efficiently initialze and maintain a clean repository. This is for my personal study.

1. Create your index.html file-- make it cute!

2. cd to its directory location, and execute $ git init 
    - the repository has been initialized
    - changes to files within this folder are being tracked
    - this creates a file call ".git" within the folder
    - remove ".git" to revert the folder back to its unversioned state.

3. $ git status will show the repository status containing:

                MY REPOSITORY STATUS
    ----------------------------------------------
        On branch main

        No commits yet

        Untracked files:
        (use "git add <file>..." to include in what will be committed)
            README.md
            index.html

        nothing added to commit but untracked files present (use "git add" to track)

4. Stage a Snapshot $ git add . and check the repository status $ git status
    - index.html is now staged for a commit
    - a staged file is a tracked file
    - these tracked files can be updated, or removed, before a commit
    - this snapshot represents the state of index.html at the time it was staged

                MY REPOSITORY STATUS
    ----------------------------------------------
        On branch main

        No commits yet

        Changes to be committed:
        (use "git rm --cached <file>..." to unstage)
            new file:   index.html

        Untracked files:
        (use "git add <file>..." to include in what will be committed)
            README.md

5.  Commit $ git commit -m "Create index page."
    - index.html has been committed to the main branch
    - The "-m" should be a brief message about what the commit accomplishes
    - Do not use a passive voice for the message
    - The committed file is safe from editing
    - Committed snapshots can restore a file in the working directory to its previous state

6. View the repository history $ git log
    - "commit cbb..." is an SHA-1 checksum
    - The checksum serves as a unique ID for the commit
    - Authorship will be "unknown" if a username hasn't been added to the git configurations
    - Following the date is a time-zone indication "-0700"
    - Tip: $ git log --name-only will provide file names
    
                MY REPOSITORY LOG
    ----------------------------------------------
        commit f870d73ccad58b596cd1c30c333077c8c6180c04 (HEAD -> main)
        Author: xroy-destroy <xroy.ocean@gmail.com>
        Date:   Fri Sep 17 09:12:07 2021 -0700

            Establish a procedure to efficiently initialze and maintain a clean repository.

        commit cbb19fa481a2ef310d1cbe32de93cbde0d031282
        Author: xroy-destroy <xroy.ocean@gmail.com>
        Date:   Thu Sep 16 16:09:38 2021 -0700

            Create index page.

7. Configure git to your username 
        $ git config --global user.name "user-name"
        $ git config --global user.email "user@email.com"
  - "--global" tells git to keep these configurations default for all repositories

8. Create orange.html and blue.html pages
    - Add boilerplate, make it cute!

9. Stage & commit the blue and orange html files
        $ git add .
        $ git -m "Create blue and orange pages."
      
                MY REPOSITORY STATUS
    ----------------------------------------------
        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md
        
        Untracked files:
        (use "git add <file>..." to include in what will be committed)
            blue.html
            orange.html


                NEW REPOSITORY STATUS
    ----------------------------------------------
        Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
            modified:   README.md
            new file:   blue.html
            new file:   orange.html

10. Modify the HTML pages by adding links, and stage them $ git add .
    - A modified file in the working directory will be red
    - A staged file will be green

        Changes not staged for commit:
            modified:   README.md
            modified:   blue.html
            modified:   index.html
            modified:   orange.html
    ----------------------------------------------
        Changes to be committed:
            modified:   README.md
            modified:   blue.html
            modified:   index.html
            modified:   orange.html

11. Commit the changes $ git -m "Add navigation links." and review $ git status
  
                  REPOSITORY STATUS
    ----------------------------------------------
        On branch main
        
    nothing to commit, working tree clean

12. For a simplified log review of a particular file file, $ git log --oneline <file>
    - Ex1: git log --oneline index.html
    - Ex2: git log --oneline blue.html
    - Note that only commits involving that file are listed
    - "e304f33" is the checksum ID
    -(head-->main) head is commited, main is main branch

        $ git log --oneline blue.html
        e304f33 (HEAD -> main) Add navigation links.
        46e2663 Create orange and blue html pages.
        
        $ git log --oneline index.html
        e304f33 (HEAD -> main) Add navigation links.
        cbb19fa Create index page.

COMMANDS USED SO FAR
----------------------------------------------
git init

git status

git add <file>

git commit -m ""

git log --oneline <file> (or no file)

git config --global user.name "name"

git config --global user.email "email"

1. Pull up a simplified log and checkout a previous repository snapshot
        $ git log --oneline
        $ git checkout <checksumID#>
    - The repository is now identical to what it was like when "Create orange and blue html pages" was committed.
    - this puts the tree in a "detached HEAD" state

2. Check out the very first revision
        $ git log --oneline
        $ git checkout <checksumeID#>

        Previous HEAD position was 46e2663 Create orange and blue html pages.
        HEAD is now at cbb19fa Create index page.

3. Check the log and the git status
    - note that there are no other present commits and the HEAD is detached
    - everything is fine, however, because the status shows that this is not the current state of the main branch, as it no longer says "on branch main" like previous statuses

        HEAD detached at cbb19fa
        nothing to commit, working tree clean

4. Return to the current version of the repository
        $ git checkout main
    - the working directory now matches the main branch
    - orange, blue, and index are updated

        Previous HEAD position was cbb19fa Create index page.
        Switched to branch 'main'

5. Tag the current state of the project as the latest stable release
        $ git tag -a v1.0 - "Stable version of the website" 
    - a tag delineates a project milestone via versions
    - the above is an annotated tag as indicated by the "-a" flag

6. Scrap the experimental site after viewing the first version 1.0 $ git checkout v1.0
        $ git revert <checksumID#>
    - all changes are reverted, but the changes are still stored
    - the commit message for the reverted commit will now be preceeded with "Revert ..."

                GIT LOG
    ----------------------------------------------    
        dfda58c (HEAD -> main) Revert "Add experimental revert page"
        4781460 Add experimental revert page
        7a3645a (tag: v1.0) Update README with tag instruction
        6a25791 Update README
        e304f33 Add navigation links.
        46e2663 Create orange and blue html pages.
        f870d73 Establish a procedure to efficiently initialze and maintain a clean repository.
        cbb19fa Create index page.

7. Add dummy.html, and create a nav link within index to that dummy page
    - it is not possible to revert this page as it is not committed, and therefore has no commit ID#

8. Undo the uncommitted changes to the snapshot $ git reset --hard
    - this undoes the modifications to a tracked file
    - without the --hard flag, the file would simply be unstaged
    - 'reset' only works within the staging area and working directory

                $ GIT RESET --HARD
    ----------------------------------------------
        HEAD is now at 5d52ff1 Update README with dummy.html instructions to undo uncommitted changes

9. dummy.html remains untracked, so delete it with $ git clean -f
    - both 'reset' and 'clean' operate on the working directory and are PERMANENT

COMMANDS USED SO FAR
----------------------------------------------
git checkout <commit-id>

git tag -a <tag-name> -m "<description>"

git revert <commit-id>

git reset --hard

git clean -f

----------------------------------------------
BRANCHES
----------------------------------------------

1. List the existing branches for this project $ git branch
    - the asterisk indicates that the branch is currently checked out
    - there are no branches at this time

        * main

2. View the git log and checkout the experimental page added for the revert
    - 'detached head' state means that any changes made to this branch will be discarded if not committed
    - Git calls the current checkout "HEAD"

3. Create a new branch named 'rainbow' $ git branch rainbow
    - while a branch was created, the branch is still not checked out

    * main
      rainbow

4. Checkout the rainbow branch and add rainbow styling to experimentalrevert.html

5. Stage and commit the newly styled experimentalrevert file to the rainbow branch
    - note that the git log shows that the current head is on the -> rainbow branch

                GIT LOG
    ----------------------------------------------
        6db5af8 (HEAD -> rainbow) Add rainbow text to experimentalrevert.html
        4781460 Add experimental revert page
        7a3645a (tag: v1.0) Update README with tag instruction
        6a25791 Update README
        e304f33 Add navigation links.
        46e2663 Create orange and blue html pages.
        f870d73 Establish a procedure to efficiently initialze and maintain a clean repository.
        cbb19fa Create index page.

6. Update the file name for experimentalrevert.html to rainbow.html
    - the file experimentalrevert.html is considered to be deleted
    - the replacement is now an untracked file

                GIT STATUS
    ----------------------------------------------
        On branch rainbow

        Changes not staged for commit:
        (use "git add/rm <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
            deleted:    experimentalrevert.html

        Untracked files:
        (use "git add <file>..." to include in what will be committed)
            rainbow.html

7. Tell Git to stop tracking experimentalrevert.html and to track rainbow.html
        $ git rm experimentalrevert.html
        $ git add rainbow.html
    - Git understands that the file is being renamed

                GIT STATUS
    ----------------------------------------------
    On branch rainbow
        Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
            modified:   README.md
            renamed:    experimentalrevert.html -> rainbow.html

8. Commit all changes with an appropriate message about changing file names and updating the README, then checkout the main branch and check its log
    - note that none of the commits on the rainbow branch are present within the main branch
    - they only share history until checksum ID 478

                GIT LOG (main)
    ----------------------------------------------
        3c6fcb5 (HEAD -> main) Update README with branch creation instructions
        a04c7af Update README with command list
        5d52ff1 Update README with dummy.html instructions to undo uncommitted changes
        dfda58c Revert "Add experimental revert page"
        4781460 Add experimental revert page
        7a3645a (tag: v1.0) Update README with tag instruction
        6a25791 Update README
        e304f33 Add navigation links.
        46e2663 Create orange and blue html pages.
        f870d73 Establish a procedure to efficiently initialze and maintain a clean repository.
        cbb19fa Create index page.

9. Create and checkout a CSS branch, and then add a CSS stylesheet to to the working directory

10. Commit the changes with the message "Add CSS stylesheet" 

11. Link the stylesheet to the html files and commit "Link HTML pages to stylesheet"

12. Merge the CSS branch to the main branch $ git merge css
    - this will only affect the main branch, as the css branch is already up to date with main
    - each HTML document has the style sheet linked, note the "1 +" line added to each
    - "fast-forward" means that the tip, or added commits, of the css branch is tacked onto the main branch
    - branch css is now a redundant branch

                $ git merge css
    ----------------------------------------------        
        Updating 3c6fcb5..ee1d1e0
        Fast-forward
        blue.html   |  1 +
        index.html  |  1 +
        orange.html |  1 +
        style.css   | 13 +++++++++++++
        4 files changed, 16 insertions(+)
        create mode 100644 style.css

                GIT LOG (main)
    ----------------------------------------------
        ee1d1e0 (HEAD -> main, css) Link HTML pages to stylesheet
        08027c0 Add CSS stylesheet
        3c6fcb5 Update README with branch creation instructions
        a04c7af Update README with command list
        5d52ff1 Update README with dummy.html instructions to undo uncommitted changes
        dfda58c Revert "Add experimental revert page"
        4781460 Add experimental revert page
        7a3645a (tag: v1.0) Update README with tag instruction
        6a25791 Update README
        e304f33 Add navigation links.
        46e2663 Create orange and blue html pages.
        f870d73 Establish a procedure to efficiently initialze and maintain a clean repository.
        cbb19fa Create index page.

13. Delete the redundant CSS branch $ git branch -d css
    - the css branch is now fully integrated, and is no longer differentiated from main
    - note that the rainbow branch is not affected

                GIT BRANCH
    ----------------------------------------------
        Deleted branch css (was ee1d1e0).
        * main
        rainbow

COMMANDS USED SO FAR
----------------------------------------------
git branch

git branch <branch-name>

git checkout <branch-name>

git merge <branch-name>

git branch -d <branch-name>

git rm <file>
