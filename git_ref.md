# git quick reference

| git | Description |
|---------|-----|
| git clone http://github.com/skooter500/csresources | Get a repo from a remote server to the local machine |
| git add . | add all files in the current directory recursively to the staging area |
| git commit -m "a commit message" | Take a snapshot of all the files |
| git push --set-upstream origin master | Send the latest commits to the server. Run this the first time |
| git push |  Send the latest commits to the server |
| git log | Show the list of previous commits. Use the 40 digit hex with git checkout to roll back to that commit |
| git checkout -b new_branch | Create a new branch and make it current |
| git checkout new_branch | Make new_branch current|
| git merge test_branch | Merge test_branch with the current branch  |
| git stash | Save changes in the stash for later retrieval |
| git init | Creates the .git hidden folder and puts the current folder under version control |
| git remote add upstream http://github.com/skooter500/csresources | Adds a remote called upstream. Useful for forking |
| git remote set-url upstream http://github.com/skooter500/csresources | Sets the url on a remote. Useful if you made a mistake with the above |
| git remote set-url origin http://github.com/skooter500/csresources | |
| git remote -v | Show the list of remotes |
| git pull upstream master | Pull changes from the upstream remote, master branch into the current branch |
| git checkout --ours src/ie/tudublin/Main.java | For resolving a merge conflict on a file. Take the local version | 
| git checkout --theirs  src/ie/tudublin/Main.java |  For resolving a merge conflict on a file. Take the remote version |

| bash | Description |
| -----|---------|
| pwd | Print Working Directory |
| cd ~ | Change directory to the home directory |
| cd .. | Change one level up |
| cd bla/bla |Change to bla/bla |
| ./compile.sh | Run the shell script in the current directory |
| mkdir bla | Create a directory |
| chmod 777 ./mrun.sh | Make the file executable |
| rm bla.txt | remove  |
| rm -r -f bla | Remove recursively and force |
| cp a.txt b.txt | Copy |
| grep -r --include *.java "some text that you want to find" . | Old skool plagorism detection |

