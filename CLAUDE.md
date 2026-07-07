# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is currently empty (no source files yet). Update this file as the codebase takes shape — add real build/lint/test commands and architecture notes once they exist.

## Git operation rules

- **Push every change to GitHub after committing.** Whenever code is modified and committed, immediately push the commit(s) to the corresponding GitHub remote branch (`git push`) so the remote stays in sync with local work. Do not leave committed changes unpushed.
- Only commit when explicitly asked to by the user, per standard workflow — but once a commit is made, the push should follow as part of the same operation unless the user says otherwise.
- Never force-push (`git push --force`) without explicit user confirmation.
