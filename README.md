# Emacs Config Guide

Currently I program in Clojure so this guide will be focused on that.
There are a few plugins that I use primarily, they are:

[Lispy](https://github.com/abo-abo/lispy)

[Helm/Projectile](https://github.com/bbatsov/projectile)

[Magit](https://magit.vc/)

# Projects (Helm/Projectile)

Projects are defined by the fact they are git projects, so for
Projectile to work, you should be working in a folder that has been
defined as a git repository.  Once you open a file that is managed by
git, that whole folder will be added as a project to projectile.  To
test this, after you have opened such a file do, `helm-projectile-switch-project`: 

    C-c p p 

You will see the folder of the project you were working on there, if
the list is longer you can narrow it down by typing letters that exist
in the project name.  You can move up and down with: `C-n` and `C-p`
commands.  When the project you want is highlighted (with green) you
can hit `Enter` and that project will be selected.  At this point all
the project files will be listed for you to narrow down like you did
the project name, so you can pick the actual file you want to work on.

The next common task is opening up another 'project' file.  To do this
use the command: `helm-projectile`, or what I just call, open project
file:

    C-c p h

Now once we have all the files we want to work on open, often we need
to switch between open files to make them active in a buffer, use the
command: `helm-mini`, or what I call, switch buffer to open file:

    C-x b (also C-x C-b)
    
Those are the main project file navigation commands, next we'll look
at editing clojure files directly.

# Lispy - Structural Editing Clojure Files

Structural editing means your editor is aware of the nature of you
clojure (lisp) file.  It knows that the paren here is matched by the
paren way down there, etc...  This allows you to navigate and
manipulate your lispy style code MUCH more easily.  To learn these
features open a clojure file (or .elisp, or any lispy like file) and
try out the following commands.

The first command is `lispy-backward`:

    [
    
This is the left square bracket.  This will take you to closest
opening paren to your left.

Lispy automatically enters a lisp modal editor mode when it is on top
of a left paren/bracket/brace OR immediately to the right of a right
paren/bracket/brace.  When you are in either of these two positions,
you cannot type as normal, instead the regular keys that you type with
take on different meaning, and run commands instead.

To test this, have your cursor be on a left paren/bracket/brace and
type the 

    s

and 

    w

keys.  These run the commands:
`special-lispy-move-down` and `special-lispy-move-up` commands, which
move sexps up and down respectively.

Just as left bracket `[` moves to the closest left paren, right bracket

] 

moves to the closest right paren.

Since lispy has 'stolen' the left and right brackets to take it to the
corresponding parens, to actually get a left/right bracket pair into
your code you need to press `S-]` and `S-[` to get brackets and curly
braces respectively.

## Copy and Paste

Often you'll want to cut/copy and paste a sexp to a different
location.  To copy a sexp, be on the opening paren and type:

    n

You can use the mnemonic *NEW*, as in it creates a new copy of the
sexp for you to paste somewhere else.  You can now paste it with the
regular: 

    C-y
    
For *YANK*ing the sexp into the current cursor location.  Here are
some more commands to try:

    d    ====>  delete
    C-,  ====>  cut
    c    ====>  clone
    i    ====>  format sexp (removing extra internal spaces)
    j/k  ====>  move down/up sexp
    f    ====>  flow down into sexp's
    A    ====>  go to top most sexp
    a/q  ====>  ace-jump inside sexp

Not to be a replace for the lispy home page, but the preceeding should
give you a good start.

# Magit - Git Client

The final piece of software I'll cover is magit.  It is an emacs
client into the git software.  For the following to work, you should
be editing a file that is part of a git project.  To activate the main
magit window do:

    C-c g

This runs the `magit-status` command.  Now hopefully you have edited
and saved a file managed by git, so that the fact that it has changed
will show up here under the listing: *Unstaged changes*.

Here you can use the `n` and `p` keys to navigate up and down the
list.  While on top of a file hit the 

    TAB
   
key, this runs the command `magit-section-toggle`.  You'll see a
nicely colored diff of the changes that you have made to that file
since your last commit.

If you want to undo your changes you can press the 

    k

key, this runs the command `magit-discard`, and your file will be
reverted to the state it was on the last commit.

To stage all of your changes for commit do:

    S S
    
after a yes/no prompt all your changed files will be staged, and ready
for being committed.  Now lets commit those by pressing:

    c c

This will bring you to the *COMMIT_EDITMSG* buffer, where you can type
your commit message.  You should also have a *magit-diff* buffer where
you can see the diff of all the files you are committing.  After you
have typed your commit message to actually commit do:

    C-c C-c
    
This will bring back to the magit status buffer with no files showing
that they need attention or have been changed.  To push your changes
up to the server you can now do:

    P u

## File History

Cool feature I just discovered.  You can scroll through versions of a
file.  First you get into magit log mode with: 

   C-c g
   l l

This will show the commits you have made on a project.  You can select
one with `n`ext or `p`revious.  Once on a commit you want to inspect
hit `Enter`.  Now that commit will be shown, including diff data.  You
can `n`ext / `p`revious to the desired filename and then hit `Enter`
again.  Now with the file open you can again use `n` or `p` to go to
next or previous revisions.  If you `n` far enough, you'll drop out of
this scrolling behaviour and just be dropped into the most recent
version of the file.

# Wrap Up

These three plugins to emacs should greatly expand your efficiency
editing clojure, happy hacking! :)
