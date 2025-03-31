# Project 2: Push and Pull local changes to GitHub

### Steps


1. **Add all modified or new files to the repository**
    ```bash
    git add .
    ```

2. **Note the change whilst committing to the repository**
    ```bash
    git commit -m "Added HelloLYIT.java"
    ```

3. **Push the changes from the local master to the remote origin**
    ```bash
    git push -u origin master
    ```

4. **Ensure that all commits are made**
    ```bash
    git status
    ```

## Pulling from an Existing Project

## Steps to follow:

5. **Create a folder assignmentFolder**
    ```bash
    cd ..
    mkdir testFolder
    ```

6. **Change directory into that folder**
    ```bash
    cd testFolder/
    ```

7. **Initialize the folder for git Repo**
    ```bash
    git init
    ```

8. **Link the local Repo to GitHub**
    ```bash
    git remote add origin https://github.com/AWS-Devops-Projects
    ```

9. **Pull a copy of the existing work on GitHub to the local Repo**
    ```bash
    git pull origin master
    ```

    ## Problems

10. **If there is a problem with origin, it can be removed**
    ```bash
    git remote rm origin
    ```

11. **If GitHub shows zero contributors, it is because you pushed using a username that is not your GitHub username. To fix:**
    ```bash
    git config --global user.name "my-github-username"
    git config --global user.email "my-github-email"
    ```

## More Sample Projects

- GitHub DevOps Projects Topic
- TechiesCamp DevOps Projects
- AWS DevOps Projects