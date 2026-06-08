# Learning GitHub The Right Way!

I started with this 

Git needs to know your name and email. It stamps every snapshot (commit) with this info. Open Git Bash and run these two commands (use the same email as your GitHub account):
 
 1. Introduce Your self

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

* If you want to check your name or email
just type:

```bash
git config --global user.name 
git config --global user.email 
``` 
I you made a mistake you can just OverWrite it With first commands

You may want to use igonre some stuff so you w'ont make your repo a mess ..here take this save your self

```bash
git .igonre
```


2. Iintilize git

```bash
git init.
```
 
what difrence in `git init` and `git init .`


They do the same thing. The . just means "this current folder" — but `git init` already assumes the current folder by default.
So no difference in practice. 
Just run:
bash `git init`

It will show you somthing like this:

```bash
Initialized empty Git repository in C:/Users/dell/Desktop/GitHub Journey/.git/
```


3. Check status

You check status by using... well you guessed it !!

```bash
git status
```

```bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```
Well it will show you somthing similair

Ok real talk let's break it down:
(break code).. ha :) did it land? no? ok i'll stop

* On branch master — you're on the default branch (we'll talk about branches soon)
* No commits yet — no snapshots taken yet, history is empty
* Untracked files: README.md — Git can see the file exists, but it's not watching it yet

This brings us to one of the most important concepts in Git — the three stages:

> Working folder  →  Staging area  →  Snapshot (commit)\
--(you edit)------(you prepare)-----(you save to history)

Right now your README is in the working folder. Git sees it but doesn't care about it yet.

Before you can take a snapshot, you have to tell Git "hey, include this file in the next snapshot." That's called staging.

Do it:

```bash
git add README.md
```
Then run `git status` again and tell me what changed.

Ehm...you migh ask 
> And if i used `git add .` will add evrything?

Exactly. `git add .` stages everything in the folder at once.

Useful when you changed many files and want to include all of them. But be careful — it adds everything, including files you might not want to commit. That's why `.gitignore` matters later.


---

OK let's mess with some time manupulating skills

Let,s you broke your file .

You can rewind time and restore it to it's latest Version !!

>How?

Ez.. Use this first to check status

```bash
git status
```

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

This is our save command

```bash
git add README.md
git commit -m "message"
```
You can do:
```bash
git commit -a -m "message"
```

And this is our Reload command

```
git restore README.md
```

Ehmm but here is the catch

this only works if you haven't committed the mistake yet. If you already committed "i broke it lol" — git restore won't help. That's a different problem with a different fix.

Ok lets try it..

First i'll save this.. lol i can't embarce my self and deltete befre save.
Worst thing OverWrite your saving file with wrong Version.

See?? too bad you can't see it. you NPCs

>OK but what if you break it while commiting.. How do you fix it

Ah...good point let's see.

```
dell@DESKTOP-VEF2DCU MINGW64 ~/Desktop/GitHub Journey (main)
$ git commit -m "Oh no~  i made a mistake!"
[main 7319005] Oh no~  i made a mistake!
 1 file changed, 6 insertions(+)

dell@DESKTOP-VEF2DCU MINGW64 ~/Desktop/GitHub Journey (main)
$ git log
commit 73190059bb95942c65770186d3515d820ff8d92a (HEAD -> main)
Author: Omar-DataSci <omarghedada@gmail.com>
Date:   Mon Jun 8 05:42:52 2026 +0200

    Oh no~  i made a mistake!

commit 088f12b9f291e4a35c2f15d9c25be427b7407fb4
Author: Omar-DataSci <omarghedada@gmail.com>
Date:   Mon Jun 8 05:38:38 2026 +0200

    Za Waardo!

commit b3b905c8fb53d547c3373bfc5abad2ff5fe654f5 (origin/main)
Author: Omar-DataSci <omarghedada@gmail.com>
Date:   Mon Jun 8 04:24:12 2026 +0200

    first commit: add README

```

Now notice something:

* origin/main is still on the first commit
* HEAD -> main is on the mistake

Meaning: the mistake is only local, not pushed to GitHub yet. That makes fixing it easier.

Option 1 — `git revert` — the safe way
Creates a new commit that undoes the mistake. History stays intact.
Option 2 — `git reset` — the aggressive way
Actually goes back in time and removes the commit from history. Like it never happened.

>Let's start with the first option i want to keeep my memory this time.

Good point.
Run 
```bash
git revert HEAD
```
This will open a text editor asking you to write a message for the revert commit. Just save and close it (in Git Bash it'll open vim ).
Then run git log and tell me what you see.

Hmmm why did you go silent now.

>..You said the V word...
vim?

>Don't name it still give me nighmares

>hmm do i have to reopen vs code now.. Hello anyone here! How to quit THis Hell?

>-Evil Vim-Quit? why quiting..you dont need to ..stay here lets have some fun -Start underssing-

>MOooM !!

..Yikes.. you had it tuogh just 
press Escape then type :wq and hit Enter

>Ok..

```
Author: Omar-DataSci <omarghedada@gmail.com>
Date:   Mon Jun 8 05:58:30 2026 +0200

    Revert "See?"
    
    This reverts commit 2c9fed296cd6d921832b03ff715c911a38af710b.
```

There it is. Read it carefully:

* Git didn't delete the mistake
* It created a new commit that undoes it
* The history still shows everything — the mistake, and the fix

That's the philosophy of `git revert`. It's honest. It says "I made a mistake, and I fixed it" — not "pretend it never happened."

>Got it..lets do the second option now.

Okay. First let's see where we are:
```bash
git log --oneline
```
The --oneline flag shows each commit in one line — cleaner. 


```bash
$ git log --oneline
2c1aaaf (HEAD -> main) Revert "See?"
2c9fed2 Broken Commit
c630c8f temp commit
7319005 Oh no~  i made a mistake!
088f12b Za Waardo!
b3b905c (origin/main) first commit: add README
```

See this.

>-Nod-

Let's say you want to go back to `Za Waardo!` — like everything after it never happened.
The command is:

```bash
git reset --hard 088f12b
```

That `088f12b` is the short ID of the commit you want to go back to.\
**Warning**: --hard means everything after that commit is gone.\
No recovery. That's why it's dangerous.
Run it and then git log --oneline again. 

But let create anohter Save and go back to it.

Probaply you wont remember it..

>I will.

Will See.