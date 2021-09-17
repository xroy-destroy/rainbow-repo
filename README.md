
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

4. Stage a Snapshot $ git add index.html & check it $ git status
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

9. Stage & commit $ git -m "Create blue and orange pages."

