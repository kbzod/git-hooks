**git-hooks** - A tool to manage project, user, and global Git hooks for multiple git repositories.

git-hooks lets hooks be installed inside git repositories, users home directory, and globally.
When a hook is called by `git`, git-hooks will check each of these locations for the hooks to run.


Install
=======

Add git-hooks to your `PATH` environment variable so `git hooks` can be run.

Run `git hooks --install` in a git project tell it to use git-hooks hooks.  You can run `git hooks --uninstall` at any time to revert to your previous hooks.  (These are usually the default hooks, which do nothing.)

Run `git hooks --installglobal` to force any new git repository or any git repository you clone to have a reminder to install git hooks. (It can't be on by default for security reasons.)


Overview
========

Hooks are powerful and useful.  Some common hooks include:

- Spell check the commit message.
- Verify that the code builds.
- Verify that any new files contain a copyright with the current year in it.

Hooks can be very project-specific such as:

- Verify that the project still builds
- Verify that autotests matching the modified files still pass with no errors.
- Pre-populate the commit message with a "standard" format.
- Verify that any new code follows a "standard" coding style.

Or very person-specific hooks, such as:

- Don't allow a `push` to a remote repository after 1AM, in case I break something and will be asleep.
- Don't allow a commit between 9-5 for projects in `~/personal/`, as I shouldn't be working on them during work hours.

For more details about the different hooks available to you, check out:

	   http://www.kernel.org/pub/software/scm/git/docs/githooks.html



Locations
=========

git-hooks provide a way to manage and share your hooks using three locations:

 - **User hooks**, installed in `~/.git_hooks/`
 - **Project hooks**, installed in `.git/git_hooks/`, `git_hooks/` or `.githooks/` in a project.
 - **Global hooks**, specified with the `hooks.global` configuration option.

The `contrib/` directory includes a number of useful hooks, and can be set by doing the following:

	   git config --global hooks.global $PWD/contrib/

You can even specify _multiple_ directories for your global hooks! Simply separate each path with spaces.


Finding hooks
=============

To keep things organized, git-hooks looks for scripts in **sub-directories** named after the git hook name.  For example, this project has the following `pre-commit` script in the following location:

	   git_hooks/pre-commit/bsd

When `git hooks` is run without arguments, it lists all hooks installed on your system.  It will run the hooks with the `--about` argument to generate the description shown.

Check out the hooks in `contrib/` for some examples.


Using hooks
===========

To use a hook script, you can copy or symlink the script into the appropriate git-hooks
subdirectory. You can use `git hooks --link` to easily symlink an existing script. For example, if
you have the hook for adding change IDs to commit messages for Gerrit in your ~/bin directory, you
can run this to symlink it as ~/.git/git_hooks/commit-msg/change-id.

    git hook --link commit-msg ~/bin/git-commit-msg-change-id change-id

To get rid of the symlink, you can use `git hooks -unlink`.

    git hook --unlink commit-msg change-id

