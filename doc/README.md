
#   Command Live Environment
##   The shell improvements :-)

CLE enhances bash with following tweaks:
 - colorized and customizable **prompt** string including server time and exit
   code highlight
 - save/edit and reuse **aliases** in easy way
 - rich **history** with timestamps, return codes and additional information
 - super easy installation ONLY on your workstation
 - **seamless** transfer of the environment from workstation to remote
   sessions without installation
 - various shell options
 - configuration from commandline with immediate effect, no restarts
 - self documenting feature
 - open framework for tweaks and further customization
 


## CLE setup and usage

All the mentioned functionality is encoded into _single file_ and no other
executables are needed. Run this file in the current shell context using
trailing dot:

    `. clerc`

The CLE is activated now and you can setup this environment as persistent with
command:

    `cle deploy`

CLE copies itself to `$HOME/.clerc` and adds two lines into your `.bashrc`
si it will be started upon each login. Note this is the *only* one
installation step you need to perform. Typically you'd do it on your account
on your workstation.


### ssg utility (ssh wrapper)

The CLE is able to pass itself over ssh. Use 'ssg' wrapper instead of regular
'ssh' for login into remote account and CLE will be copied over and started
seamlessly:

    `ssg username@remote.host`


### suu, sudd, kksu utilities (su/sudo/ksu wrappers)

Those wrappers serve the same purpose like original su, sudo and ksu utilities
however they add CLE to the sessions.


### scrn - GNU screen wrapper

This wrapper is workaround allowing starting CLE inside screen session. By
default it searches for _yours_ opened/detached session and joins them.
Otherwise creates new one. You can also run `scrn -j` to obtain list of
sessions opened on this account by all users and join them in cooperative
mode. (Imagine this in environment whre more users access root's account.)

Another added value is configuration file with nice status line and shortcut
Ctrl-Left/Right to switch between windows.


### other utilities
- `aa`  manages aliases
- `hh`  makes history searches easier
- `cle` the most important one - this is the command and control center
      of the environment. Issue `cle help` to read more.

Read HOWTO.md and other documents to find out more about this environment.


## Compatibility

CLE has been tested on various systems containing bash version 3.x and 4.x
and different flavors of basic utilities (GNU vs. BSD) High attention was paid
to write highly compatible code so some of nice features of bash4 couldn't be
used. And, various flavor of 'sed' utility is another different story.

Tested systems include following:
- Linux Mint
- Fedora 23+
- RHEL 5 (bash v3)
- RHEL 6
- RHEL 7
- NetBSD
- FreeBSD
- OS X
- Android (some terminal software requires different tweaks, WIP) 

It also works well with at least following terminal emulators:
- Terminator
- Gnome Terminal
- xterm
- rxvt
- screen



## Requirements

Generaly basic OS installation should be sufficient. Some systems might however
require to add missing utilities. Those really necessary are:
- bash (yeah, minimal FreeBSD setup did't contain this!)
- sed
- base64
- curl
- ssh (note, no scp required, e.g no openssh-clients on RHEL)
- GNU screen (only if you want to use it with 'scrn' wrapper)



## Why 'CLE' and bit of history

 CLE was developed over years of work in command line, where I always tried
to have easily distinguished prompt. It has been possible to accomplish
this goal in diferent ways. Basically by editing shell resource files like
.bashrc .kshrc and/or manually transfer those files to each new server and
account. So the very first version was just a backup of my .kshrc (yes, long
ago I used mainly Korn Shell) This version does exist probably on some old
boxes and in scattered backup files. You all probably have something similar.

 Second version contained resource file itself and minimal set of
utilities (scripts like 'cle', 'hlp', etc - some of them are part of different
project 'rootils' now) This version worked without 'ssg' however required to be
installed on each particular account. The setup was done using 'cle' script
but installation was necessary step. Also, changes on those accouts might be
unwelcomed by other administrators. BTW, in version 2, the current name was
introduced as I considered it was bringing more live into poor, plain command
line.

 In third version I removed necessity to setup by ingenious way -
passing resource file encoded with base64 through a shell variable to the
remote system. To be honest, I was inspired by 'sshrc' project. Result is no
setup, no tweaks on remote site and no harm to the current environment! Whoa!
The only thing you need is working CLE on your workstation from where you
manage the world :-) Everywhere you go use the same and still customizable
environment.

Incorporating `ssg`, `su*` wrappers together with `cle` managment function into
one single resource file was just a nature evolution that gave the word 'Live'
its true meaning -- the `clerc` now contains a mechanism of multiplication it's
own DNA [1].

[1] CLE is not a virus :-) It doesn't run itself on any host. Everything is
under user's (your) control and responsibilty. All the spreading is initiated
and driven by user who must know what he's doing. Feel free to inspect the
source code.



## LICENSE
 This program is free software; you can redistribute it and/or
 modify it under the terms of the GNU General Public License
 as published by the Free Software Foundation; either version 2
 of the License, or (at your option) any later version.

 Find complete text in file LICENSE.md or at following URL:
 https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html
