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
