##File structure

A directory called work and subdirectory called hello is created using the commands in the order below
```bash
mkdir work
```
Make the directory a working directory  with the command
```bash
cd work
```
```bash
mkdir helllo
```
Make the directory a working directory  with the command
```bash
cd hello
```
Create a file called hello.sh inside working directory
```bash
touch hello.sh
```
Echo the words "Hello, World" into the hello.sh file with the command below
```bash
echo Hello, World 
```
Initializing a git repository in the current working directory(hello) using the command below
```bash
git init
```
Check the status using the command
```bash
git status
```
At this point the changes in the current directiory(hello) and its content( hello.sh) is untracked.To track the file.Use the command below
```bash
git add .
```
The file is now tracked/Staged(ready for commit).Note the color change from red to green.You can confirm the status using command
```bash
git status
```
Now we can make changes to our file  before commiting it. Example,We can change contents of hello.sh as below
```
#!/bin/bash 
echo "Hello, $1" 
```
We can now stage and commit our changed file as below
```bash
git add .
git commit -m "Chore:First change of hello.sh"
```
#NOTE

Now that you have commited the file .A git status command will tell you that the working tree is clean and there is nothing to commit

Now we will again modify the contents of the file with  two different commits.
        The first commit should be for the comment in line 3.
        The second commit should include changes made to lines 4 and 5.


To do that.Proceede as follows;
change contents of your file to
```
#!/bin/bash

# Default is "World"
name=${1:-"World"}

echo "Hello, $name"
```
Stage input.sh using the command
```bash
git add -p.
```
An interractive screen appears.Choose e to edit the hunk and stage line 1-3
Commit the input.sh file using the command
```bash
git commit -m "Chore:second change of hello.sh"
```
Repeat the previous foremost staging command and stage line 4 and 5
Commit the input.sh file using the command
```bash
git commit -m "Chore:Third change of hello.sh"
```

To view the history of commits on the working directory,use the command below
```bash
git log
```
The output will be something like 
![alt text](<Screenshot from 2024-06-20 14-56-41.png>)

To view a One-Line History for a condensed view showing only commit hashes and messages,use the command below
```bash
git log --oneline
```
The output will be something like
![alt text](<Screenshot from 2024-06-20 15-06-42.png>)

Suppose we want to limit the output of git log to two,we can use the command
```bash
git log -2
```
Alternatively 
```bash
git log -n 2    or  git log --max-count=2
```
The output is the most  recent 2 commits,such as

![alt text](<Screenshot from 2024-06-20 15-19-05.png>)

To view commits made within a range of time ,say the last 5 minutes.Use the command below
```bash
git log --since="5 minutes ago"
```
The output is of commits made within the last 5 minutes,such as

![alt text](<Screenshot from 2024-06-20 16-05-05.png>)

To personalize the output format of git log one can use the pretty options
```bash
%h = abbreviated commit hash
%x09 = tab (character for code 9)
%an = author name
%ad = author date (format respects --date= option)
%as =author date, short format (YYYY-MM-DD)
%s = subject
To shorten the date (not showing the time) use --date=short
```
The command to display including the commit hash, date, message, branch information, and author name, resembling * e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe] is
```bash
 git log --pretty=format:"* %h  %as | %s %d [%an]"
 
```
The output looks something like
![alt text](<Screenshot from 2024-06-20 16-52-04.png>)

#### CHECKING OUT

Suppose we want to revert the working tree to its initial state(b6b1fb6f438e77d0469e8b77f950236a0d7d2987).We use the command 
```bash
git checkout b6b1fb6
```
To  restore second snapshot(8a22d8f6cf2a5e06e20479d86d604f6da9ed699c).Use the command
```bash
git checkout 8a22d8f
```
To restore file to its most recent snapshot(c985186cc17dcfcacdf83db5974babf0f026dc4b) without specifying the hash.Use command
```bash
git checkout master
```

#### TAG ME
To tag current version (c985186cc17dcfcacdf83db5974babf0f026dc4b)of the repository as v1.Use the command below
```bash
git tag v1 c985186
```

To tag previous version (8a22d8f6cf2a5e06e20479d86d604f6da9ed699c) of repository as v1-beta without using commit hashes to navigate.Use command
```bash
git tag v1-beta HEAD^
```
Moving back and forth between the tagged versions using the command
```bash
git checkout v1
git checkout v1-beta
```
Listing all tags
```bash
git tag
```
#### REVERT CHANGES

Unstaged changes 
```bash 
git restore hello.sh
```
Staged changes
```bash
git reset --hard
```
Committed changes
```bash
git revert HEAD
```
 ## Tagging and Removing Commits:
Tag the latest commit with oops, then remove commits made after the v1 version. Ensure that the HEAD points to v1.
```bash
git tag oops HEAD
git reset v1
```
## Displaying Logs with Deleted Commits:
Show the logs with the deleted commits displayed, particularly focusing on the commit tagged oops.
```bash
git reflog HEAD{1}
```
## Cleaning Unreferenced Commits:
Ensure that unreferenced commits are deleted from the history, meaning there should be no logs for these deleted commits.
```bash
git reflog expire --expire=now --expire-unreachable= now --all
git gc --prune -n -v  --expire=now
```
Suppose you want to change a snapshot and/or its commit message without introducing a new commit ,stage the changes and use the command
```bash
git commit --amend -m "commit message"
git commit --ammend --no-edit 
```
## Move it 
 moving hello.sh to lib directoty which is a hello subdirectory
 ```bash
 mkdir lib
 git mv -k -f hello.sh ... lib
 ```
## Exploring .git submodules
 [Study Link](https://dev.to/rajaniraiyn/understanding-the-contents-of-the-git-folder-ef) More explanation found here.
```bash
 Content 	Description
HEAD File       Keeping Track of Your Current Branch
refs Folder 	Storing References to Commits and Branches
objects Folder 	Storing Your Codebase as a Series of Snapshots
config File 	Storing Configuration Information for Git
hooks Folder 	Running Scripts at Specific Points in the Git Workflow

```
## Latest Object Hash
First list all the objects using the command.
```bash
find .git/objects -type f
```
copy the hash of the most recent object(e96b21eafb723f2c512d61986d9e028b65df718d) and find its  type using command
```bash
git cat-file -t e96b21eafb723f2c512d61986d9e028b65df718d
```
object content use the command
```bash
git cat-file -p e96b21eafb723f2c512d61986d9e028b65df718d
```
## Dumping directory tree
To print the contents of directory tree,use the command
```bash
git ls-tree -r HEAD
```
Contents of the lib directory.Run the command
```bash
git ls -tree -d HEAD
```
Copy the SHA1 from previous command(cdd38d5f83befbd8df5fa9e70c90a2e863c940cd) and use the command below.
```bash
 git cat-file -p cdd38d5f83befbd8df5fa9e70c90a2e863c940cd
```
Contents of hello.sh.Copy the SHA1 from previous command(8bdab3f49d7999c4bd178f2fd8d17830bdd69cda) and use the command
```bash
git cat-file -p 8bdab3f49d7999c4bd178f2fd8d17830bdd69cda
```
## Branching
Creating greet branch and switching to it
```bash
git branch greet
git checkout greet
```
















































