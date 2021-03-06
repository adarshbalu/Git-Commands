# Comparing Differences


We're going to compare differences with the "diff" command.
I'm going to use my newly created "hist" alias to show my 
history, at least thus far.
If I wanted to see the differences between two commit points,

I could use the "git diff" command to do so.
I'm going to select the any commit, and then the second point, 
I'm going to use the special pointer called "HEAD",

* git diff "Commit_name " HEAD

Note : "" should be replaced by any commit that you want to 
check the diffrence.
then press enter. 
-> Now we get a difference between the "HEAD", 
which is the last commit on the current branch, which is master, 
and that 
specific commit.
We could use the same command,
except using the "difftool" command,again, the same parameters,
and Git will launch the configured 
diff tool,

* git difftool "Commit_name " HEAD

Note : The same note applies here as well

-> Since I have multiple files that are associated with this 
diff,
I'm going to cycle through each one of them ,
Once we've cycled through all the files that are associated with 
the diff,
Git returns us back to the terminal.

I'm going to modify the "README.md" file.
in order to cycle to the next file involved in the diff.

I've saved those changes, and now I know I have a modified 
Readme file,
but I don't know what those changes are.
Again, "git diff" to 
the rescue.
If I just type "git diff",

* git diff

-> I get a difference between
what's recently changed in the working directory,
versus the "HEAD" position in the Git repository, which is the 
last commit on this branch.

In the same fashion, if we type "git difftool",
we do the same thing
Once you're done looking at the differences between "HEAD" and 
the working directory,

The "diff" command is actually extremely powerful;
I recommend that you look at the help page for the "diff" 
command.
There are many many different options,
and it's extremely flexible and can be used in a number of 
cases.

And, for the most part, anything that can be passed into the 
"diff" command can also be passed into the "difftool" command.



# More about Head and pointers


-> In addition to branches, tags, and other labels for commits
Git has special markers or pointers. 
One popular marker is 
called HEAD.
* HEAD is normally the last commit of the current branch.
That means that, as we switch branches, the location of HEAD moves
to match the last commit location of that branch.
While this is generally true, it is also possible to manually 
move the head location someplace other than the last commit
For now, HEAD points to the last commit of the current branch.


# Branching and Merge Types


Branching and merging are important 
concepts in Git.
Git makes doing both branching and merging 
a lot easier than previous tools,
and thus, many workflows rely upon them.
 a branch is just a timeline of commits.

More accurately, branches are the names or 
labels we give timelines in Git.
We can create and delete branches without 
affecting timelines;
all we are doing is creating or deleting 
labels of commit rages in Git.

So far, we have been working on the 
default master branch.
Now, we can create a new branch to do a 
bit of work, and then rejoin the master 
branch by merging in any changes that 
occurred on 
the new branch.
While merging, Git tries it's best to 
automatically merge when possible,
which leads to several types of merge 
scenarios possible.

-> First, the fast-forward merge; this 
happens in the simplest of cases,
when no additional work has been detected 
on the parent branch, or in our case 
master.
Git will simply apply all commits from the 
other branch directly onto the parent 
branch,
as if we never branched off to begin with.
Of course, we can disable the fast-forward 
merges if they are undesired for some 
reason.

-> Secondly, automatic merges; this 
happens 
when Git detects
non-conflicting changes in the parent 
branch.
Git is able to automatically resolve any conflicts.
In doing so, the old branch's timeline is 
preserved, and a new merge commit
is created to show the merging of the two 
branches. 

-> Thirdly, manual merge
this happens when Git is unable to 
automatically resolve any conflicts.
Git enters a special conflicting merge 
state, which means that
all merge conflicts must be resolved prior 
to moving forward with a commit.
Once all conflicts have been resolved, 
those changes are saved as a merge commit.



# Simple Branching Example


We have a modified "README.md" file.
And that's ok; maybe we intended that this 
file should be modified experimentally,
or as part of a feature of a next update.
Either way, we can use feature or topic 
branches
in order to separate out changes that we 
want to make off of master.
If we use the "git branch" command,

* git branch

-> we can 
see that we have a single branch named 
master.
And, right now, it's highlighted green, 
and with an asterisk,
which denotes that that's the current 
branch.
Now, I could create another branch by 
using the "branch" command
and then separately switching to that 
branch, but I can accomplish both
by using the checkout command with a "-b" 
option.

Type "git checkout -b", for creating the 
branch; space;
and then the name of the branch you wish 
to create and switch to,
I'm calling it "updates";

* git checkout -b updates

