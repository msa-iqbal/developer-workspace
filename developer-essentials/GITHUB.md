
```
sudo apt update
sudo apt install git
```

# Git

**Git** is a distributed version control system used to track changes in source code during software development.

## 🟪🟦🟩 General

---

**❏❏❏ Check Git Version**

```powershell
git -v
```

**❏❏❏** Check if the username and email are set to get

```powershell
git config --get user.name  # By Username
git config --get user.email # By Email
```

**❏❏❏** How do you set the username and email address if they are not set correctly?

```powershell
git config --global user.name "YOUR_USER_NAME"
git config --global user.email "YOUR_EMAIL_ADDRESS"
```

Example:

```bash
git config --global user.name "msa-iqbal"
git config --global user.email "mdshahalamiqbal@gmail.com"
```

## 🟪🟦🟩 Stage & Commit

---

```plaintext
Working Directory → Stage → Local Repository
```

**❏❏❏ Step 1: Initializing a Git Repository**

To start using Git, you need to initialize a repository in your project folder.

Firstly, checking `.git` directory/folder already exists in the project.

(Go to the Project folder & open the terminal with the command)

```powershell
ls -a # Showing Hidden Folder & Files
```

If it doesn’t exist, `.git` directory, then initialize Git on your project below this command:

```bash
git init
```

**Explanation**: This command creates a new `.git` directory in your project, marking it as a Git repository.

**🛠️🛠️🛠️ Checking the Status of the Repository**

To see the current state of your repository and check which files have been modified or added.

```bash
git status
```

**Explanation**: Shows modified files, untracked files, and changes staged for commit.

**❏❏❏ Step 2: Adding Files to the Staging Area**

To prepare files for committing to the repository, use `git add`.

```bash
git add <filename>        # Adds a specific file
git add .                 # Adds all modified and untracked files
```

**Explanation**: Adds changes from your working directory to the staging area, making them ready to commit.

**🛠️🛠️🛠️ Remove the file or stop tracking a file added by mistake**

```powershell
git rm --cached [<options>] <pathspec>…

# Example: git rm --cached index.html

### Note: If you don't use "--cached", the file will be permanently deleted. 
```

What It Does:

- **Removes** the specified file(s) from the **index** (staging area)
- **Leaves** the file(s) untouched in your working directory
- Marks the removal to be recorded on the **next commit**

**❏❏❏ Step 3: Committing Changes**

After staging your files, you can commit the changes to the repository.

```bash
git commit -m "(messageTag) Your commit message" 

# Example:
# git commit -m "(feat) This is first message"
# git commit -m "(fix) fix the form validation"
```

**Explanation**: This command saves the changes in the repository with a descriptive message.

**🛠️🛠️🛠️ { Optional } Add and commit together in one go**

```bash
git commit -am "Your commit message"             # **Add All Changes & Commit (Single Line)**
# OR
git add . && git commit -m "Your commit message" # **Add All (including new files) & Commit
# OR**
git add index.html app.js && git commit -m "Updated homepage and app logic" 
```

**Summary Table**

|Command|Includes New Files|Includes Modified|Includes Deleted|
|---|---|---|---|
|`git commit -am`|❌|✅|✅|
|`git add .`|✅|✅|✅|
|`git add -A`|✅|✅|✅|

## 🟪🟦🟩 Undo & Reset

---

**Undo & Reset (Version Control)**

**❏❏❏ Step 1: Viewing the Commit History**

To see the list of commits made in the repository.

```bash
git log              # Will show a long description 
# OR
git log --oneline    # Will show a short description as single-single as simple
```

**Explanation**: Shows the commit history, including commit hashes, messages, author information, and timestamps.

**❏❏❏ Step 2: Reset to a specific commit**

Resets the **staging area** (index) to match that commit.

```bash
git reset --hard <commit-hash>

# Example: git reset --hard a034e97ecf6d54f1c7ec0d68d536cde4ce53bc57
```

**What It Does**

- **Moves the HEAD** to the specified commit.
- **Changes the index (staging area)** to match the commit.
- **Changes the working directory** to match the commit.
- **Deletes all changes** after that commit (both staged & unstaged).
- **Removes commits** from history that came after `<commit-hash>` (only in your local branch).

**🛠️🛠️🛠️ Recovery Or See the History of Commit Changing**

If you accidentally reset, you can still recover commits (before their garbage collected) using:

```bash
git reflog
```

Then find the commit hash you lost and recover:

```bash
# Example: git reset --hard <old-commit-from-reflog>
```

## 🟪🟦🟩 Branching

---

A **branch** is simply a movable pointer to a commit in your repository’s history. By default, you start on the **`main`** (or **`master`**) branch.

_Creating a new branch lets you diverge from the main line of development and work in isolation without affecting other branches._

