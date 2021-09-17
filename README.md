
I'm following Ry's Git Tutorial, a guide I found while desperately searching Google.
My object is to establish a procedure to efficiently initialze and maintain a clean repository.

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

5.  Take a Snapshot $ git commit -m "Create index page."
    - index.html has been committed to the main branch
    - The "-m" should be a brief message about what the commit accomplishes
    - Do not use a passive voice for the message.
    

