
I'm following Ry's Git Tutorial.
My object is to establish a procedure to efficiently initialze and maintain a clean repository. This is for my personal study.


----------------------------------------------
THE BASICS
----------------------------------------------
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

NEW COMMANDS
----------------------------------------------
git init

git status

git add <file>

git commit -m ""

git log --oneline <file> (or no file)

git config --global user.name "name"

git config --global user.email "email"


----------------------------------------------
UNDOING CHANGES
----------------------------------------------
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

NEW COMMANDS
----------------------------------------------
git checkout <commit-id>

git tag -a <tag-name> -m "<description>"

git revert <commit-id>

git reset --hard

git clean -f


----------------------------------------------
BRANCHES I
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

NEW COMMANDS
----------------------------------------------
git branch

git branch <branch-name>

git checkout <branch-name>

git merge <branch-name>

git branch -d <branch-name>

git rm <file>


----------------------------------------------
BRANCHES II
----------------------------------------------
1. Checkout the rainbow branch, and then $ git merge main
    - changes made to the main branch, like the CSS styling, need to be merged into the rainbow feature branch
    - modifications that affect the rainbow branch will be staged for commit
    - any conflicts will be noted and Git will request a manual resolve by the user

                GIT STATUS
    ----------------------------------------------
        On branch rainbow
        All conflicts fixed but you are still merging.
        (use "git commit" to conclude merge)

        Changes to be committed:
            modified:   README.md
            modified:   blue.html
            modified:   index.html
            modified:   orange.html
            new file:   style.css

2. Commit the changes git commit -m "Merge branch MAIN with RAINBOW"
    - styling added to the main branch has been been updated to the rainbow branch
    - note that the commit is only logged on the rainbow branch
    - this is a "3-way merge" as rainbow now has an ancestor, a 

        [rainbow fca04c9] Merge branch MAIN with RAINBOW

3. Link the CSS file to rainbow.html and commit the change

4. Link navigation to the rainbow page 

5. Fork an alternative rainbow topic branch $ git branch rainbow-alt
    - this branch is an experiment on the experiment

6. Modify rainbow.html and the stylesheet by changing from colorful text to a colorful background while on branch rainbow-alt

7. Git commit -a -m "Make a REAL rainbow"


HOTFIX
----------------------------------------------
1. Checkout the main branch, create a new branch called news-hotfix, and then check it out
    - a time-sensitive update is often required to a main project
    - rainbow and rainbow-alt will be unaffected

2. Add Indigo page news-1.html, link it to the index news section, link the stylesheet, and add a navigation link back to index from the Indigo page

3. Stage and commit all of these changes

3. Merge the news-hotfix branch with the main branch
    - this is a simple fast-forward merge
        $ git checkout main
        $ git merge news-hotfix

        Updating fc2ed2f..ad69016
        Fast-forward
        index.html  |  7 +++----
        news-1.html | 18 ++++++++++++++++++
        2 files changed, 21 insertions(+), 4 deletions(-)
        create mode 100644 news-1.html

4. Delete the news-hotfix branch
    - this branch is no longer needed
    - this is a simple, but safe, way to add updates to main

RETURN TO RAINBOW FEATURE BRANCH
----------------------------------------------
8. Checkout the feature branch rainbow, and add a news item to index.html 'Check out our new RAINBOW page!' that links to rainbow.html
    - clearly this will create conflict, as the news-hotfix branch merge modified these lines

9. Commit all changes and then merge rainbow to main
    - a merge conflict will require manual resolution
    - this manual was updated (no conflicts, just added lines), 
    - git uses these <<==>> symbols to indicate merge conflict locations
    - $ git diff in the CLI, vs code, and live site all have these symbols

                    GIT BRANCH (main)
    ----------------------------------------------
        Auto-merging index.html
        CONFLICT (content): Merge conflict in index.html
        Automatic merge failed; fix conflicts and then commit the result.

                    VS CODE
    ----------------------------------------------
 <!-- 
 <<<<<<< HEAD
            <li><a href="news-1.html"><em>Indigo is the way to go!</em></a></li>
    =======
            <li><em>Check out our new <a href="<a href="rainbow.html"><span style="color: red;">R</span><span style="color: #f90;">A</span><span style="color: rgb(228, 228, 9);">I</span><span style="color: rgb(134, 180, 42);">N</span><span style="color: rgb(13, 172, 172);">B</span><span style="color: rgb(98, 14, 158);">O</span><span style="color: rgb(105, 7, 105);">W</span></a> page!</em></li>
>>>>>>> rainbow
-->

10. Accept both changes in VS Code; stage and commit (no message) to resolve the conflict
    - no -m is required as git creates its own conflicts list
    - a commit is required after resolving a conflict resolution


                  GIT STATUS (pre-conflict resolution)
    ----------------------------------------------
        On branch main
        You have unmerged paths.
        (fix conflicts and run "git commit")
        (use "git merge --abort" to abort the merge)

        Changes to be committed:
            modified:   README.md
            modified:   blue.html
            modified:   orange.html
            new file:   rainbow.html

        Unmerged paths:
        (use "git add <file>..." to mark resolution)
            both modified:   index.html


                  GIT STATUS (post-conflict resolution)
    ----------------------------------------------
        On branch main
        All conflicts fixed but you are still merging.
        (use "git commit" to conclude merge)

        Changes to be committed:
            modified:   README.md
            modified:   blue.html
            modified:   index.html
            modified:   orange.html
            new file:   rainbow.html

11. Merge rainbow-alt (i like it better)

12. Clean up the feature branches
    - accidentally created a branch named 'checkout'
    - if any changes were present in 'checkout', the '-D' flag would be required as it is not merged with the main branch
    - rainbow no longer needed
        $ git branch -d rainbow
        $ git branch -d rainbow-alt
        $ git branch -D checkout

NEW COMMANDS
----------------------------------------------
$ git branch -d
$ git branch -D

