# Notes for My PUSH & PULL

## First Program

A Java file is created using Notepad (use any editor).

```bash
git add .
is used to add all modified or new files to the repository.

git commit -m "Added HelloLYIT.java"
is used to note the change whilst committing to the repository.

git push -u origin master
pushes the changes from the local master to the remote origin.

git status
is run to ensure that all commits are made.

public class HelloATU {
    public static void main(String[] args) {
        // Prints "Hello, ATU from Maria" as output
        System.out.println("Hello, ATU from Maria");
    }
}
In this way, files can be added to the repository and the changes are reflected in the remote repository. Open the browser and refresh the page. The new Java file is available on the remote repository.

Now that pushing data to the repository can be seen, it is clear why GitHub can be very useful to a development team.

Problems
If there is a problem with origin, it can be removed using:

git remote rm origin
If GitHub shows zero contributors, it is because you pushed using a username that is not your GitHub username. To fix:

git config --global user.name "my-github-username"
git config --global user.email "my-github-email"
Pulling from an Existing Project
Create a folder assignmentFolder (NOT IN THE DEMO FOLDER!!) and change directory into that folder.
Initialize the folder as a Git repository.
Use git remote add to link the local repository to the remote repository on GitHub.
Pull a copy of files and folders from the remote directory onto the local directory.
Congratulations, you have successfully ‘pulled’ down a project from GitHub!!

Push Local Changes to the Remote Repository
In this example, changes are made to the local repository and then pushed up to the remote repository.