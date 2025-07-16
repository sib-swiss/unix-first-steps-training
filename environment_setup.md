# Introduction to Linux / UNIX and the Bash shell: setting-up your environment

Please complete the setup instructions given in this document
**before the start of the course**.

<br>

## MacOS

**No need to install anything**: MacOS comes by default with a "Terminal"
application that launches a **`zsh` shell**. For the most part, the `zsh` and
the **`bash` shell** behave very similarly, and it is possible to do this
course using `zsh` instead of `bash`.

:sparkles:
**Note**: Mac OS also comes with `bash` pre-installed, but `bash` is no longer
the default shell on Mac OS. Instead, the default shell is now `zsh` (since
Mac OS Catalina, released in 2019).  
If you are in `zsh` and would like to **switch to `bash`**, you can simply
type `bash`.

<br>

## Windows

Windows does not natively come with a `bash` shell, but it can be installed
via different means.

We here suggest 2 options, in order of ease of installation (easiest first):

* Install [Git for windows](https://gitforwindows.org), which comes with the
  `bash` shell emulator `GitBash`.
* Install/Enable **WSL**, the Windows Subsystem for Linux. This essentially
  installs a small Linux distribution in your Windows machine. The **WSL** is
  best installed via the Microsoft Store. Search for "Ubuntu" and select for
  instance "Ubuntu 22.04".  
  There are also other Linux distributions available for WSL. You can find
  them in the Microsoft Store by searching for "linux".

<br>

## Linux

**No need to install anything**: virtually all Linux distribution come with a
recent version of **`bash`** installed out-of-the-box.

To check your version of `bash`, open a terminal and run:

```sh
bash --version
```

Ideally you should have version of bash >= `5.x` (but at least >= `4.x`).
