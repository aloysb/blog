---
title: 'Find and execute package.json scripts the easy way'
date: 2024-10-02T21:07:37+10:00
draft: false
asciinema: true
tags: 
    - cli
    - fzf
    - jq
category: scripts
---

# How to quickly find and execute scripts in a large package.json

Sometimes, package.json's scripts section gets very long.

Very, very long.

Especially if you work in a monorepo.

Once again, `fzf` + `jq` makes a great combo to quickly find and execute package.json's scripts.

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

1. Retrieve the script names:

Using `jq`, we retrieving all the `keys` of the `scripts`.

The quotes are stripped with the raw flag `-r`

`jq -r '.scripts | keys[] package.json` 

_Note: we assume that the script is execute in directory containing the `package.json` file._

1. Pipe the result to `fzf`:

Then we simply pipe the result to `fzf`.

To enhance the UX, we add a header to the search.

1. Optional) Save the command to a scripts:

In my case, I saved it as `psc`.

This allows me to `cd` into a repository directory and type `psc`


Enjoy,
Aloys.