then press enter.
-> Now, a couple things have happened. 
One: 
it created a new branch called "updates",
then it switched to that new branch and, 
since there were modifications
pending in the working directory, it 
carried those modifications forward into 
that new branch.
This is a technique you can use when you 
start working on master,
and you decide later that, before 
committing, that these changes really 
should be isolated
into their own feature or topic branch. 

Alright, let's continue,
and I'm going to add some changes to the 
readme; save 
and close.

Back at the terminal, we're going to add 
those changes.

And now, let's commit: "Adding updates 
from branch".

Great, so if I do a "git status", it shows 
that I'm on branch "updates",
and I'm in a clean working directory with 
nothing to commit.

If I do a "git hist". Something that 
should be noted, we have the latest 
commit,
which is on head and updates, but if we go 
one back,
we see that is the commit that "master" is 
associated with.

We can see what the changes are by using 
our "diff" command.
And, the "diff" command will allow us to 
pass in the names of branches instead of 
commit IDs.
So, I'm using "git diff updates master", 
and it shows us what's different.

Alright, let's say that I'm finished with 
whatever updates I needed on the "updates" 
branch.
In order to integrate any changes on my 
branch,
I need to first switch to my parent 
branch, which is master.
In order to switch branches, we use the 
checkout command
"git checkout", branch name; in this case 
"master",

* git checkout master

and press enter.
-> Great now let's look at our history 
from 
the master perspective.
Again, it shows that HEAD is now on 
"master",
since head typically means the last commit 
on the current branch.
And, since the current branch is "master", 
HEAD and "master" are sharing the same 
commit id.
Since our "hist" command specifies the 
"--all" parameter to our log command,
we also notice the commit id associated 
with the "updates" branch.Well, let's go 
ahead and merge in those changes. Type 
"git merge"; space;
and then the name of the branch you wish 
to merge into the current branch,

* git merge updates

then press enter. 
-> For this merge, it's 
such a simple merge
that it's able to do something called a 
fast-forward,
which means that we're going to pretend 
that you never really
switched away from "master" in order to 
make those updates.
So, we're going to apply those commits 
directly to the master branch.
Now, if we do a "git hist", we see that 
HEAD, "updates", and "master",
all point to the same commit id; that's 
the effect of a fast-forward merge.
There are options to disable fast-forward 
merges from happening,
even though they may be possible, but most 
of the time, you'll want this behavior.
Once we have completed merging in our 
changes, we no longer need the updates 
branch.
Effectively, branches in Git are just 
labels of timelines
and, once they've been integrated into the 
main timeline, there's no need for them 
anymore.

Let's use the "git branch" command: "git 
branch -d", for delete;
followed by the name of the branch that we 
wish to delete,
in this case, "updates"; 

* git branch -d updates

press enter.
-> Great, we've deleted that branch;
we're back to just the "master" branch.
We do a "git hist"; we see we no longer 
have the "updates" branch associated with 
that  commit id.
Note: the history didn't go away, just the 
label, "updates", did.


# Conflict Resolution


We're going to walk through the steps 
necessary to cause a conflict, and then 
resolve that 
conflict when working with branches.
In my terminal, I'm currently in the 
"demo" Git repository.
I'm on the master branch, with nothing to 
commit, since I'm in a clean working 
directory.
While on the master branch, let's take a 
look at our Readme file.
Alright, so we have our updates that were 
integrated from our previous example.
We can close out of here; let's create our 
branch that we're going to work on.
I'm going to create a branch called 
"very-bad"; now switch to it.
"git branch -a", which shows us all 
branches;

* git branch -a

we see that we have our "master" branch, 
and our "very-bad" branch.
And, at this point, our "very-bad" branch 
has the green highlighting
and the asterisk, denoting this is the 
current branch.
Let's modify our Readme file; let's do it 
in such a way that will cause a conflict,
which means updating the same part of the 
file on both branches.
So, I changed that line to "This is bound 
to cause trouble!".
Let's go ahead and save and close.

I'm going to use my express commit 
technique, saying it's a "very bad 
update".
And, we have "very bad update" at the very 
top, which is the last commit.

Let's return back to master, and before I 
merge in those changes
I'm going to pretend to be another 
developer, or perhaps I'll just forget
about those changes that I made on the 
"very-bad" branch.
I'll modify our Readme file exactly in the 
same location.
Change that to "I hope this isn't much of 
a problem", save and close.
Back at the terminal, again, another 
express commit: "Causing issues again".
Now, let's merge our "very-bad" branch 
into our master branch.

