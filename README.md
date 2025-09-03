# Introduction to Linux / UNIX and the Bash shell

Welcome to the home page of the
**First steps with Linux / UNIX and the Bash shell** SIB course.

This one-day course provides an introduction to the open source
**[Linux](https://en.wikipedia.org/wiki/Linux)** /
**[UNIX](https://en.wikipedia.org/wiki/Unix)**
operating system, and the **[Bash shell](https://www.gnu.org/software/bash)**.

<br>

## Course material and environment setup :hatching_chick:

### Course material

* [Course slides](slides_intro_to_unix.pdf)
* [Exercises instructions](exercise_instructions.md)
* [Exercises material](https://github.com/sib-swiss/unix-first-steps-training/raw/main/exercises.zip)
* [Exam instructions](exam_instructions.md)
* [FAQ](faq.md) - a list of questions asked during previous instances of the
  course.

### Environment setup

The only technical requirement for the course is having a laptop with a
reasonably recent version of either a `bash` shell (version >= `4.0`), or a
`zsh` shell (the default shell on Mac OS since 2019).
You can display your version of `bash` with the command `bash --version`.

* Please read the **[environment setup instructions](environment_setup.md)**
  for details.
* Make sure to setup your environment **before the start of the course**.

<br>
<br>

## Course description

### Overview :owl:

With the constant evolution of technologies, life scientists such as laboratory
**biologists** are faced with an increasing need for **bioinformatics skills**
to deal with high-throughput data storage, retrieval and analysis.

Although several resources developed for such tasks have a graphical user
interface, many operations can be more efficiently handled with
**command-line** programs and utilities.

This course provides an **introduction to using the Linux / UNIX** operating
system via the **command line interface (CLI)**, as well as an introduction to
the **[Bash shell](https://www.gnu.org/software/bash/)** and some of the
Linux / UNIX **core utilities** commands.

More specifically, the course covers the following topics:

* What are shells and core utilities, and why use them ?
* Connecting to remote servers with `ssh` (not covered in details)
* Filesystem overview and navigation: `ls` and `cd`
* Basics of the bash shell syntax
* Shell command history and help: `history`, `man`
* Filename expansion (globbing)
* File and directory management: `mkdir`, `mv`, `cp`, `rm`, `rmdir`
* File access permissions and ownership
* Locating files: `find`
* Displaying file content: `head`, `tail`, `cat`, `less`, `wc`
* Archiving and compressing data: `tar` and `gzip`
* Standard input/output and pipes
* Text processing utilities: `tr`, `sort`, `uniq`, `cut`, `cat` and `paste`
* Introduction to `grep` and regular expressions

### Audience :mega:

This course is addressed to **beginners** wanting to become familiar with the
Linux / UNIX environment, its basic commands, and the Bash shell.

### Learning objectives :dart:

At the end of the course you should:

* Be able to execute most of the basic Linux / UNIX commands.
* Be able to build simple pipelines by combining different UNIX commands.
* Be sufficiently skilled for further courses requiring basics of Linux / UNIX,
  like HPC or NGS courses.

An optional exam can be taken at the end of the course to get a recommendation
for 0.25 ECTS credits.

<br>

## Prerequisites

### Knowledge / Skills :bulb:

This is a **course for beginners**, no background in Linux / UNIX or any
programming language is required.

### Technical :computer:

A laptop with a command line terminal and a relatively recent version of
Bash (>= `4.0`).
