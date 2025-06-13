# git-workshop

This repository is created to let interns understand git and github and give them hands-on experience on it.

Git vs GitHub
=============

## 🔍 Git vs GitHub — What's the Difference?

| Feature           | **Git**                                           | **GitHub**                                                   |
|-------------------|---------------------------------------------------|---------------------------------------------------------------|
| **What it is**    | A **local version control system**                | A **cloud-based hosting platform** for Git repositories       |
| **Who owns it**   | Open-source, maintained by the Git community      | Owned by Microsoft                                            |
| **Purpose**       | Tracks code changes locally                       | Enables **collaboration**, **sharing**, and **management** of Git projects |
| **Where it runs** | On your **local machine**                         | On the **web (cloud platform)**                               |
| **Command-line?** | Yes (terminal/CLI or GUI)                         | Mostly GUI, but also CLI/API support                          |
| **Key Features**  | - Commit history<br>- Branching<br>- Merging<br>- Stashing<br>- Rebase | - Remote repos<br>- Pull Requests<br>- Issues<br>- Reviews<br>- CI/CD via Actions |
| **Example Use**   | `git commit -m "fix: update footer"`              | Creating a Pull Request for review on GitHub                  |

<br />

### 🧠 In Simple Words:

- **Git** is a **tool** to track code changes locally.
- <a href="http://git-scm.com/about">http://git-scm.com/about</a>
- **GitHub** is a **website** where developers host and collaborate on Git repositories.
- <a href="https://github.com/">https://github.com/</a>
<br /><br />
---
<br /><br />

## Getting Git

Before we dive into version control, let's make sure Git is installed and configured on your system.

### 🐧 For **Linux (Debian/Ubuntu)**

1. Open your terminal.
2. Run the following commands:
   ```bash
   sudo apt update
   sudo apt install git -y
3. Verify Installation:
   ```bash
   git --version

### 🍎 For **Mac OS**

1. Open your terminal.
2. Install Homebrew (if not already):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
3. Install Git
   ```bash
   brew install git
4. Verify Installation:
   ```bash
   git --version



## Setup

First thing to do is to setup your identity. This identifies you to
other people who download the project.

    git config --global user.name "Your Name"
    git config --global user.email your.email@example.com

Verify your config using:

    git config --list


<br /><br />

## 🔐 Use SSH with Git

SSH (Secure Shell) is a secure cryptographic protocol used to **authenticate and communicate securely** between two systems over a network.

<br />

### 💼 Common Use Cases of SSH in Git/GitHub

| Use Case                             | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| ✅ **Password-less Authentication**  | Avoid entering your GitHub username/password every time you push/pull.     |
| 🔐 **Secure Data Transfer**          | All data is encrypted between your system and GitHub over SSH.             |
| 🔄 **Push/Pull Git Repos**           | Use `git push` and `git pull` securely over SSH.                           |
| 🧑‍💻 **Automated Scripts/CI Systems** | SSH keys are used in scripts or CI/CD pipelines for accessing private repos without manual intervention. |
| 🤝 **Multiple Accounts/Devices**     | Developers managing multiple GitHub accounts or devices can configure SSH identities for each. |
| 🏢 **Enterprise Git Servers**        | Many companies use self-hosted Git (e.g., GitLab, Bitbucket) with SSH access for security. |
| 🌍 **Remote Server Access**          | SSH is also commonly used for logging into remote servers (like AWS EC2, VPS, etc.). |

<br />

### 🔧 HTTPS vs SSH in Git

| Feature               | **HTTPS**                                     | **SSH**                                     |
|-----------------------|-----------------------------------------------|---------------------------------------------|
| Authentication        | Username + password / token                   | SSH key pair (private + public)             |
| Password prompts      | Often required (unless token cached)          | No prompt after initial setup               |
| Security              | Encrypted, but credentials are sent each time | Encrypted, more secure after first setup    |
| Setup complexity      | Easy (out-of-the-box)                         | Slightly more setup (generate + add key)    |
| Best For              | Beginners, quick setups                       | Developers, long-term usage, automations    |

<br />