Let's remind ourselves of our branch 
names. "git merge very-bad";
and, as expected, the auto-merging was 
unable to resolve the conflict.
Auto merging's pretty good, but it's not 
perfect, and it can't read minds,
so it doesn't know which version of our 
file we want.
This places us in a merging state, which 
is denoted by our command prompt
with the branch name on one side, and 
"|MERGING".
The "README.md" file is the file that's 
implicated in the merge conflict;
if we "cat" the file, which just outputs 
the entire contents of that file,

the current version has these weird 
carrots that denote the parts of the file 
that are conflicted.

And, you can see that "HEAD" versus 
"very-bad".
Since this happens to be a very simple 
case, we could manually modify this file;
if we have a merge tool configured with 
Git, 
so let's use it.
While in a merging state, just type "git 
mergetool", then press enter.

And, we can see that we have the various 
versions of our file,
and the possible solution at the bottom.
Any number of these possible solutions can 
be incorporated;
let's say I like that one. Once I'm done, 
I need to click the save button
in order to save those changes that I've 
made to the Readme file.
Now, once I've done that, and I have no 
further conflicts to resolve,

If there are no more files with merge 
conflicts,
then you'll simply return back to the 
command prompt.

To complete the merge, we need to commit 
what we've saved: "git commit -m",
we can pass in our commit message: 
"Resolving conflict", then press enter.

If that successfully resolves the 
conflict,
you'll be returned back to a command 
prompt that looks more normal.
In this case, we're back to our branch 
name, simply in parenthesis.

If we do a "git status", we can see we 
have a ".orig" file that is untracked.
".orig" is the original version of the 
Readme file.
Well, I don't like ".orig" files lying 
around in my Git repository
that I might accidentally add back to my 
repository.

Let's add this back to our ".gitignore".

Let's do our express commit: "updating 
ignore to exclude merge files".
Great, so we still have that ".orig" file;
I really don't like that guy hanging 
around, so I'm just going to delete him. 
Great.


# Marking Special Events with Tagging


We're going to look at Git tags.
If I do a "git hist", you can see that we 
have several commits that are part of this 
repository.
And, at this point, we've been working 
with the repository for a pretty good long 
time.

So, I'd like to mark this point in the 
repository with some type of milestone.
To do that, Git supports a notion of tags.
Tags are just labels that you can put at 
any arbitrary commit point,
and, by default, if you don't specify a 
commit, it will be the current commit or 
HEAD.

And, there are two types of tags; 
lightweight tags, which you can just give 
a name,
and Git creates it for you. 
If you do a 
"git tag --list",

* git tag --list

-> You can see that my tag 
is listed.
Also, when we do our "git hist" command, 
we see "tag: mytag".
Now, this is a lightweight tag; there's no 
associated information with it.

What I prefer using are what's called 
annotated tags,
which means they have extra information 
associated with the tag.
So, before we do that, let's delete 
"mytag"; type "git tag -d" for delete, 
then the tag name.

* git tag -d mytag

-> Great, we've deleted that tag.
If we use the syntax "git tag -a", for 
annotated tag; then the tag name "v1.0";
then "-m"; followed by, in double quotes, 
a commit message:
effectively, we're associating a commit 
message with this tag.

* git tag -a v1.0 -m "Release 1.0"

Double check, and then press enter;

"git tag --list"
-> We have our "v1.0" tag.
And we see that we have our "tag: v1.0" 
mentioned in our commit history,
but so far we haven't seen anything 
different than our lightweight tag.
So, where does the annotation come in?

Well, if we use our "git show" command, 
and then specify our tag name,
"git show v1.0", 

* git show v1.0

then press enter,
-> It shows us that we have our tag, 
"v1.0"; 
the tagger, which is myself;
the date that it was tagged; the quote on 
quote commit message that goes with that 
tag;
followed by the rest of the information 
for that commit that's associated with 
that tag,
including its own commit message from 
before.
This is really useful when you're trying 
to note major milestones
and you might want to associate some 
information with it.


Saving Work in Progress with Stashing


We're going to take a quick look at 
stashing.
I'm currently in the "demo" Git 
repository, on the master branch,
in a clean working directory. Let's modify 
the "README.md" file.
And, doing a "git status" we see we have 
our modified file.
But, what if we decide that we're really 
not supposed to be doing that right now?
What if we decide that we really should 
have started this on a branch,
or maybe we need to change content and 
work on something else for a while?
Well, we can do that by using Git's 
stashing ability.
Alright, so let's do that; do a "git 
stash"

* git stash

and it tells me that the HEAD was 
saved,
which is the last commit on the current 
branch, which is master.
And, it saved it in a work in progress.
If we do a "git stash list", 

* git stash list

it shows us 
our stashes.

