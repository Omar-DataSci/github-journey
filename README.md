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

question is this how we change the branch name from master to main git branch -M main

4:31 AM
Exactly right.

git branch -M main renames your current branch from master to main.

GitHub now uses main as the default name, but Git itself still creates master by default. So a lot of people run this to keep them consistent.

You can do it now before we connect to GitHub:

bash
git branch -M main
Then git log again — you'll see HEAD -> main instead of HEAD -> master.



whats the diffrence in git@github.com:Omar-DataSci/github-journey.git and https://github.com/Omar-DataSci/github-journey.git

Good catch — GitHub gives you two options and it's worth understanding the difference.
HTTPS (https://github.com/...)

Uses your GitHub username and password (or a token) to authenticate
Easier to set up, works anywhere
GitHub will ask for your credentials when you push

SSH (git@github.com:...)

Uses a special key pair — a private key on your machine, a public key on GitHub
Once set up, you never type a password again
More secure, preferred by most developers


For now, use HTTPS — it's simpler and you're on a new PC with nothing set up yet.
Later when you're on your own machine, we can set up SSH properly and you'll never be asked for a password again.
So run:
bashgit remote add origin https://github.com/Omar-DataSci/github-journey.gitYou said: hmm i want to use ssh.hmm i want to use ssh..4:50 AMClaude responded: Good choice — let's set it up properly then.Good choice — let's set it up properly then.
First, generate an SSH key on this PC:
bashssh-keygen -t ed25519 -C "omarghedada@gmail.com"
It will ask you where to save it — just press Enter to accept the default location.
Then it will ask for a passphrase — you can set one or just press Enter twice to skip it.
Tell me when it's done.You said: explain each part firstexplain each part first4:52 AMClaude responded: Alright.Alright.

ssh-keygen — the tool that generates the key pair
-t ed25519 — the type of encryption algorithm to use. Ed25519 is modern, fast, and secure. The old default was RSA — ed25519 is better.
-C "omarghedada@gmail.com" — just a label/comment attached to the key so you know which account it belongs to. Doesn't affect anything technically.

The result will be two files:

id_ed25519 — your private key. Never share this with anyone. Ever.
id_ed25519.pub — your public key. This is what you give to GitHub.

Think of it like a lock and key. You give GitHub the lock (public key). You keep the key (private key). When you push, your machine proves it has the matching key — no password needed.
Run it now:
bashssh-keygen -t ed25519 -C "omarghedada@gmail.com"You said: where i find itwhere i find it4:57 AMClaude responded: Run this in Git Bash:Run this in Git Bash:
bashcat ~/.ssh/id_ed25519.pub
It will print your public key. It looks something like:
ssh-ed25519 AAAAC3Nza... omarghedada@gmail.com
Copy the whole thing — from ssh-ed25519 all the way to your email at the end.
Then go to GitHub → Settings → SSH and GPG keys → New SSH key → paste it there → save.
Tell me when done.You said: donedone5:06 AMClaude responded: Now test the connection:Now test the connection:
bashssh -T git@github.com
It might ask you something like "are you sure you want to connect?" — type yes and press Enter.
Tell me what it prints.You said: Warning: Permanently added 'github.Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi Omar-DataSci! You've successfully authenticated, but GitHub does not provide shell access.5:07 AMClaude responded: Perfect.Perfect. GitHub recognized you.
"but GitHub does not provide shell access" — that's normal, ignore it. It just means you can't control GitHub's servers directly, which you don't need to.
Now add the remote using SSH this time:
bashgit remote add origin git@github.com:Omar-DataSci/github-journey.git
Then verify:
bashgit remote -v
Tell me what you see.You said: why this git remote -vwhy this git remote -v5:09 AM2 / 2Claude responded: The -v means verbose — it tells Git "show me the details.The -v means verbose — it tells Git "show me the details."
Without it, git remote just prints the name:
origin
With -v it prints the full address:
origin  git@github.com:Omar-DataSci/github-journey.git (fetch)
origin  git@github.com:Omar-DataSci/github-journey.git (push)
You'll notice it shows two lines — one for fetch (pulling from GitHub) and one for push (pushing to GitHub). Usually they're the same address, but they can technically be different.
So -v is just "show me everything, not just the name." Run it and tell me what you see.You said: origin  git@github.origin  git@github.com:Omar-DataSci/github-journey.git (fetch)
origin  git@github.com:Omar-DataSci/github-journey.git (push)5:12 AMClaude responded: Perfect.Perfect. Git knows where GitHub is.
Now let's send your snapshot up. This is the push:
bashgit push -u origin main
The why:

git push — send my commits to GitHub
origin — send it to that address we just saved
main — send the main branch
-u — this is a one time flag that links your local main to GitHub's main permanently. After this first time, you just type git push and Git knows where to send it.

Run it and tell me what you see.


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

```bash
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


>how can i open the redme of other banch

```bash
git show parallel:README.md
```

```bash
git merge parallel
```

```bash
fba348b (HEAD -> main) Will you remember?
3a97f98 Save Point
2c1aaaf Revert "See?"
2c9fed2 Broken Commit
c630c8f temp commit
7319005 Oh no~  i made a mistake!
088f12b Za Waardo!
b3b905c (origin/main) first commit: add README
```

```bash
$ git reset --hard 3a97f98
HEAD is now at 3a97f98 Save Point
```

...

>hm?

See Told You..You Won't remember..

I don't blame you 

```bash
3a97f98 (HEAD -> main) Save Point
2c1aaaf Revert "See?"
2c9fed2 Broken Commit
c630c8f temp commit
7319005 Oh no~  i made a mistake!
088f12b Za Waardo!
b3b905c (origin/main) first commit: add README
```

You can do this to show you file back then
```bash
git show 3a97f98:README.md
```
after
```bash
git log --oneline
```
---

Ok..Move on..to time branches

The why first.

Imagine you're working on `hydrodz` and it's stable. Then you get an idea — you want to add a new feature. But it might break everything while you're building it.

Without branches you have two bad options: either don't build it, or risk breaking the stable version.

**Branches solve this.**

A branch is just a parallel version of your project. You create one, work in it, break it, fix it — and your `main` branch stays completely untouched. When you're done and happy, you merge it back.

It looks like this:

```
main:     A → B → C
                    ↘
feature:              D → E → F
                    ↗
main:     A → B → C → merged
```

---

Let's create one. Run:

```bash
git branch new-feature
```

Then:

```bash
git branch
```

```bash
git branch -m new-feature parallel
```

Tell me what you see.


Ehmmm tbh ..i lost some content while writing i don't know when or how .. but it's gone.

I talked about how to change Branch name and how to set SSH key ..

I mocked you for forgeting and i was the bucket who licked memories..

Good.Good. Two branches now. The * means you're currently on main.
Now switch to the parallel branch:
```bash
git switch parallel
```
Then run git branch again — where's the * now?


```bash
$ git switch parallel
M       README.md
Switched to branch 'parallel'
```
```bash
$ git branch 
  main
* parallel

```
```bash
git switch -c new-feature
```

>because it creates and switches in one step.

```bash
git add .
git commit -m "changes in parallel branch"

```



## Commands to run before making the situation worse

```bash
git status
git log --oneline
git reflog
```