<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="300" height="300" viewBox="0 0 512 512">
    <path d="M 502.34111,278.80364 278.79809,502.34216 c -12.86794,12.87712 -33.74784,12.87712 -46.63305,0 l -46.4152,-46.42448 58.88028,-58.88364 c 13.68647,4.62092 29.3794,1.51948 40.28378,-9.38732 10.97012,-10.9748 14.04307,-26.80288 9.30465,-40.537 l 56.75401,-56.74844 c 13.73383,4.73404 29.56829,1.67384 40.53842,-9.31156 15.32297,-15.3188 15.32297,-40.15196 0,-55.48356 -15.3341,-15.3322 -40.16175,-15.3322 -55.50254,0 -11.52454,11.53592 -14.37572,28.47172 -8.53182,42.6722 l -52.93386,52.93048 0,-139.28512 c 3.73267,-1.84996 7.25863,-4.31392 10.37114,-7.41756 15.32295,-15.3216 15.32295,-40.15196 0,-55.49696 -15.32296,-15.3166 -40.16844,-15.3166 -55.48025,0 -15.32296,15.345 -15.32296,40.17536 0,55.49696 3.78727,3.78288 8.17299,6.64472 12.85234,8.5604 l 0,140.57336 c -4.67935,1.91568 -9.05448,4.75356 -12.85234,8.56264 -11.60533,11.60168 -14.39801,28.6378 -8.4449,42.89232 L 162.93981,433.11336 9.6557406,279.83948 c -12.8743209,-12.88768 -12.8743209,-33.768 0,-46.64456 L 233.20978,9.65592 c 12.87017,-12.87456 33.74338,-12.87456 46.63305,0 l 222.49828,222.50316 c 12.87852,12.87876 12.87852,33.76968 0,46.64456"
          style="fill:#f03c2e;stroke:none"/>
</svg>
# Git

------

### What is Git?
- A version control tool
- A tool to facilitate collaboration

---

### What isn't Git?
- A filesystem
- "Sorta like Google Docs"
- A data storage/tracking tool
- A substitute for documentation

------

## Basic Concepts

---

### Distributed Version Control
<img src="resources/version-control-fig3.png"> 
<div class="source">Source: https://homes.cs.washington.edu/~mernst/advice/version-control.html</div>

Notes:
- Server has centralized copy of repository
- Each collaborator's computer has its own copy of entire repo as well
- At MPR, we use Team Foundation Server (TFS) to house the central copy
- This is what you will see most of the time at MPR, but DVCS can be more complex
    + No need for central repository

---

### Local Workflow
<img src="resources/areas.png"> 
<div class="source">Source: https://git-scm.com/book/en/v2/Getting-Started-Git-Basics</div>

---

### Areas
1. Working directory
    - What you see in your folders 
    - Not tracked by Git in any way
2. Staging area
    - Place to move files before committing
    - Allows for flexibility in commits
3. Git directory
    - Not visible
    - Where all snapshots and history is stored

------

## Typical Workflow

---

### Step 1: Clone the remote repository

<div class="code-file-name">CONSOLE</div>
```bash
    git clone https://github.com/linusmarco/git-training
    cd git-training
```

---

### Step 2: Make changes to files
As you normally would when not using Git

<div class="code-file-name">testfile.txt</div>
```
    This is a test
```

---

### Step 3: Stage your changes

<div class="code-file-name">CONSOLE</div>
```bash
    git status
    git add testfile.txt
```


---

### Step 4: Commit your changes

<div class="code-file-name">CONSOLE</div>
```bash
    git status
    git commit -m "Descriptive commit message"
```

---

### Step 5: Sync your changes with remote repo

<div class="code-file-name">CONSOLE</div>
```bash
    git status
    git pull
    git push origin master
```

------

## Rules

---

## DO NOT

---

### DO NOT commit sensitive data or PII/PHI 
- Big security concern: TFS is not as secure as other locations

#### Corollary: DO NOT commit any data
- Git is not a data management solution
- Few exceptions

Notes:
- Most importantly, it is a security concern. Our remote TFS repos are housed on the MPR network, and thus behind some security and firewalls, but they are not secure to the same extent that our “Restricted” N-drive folders or other approved data storage locations are. When you commit data and push it up to TFS, you are copying it to a less-than-fully-secure location.
- Even if the data you track is not sensitive, or if it’s public an carries no security restrictions, git is not a tool meant to be used to track data. It will just clutter up the repository’s history. Exceptions to this rule might be storing static metadata or data used for unit testing or other testing, along with some other well thought-out special cases. But please think very carefully about whether you have a good reason to put data in the repository before you do (and always feel free to reach out to myself or another experienced git user if you’re not sure).

---

### DO NOT commit binary files
- What's a binary file?
    + .doc, .docx, .xls, .xlsx, .jpg, .png, .exe, .dll, etc.
- Clogs up repository
- Git will not help you track changes for these
- Few exceptions

