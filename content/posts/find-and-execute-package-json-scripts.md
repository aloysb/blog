---
title: 'Find and Execute Package.json Scripts the Easy Way'
date: 2024-10-02T21:07:37+10:00
draft: false
asciinema: true
tags: 
    - cli
    - fzf
    - jq
category: scripts
---

# How to Quickly Find and Execute Scripts in a Large package.json

Sometimes, package.json's scripts section gets very long - especially in a monorepo.

Fortunately, `fzf` + `jq` makes a great combo to quickly find and execute package.json's scripts.

{{< asciinema key="psc" >}}

## Prerequisites

You will need the following CLI:
- `jq`: a utility to work with JSON files
- `fzf`: a powerful, versatile fuzzy finder


## TL;DR:
```bash
#!bin/bash
# Display the list of npm scripts in a fuzzy finder to execute
jq -r '.scripts | keys[]' package.json | fzf \
  --header "Select a script to execute" \
```

## Step by step explanation

1. Retrieve the Script Names:

Using `jq`, we extract all the `keys` of the `scripts`.

The `-r` flag ensure quotes are stripped from the result.

`jq -r '.scripts | keys[] package.json` 

_Note: we assume that the script is executed in the directory containing the `package.json` file._

1. Pipe the Result to `fzf`:

Next, we simply pipe the result to `fzf`.

We add a header to enhance the UX.

1. (Optional) Save the Command as a Script:

You can save the command as a script (e.g., `psc`). 

This way, you can `cd` into a repository directory and simply type `psc` to execute the script finder.


Enjoy,
Aloys.


