---
title: 'Bulk Archive Github Repositories'
date: 2024-10-01T17:07:37+10:00
draft: false
tags: 
    - cli
    - fzf
    - jq
    - xargs
    - gh
category: scripts
---

# Clean up your Github profile by bulk archiving repos

If you have been on Github for more than a few months, you most likely have been accumulating repositories.

While it's great to see your progress, you might not want older, unfinished projects cluttering your profile. 

Instead of deleting them and losing your stats, you can archive them.

> If you are not embarassed of your former self, you are not growing fast enough.


## Prerequisites

What you will need:
- `gh`: Github's CLI tool
- `jq`: A very powerful tool for working with JSON data
- `fzf`: A fast, versatile fuzzy finder
- `xargs`: A utility for executing commands on the output of other commands

These tools are must-haves in your developer's toolbox for creating efficient workflows.

Spending some time on their documentations will be save you countless hours down the track.

## TL;DR:
```bash
gh repo list --visibility public --no-archived --json name |\
    jq -r ".[].name" |\
    fzf -m --print0 |\
    xargs -0 -I {} gh repo archive -y {}
```

## Step by step explanation


1. Login in Github's CLI:

Simply run `gh` and follow the prompts.

1. Get a list of repositories:

Fetch a list of your public repositories that are not archived. Use JSON to output only the names.

`gh repo list --visiblity public --no-archived --json name` 

1. Use `jq` to extract the names in a list:

Extract the value of the name for each entry and strip the quotes (`-r`).

`jq -r ".[].name"`

1. Select repositories with `fzf`: 

Pipe the list of names to `fzf` in multi-select mode (`-m`), separating the result by the 'null' value (`--print0`).

`fzf -m --print0`

1. Archive selected repositories:

Finally, pass the selected names to `gh repo archive -y` via `xargs`.

We skip the confirmation with `-y`.

We inform `xargs` that the list is separated by the 'null' character (`-0`) and use `-I` to execute the command for each argument in the list.

## Complete command

Putting it all together, the command looks like this:
```bash
gh repo list --visibility public --no-archived --json name |\
    jq -r ".[].name" |\
    fzf -m --print0 |\
    xargs -0 -I {} gh repo archive -y {}
```

## Execution


Run the command, use `TAB` to select repositories and press `ENTER` to confirm.

You should see an output similar to this:

```bash
✓ Archived repository abitbetterthanyesterday/angular-todo
✓ Archived repository abitbetterthanyesterday/zxb
✓ Archived repository abitbetterthanyesterday/C-Lisp
✓ Archived repository abitbetterthanyesterday/web-dev-course
✓ Archived repository abitbetterthanyesterday/zefo
...

```


Enjoy!
