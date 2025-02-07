## Check IntelliCode

1. **Open Extensions**: Press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (Mac) to open the Extensions view.
2. **Search for IntelliCode**: Type "IntelliCode" in the search bar and ensure the extension is installed and enabled.
3. For Bash scripts, you might also want to install the **"Bash IDE"** extension, which provides language support for Bash, including code completion and other IntelliSense features.
## Fixing Directory Structure

If you accidentally nested directories and need to move files up one level, follow these steps:

1. **Navigate to the nested directory**:
   ```bash
   cd C:\Users\hunts\Documents\devops-learning-journey\devops-learning-journey

step.1 	mv -i * ../
step.2	cd ..
step.3	rm -r devops-learning-journey
