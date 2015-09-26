# Git Tips for a Better Work Flow

### Setting your identification


```sh
git config --global user.name "Your Name"
git config --global user.email "your_email@domain-name.com"
```

### Setting a local repository

Initiate a empty repository:

```sh
git init
```

Add files to project:

```sh
git add .
```

Commit files to local repository:

```sh
git commit -am "Message Description"
```

### Check informations about local repository.

##### Statuses:

Checking the status of changes:

```sh
git status
```

Checking the status of changes at resuming mode:

```sh
git status -s
```

##### Branches

Listing the local branchs:

```sh
git branch
```

Listing the local and remote branchs:

```sh
git branch --all
```


##### Logs
Shows the commit log:

```sh
git log
```

Shows the commit log whith their changes:

```sh
git log -p
```

Shows the commit log in summarized mode:

```sh
git log --pretty=oneline'
```

##### Remote Repositories
Listing remotes repositories:

```sh
git remote
```

Listing remotes repositories with remote url after name:

```sh
git remote -v
```

Show the status of local and remote repository. After this, you could perform a push to update server with local data repository or pull for update local with remote data repository: 

```sh
git remote show <remote_repository>

# Local is fast forward? So:
git push origin master

# Remote is fast forward? So:
git pull origin master
```


### Branchs operations.
Creating a branch:

```sh
git checkout -b <branch_name>
```

Listing the local branchs:

```sh
git branch
```

Listing the local and remote branchs:

```sh
git branch --all
```

Switching between branchs:

```sh
git checkout <branch_name>
```

Mergin data between branchs:

```sh
# First go to the target_branch to get data from source_branch.
git checkout <target_branch>

# Now run merge for update target_branch with source_branch data.
git merge <source_branch>
```

### Settings for remote repositories

##### Setting a remote repository.
    
On **GitHub**, creates a repository and assuming that we have already created a local repository, follow the steps below:

```sh
cd <project_path>
git remote add origin https://github.com/<user_name>/<repository_name>.git
# On the first push, you must use --all to send all branchs to remote repository.
git push -u origin --all
# Later, just need use push like below:
git push origin <branch_name>
```

On **Bitbucket**, creates a repository and assuming that we have already created a local repository, follow the steps below:

```sh
cd <project_path>
git remote add origin git@bitbucket.org:<user_name>/repository_name.git
# On the first push, you must use --all to send all branchs to remote repository.
git push -u origin --all
# Later, just need use push like below:
git push origin <branch_name>
```


##### Setting a SSH server as a remote repository.

Create the SSH repository:

```sh
# First access remote SSH server via ssh.
ssh <user_name>@server_ssh_name

# Create and access the local of repository.
mkdir -p ~/directory_name/<repository_name>.git
cd ~/<directory_name>/<repository_name>.git

# Initiate the repository.
git init --bare

# Exit server to back to developer machine.
<ctrl> + <d>

# Add remote SSH repository to local project.
git remote add ssh ssh://<user_name>@server_ssh_name/~/<directory_name>/<repository_name>.git

# On the first push, you must use --all to send all branchs to remote repository.
git push -u ssh --all

# Later, just need use push like below:
git push ssh <branch_name>

# If local repository is outdated, you can update the local project with local repository, as below.
git pull ssh <branch_name>
```

Now, every time that has repository request, it will be necessary typing the password. To make the request more agile, you can copy the ssh key of the your machine to server and in future requests, the access will be granted whithout typing password.

To performe this, run commands as below:

```sh
cd ~
mkdir ~/.ssh
ssh-keygen -t rsa
ssh-copy-id <user_name>@server_name
```

On Mac OS **ssh-copy-id** is not available, so you can install it with Home Brew, command as below:

```sh
brew install ssh-copy-id
```

##### Setting a local remote repository.

Create the local repository:

```sh
# Create and access the local of repository.
mkdir -p ~/directory_name/<repository_name>.git
cd ~/<directory_name>/<repository_name>.git

# Initiate the repository.
git init --bare

# Add local repository to local project.
git remote add local ~/directory_name/<repository_name>.git

# On the first push, you must use --all to send all branchs to remote repository.
git push -u local --all

# Later, just need use push like below:
git push local <branch_name>

# If local repository is outdated, you can update the local project with local repository, as below.
git pull local <branch_name>
```

##### Updating the remote repository with local data.

```sh
git push origin <branch_name>
```

##### Updating the local project with remote repository data.

```sh
git pull origin <branch_name>

# You also can use git fetch, but later you have to execute git merge to complete operation.
git fetch origin <branch_name>
git merge origin
```

##### Cloning a remote repository to start a projec from it.

```sh
# Just tell the project_name if you want change the name of project directory.
git clone <remote_repository_address> [project_name]
```

### File Changes

To see what files was changed.

```sh
git status

# For summarized display:
git status -s
```


To view changes made to any given file.

```sh
git diff [file_name]

# If file_name was ommited, you will see differences of the all files.
git diff
```

To revert the changes and back to previous version of the file.

```sh
git checkout <file_name>

# To revert all the changes of the current project, use git checkout as below:
git checkout .
```

### Deleting Files from git repository.

To delete a commited file, uses git as below:

```sh
git rm <file_name>

# To delete all files in a directory:
git rm <path_to_directory>/. -r

# You also can use git add with parameter -u. This will not add new files, but will check the structure of files project  and delete unused files of git repository, as below:
git add -u
```


### Tags

Tags normally is used to create releases of the product.

##### Creating Tags:

```sh
git tag -a <version> -m 'descrition of tag release'
```

##### Listing Tags:

```sh
git tag 
```

##### Locating Tags:

```sh
git tag -l '1.4.2.*'

# Result:
v1.4.2.1
v1.4.2.2
v1.4.2.3
v1.4.2.4
```

##### Tagging Later


```sh
# Listing the commit logs.
git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
4682c3261057305bdd616e23b64b0857d832627b added a todo file
166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme

# Adding a tag release for a previous commit.
git tag -a v1.2 9fceb02

# Showing details.
git show v1.2
tag v1.2
Tagger: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Feb 9 15:32:16 2009 -0800

version 1.2
commit 9fceb02d0ae598e95dc970b74767f19372d61af8
Author: Magnus Chacon <mchacon@gee-mail.com>
Date:   Sun Apr 27 20:43:35 2008 -0700

    updated rakefile
...
```
