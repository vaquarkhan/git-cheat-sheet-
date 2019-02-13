# git-cheetsheet



![Alt Text](https://www.git-tower.com/learn/content/02-cheat-sheets/01-git/git-cheat-sheet-large01.png)


![Alt Text](https://zeroturnaround.com/wp-content/uploads/2016/02/Git-Cheat-Sheet-pdf-v2.png)



-------------------------------

 ###             GETTING GIT REPOSITORY            =
====================================================

Get git:
http://code.google.com/p/git-osx-installer

Check settings:
$ git config --list

Initialise repository in existing directory
$ git init

Clone existing repository
$ git clone [url] [new target directory]

Move to directory
cd Documents/[directory_name]

Run server
jekyll --server --auto
(then open new window in Terminal)

====================================================
###        RECORDING CHANGES TO REPOSITORY          =
====================================================

Check status of files
$ git status

Track new (or stage current) file
$ git add [filename]

Track all new (or stage all current) files
$ git add .

See changes
$ git diff

See what is staged so far
$ git diff --cached

Commit changes
$ git commit
(Write message, then ctrl-o, return & ctrl-x)

Commit changes & see diff
$ git commit -v

Commit with inline message
$ git commit -m "[message]"

Skip staging area
$ git commit -a -m '[message]'

Remove file
$ git rm [directory].[filename] (makes unstaged)
$ git rm

Untrack, but keep file on HD
$ git rm --cached [filename].[ext]

Rename file
$ git mv [old_filename] [new_filename]


====================================================
###            VIEWING COMMIT HISTORY               =
====================================================

View commit history, reverse chronological
$ git log

Show diff introduced in each commit
$ git log –p

Limit to last two entries
$ git log –p -2

Abbreviated stats for each commit
$ git log --stat 

Choose log output
$ git log --pretty=oneline/short/full/fuller

Choose your own output format
$ git log --pretty=format:"%h - %an, %ar : %s"

%H		Commit hash
%h		Abbreviated commit hash
%T		Tree hash
%t		Abbreviated tree hash
%P		Parent hashes
%p		Abbreviated parent hashes
%an		Author name
%ae		Author e-mail
%ad		Author date (format respects the –date= option)
%ar		Author date, relative
%cn		Committer name
%ce		Committer email
%cd		Committer date
%cr		Committer date, relative
%s		Subject

(author is the person who originally wrote the work, whereas the committer is the person who last applied the work)

-p				Show the patch introduced with each commit.
--stat			Show statistics for files modified in each commit.
--shortstat		Display only the changed/insertions/deletions line from the --stat command.
--name-only		Show the list of files modified after the commit information.
--name-status		Show the list of files affected with added/modified/deleted information as well.
--abbrev-commit		Show only the first few characters of the SHA-1 checksum instead of all 40.
--relative-date		Display the date in a relative format (for example, “2 weeks ago”) instead of using the full date format.
--graph			Display an ASCII graph of the branch and merge history beside the log output.

Filter log output:

-(n)				Show only the last n commits
--since, --after	Limit the commits to those made after the specified date.
--until, --before	Limit the commits to those made before the specified date.
--author			Only show commits in which the author entry matches the specified string.
--committer		Only show commits in which the committer entry matches the specified string.

EG:
$ git log --pretty="%h - %s" --author=[author_name] --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/

GUI history
$ gitk


====================================================
###                  UNDOING THINGS                  =
====================================================

Remove all .DS_Store
find . -name '*.DS_Store' -type f -delete

Overwrite last commit
$ git commit --amend

Unstage staged file
$ git reset HEAD [filename].[ext] 

Unmodify modified file (all changes lost forever if never committed)
$ git checkout -- [filename].[ext]


====================================================
###             WORKING WITH REMOTES               =
====================================================

Show your remotes (origin — default name Git gives cloned server)
$ git remote

Show URL for shortname
$ git remote -v

Add new git repository as a shortname
$ git remote add [shortname] [url]

Fetch all data (& branches) using shortname (must merge manually)
$ git fetch [shortname]

Automatically fetch and merge (if tracking set up)
$ git pull

Push data to remote
$ git push [remote-name] [branch-name]

Push master branch to origin server (if you have write access)
$ git push origin master

Inspect a remote
$ git remote show [remote-name]

More info on origin
$ git remote show [remote-name]

Rename remote reference
$ git remote rename [old_reference_name] [new_reference_name]

Remove reference
$ git remote rm [reference_name]


====================================================
###                  TAGGING                       =
====================================================

List all tags (alphabetical order)
$ git tag

Create annotated tag
$ git tag -a [tagname] -m 'my version 1.4'

Show tag and commit data
$ git show [tagname]

Sign tag with GPG (if you have private key)
$ git tag -s [tagname] -m 'my signed 1.5 tag'

Verify signed tag (requires signers public key in your keyring)
$ git tag -v [tagname]

Tag previous commit
$ git tag -a [tagname] [checksum]

By default git push does not transfer tags to remote servers, so
$ git push origin [tagname]

To push all tags
$ git push origin --tags


====================================================
###              BRANCHING                      =
====================================================

Create branch & switch to it
$ git checkout -b [branch_name]

This is shorthand for:
$ git branch [branch_name]
$ git checkout [branch_name]

Merge branch
$ git merge [branch_name]

Now you may want to delete it
$ git branch -d [branch_name]

View merge conflicts
$ git status

Visual merge tool
$ git mergetool


====================================================
###              BRANCH MANAGEMENT                 =
====================================================

List all branches
$ git branch

See last commit on each branch
$ git branch -v

See which branches are merged into the branch you're on
$ git branch --merged
(generally ok to delete these branches, except *)

See all branches not merged in
$ git branch --no-merged


====================================================
###               REMOTE BRANCHES                  =
====================================================

Synchronise with remote
$ git fetch origin

Push local branch to remote
$ git push [remote_name] [branch_name]

Push to different branch
$ git push [remote_name] [branch_name1]:[branch_name2]

Pull from remote
$ git pull 

Fetching new branches aren't editable. To edit
$ git checkout -b [branch_name] [remote_name]/[branch_name]

Checkout and track a remote branch
$ git checkout --track [remote_name]/[branch_name]

Checkout and rename remote branch
$ git checkout -b [new_name] origin/[old_name]

Delete a remote branch
$ git push origin :[branch_name]


====================================================
###                    REBASING                     =
====================================================

Do not rebase commits that you have pushed to a public repository.

Works by going to the common ancestor of the two branches (the one 
you’re on and the one you’re rebasing onto), getting the diff 
introduced by each commit of the branch you’re on, saving those diffs 
to temporary files, resetting the current branch to the same commit as 
the branch you are rebasing onto, and finally applying each change in 
turn.

$ git checkout [branch_name]
$ git rebase [master or branch_name]

Checkout branch2, figure out patches from the common ancestor 
of branch2 and branch1, and then replay them onto master
$ git rebase --onto master [branch_name1] [branch_name2]

Now you can fast forward master
$ git checkout master
$ git merge [branch_name2]

Rebase a branch without checking it out
$ git rebase master [branch_name]

Do not rebase commits that you have pushed to a public repository.


====================================================         
### COMMIT GUIDELINES                  =
====================================================

Check for whitespace
$ git diff --check


- http://progit.org/book/
- http://www.007dev.com/Downloads/GitCommands.htm
