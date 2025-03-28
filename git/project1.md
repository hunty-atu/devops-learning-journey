# GIT Basic Commands

## Local Version Control

**Created on:** 28/03/2025
**Created with:** Git 2.46.0  
**Tested On:** Windows 11  

### Steps

1. **Open Git Bash on your machine**.

2. **Create a new folder** called `demo` and then change into that folder:
    ```bash
    mkdir demo
    cd demo
    ```

3. **Initialize the Git repository** using the command:
    ```bash
    git init
    ```

4. **Create a `README.md` file** using Notepad with two comment lines:
    ```markdown
    # README.md
    This is a demo project for Git commands.
    ```

5. **Save the file** and add it to the staging area:
    ```bash
    git add README.md
    ```

6. **Commit the file** with a message:
    ```bash
    git commit -m "Add README.md"
    ```

7. **Check the status** of your repository:
    ```bash
    git status
    ```

8. **Create a `LICENCE.md` file** using Notepad:
    ```markdown
    # LICENCE.md
    This is the license file for the demo project.
    ```

9. **Add all changed files** to the staging area:
    ```bash
    git add .
    ```

10. **Commit the files** with a message:
    ```bash
    git commit -m "Add LICENCE.md"
    ```

11. **Edit `README.md`** in Notepad and add a line of text.

12. **Check the status** to see the file is modified:
    ```bash
    git status
    ```

13. **Add the changes** to the staging area:
    ```bash
    git add .
    ```

14. **Commit the changes**:
    ```bash
    git commit -m "Update README.md"
    ```

15. **Unstage a file** if you added it by mistake:
    ```bash
    git reset README.md
    ```

16. **Revert to the last good version** of the file:
    ```bash
    git checkout -- README.md
    ```

17. **Find the commit ID** using:
    ```bash
    git log --oneline
    ```

18. **Revert to a previous commit**:
    ```bash
    git reset <commit_id> --hard
    ```

19. **Push your changes** to GitHub:
    ```bash
    git remote add origin <your_repository_url>
    git push -u origin master
    ```

These examples work with Git. Remember that Git commands shown here provide version control on your local copy only.