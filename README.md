# The webdev site

[![Build Status](https://travis-ci.org/dart-lang/site-webdev.svg?branch=master)](https://travis-ci.org/dart-lang/site-webdev)
[![first-timers-only](http://img.shields.io/badge/first--timers--only-friendly-blue.svg?style=flat-square)](http://www.firsttimersonly.com/)

This repo implements the [webdev.dartlang.org](http://webdev.dartlang.org) website. It uses the tools and infrastructure of
www.dartlang.org (which is implemented in [github.com/dart-lang/site-www](https://github.com/dart-lang/site-www)).

[We welcome contributions](CONTRIBUTING.md), and we're [first-timer friendly](http://www.firsttimersonly.com)!

For simple changes (such as to CSS and text), you probably don't need to build this site.
But if you want/need to build, here's how.

## Before you build this site

### 1. Get the prerequisites

Install the following tools if you don't have them already.

- **[nvm][]**, the Node Version Manager. Then install the required version of node
  (6 or later LTS release):
  - `nvm install 8`
- **[rvm][]**, the Ruby Version Manager. Then install the required version of ruby:
  - `rvm install 2.4.2`\
  **Can't install ruby?** If installation fails because `curl` is reported as missing—even
  though it exists—use the workaround from https://github.com/ilios/frontend/pull/1963/.
- **[Dart][]**, _including_ both browsers used for testing doc examples:
  - **Dartium**
  - **content shell**

> IMPORTANT: Follow the installation instructions for each of the tools
carefully. In particular, configure your shell/environment so
that the tools are available in every terminal/command window you create.

### 2. Clone this repo

1. **Create or choose a directory** to hold this site's Git repository, and the
   other repositories needed to build this site (which will be fetched later);
   for example, `~/git`.
1. **Clone this repo** ([site-webdev][]) into the chosen directory by following
   the instructions given in the GitHub help on [Cloning a repository][].

### 3. Run installation scripts

> NOTE: It is safe to (re-)run all of the commands and scripts given below even
if you already have the required packages installed.

**Open a terminal/command window** and execute the following commands:

1. <code>cd <i>\<path-to-webdev-repo></i></code> &nbsp;&nbsp;# change to
   **root of this repo**, e.g.: `~/git/site-webdev`
1. `source ./scripts/env-set.sh` &nbsp;&nbsp;#
   initialize environment variables, set node & ruby version
1. `./scripts/before-install.sh` &nbsp;&nbsp;#
   install required tools
1. `./scripts/install.sh`

> IMPORTANT: Any time you create a **new terminal/command window** to work on
this repo, **repeat steps 1 and 2** above.

## Building this site

Once everything is installed, you need to do a full site build at least once:

- `gulp build --dartdoc` &nbsp;&nbsp;# full site build including API docs

The generated site is placed in the `publish` folder. To serve this folder use:

- `superstatic --port 4001`

To view the generated site open [localhost:4001](http://localhost:4001/) in a browser.

You can build, serve, and have a watcher for changes by running the following command:

- `./scripts/serve_local.sh`

If you'd like to separately build and then serve, the commands are:

- `gulp build --no-dartdoc` &nbsp;&nbsp;# build site without regenerating API docs
- `superstatic --port 4001` &nbsp;&nbsp;# serve site under `publish`

Some `gulp build` options include:

- `--clean` &nbsp;&nbsp;# deletes `publish` and file fragments (nothing else)
- `--[no-]dartdoc[=all|acx|ng|forms|router|test]` &nbsp;&nbsp;# generates API docs for named packages (default `all`)
- `--fast` &nbsp;&nbsp;# skips some one-time setup tasks (can spead up repeated builds)
- `--log=x` &nbsp;&nbsp;# logging level: `debug`, `info`, `warn` (default), `error`

[Cloning a repository]: https://help.github.com/articles/cloning-a-repository
[Dart]: https://www.dartlang.org/install
[Dart install]: https://www.dartlang.org/install
[nvm]: https://github.com/creationix/nvm#installation
[rvm]: https://rvm.io/rvm/install#installation
[site-webdev]: https://github.com/dart-lang/site-webdev
[./scripts/env-set.sh]: https://github.com/dart-lang/site-webdev/blob/master/scripts/env-set.sh

[./scripts/before-install.sh]: https://github.com/dart-lang/site-webdev/blob/master/scripts/before-install.sh
[./scripts/get-ng-repo.sh]: https://github.com/dart-lang/site-webdev/blob/master/scripts/get-ng-repo.sh
[./scripts/install.sh]: https://github.com/dart-lang/site-webdev/blob/master/scripts/install.sh
[./scripts/serve_local.sh]: https://github.com/dart-lang/site-webdev/blob/master/scripts/serve_local.sh


## Rebuilding this site from scratch

If you encounter build problems, or if you haven't build this site in a while,
you might want to rebuild it from scratch,
doing all of the following steps (in order):

```
source ./scripts/env-set.sh --reset  # reinitializes environment vars
gulp clean                           # cleans out all temporary site folders
gulp build --dartdoc                 # full site regeneration
./scripts/serve_local.sh
```

If you are still having build problems, you might need to once again step
through the installation instructions.

## Other useful Gulp tasks

```
gulp clean && gulp build --dartdoc  # do a full build from a clean slate
gulp build-deploy                   # builds & deploys to active firebase project
gulp git-clean-src                  # WARNING: runs `git clean -xdf src`,
                                    # so you'll lose uncommitted work!
```

## Prepping for Dart 2.0

Please add the following comment to docs that will need
updating for Dart 2.0. We're doing what we can now, but some things
are not yet ready.

<pre>
{% comment %}
update-for-dart-2
{% endcomment %}
</pre>
