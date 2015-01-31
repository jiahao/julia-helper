# julia-helper

Scripts to help Julia developers

## What's this?

This repository contains some [`git` hooks][githooks], which are user level
scripts that are run by [`git`][git] automatically when certain commands are
executed. Currently `pre-commit` and `pre-push` hooks are provided, which are
run before the usual `git commit` and `git push` commands respectively.
The idea is to provide checks to be run each time code is checked in.
These `git` hooks can be bypassed with `--no-verify` to the appropriate `git`
command.

`pre-commit` runs `make whitespace` to check for whitespace.

`pre-push` runs more extensive checks before allowing commits to be pushed:
  - Checks `.travis.yml` to ensure that it is a valid Travis configuration
  - Checks that the documentation can be built in both HTML and PDF formats
  - Runs the entire Julia test suite

[git]: http://git-scm.com
[githooks]: http://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks

## Prerequisites

- A git checkout of [Julia](https://github.com/JuliaLang/julia). The path will
  be referred to here as `$JULIAHOME`.
- A build environment suitable for building Julia.
- (Optional) [travis-yaml](https://github.com/travis-ci/travis-yaml), the
  Travis Configuration Parser
- (Optional) [Python](http://python.org) with
  [virtualenv](https://virtualenv.pypa.io/en/latest/) installed, for testing
  that the documentation builds
- (Optional) `pdflatex` for building PDF documentation. (Some documentation
  issues are only uncovered in the PDF build.)

## Installation

Simply copy the `git` hooks to the appropriate `.git/hooks` subdirectory of
your Julia repository, or append to your existing `git` hooks.

Example:

    ln -s julia-helper/julia/git-hooks/pre-push.sample $JULIAHOME/.git/hooks/pre-push
    ln -s julia-helper/julia/git-hooks/pre-commit.sample $jULIAHOME/.git/hooks/pre-commit