![Figure: Git Branching](https://res.cloudinary.com/du7tjwbyi/image/upload/v1787766374/GitHub_Branch_Transparent_ezct3n.png "Figure: Git Branching")


**Why Use Branches?**

- **Isolation of work:** Develop features, bug‑fixes, or experiments safely.
- **Parallel development:** Multiple people or tasks can proceed independently.
- **Contextual clarity:** Branch names (e.g. `feature/login`, `hotfix/typo`) document intent.
- **Safe integration:** You can review, test, and merge only when ready.

```powershell
### List all branches
git branch                     # OR
git branch --list              # OR
git branch -a    

### Creates a new branch
git branch <branch_name>       

### Switches to an existing branch
git switch <branch_name>       # OR
git checkout <branch_name>     # OR
git checkout -b <branch_name>  # Creates and switches to a new branch

### Rename the branch. (Go to that branch and type the command)
git branch -m <branch_name>

### Delete Branch. (First, switch to a different branch, then delete the target branch)
git branch -d <target_branch_name>      # Normal Delete
#OR
git branch -D <target_branch_name>      # Permanent Delete
```

> বিঃ দ্রঃ: সাব-ব্রাঞ্চ গুলোতে কোনো ব্রাঞ্চে কোন ফাইলকে Stage এ তুলে Commit না করে রাখলে এবং এমতাবস্তায় যদি নতুন কোনো ব্রাঞ্চ তৈরী করা হয় তবে ওই নতুন ব্রাঞ্চটি Commit না হওয়া ফাইল গুলো দেখতে পাবে। অর্থাৎ কোন ফাইলকে Stage এ তুলে Commit না করলে সেটির পরিবর্তন গুলো নতুন ব্রাঞ্চ দেখতে পারবে।

**❏❏❏ Merging Branches**

To combine the changes from one branch into another.

Firstly, switch to the branch you want to merge into

```powershell
# Example: git checkout <target_branch>
```

এরপর আপনি অন্য যেকোনো ব্রাঞ্চ কে যদি কোনো নির্দিষ্ট ব্রাঞ্চ মার্জ করতে চান তবে,

- প্রথমে ঐ নির্দিষ্ট ব্রাঞ্চ এ যান। কারণ ঐটি আপনার টার্গেট ব্রাঞ্চ।
- এরপর কমান্ড টাইপ করুন:

```bash
git merge <source_branch>

# Example:  c/dir/gitProject (main_branch)>> git merge <source_branch>   
```

**Explanation**: This command merges the changes from the `source_branch` into the `target_branch`.

**🛠️🛠️🛠️ Merge Conflict Resolution**

A **merge conflict** happens when Git cannot automatically merge two branches because the same parts of the same file were changed differently in each branch.

**Example:**

If there's a conflict, Git will show a message like:

> _CONFLICT (content): Merge conflict in file.js_
> 
> _**Automatic merge failed; fix conflicts and then commit the result.**_

It means there's a conflict in `file.js`, and you’ll see something like this inside the file:

```
<<<<<<< HEAD
Your changes (current branch)
=======
Incoming changes (other branch)
>>>>>>> branch-name
```

You need to edit this part, choose which changes to keep, and remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

**Solution**:

**Manually Resolve the Conflict**

Edit the file to keep the desired changes. For example:

**Before**:

```jsx
<<<<<<< HEAD
let message = "Hello from main!";
=======
let message = "Hello from feature!";
>>>>>>> feature-branch
```

After:

```jsx
let message = "Hello from both sides!";
```

Then, **delete the conflict markers** (`<<<<<<<`, `=======`, `>>>>>>>`).

Once you’ve fixed the file(s), mark them as resolved: ( Add to Stage )

```bash
git add file.js
```

After adding all resolved files:

```bash
git commit -m "resolved the merge conflict"
```

Done!

You’ve successfully resolved the merge conflict!

**Best Practices**

- **Naming:** Use clear, consistent prefixes (`feature/`, `bugfix/`, `release/`).
- **Keep them short‑lived:** Merge back or often rebase to avoid large merge conflicts.
- **Clean up:** Delete stale branches after merging to avoid clutter.
- **Don’t rewrite published branches** (avoid `-force` on shared branches).

## 🟪🟦🟩 Git Stash

---

**Save Your Work Temporarily or Hidden Treasure**

`git stash` হলো এমন একটি উপায়, যার মাধ্যমে আপনি আপনার বর্তমান (এখনো কমিট না করা) পরিবর্তনগুলো অস্থায়ীভাবে সংরক্ষণ করতে পারেন। এর ফলে আপনি নির্বিঘ্নে অন্য কোনো কাজ করতে পারেন বা ব্রাঞ্চ পরিবর্তন করতে পারেন, পরিবর্তন হারানোর চিন্তা না করেই।

```bash
### Stash unstaged and staged changes ( বর্তমান পরিবর্তনগুলো সংরক্ষণ করে )
git stash                                           # OR                       
git stash save <current_branch> "related message"   # OR
git stash <current_branch> -a                       # Stash all files

### Show "Git Stash" Stack list
git stash list

### সর্বশেষ stash-এ কী পরিবর্তন আছে, তা দেখায়
git stash show           # OR
git stash show -p

### সর্বশেষ stash করা কাজ ফেরত আনে এবং মুছে ফেলে
git stash pop
```


