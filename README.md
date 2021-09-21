
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
    - a tag delineates a project milestone via versions