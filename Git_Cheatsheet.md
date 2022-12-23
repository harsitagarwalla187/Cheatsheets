# **GIT CHEATSHEET**

> # What Is Staging Area?
### Basically, It's just a area or for clearing understanding say it as space where we can save our files that we want to commit.
**Note:** The files only in Staging Area can be commited.

> # Initialise Git 
### To initialise git in a directory.
**Note:** Without initialising git we cannot perform anyone of the below operations.
```
git init
```

> # Create A New Local Branch
- ### To create a branch only:
```
git branch <branch-name>
```

- ### To create a branch and switch to the branch:
```
git checkout -b <branchname>
```

> # Show Branch
- ### To show all remote and local Branch:
```
git branch
```
- ### To show all remote branch:
```
git branch -r
```

- ### To show all branches along with deatils(local or remote, commit ids, commit messages):
```
git branch -vva
```

> # Rename A Branch
### To rename an existing branch:
```
git branch -m <Branch Name>
```
**Note:** You should switch to the Branch that you want to rename it.

> # Delete A Branch
### To delete an existing branch:
```
git branch --delete <branch_name>
```

> #  Clone A Repository
### Clone a Repository from Remote(GitHub) to Local System.
```
git clone <Repository URL>
```
> # Add To Staging Area
### To add all the updated/newly created files or changes made in the directory(folder) to the staging area.
- #### To add all the files/folders : 
```
git add .                
```
- #### To add particular file/folder :
```
git add <File/Folder name>     
```
> # Adding Remote Repository
```
git remote add origin <Repository Link>
```
> # Obtain The Remote URL 
### To obtain the remote url that we have saved as origin:
```
git config --get remote.origin.url
```
> # To Reset Remote URL
### To change the URL that we have saved as origin:
```
git remote set-url origin new.git.url/here
```
> # Unstage All Git Files
### To unstage/remove files/folders from Staging area
- #### To unstage/remove all files/folder:
```
git reset
```
- #### To unstage/remove particular files/folder:
```
git restore --staged <files/folders name to unstage>
```