---
layout: post
title:  "'TIL' about git submodules"
date:   2019-02-26
categories: TIL
---

Today I kick-start the post category "Today I Learned" (TIL), and it's about a feature of git: [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

## What I needed

I developed a simple script in python to [match email addresses from a list with a list of names](https://github.com/asuccurro/anonyque/blob/master/python/matchEmails.py). At (German) academic institutions, usually you get assigned an email address that is composed of your surname or some sort of abbreviations of it, so it is not too hard to consider possible patterns to match a work email with the person's name. I wanted this code to be available (hence, on github), but I do not want to make the input files I will use public, yet I would like to keep those files under revision control, because "rm -r" happens. I also did not want to copy the scripts and keep different versions on different repositories, because it is way too easy to lose sight of changes.

## The solution

With just a little bit of googling (actually, [duck-duck-going](https://duckduckgo.com)), after I used the right search words, [I found out about git submodules](https://stackoverflow.com/questions/1871282/nested-git-repositories#1871304). It is pretty [straight-forward to use](https://git-scm.com/book/en/v2/Git-Tools-Submodules), you just go anywhere into your "mother repository" and do:

```bash
cd motherrepo
git submodule add git@githost:username/subreponame.git
git push origin master
```

This will create the directory ~/motherrepo/subreponame that is under git@githost:username/reponame.git revision control. This means that any modification done "downstream" of ~/motherrepo/subreponame/ will *not* be under motherrepo.git revision control. If you have commit rights for the subreponame, you will be able to push there just by moving into the directory, while outside of it you will be pulling/pushing into motherrepo.


## Worth mentioning

Apparently there is also the possibility to use [subtrees](https://git-scm.com/book/en/v1/Git-Tools-Subtree-Merging), here a post discussing the [difference between subtrees and submodules](https://stackoverflow.com/questions/31769820/differences-between-git-submodule-and-subtree).