### 🧠 Real-World Scenarios
- ✅ Push code to GitHub in your daily development workflow
- 🔄 Sync changes with a team repo without typing passwords
- 🤖 Automate deployments using CI/CD (GitHub Actions, Jenkins)
- 📁 Access private GitHub repositories from cloud servers
<br />

**In short:** SSH is the developer’s trusted key for secure, automated, and seamless workflows.


### 🛠️ Generate a New SSH Key
1. Generate a New SSH Key
   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   Press Enter to accept the default file path.<br />
   Optionally add a passphrase (or press Enter to skip[recommended as of now])

2. Start the SSH Agent
   ```bash
   eval "$(ssh-agent -s)"

3. Add your new key
   ```bash
   ssh-add ~/.ssh/id_rsa

4. Copy the SSH Public Key
   ```bash
   cat ~/.ssh/id_rsa.pub

5. Add SSH Key to GitHub

   Go to: <a href="https://github.com/settings/keys">https://github.com/settings/keys</a>

   Click "New SSH key"

   Add a title (e.g., "My Laptop")

   Paste your public key (id_rsa.pub)

   Click "Add SSH key"

6. Test Your SSH Connection

   Run:
   ```bash
   ssh -T git@github.com
   ```
   If successful, you’ll see:
   ```bash
   Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.


<br />

--------
<br /><br />

## Starting your journey


### Clone a Repository 

First, clone this repository:

    git clone https://github.com/jtg-inductions-fe/git-workshop

