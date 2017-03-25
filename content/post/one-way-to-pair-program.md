---
author: ""
categories: [flatiron blog]
date: 2017-03-18T23:07:23-05:00
description: ""
featured: ""
featuredalt: ""
featuredpath: ""
linktitle: ""
title: One Way To Pair Program
---

Tonight a couple people were wanting to know the best way to pair program together. They had both done the beginning parts of the Tic-Tac-Toe with AI project (the one I'm getting ready to start) and wanted to work on the AI part together. The exact question was:

> Hey @**\*\*\*** and I are doing parallel pairing :slightly_smiling_face: what is the best way to go about this, to work on the same repo on separate branches or just copy on paste. She is on IDE, I'm on local. Any help muchly appreciated!

The always awesome and helpful instructor [Cernan Bernardo][1] quickly gave a how-to that I knew others could use. I'm just going to abbreviate what he said and turn it into a numbered list.

1.  Grab each other's SSH URL for your respective GitHub repos.
2.  In your respective terminals (local or IDE) you would each run the command `git remote add upstream *copy_ssh_url_here*`.
3.  After running those commands when you run `git remote -v` you will see two remotes...one for your origin which is your respective GitHub repo and one for upstream which is your partner's repo.

Now the setup is done, here is the work flow to be done _before_ either starts working on the app:

1.  Run `git pull upstream master`...this will pull down any code your partner has added to the app and pushed up to their GitHub.
2.  Work on your part of the app.
3.  Run `git push` or `git push origin master`...this will push your new code to YOUR repo.

> With that work flow you will each have your code in sync. Just remember to _pull before you push_.

So there you have it. Questions feel free to ask and I'll ask Cernan ;-)

[1]: https://github.com/cernanb
