# GitHub Basics 🐈‍⬛

<h2>Table of Contents</h2>

- [What is GitHub?](#what-is-github-)
- [How Does it Work?](#how-does-it-work-)
- [What are "Branches"?](#what-are-branches-)
- [Getting Started with GitHub + Git](#getting-started-with-github--git-)
- [Commands](#commands-)
- [Keywords](#keywords-)
- [Feedback](#feedback-)
<br>

## What is GitHub? 🌸
[GitHub](www.github.com) is a website that stores your code and projects.
- It's like Google Drive, but for your code.
- Code is stored in **`repositories`**, and you can share your repositories and collaborate with others.
- GitHub can also be used as a portfolio to showcase your projects!
<br>

## How Does it Work? 🌸
GitHub runs on [Git](https://git-scm.com/), which is a tool used for **`version control`**.
- It stores versions of your code that you have "pushed" to the repositories. These "pushes" are called **`commits`**.
- You will be able to see all your past commits.
- If you accidentally push code that breaks everything, you can roll back to a previous commit where everything was still working!
<br>

## What are "Branches"? 🌸
In Git, you have **`branches`**, and you will start with a **`main`** branch. It's important that the **`main`** branch **always** has working code.

> 🖤 Older repositories will name the branch **master** instead of **main**, but now its best practice to use **main**.

When you want to add a new feature, you create a branch that branches off from **`main`**. You now have the same code as main, but it's separate so you can experiment and break things.

<img src="/images/git-branch.jpg" style="border:solid 1px">

When you have completed your feature and it's working, you can merge your branch back into main.
<br>
<br>
## Getting Started with GitHub + Git 🌸
1. Create a GitHub account.
    <br>
2. Navigate to the **`Repositories`** tab at the top, and click the **`New`** button. This will open a form to create a new repository.
    <div align=center>
        <img src="/images/new-repo-btn.jpg" height="50px">
    </div>
    <br>
3. To create the repository:
    - call it anything! but use kebab-case for the name,
    - include a **`README.md`**,
    - add a **`.gitignore`** and choose the template of whatever language or IDE you're using (this can be added later as well),
    - choose whether you want it to be public or private,
    - and click **`Create Repository`**!!
    <br>
4. Once your repository is created, click the green **`Code`** button at the top, and copy the link it gives you under the **`HTTPS`** tab and save it somewhere:
    <div align=center>
        <img src="/images/git-clone.jpg" height="300px">
    </div>
    <br>
5. Install [Git](https://git-scm.com/downloads) (not required for Mac users usually):
    1. go through the installation process and choose all the recommended settings,
    2. and make sure your main branch is called main and NOT master (this should now be defaulted to main anyway)
    <br>
6. Cloning and setting up your repo: Open your **`terminal`**, you can do this by searching it in your PC's start bar.
    1. Check git installed correctly by running this command:
        ```bash
            git --version
        ```
    2. Set your git username and email (the details you used when you created your account)  (run these one at a time):
        ```bash
            git config --global user.name "Your Name"
            git config --global user.email "you@example.com"
        ```
    3. Create a folder somewhere to hold all your future projects, then navigate to it:
        ```bash
            mkdir Projects && cd Projects
        ``` 
    4. Clone your repo using the URL you copied earlier, e.g.:
        ```bash
            git clone https://github.com/yourname/yourrepo
        ```
    5. Navigate into your repo's folder:
        ```bash
            cd yourrepo
        ```
        <br>
7. Now it's time to push your first commit to GitHub! 🌸  
   We’ll keep it simple and just push a small change to the `main` branch.

   1. Open the `README.md` file in VS Code, Notepad, or any text editor.
   2. Add a line! Just type something like `“This is my first GitHub project”`
   3. Save the file and go back to your terminal.
   4. Run `git status` to see the changes.
   5. (Optional) Run `git diff` to view what exactly changed.
   6. Staging is just preparing your files to be pushed to the repository. Stage your changes with:
      ```bash
      git add README.md
      ```
      or just:
      ```bash
      git add .
      ```
   7. Commit your changes with a message:
      ```bash
      git commit -m "Update README with a cute message 🌸"
      ```
   8. Push it to GitHub!
      ```bash
      git push
      ```
    > **🖤 FOR NEXT TIME:** Before pushing next time, remember to pull any new changes using:
        **`git pull`**
        This helps prevent conflicts, especially if you've made changes on GitHub directly, or you're collaborating with others. Even if you're working solo, it's a good habit to **`pull`** before every **`push`**.


**That’s it!** 💕 Refresh your repository on GitHub and you’ll see your first commit there! 😁

   > 🖤**Tip:** The **`README.md`** is your project's intro page. You can write what the project does, how to install it, features, goals, or anything you want!
<br>

## Commands 🌸

<details>
    <summary>Click to expand Git commands 🖤</summary>
<h3> Git </h3>

- **`git clone [url]`** – copies a GitHub repository onto your computer so you can work on it locally.  

- **`git init`** – turns a normal folder into a Git repository so Git can start tracking changes.  

- **`git add [file/folder]`** – stages specific changes (adds them to the "ready to commit" list).  

- **`git add .`** – stages ALL changes (be careful with this, as you may not want to stage all your changes).  

- **`git commit -m "message"`** – saves a snapshot of your changes with a message.  

- **`git push`** – sends your commits to the remote repository (e.g., GitHub).  

- **`git pull`** – brings the latest changes from GitHub into your local project.  

- **`git pull --rebase`** – similar to `git pull` but avoids extra merge commits.  

- **`git status`** – shows which files have been changed and whether they’re staged.  

- **`git branch`** – lists all branches in your project.  

- **`git checkout [branch]`** – switches to a different branch.  

- **`git checkout -b [branch]`** – creates a new branch **and** switches to it.  

- **`git merge [branch]`** – merges the specified branch into your current one.  

- **`git stash`** – temporarily saves your uncommitted changes (so you can switch branches safely).  

- **`git stash pop`** – restores the changes you stashed earlier.  

- **`git log`** – shows a history of your commits.  

- **`git remote -v`** – shows the GitHub URL(s) your project is connected to. 

- **`git reset --hard HEAD`** – resets all changes and returns to the last commit.  

</details>

<details>
    <summary>Click to expand Terminal commands 🖤</summary>
<h3> Terminal </h3>

_These are commands you type into your terminal or command line — not Git-specific, but super useful!_

- **`cd foldername`** – moves into a folder.

- **`cd ..`** – moves out of current folder.

- **`ls`** – lists everything in the current folder.

- **`mkdir foldername`** – creates a new folder.

- **`touch filename.txt`** – creates a new file.

- **`code .`** – opens the current folder in VS Code (only works if VS Code is installed properly). 

</details>
<br>

## Keywords 🌸

- **branch** – a separate line of work in your project. Useful for trying out new features without touching your main code.

- **commit** – a saved snapshot of your code at a specific moment.

- **push** – sending your saved changes (commits) to GitHub.

- **rollback** – going back to a previous version of your code if something breaks.
<br>

## Feedback 🌸
If you found this useful, have suggestions, or just want to chat, feel free to send me a message! 🖤

- tiktok: [@nahdaaj](https://tiktok.com/@nahdaaj)
- github: [@nahdaaj](https://github.com/nahdaaj)
- personal website: [nahdaajawed.com](https://nahdaajawed.com/)
