### Version Control with Git

#### Why is version control so important?

---

- Problem
  - Large development teams
  - Distributed dev teams
  - Multiple changes being made at once
- Version control
  - Allows monitoring code changes
  - Approve/deny/rollback
- Git
  - Developed by Linus Torvalds
  - Used originally to maintain the Linux kernel

#### How do we get started with Git?

---

- Installed by default on many distros
  - `sudo yum install git`
- Download a repo
  - `git clone <url>`
  - `git clone https://github.com/donpezet/awsdemophpwebapp.git`
- Working with a repo
  - `git config --global user.email "you@example.com"`
  - `git config --global user.name "Your Name"`

#### What if we are starting from scratch? How do we make our own repo?

---

- Create a new repo
  - `mkdir test;cd test`
  - `git init`
- View status
  - `git status`

#### Now that the repo is initialized, do we just copy our files over?

---

- Add files to be tracked by Git
  - `git add <changed_files>`
- Add all files to Git
  - `git add .`
  - `git status`

#### How do we commit changes to our repository?

---

- Save changes
  - `git commit -m "<description>"`
- View changes
  - `git log`

#### How do we submit changes to someone else's repository?

---

- Branching
  - Makes an independent copy of a repo
  - Changes can be pushed upstream
- List branches
  - `git branch`
- Create a branch
  - `git checkout -b <branch_name>`
- Push changes to a branch
  - `git commit -a -m "Updated about page"`
- Switch back to master and resync
  - `git checkout master`
  - `git merge <branch_name>`
  - `git status`
