%title: Unix Fundamentals Session 1
%author: Nathan Dotz
%date: 2017-05-05










-> Unix Fundamentals <-
=======================

-> Session 1 <-
------------------

-> A Detroit Labs Developer Coaching Course <-

--------------------------------------------------------------------------------

-> What's a Unix anyways? <-
============================

*_Unix_* describes a family of operating systems and international
standard deriving from the AT&T Unix operating system developed at
Bell Labs in 1970s

--------------------------------------------------------------------------------

-> Features of Unix <-
======================

* portable
* multi-tasking
* time-sharing multi-user

--------------------------------------------------------------------------------

-> The Unix Philosophy <-
=========================

* plain-text
* heirarchical file system
* devices, IPC, everything are files
* user environment is programming environment
* many small programs which interact

> "the idea that the power of a system comes more from the
> relationships among programs than from the programs themselves"
>
> The Unix Programming Environment, Kernighan & Pike

--------------------------------------------------------------------------------

-> Unix History <-
==================

* Bell Labs, 1960s
* Ken Thompson & Dennis Ritchie
* Ported to C in 1972
* BSD 1977-1995
* System V
* GNU Project, 1983
* Linus Torvalds releases Linux, 1991
* SCO sues everyone
* FreeBSD/NetBSD/OpenBSD
* MacOS, iOS, Android

--------------------------------------------------------------------------------

-> What is an Operating System? <-
==================================

> An *_Operating System_* is *system software* that manages computer
> hardware and software resources to provide common services for
> computer programs.
> - Wikipedia

* Kernel
* System Call Library
* System Utilities
* Shell
* User Applications

--------------------------------------------------------------------------------

-> The Unix Shell <-
====================

* Command-line interpreter
* Text access to applications
* Terminal Emulator
* Allows Scripting
* Programmable

--------------------------------------------------------------------------------

-> First commands <-
====================

    ~$ date
    Mon May  8 23:55:57 EDT 2017

    ~$ who
    sleepynate console  May  2 17:48
    sleepynate ttys000  May  2 17:48
    sleepynate ttys003  May  7 23:46

    ~$ who am i
    sleepynate ttys005  May  8 23:59

    ~$ echo "hello world"
    hello world

--------------------------------------------------------------------------------

-> The Unix File System <-
==========================

* files
* directories
* device files
* sockets/fifo
* symlinks

--------------------------------------------------------------------------------

-> Standard Directory Layout <-
===============================

/        root of the filesystem
/bin     *binaries* fundamental to the system
/boot    stuff for booting the system
/dev     device files
/etc     system configuration files
/home    user home directories
/lib     C headers & libraries
/mnt     mounting point for file system devices
/root    home directory of the root user
/sbin    *system binaries* essential to systems administration
/tmp     temporary file area that is purged regularly
/usr     holds *user* programs and libraries that aren't system critical
/var     a place for logs, databases, system mail

