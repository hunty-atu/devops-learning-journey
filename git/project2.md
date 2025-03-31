## Project 2: Push and Pull projects from GitHub

## Push local changes to GitHub

- **Add all modified or new files to the repository**
    ```bash
    git add .
    ```

- **Note the change whilst committing to the repository**
    ```bash
    git commit -m "Added HelloLYIT.java"
    ```

- **Push the changes from the local master to the remote origin**
    ```bash
    git push -u origin master
    ```

- **Ensure that all commits are made**
    ```bash
    git status
    ```

## Problems

- **If there is a problem with origin, it can be removed**
    ```bash
    git remote rm origin
    ```

- **If GitHub shows zero contributors, it is because you pushed using a username that is not your GitHub username. To fix:**
    ```bash
    git config --global user.name "my-github-username"
    git config --global user.email "my-github-email"
    ```

# Pulling from an Existing Project

## Steps to follow:

1. **Create a folder assignmentFolder**
    ```bash
    cd ..
    mkdir testFolder
    ```

2. **Change directory into that folder**
    ```bash
    cd testFolder/
    ```

3. **Initialize the folder for git Repo**
    ```bash
    git init
    ```

4. **Link the local Repo to GitHub**
    ```bash
    git remote add origin https://github.com/AWS-Devops-Projects
    ```

5. **Pull a copy of the existing work on GitHub to the local Repo**
    ```bash
    git pull origin master
    ```

## More Sample Projects

- GitHub DevOps Projects Topic
- TechiesCamp DevOps Projects
- AWS DevOps Projects