We have a "WIP on master", and it shows us 
the last commit,
and the associated commit message.
After the "stash", we're actually back on 
a clean working directory.
Let's apply our "emergency fix" if you 
will; save and close.
"updating the license file"; this will 
qualify as our interruption that we had to 
take care of.

Back to a clean working directory.
Now, let's apply our stash; do a "git 
stash pop".

* git stash pop

So, that will do two actions at once; one 
is an "apply", and then the next is a 
"drop".

The "stash apply" will apply whatever the 
stash is: the last stash.
In this case, we put those changes back in 
the Readme file,
then, after that, it dropped that stash 
that was applied.
Now, if I do a "git stash list" 

* git stash list

I have no 
results.
If I go back to the "README.md" file,
you can see the Readme file was updated 
like it was prior to the stash.

Let's move forward by committing our 
update: "updating readme again".
Back to a clean working directory, and 
we're done.


# Reset and Reflog

We're going to do a little bit of time 
travel with "reset" and "reflog".
Let's take care of that; in another line, 
I'm going to put "Updates in stage".
So, I did the "git add" to add that Readme 
file change to stage,
and then I put another line to denote some 
changes that we have in our working 
directory.

If we do a "git status", we see we have 
our modifications detected,
in both the staging area, and just in our 
working directory
.
Now, there may be times when you need to 
go to a different commit point;
if you made a mistake in the last commit, 
for example, that you didn't need to have 
committed.
You want to roll back to a previous 
commit; that's certainly fine.
Do a "git hist"; you can see we have 
several commits to choose from.

So, I'm going to do a "git reset"; I'm 
passing in the commit id that I want to 
reset to.
And, the option "--soft".

* git reset (commit id) --soft

-> And, the reason I'm doing that, 
There are actually 3 distinct ways of 
resetting:
there is a soft reset, which is what I'm 
about to do;
there's the default, which is called 
mixed; and then there is hard.

The soft reset is the least destructive of 
them all;
basically, all it does is change where 
HEAD is pointing.
So, let's try that out;
Make a note of where HEAD is pointing to 
right now.
If we do a "git hist', as expected, HEAD 
is now pointing to another commid it,
which is the commit id that we passed in 
to the reset command.
Let's check out our "git status"
We have files that have been modified,
and in our staging area. 
That's what soft allows us to do,
is simply change the commit id that head 
is pointing to,
which means it preserves the Git staging 
area, and our working directory.

Effectively, we can back out our changes, 
make minor modifications to them,
and then commit where head is currently 
pointing.
Let's try this another time; I'm going to 
choose another commit id .

And, although "mixed" should be default, 
there's no harm in specifying it
just to make sure for our example; let's 
go ahead 

* git reset (commit id) --mixed

and press enter.
Now, what's interesting, it actually 
unstaged the number of changes.
If we do a "git hist", we can see that 
HEAD is now pointing to that commit id.

If we do a "git status", we have several 
files that have been unstaged,
and placed into our working directory; 
there's nothing in our staging area.
Let's try this one last time. Now type 
"git reset", followed by the commit id:
I'm using " (another commit id) --hard".
This is the most destructive of all the 
reset modes.


Now, press enter. It simply tells us that 
our HEAD is now at a new location;
if we do a "git status", we see that our 
working directory is now clean,
which means that any changes that were 
pending have been wiped out,
along with anything that was in the 
staging area.
Again, a hard reset is the most 
destructive type of a reset.
Apart from the handful of changes we made 
at the very beginning,
we really haven't lost a whole lot.

And, you're thinking; well, if we do a 
"git hist", our head is now pointing all 
the way down
to the second commit in our history.
If we just do "git log --oneline", that is 
we leave out the "--all",
we see we only have two commits being 
listed.

So, if you see this list of history, then 
you might be a little worried;
that's ok, because there's another command 
we can use in conjunction with reset
that makes things a lot better, it's 
called "reflog".
Although both "git log" and "git reflog" 
share similar sounding names,


"git log" shows us our commit ids, and 
"git reflog" shows us
all the different actions we've taken 
while in this repository.

* git reflog

This allows us to get all the way back to 
a specific commit id if we need to.
For example, let's go to "head@{3}",
which is the last commit before we did any 
resets; that's "(commit id)".
I'm going to copy that commit id, do a 
"git reset";

* git reset --hard (commit id)

at this point, since there's no pending 
work, we can leave it at the default,
or we can specify hard; then paste in our 
commit id; and then press enter.

We've now moved our commit id back. 
Do a "git log --oneline";
looks like we have our history back again. 
And using our "git hist" alias,
we can see our Git history looks like the 
repo prior to doing any of the resets.
Using "reset"+"reflog" really does provide 
you full control
over time travel within your Git 
repository.