Notes:
- What’s a binary file? A binary file is any file that cannot be opened by a text editor (Notepad, Atom, Sublime, etc.). This includes the following: Word documents (.doc, .docx), Excel files (.xls, .xslsx, .xlsm, .xlsb, ...), images (.jpg, .png, …), executables (.exe, .dll, …), SAS/Stata/other data files (.sas7bdat, .dta, .dat (sometimes), …)  and many more. If you are unsure about whether a file is a binary file, just try to open it in Notepad—if you see a bunch of gibberish then it is! If you see a proper text representation of what you know the file contains, then it isn’t!
- Git is a version control tool, meaning that it tracks changes to the contents of a file. This works great for text files, but not at all for binary files. If you change a single character of a Word document, all of the contents of the binary file will change. This means that git will not be able to show you what changed about the file, but only that the file changed.
- There can be exceptions to this rule, but generally it is bad practice to version control this type of file. They, like data, will bloat the repository for no good reason.

---

### DO NOT commit temporary files
- .bak
- ~$File.tmp

Notes:
- Windows or programs themselves often create temporary files when a file is in the process of being written or when someone has the file open. They often have weird names starting with “~$” or extensions like “.bak”. We don’t need or want these files for obvious reasons.

---

### DO NOT commit output files
- .log, .lst
- Frequent, large changes
- Put these with your data

Notes:
- This includes log files and other direct program output. Like binary files, these files are likely to change a lot when they change, but they are also conceptually more like data than they are like code.

---

###  DO NOT use name versioning for files tracked by git
- No `archive`, `old` or `2017_12_06` folders
- No `Document_final.docx`
- This is why we have Git :)

Notes:
- Git takes care versioning for you! No need to create an “archive” or “old” folder or add “_old” or “_20171108” to the file name. Just make your change and commit it. Then, to access the previous version, just use “git checkout” or use “git diff” or “git show” to view changes.

---

## DO

---

### DO write concise and informative commit messages
- Commits are everyone's guide to the repo's history
- Helps error tracking
- Helps keep track of features and changes

Notes:
- Commit messages are the easiest way for other collaborators and future versions of yourself to figure out what changes were made in each commit. This makes it easier to trace errors, keep track of features, and find explanations for changes.

---

### DO try to make each commit a single, cohesive change
- Shouldn't need to use "and" in your commit messages
- Helps track changes
- Makes for easier roll-back of changes
- Avoid `git add .` or git `git add --all`

Notes:
- Conceptually, each commit should be a single unit of work (e.g. “fixed bug X” or “added X section to report” or “changed working in section X”). This unit of work could be small (a couple lines of code, or even fixing a typo) or it could be large (adding an entire section to a program), but all changes/additions/deletions within a commit should be related. A quick rule is that you should rarely need to use the word “and” in a commit message—if you are, then you should probably make that commit into two or more commits.
- Doing this helps everyone get a better sense of what each commit changed, but also makes it easier to inspect and roll back changes. We wouldn’t want to have to undo a change unrelated to the one that actually needs to be reversed
- When adding files to be committed, use “git add [file/s]” to add only certain modified files to staging. Use “git reset” to unstage all files if you accidentally add too many

---

### DO review all your changes before you commit
- `git status` is your new best friend
- Helps avoid all of the DO NOTs

<div class="code-file-name">CONSOLE</div>
```
    git status
    git diff
    git add file.txt
    git status
    git diff --staged
    git commit -m "My commit message"
```

Notes:
- This quick and simple step should make sure that you avoid all of the “do nots” above 99% of the time. 
    + First add the files you want to commit: “git add [files]” or “git add .” to stage all files for commit
    + Review the changes: “git status” to see a list of all files that will becommitted, and “git diff --cached” to see a detailed view of all changes to each staged file
    + Commit! git commit -m “[my concise and informative commit message]”

---

### DO use a good .gitignore
- Tells git to ignore certain files or folders

<div class="code-file-name">.gitignore</div>
```
    data/
    logs/
    *.log
    *.csv
    *.sas7bdat
    *.xlsx

    !config.csv
```

Notes:
- A good .gitignore file will help a lot. In this file, you can specify all file types that you don’t want git to track. Git will ignore any files that match patterns specified in the .gitignore.

---

### DO store data and output outside of your Git repo 
- Completely avoids committing data
- Allows others to see output more easily

Notes:
- It is often a good idea to store data in a separate folder outside of your repository (on N, probably). This is not always possible or practical, but it will help avoid some of the issues discussed above.

------

## Tips

---

### Browsing the log

```
    git log

    git log --oneline

    git log --pretty=format:"%C(cyan)%h%Creset %Cgreen|%Creset %C(red)%<(15)%an%Creset %Cgreen|%Creset %C(yellow)%<(31)%ad%Creset %Cgreen|%Creset %s"
```

---

### Viewing old snapshots

```
    git checkout d78e
    git checkout master
```

---

### Comparing snapshots

```
    git diff d78e 45c7
```

------

### Other Topics
- Branches
- Merging and resolving conflicts
- Pull requests
- More complex DVCS workflows

------

### Resources
- [Documentation](https://git-scm.com/docs)
    + Commands and options (dense)
- [Atlassian Tutorial](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud)
    + Not just a tutorial
- [Codecademy Tutorial](https://www.codecademy.com/learn/learn-git)



