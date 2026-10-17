## Introduction

This repository contains a workflow for Alfred that uses the embedded HTTP server of my [Markdown Curator](https://github.com/voostindie/markdown-curator) tool.

## Features

- List all available curators and set one active. 
    - Keyword: `focus`
    - Shortcut: *Hyper* + `F`
- Browse documents and folders in the active curator
    - Keyword: `documents`
    - Shortcut: *Hyper* + `D`
- Browse a specific category of documents and folders:
    - *Hyper* + `C`: Contacts
    - *Hyper* + `P`: Projects
    - *Hyper* + `R`: Reminders
    - *Hyper* + `T`: Teams
    - *Hyper* + `Y`: Third parties
    - *Hyper* + `S`: Systems
- Paste a document name from a specific category as a snippet:
    - *Shared prefix* + `C`: Contacts
    - …(the same categories as above)
- Act on a single document. Supported actions are:
    - Opening it in the default editor
    - Optionally, opening it in [Marked](https://markedapp.com), if enabled in the settings
    - Optionally, opening it in [iA Writer](https://ia.net/writer), if enabled in the settings
    - Browsing external links for the document
    - Applying Alfred’s built-in file actions
    - Optionally, opening it in [OmniFocus](https://www.omnigroup.com/omnifocus), if the document refers to a project in it.
- Act on the active document in Obsidian using my [Alfred Trigger](https://community.obsidian.md/plugins/alfred-trigger) plugin.
    - Run the “Trigger Alfred” command (I have configured Command + Option + `A`) and it pops up all actions from the previous bullet.

*Hyper* is the combination of Control + Option + Shift + Command. That’s not an easy key combination to hit, I know. It’s also a combination that no application uses. I use the free [Karabiner-Elements](https://karabiner-elements.pqrs.org) with the “Change caps lock to hyper key” to make using it a breeze.

The *Shared prefix* is a local setting in Alfred. For me it’s a semicolon, “;”. Because in any language there’s nothing but a space following it.

## Technical details

The workflow relies on a number of shell scripts. These scripts on purpose do not have any dependencies on tools other than those that come bundled with macOS, for maximum portability.

The scripts rely on a number of environment variables:

- `URL`: URL to the HTTP endpoints of the Markdown Curator.
- `CONFIG`: path to the file containing the name of the active curator.
- `ENABLE_MARKED_APP`: whether to enable support for Marked.
- `ENABLE_IA_WRITER`: whether the enable support for iA Writer.

If not set, the scripts use defaults as defined in the aptly named `defaults` script sourced by all other scripts. 

Note: I’m not proficient in ZSH, nor do I have the ambition to be. The scripts are far from pretty. The approach in these scripts is to be DRY and to bail out ASAP when something is wrong. Error handling can be better.

## How to install

I'm not (yet) releasing this code as an official Alfred workflow. Because of that, installing it on your machine is more complicated then downloading it from the Alfred workflow directory:

- Clone this repository to a directory on disk.
- Create a symlink from `~/Library/Application Support/Alfred/Alfred.alfredpreferences/workflows` to the directory where you cloned this repository.

Alfred will automatically detect the workflow and make it available. Updates that you pull in later will automatically be available.

## Historical background

I once built [Vincent’s Productivity Suite for Alfred](https://github.com/voostindie/vincents-productivity-suite-for-alfred) (vps).

This is a tool written in Ruby that is highly flexible in terms of supporting multiple areas of focus with custom configurations and multiple plugins.

Over time some things happened:

- I standardized my way of working more and more. I no longer require the functionality offered by the tool, leading to maintenance issues.
- I built and embraced the [Markdown Curator](https://github.com/voostindie/vincents-markdown-curator) (Java), which over time resulted in my notes being the golden source for everything I manage: projects, contacts, teams and more.
- I added an HTTP interface to my Markdown Curator tool, allowing my notes to be queried live through GET requests that spit out structured JSON (instead of Markdown).
- At work, I can’t run the latest Ruby anymore, nor can I install Gems. My machine is getting increasingly locked down for security reasons.

To cater for all this, I created this new project. Much less flexible, much less fancy. No Ruby, just plain shell scripting.
