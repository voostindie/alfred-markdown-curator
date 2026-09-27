## Introduction

This repository contains scripts to use within Alfred in combination with the embedded HTTP server of my Markdown Curator tool.

With these scripts, “plain” JSON output from the various HTTP endpoints is converted into the [Alfred Script Filter JSON format](https://www.alfredapp.com/help/workflows/inputs/script-filter/json/).

Eventually this set of scripts is intended to grow out into a complete Alfred workflow that can be shared across machines and people.

The scripts on purpose do not have any dependencies on tools other than those that come bundled with macOS, for maximum portability.

The scripts have been tested on macOS 27 with:

- `zsh --version`: zsh 5.9 (arm64-apple-darwin26.0)
- `jq --version`: jq-1.7.1-apple

The scripts rely on a number of environment variables:

- `URL`: URL to the HTTP endpoints of the Markdown Curator.
- `CONFIG`: path to the file containing the name of the active curator.

If not set, the scripts use defaults as defined in the aptly named `defaults` script sourced by all other scripts. That script also includes a number of reusable functions.

Note: I’m not proficient in ZSH, nor do I have the ambition to be. The scripts are far from pretty. The approach in these scripts is to be DRY and to bail out ASAP whenever something is wrong. Error handling can probably be better.

## Background

I once built [Vincent’s Productivity Suite for Alfred](https://github.com/voostindie/vincents-productivity-suite-for-alfred) (vps).

This is a tool written in Ruby that is highly flexible in terms of supporting multiple areas of focus with custom configurations and multiple plugins.

Over time some things happened:

- I standardized my way of working more and more. I no longer require the functionality offered by the tool, leading to maintenance issues.
- I built and embraced the [Markdown Curator](https://github.com/voostindie/vincents-markdown-curator) (Java), which over time resulted in my notes being the golden source for everything I manage: projects, contacts, teams and more.
- I added an HTTP interface to my Markdown Curator tool, allowing my notes to be queried live in a meaningful way through GET requests that spit out structured JSON (instead of Markdown).
- At work I can’t run the latest Ruby anymore, nor can I install Gems. My machine is getting increasingly locked down for security reasons.

To cater for these things I created this new project. Much less flexible, much less fancy. No Ruby, just plain shell scripting.

## Attributions

- [Markdown icon created by brajaomar_j - Flaticon](https://www.flaticon.com/free-icons/markdown)