[Another Chart on Wikipedia shows better structure](https://upload.wikimedia.org/wikipedia/commons/f/f3/Standard-unix-filesystem-hierarchy.svg)

--------------------------------------------------------------------------------

-> What's in my home directory? <-
==================================

    ~$ ls
    Applications           Music
    Audiobooks             Pictures
    BattleScribe           Public
    Desktop                Refridgerator
    Documents              Samples
    Downloads              VirtualBox VMs
    Dropbox                asset_copy.sh
    Dropbox (Detroit Labs) big_dickbutt.jpg
    Dropbox (Personal)     code
    Games                  good job.png
    Library                todo.org
    Movies                 todo.org_archive

--------------------------------------------------------------------------------

-> How do we get around? <-
===========================

    ~$ pwd
    /Users/sleepynate
    ~$ cd code/
    code$ pwd
    /Users/sleepynate/code
    code$ cd dl-coaching
    dl-coaching$ cd unix-fundamentals/session1/
    session1$ ls
    dir1		myprogram	names
    session1$ pwd
    /Users/sleepynate/code/dl-coaching/unix-fundamentals/session1

--------------------------------------------------------------------------------

-> How do we get around? <-
===========================

    session1$ cd ..
    unix-fundamentals$ pwd
    /Users/sleepynate/code/dl-coaching/unix-fundamentals
    unix-fundamentals$ cd session1
    session1$ cd ../..
    dl-coaching$ pwd
    /Users/sleepynate/code/dl-coaching

--------------------------------------------------------------------------------

-> What's in a file? <-
=======================

    ~$ cat names
    Ken Thompson
    Dennis Ritchie
    John McCarthy
    Simon Peyton Jones
    Robin Milner

--------------------------------------------------------------------------------

-> Command Options <-
====================

    ~$ wc names
        5      11      74 names

    ~$ wc -l names
        5 names

    ~$ wc -c names
        74 names

    ~$ wc -w names
        11 names

--------------------------------------------------------------------------------

-> Managing files <-
====================

    dl-coaching$ cd unix-fundamentals/session1
    session1$ ls
    dir1		myprogram	names
    session1$ cp names saved_names
    session1$ ls
    dir1		myprogram	names		saved_names

    session1$ mv saved_names hold_it
    session1$ ls
    dir1		hold_it		myprogram	names

    session1$ cp names old_names
    session1$ ls
    dir1		hold_it		myprogram	names		old_names
    session1$ rm hold_it old_names
    session1$ ls
    dir1		myprogram	names

--------------------------------------------------------------------------------

-> Managing files <-
====================

    session1$ ls -l
    total 16
    drwxr-xr-x  6 sleepynate  staff  204 May  9 23:05 dir1
    -rwxr-xr-x  1 sleepynate  staff  114 May  9 23:20 myprogram
    -rw-r--r--  1 sleepynate  staff   74 May  9 16:02 names

total line shows number of storage blocks
first column is directory(d), file(-), or
columns 2-4 show owner read(r), write(w), execute(x) permissions, or not(-)
columns 5-7 show group read(r), write(w), execute(x) permissions, or not(-)
columns 8-10 are global read(r), write(w), execute(x) permissions, or not(-)
next column is link count
owner's name
owning group's name
size in bytes
date modified
file name

--------------------------------------------------------------------------------

-> Managing files <-
====================

    session1$ ls -l dir1
    total 16
    drwxr-xr-x  5 sleepynate  staff  170 May  9 23:08 dir2
    drwxr-xr-x  4 sleepynate  staff  136 May  9 23:08 dir3
    -rw-r--r--  1 sleepynate  staff   11 May  9 23:05 file1
    -rw-r--r--  1 sleepynate  staff   11 May  9 23:05 file2

    session1$ ls -l dir1/dir2/
    total 24
    -rw-r--r--  1 sleepynate  staff  11 May  9 23:07 file3
    -rw-r--r--  1 sleepynate  staff  16 May  9 23:07 file5
    -rw-r--r--  1 sleepynate  staff  23 May  9 23:08 file7

--------------------------------------------------------------------------------

-> Linking Files <-
===================

    session1$ ln myprogram mylinkedprogram
    session1$ ls -l
    total 24
    drwxr-xr-x  6 sleepynate  staff  204 May  9 23:05 dir1
    -rwxr-xr-x  2 sleepynate  staff  114 May  9 23:20 mylinkedprogram
    -rwxr-xr-x  2 sleepynate  staff  114 May  9 23:20 myprogram
    -rw-r--r--  1 sleepynate  staff   74 May  9 16:02 names

--------------------------------------------------------------------------------

-> Linking Files <-
===================

    session1$ ln -s mylinkedprogram symprogram
    session1$ ls -l
    total 32
    drwxr-xr-x  6 sleepynate  staff  204 May  9 23:05 dir1
    -rwxr-xr-x  2 sleepynate  staff  114 May  9 23:20 mylinkedprogram
    -rwxr-xr-x  2 sleepynate  staff  114 May  9 23:20 myprogram
    -rw-r--r--  1 sleepynate  staff   74 May  9 16:02 names
    lrwxr-xr-x  1 sleepynate  staff   15 May 10 17:10 symprogram -> mylinkedprogram

--------------------------------------------------------------------------------

-> Linking Files <-
===================

    session1$ rm mylinkedprogram
    session1$ ls -l
    total 24
    drwxr-xr-x  6 sleepynate  staff  204 May  9 23:05 dir1
    -rwxr-xr-x  1 sleepynate  staff  114 May  9 23:20 myprogram
    -rw-r--r--  1 sleepynate  staff   74 May  9 16:02 names
    lrwxr-xr-x  1 sleepynate  staff   15 May 10 17:10 symprogram -> mylinkedprogram
    session1$ ./symprogram
    bash: ./symprogram: No such file or directory

`symprogram` is now a *dangling symbolic link*.

--------------------------------------------------------------------------------

-> Creating and Removing Directories <-
=======================================

    session1$ mkdir tmpdir
    unix-fundamentals$ mkdir -p tmpdir/tmpdir2/tmpdir3
    unix-fundamentals$ ls tmpdir/tmpdir2/
    tmpdir3
    session1$ rmdir tmpdir
    rmdir: tmpdir: Directory not empty
    session1$ rmdir tmpdir/tmpdir2/
    rmdir: tmpdir/tmpdir2/: Directory not empty
    session1$ rm tmpdir/tmpdir2/tmpdir3/
    rm: tmpdir/tmpdir2/tmpdir3/: is a directory
    session1$ rmdir tmpdir/tmpdir2/tmpdir3/
    session1$ ls tmpdir/tmpdir2/
    session1$ rm -r tmpdir/
    session1$ ls
    dir1		myprogram	names

--------------------------------------------------------------------------------

-> Globbing <-
==============

    session1$ cd dir1/
    dir1$ ls
    dir2	dir3	file1	file2
    dir1$ cat file1 file2
    I am file1
    I am file2
    dir1$ cat file2 file1
    I am file2
    I am file1
    dir1$ cat *
    cat: dir2: Is a directory
    cat: dir3: Is a directory
    I am file1
    I am file2
    dir1$ echo *
    dir2 dir3 file1 file2
    dir1$ echo * : *
    dir2 dir3 file1 file2 : dir2 dir3 file1 file2

--------------------------------------------------------------------------------

-> Globbing <-
==============

    dir1$ ls f*
    file1	file2
    dir1$ ls *2
    file2

    dir2:
    file3	file5	file7
    dir1$ ls *ir*
    dir2:
    file3	file5	file7

    dir3:
    file4	file8
    dir1$ ls -d *ir*
    dir2	dir3

--------------------------------------------------------------------------------

-> Globbing <-
==============

    dir1$ echo [df]i*2
    dir2 file2

    dir1$ echo [d-f]i*2
    dir2 file2

    dir1$ echo *[!2]
    dir3 file1

--------------------------------------------------------------------------------

-> I/O Redirection <-
=======================

- Commands normally read from the *standard input* device
- The output of your commands goes to the *standard output* device
- If a command fails, you may see output from the *standard error* device

These are referred to as `stdin`, `stdout` and `stderr`

    dir1$ wc
    This is some text
    that I am
    typing into
    standard input
    ^D
        4      11      55

--------------------------------------------------------------------------------

-> Output Redirection <-
=======================

    dir1$ who > users
    dir1$ cat users
    sleepynate console  May  2 17:48
    sleepynate ttys000  May  2 17:48
    sleepynate ttys003  May  7 23:46
    sleepynate ttys005  May  9 00:09

--------------------------------------------------------------------------------

-> Output Redirection <-
=======================

    dir1$ echo  "cooluser   ttys999  May 99 99:99" >> users
    dir1$ cat users
    sleepynate console  May  2 17:48
    sleepynate ttys000  May  2 17:48
    sleepynate ttys003  May  7 23:46
    sleepynate ttys005  May  9 00:09
    cooluser   ttys999  May 99 99:99

But be careful, non-appending redirection will clobber your files.

    dir1$ echo "nobody" > users
    dir1$ cat users
    nobody

--------------------------------------------------------------------------------

-> Input Redirection <-
=======================

    dir1$ cat file1
    I am file1
    dir1$ wc < file1
        1       3      11

--------------------------------------------------------------------------------

-> Piping <-
============

Because commands generally read from `stdin` and write to `stdout`, of
course there is a redirection mechanism to link the `stdout` of one
command to the `stdin` of the next, the pipe.

    dir1$ who > users
    dir1$ wc < users
        4      20     136
    dir1$ who | wc
        4      20     136

--------------------------------------------------------------------------------

-> The Error Output Stream <-
=============================

    dir1$ cat *
    cat: dir2: Is a directory
    cat: dir3: Is a directory
    I am file1
    I am file2

    dir1$ cat * 2> errors
    I am file1
    I am file2
    dir1$ cat errors
    cat: dir2: Is a directory
    cat: dir3: Is a directory
