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
asciinema: true
---


# Clean Up Your GitHub Profile by Bulk Archiving Repos

If you have been on github for more than a few months, you most likely have been accumulating repositories.

While it's great to see your progress, you might not want older, unfinished projects cluttering your profile. 

Instead of deleting them and losing your stats, you can archive them.

> If you are not embarassed of your former self, you are not growing fast enough.

{{< asciinema key="gh_bulk_archive" >}}

## Prerequisites

What you will need:
- `gh`: github's cli tool
- `jq`: a very powerful tool for working with json data
- `fzf`: a fast, versatile fuzzy finder
- `xargs`: a utility for executing commands on the output of other commands

These tools are must-haves in your developer's toolbox for creating efficient workflows.

Spending some time on their documentations will be save you countless hours down the track.

## TL;DR:
```bash
gh repo list --visibility public --no-archived --json name |\
    jq -r ".[].name" |\
    fzf -m --print0 |\
    xargs -0 -i {} gh repo archive -y {}
```

## Step By Step Explanation


1. Login in github's cli:

Simply run `gh` and follow the prompts.

2. Get a List of Repositories:

Fetch a list of your public repositories that are not archived. use json to output only the names.

`gh repo list --visiblity public --no-archived --json name` 

3. Use `jq` to Extract the Names in a List:

Extract the value of the name for each entry and strip the quotes (`-r`).

`jq -r ".[].name"`

4. Select Repositories with `fzf`: 

Pipe the list of names to `fzf` in multi-select mode (`-m`), separating the result by the 'null' value (`--print0`).

`fzf -m --print0`

5. Archive Selected Repositories:

Finally, pass the selected names to `gh repo archive -y` via `xargs`.

We skip the confirmation with `-y`.

We inform `xargs` that the list is separated by the 'null' character (`-0`) and use `-i` to execute the command for each argument in the list.

## Complete Command

Putting it all together, the command looks like this:
```bash
gh repo list --visibility public --no-archived --json name |\
    jq -r ".[].name" |\
    fzf -m --print0 |\
    xargs -0 -i {} gh repo archive -y {}
```

## Execution

Run the command, use `tab` to select repositories and press `enter` to confirm.

You should see an output similar to this:

```bash
✓ archived repository abitbetterthanyesterday/angular-todo
✓ archived repository abitbetterthanyesterday/zxb
✓ archived repository abitbetterthanyesterday/c-lisp
✓ archived repository abitbetterthanyesterday/web-dev-course
✓ archived repository abitbetterthanyesterday/zefo
...

Enjoy,
Aloys
