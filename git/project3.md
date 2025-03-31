# Project 3: Create Clone & Create Branching


**Cloning the Repository**
Open Git Bash and create a directory named uni:
 mkdir uni
 cd uni
 ```

**Clone the repository:**
 git clone https://github.com/mariagriffin/Spring_uni
 cd Spring_uni
 ```

**Creating a Branch**
Check the status of Git:
 git status
 ```

**Create a new branch using your student number (e.g., l0012345Branch):**
 git checkout -b l0012345Branch
 ```

**Adding and Committing Changes**
Create a file named l0012345.md with the content 12345:
 echo "12345" > l0012345.md
 ```

**Add the file to the staging area:**
 git add .
 ```

**Commit the changes to the local repository:**
 git commit -m "Added l0012345.md"
 ```

**Pushing Changes to Remote**
Check the status to ensure the branch is clean:
 git status
 ```

**Push the branch to the remote repository:**
git push origin l0012345Branch


**Merging Changes**
Pull the latest changes from the main branch:
git pull origin main


**Switch to the main branch:**
git checkout main


**Merge your branch into the main branch:**
git merge l0012345Branch


**Push the merged changes to the remote repository:**
git push origin main


**Viewing Changes**
Refresh the GitHub page to see your new branch and file.