You may want to fork (create your own copy of) the project on github and
clone from your own repo. You can find the fork button at the top right of
the screen on a github repository, or more help about doing that [here](https://help.github.com/articles/fork-a-repo/).

Once you have cloned your repository, you should now see a directory
called `jtg-fe-git-workshop`. This is your `working directory`

    cd jtg-fe-git-workshop
    ls

<br />

For the curious, you should also see the `.git` subdirectory. This is
where all your repository’s data and history is kept.

    ls -a .git

You will see :

    branches  config  description  HEAD  hooks  info  objects  refs

<br />

### Fetch a branch

`git fetch` downloads changes (like new commits, branches, and tags) from the remote repository to your local repository, but without merging them into your working branch.

When you run:
  ```bash
  git fetch origin
  ```

Git fetches all branches and updates your local references to the remote ones (like origin/main, origin/dev, etc.).

But if you want to fetch only one specific branch instead of all, you can do:
  ```bash
  git fetch origin branch-name
  ```

What This Does:
1. It downloads only the latest commits from the branch-name branch on the origin remote.

2. It updates your local reference to origin/branch-name.

3. It does not create a new local branch or switch to it.

<br />


### Branching and Checking out

Most large code bases have at least two branches - a ‘live’ branch and a
‘development’ branch. The live branch is code which is OK to be deployed
on to a website, or downloaded by customers. The development branch
allows developers to work on features which might not be bug free. Only
once everyone is happy with the development branch would it be merged
with the live branch.

List all branches:
  ```bash
  git branch
  ```

The `*` should indicate the current branch you are on, which is
`main`.

Create a branch:
  ```bash
  git branch branch-name
  ```  

Switch to an existing branch:
  ```bash
  git checkout branch-name
  ```

Creating and Switching to a branch:
  ```bash
  git checkout -b branch-name
  ```

<br />

### Adding Changes

Now, let’s try adding some files into the project. Create a couple of
files.

Let’s create two files named `bob.txt` and `alice.txt`.

    touch alice.txt bob.txt

Add some data into these files.

Track a new file:
  ```bash
  git add filename.txt
  ```

Track all changes:
  ```bash
  git add .
  ```

<br />


### The staging area

In Git, you first add content to the `staging area` by using `git add`.
This is like putting the stuff you want to send into a cardboard box.
You finalize the process and record it into the git index by using
`git commit`. This is like sealing the box - it’s now ready to send.


Files added using git add are placed into the staging area.
This allows you to prepare a commit with only selected changes.

Check staged and unstaged changes:
  ```bash
  git status
  ```

<br />

### Committing

You are now ready to commit. The `-m` flag allows you to enter a message
to go with the commit at the same time.

    git commit -m "I am adding two new files"


#### Let’s see what just happened

We should now have a new commit. To see all the commits so far, use:

    git log

The log should show all commits listed from most recent first to least
recent. You would see various information like the name of the author,
the date it was commited, a commit SHA number, and the message for the
commit.

<br />


### Stash

Git is good enough to handle your files when you switch between
branches. Switch back to the `main` branch

Try switching back to the main branch (Hint: It’s the same command we
used to switch to the exp1 branch above)

Now, where’s our `alice.txt` and `bob.txt` files ?

    ls
  README.md

As you can see the new file you created in the other branch has
disappeared. Not to worry, it is safely tucked away, and will re-appear
when you switch back to that branch.

Now, switch back to the exp1 branch, and check that the `alice.txt` and `bob.txt`` are now present.

<br />

Sometimes you're working on something but suddenly need to:

1. Switch to another branch

2. Pull the latest changes

3. Do a quick fix elsewhere

…but you don’t want to commit unfinished work yet.
This is where `git stash` helps!


<br />

`git stash` temporarily hides your uncommitted changes (both staged and unstaged) and gives you a clean working directory. You can then reapply the changes later.

Use:
  ```bash
  git stash
  ```
1. Stashes all changes (tracked files) and resets your working directory.

2. Good before switching branches without committing.

To stash untracked (new) files as well:
  ```bash
  git stash -u
  ```

<br />

View Stash List:
  ```bash
  git stash list
  ```

When you're ready to resume your work:
  ```bash
  git stash apply
  ```
This re-applies the most recently stashed changes but keeps them in the stash list.

Or:
  ```bash
  git stash pop
  ```
This re-applies the most recent stash and removes it from the stash list.


Apply a Specific Stash:
  ```bash
  git stash apply stash@{1}
  ```

Delete a specific stash:
  ```bash
  git stash drop stash@{1}
  ```

Delete all stashes:
  ```bash
  git stash clear
  ```

<br />

### Pushing

Now we will push our local commit to the remote repository for everyone to see and checkout:
  ```bash
  git push origin branch-name
  ```

Now go checkout the github repository and you'll see your branch pushed to it. You can create a PR from it and let others review it and then merge it after approval.

<br />

### Merging

We now try out merging. Eventually you will want to merge two branches
together after the conclusion of work.
`git merge` allows you to do that.

Git merging works by first switching the branch you want to *into*, and
then running the command to merge the other branch in.

We now want to merge our `branch-2` branch into `branch-1`. First, switch to
the `branch-1` branch.

    git checkout branch-1

Next, we merge the `branch-2` branch into `branch-1` :

    $ git merge branch-2

Do you see the following output ?

    Merge made by recursive.
     test.txt |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)
     create mode 100644 bob.txt

You have to be in the branch you want merge *into* and then you always
specify the branch you want to merge.

<br />


### Pulling changes from a branch
Pull is used to update your local branch with changes from the remote repository (like GitHub).

It does two things in one step:
  ```bash
  git pull origin branch-name
  ```

This is equivalent to:
  ```bash
  git fetch origin branch-name   # Step 1: Get latest changes
  git merge origin/branch-name  # Step 2: Merge them into current branch
  ```

### Conflicts

Git is pretty good at merging/pulling/rebasing automatically, even when the same file is edited. There are however, some situations where the same line of code is edited there is no way a computer can figure out how to pick. This will trigger a conflict which you will have to fix.

We now practice fixing merge conflicts. Recall that conflicts are caused
by merges which affect the same block of code.

Here’s a branch I prepared earlier. The branch is called `JUNE-2025`. I will push some code into it with same alice.txt file. This create conflicts in your PRs as you were working on the same file and content was different.

#### Fixing a conflict

You should see a `conflict` with the `alice.txt` file. This means that
the same line of text was edited and committed on both the main branch
and the `June-2025` branch. The output below basically tells you the current
situation :

    Auto-merging alice.txt
    CONFLICT (content): Merge conflict in alice.txt
    Automatic merge failed; fix conflicts and then commit the result.

If you open the `alice.txt` file, you will see something similar as
below:

    <<<<<<< HEAD
    Some text entered by you
    =======

    Some text entered by Me
    >>>>>>> JUNE-2025

Git uses pretty much standard conflict resolution markers. The top part
of the block, which is everything between `<<<<<< HEAD` and `======` is
what was in your current branch.\
The bottom half is the version that is present from the `JUNE-2025` branch.
To resolve the conflict, you either choose one side or merge them as you
see fit.

For example, I might decide to choose the version from the `JUNE-2025`
branch.

Now, try to **fix the merge conflict**. Pick the text that you think is
better.

Once I have done that, I can then mark the conflict as fixed by using
`git add` and `git commit`

Congratulations. You have fixed the conflict. All is good in the world.

<br />

### Rebase

Rebase is used to move or combine a sequence of commits from one branch onto another.
It gives your project history a linear and cleaner structure by avoiding unnecessary merge commits.

| Action       | Result             | Commit History                           |
| ------------ | ------------------ | ---------------------------------------- |
| `git merge`  | Combines branches  | Keeps all commits, creates merge commits |
| `git rebase` | Moves your commits | Linear history, no merge commits         |


When to Use Rebase
1. Before pushing a feature branch: rebase it on the latest main to integrate changes cleanly.

2. To squash or tidy up your commit history before merging.

3. When you want to avoid merge commits and keep commit history readable.


Steps to rebase:
1. Checkout your branch

2. Add command:
   ```bash
   git rebase JUNE-2025

3. If there are conflicts, Git will pause and ask you to fix them.
Fix the files. Then:
   ```
   git add .
   git rebase --continue

4. If needed, you can abort the rebase at any time:
   ```bash
   git rebase --abort

If done correctly, you'll be successfully able to rebase your branch.

<br />

### Interactive Rebase

Use to edit, squash, or reword commits.

```bash
git rebase -i HEAD~3
```


This will open an interactive editor:
```bash
pick abc123 First commit
pick def456 Add login form
pick ghi789 Fix styles
```

You can change pick to:
1. reword: Edit commit message
2. edit: Edit the commit itself
3. squash: Combine into previous commit
4. drop: Get rid of the commit

<br />

### Undoing Changes

In this section, we are going to add more changes, and try to recover
from mistakes.

Open `alice.txt` and type in:

Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit
voluptatem accusantium doloremque laudantium

Then **save** the file

What did we change? A very useful command is `git diff`. This is very
useful to see exactly what changes you have done.

    git diff

You should see something like the following:

    diff --git a/alice.txt b/alice.txt
    index e69de29..2aedcab 100644
    --- a/alice.txt
    +++ b/alice.txt
    @@ -0,0 +1 @@
    +Lorem ipsum Sed ut perspiciatis, unde omnis iste natus error sit voluptatem accusantium doloremque laudantium



Now let’s add our modified file, `alice.txt` to the staging area. Do you
remember how ?

Next, check the `status` of `alice.txt`. Is it in the staging area now?



git reset is used to undo changes in your Git history. You can:

1. Unstage files

2. Move the HEAD pointer to a previous commit

3. Completely erase commits from history (careful!)

Depending on the mode used (--soft, --mixed, or --hard), it affects your staging area, working directory, and commit history differently.


| Mode      | Affects Staging? | Affects Files? | Use Case                                             |
| --------- | ---------------- | -------------- | ---------------------------------------------------- |
| `--soft`  | ✅ Yes            | ❌ No           | Undo commit but keep staged changes                  |
| `--mixed` | ✅ Yes (default)  | ❌ No           | Unstage changes but keep in working dir              |
| `--hard`  | ✅ Yes            | ✅ Yes          | **Dangerous**: Undo everything, delete local changes |

#### Reset file from stage

Let’s say we did not like putting Lorem ipsum into `alice.txt`. One
advantage of a staging area is to enable us to back out before we
commit - which is a bit harder to back out of. It’s easier to take mail out of the cardboard box before you seal it than after.

Here’s how to back out of the staging area :

    git reset HEAD alice.txt

    Unstaged changes after reset:
    M   alice.txt

Compare the `git status` now to the git status from the previous
section. How does it differ?

Your staging area should now be empty. What’s happened to the Lorem
Ipsum changes? It’s still there. We are now back to the state just
before we added this file to staging area. Going back to the mail
analogy, we just took our letter out of the box.


#### Reset the Last Commit (but keep changes staged)

```bash
git reset --soft HEAD~1
```


<br />

Thanks! If you have doubt after the session or stuck somewhere sync with your mentors.