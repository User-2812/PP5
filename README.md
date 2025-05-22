# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
-git branch feature-1
-git checkout feature-1
;Switched to branch ˋfeature-1ˋ
-vim feature.txt
-git commit --m feature.txt
;On branch feature-1
;Untracked files:
;(use "git add <file>..." to include in what will be committed)
feature.txt
;nothing added to commit but untracked files presant (use "git add" to track)
-git commit feature.txt
;error: pathspec ˋfeature.txtˋ dit not match any file(s) known to git
-git add feature.txt
-git commit --m teature.txt
;[feature-1 dde7258] feature.txt
; 1 file changed, 0 insertions(+), 0 deletions(-)
;create mode 100644 feature.txt
-git branch --list
;*feature-1
; master
-git checkout master
;Switched to branch ˋmasterˋ
-git merge feature-1
;Updating 001422c..dde7258
;Fast-forward
;feature.txt |0
;1 file changed, 0 insertions(+), 0 deletions(-)
;create mode 100644 feature.txt
-git log
;commit dde72580a36ac26e2bc5fd2c8ea336f8e852fa89 (HEAD->master,feature-1)
;Author: User-2812 <wrobla28@stud.thga.de>
;Date: Tue May 20 17:54:21 2025 +0200

; feature.txt

# and the relevant terminal output (e.g., branch listing, merge messages)
```

---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
user-2812@Desktop:~/PP5$ git push origin-ssh master
user75@128.140.85.215's password:
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 4 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.01 KiB | 1.01 MiB/s, done.
Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
To 128.140.85.215:~/repos/myproject.git
 * [new branch]      master -> master

user-2812@Desktop:~/PP5$ git clone user75@128.140.85.215:~/repos/myproject.git myproject-clone
Cloning into 'myproject-clone'...
user75@128.140.85.215's password:
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (2/2), done.
```

---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs

Github
user-2812@Desktop:~/PP5t3$ git remote add github git@github.com:User-2812/myproject-gh.git
user-2812@Desktop:~/PP5t3$ git push -u github master
error: src refspec master does not match any
error: failed to push some refs to 'github.com:User-2812/myproject-gh.git'
user-2812@Desktop:~/PP5t3$ vim testgh
user-2812@Desktop:~/PP5t3$ git push -u github master
error: src refspec master does not match any
error: failed to push some refs to 'github.com:User-2812/myproject-gh.git'
user-2812@Desktop:~/PP5t3$ git init
Reinitialized existing Git repository in /home/user-2812/PP5t3/.git/
user-2812@Desktop:~/PP5t3$ git add testgh
user-2812@Desktop:~/PP5t3$ git commit -m "Initial commit with testgh"
[master (root-commit) 2aae735] Initial commit with testgh
 1 file changed, 3 insertions(+)
 create mode 100644 testgh
user-2812@Desktop:~/PP5t3$ git remote add github git@github.com:User-2812/myproject-gh.git
error: remote github already exists.
user-2812@Desktop:~/PP5t3$ git push -u github master
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 259 bytes | 129.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:User-2812/myproject-gh.git
 * [new branch]      master -> master
branch 'master' set up to track 'github/master'.
user-2812@Desktop:~/PP5t3$

Gitlab

user-2812@Desktop:~/PP5t3$ git remote add gitlab git@gitlab.thga.de:laurenz.wrobel/myproject-gl.git
user-2812@Desktop:~/PP5t3$ git push -u gitlab master
The authenticity of host 'gitlab.thga.de (195.37.5.155)' can't be established.
ED25519 key fingerprint is SHA256:4+4+prKVzsU8Bw0eBjkbBm86bl9+OinZJIidEMGHpqc.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'gitlab.thga.de' (ED25519) to the list of known hosts.
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 259 bytes | 259.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: To create a merge request for master, visit:
remote:   https://gitlab.thga.de/laurenz.wrobel/myproject-gl/-/merge_requests/new?merge_request%5Bsource_branch%5D=master
remote:
To gitlab.thga.de:laurenz.wrobel/myproject-gl.git
 * [new branch]      master -> master
branch 'master' set up to track 'gitlab/master'.
user-2812@Desktop:~/PP5t3$
```
---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
