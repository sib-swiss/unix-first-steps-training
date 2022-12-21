# First Steps with UNIX: setting-up your environment

Please complete the setup instructions given in this document
**before the start of the course**.

<br>

### Mac OS
**No need to install anything**: Mac OS comes by default with a "Terminal"
application that launches a `zsh` shell. For the most part, `zsh` and `bash`
behave very similarly, and it is possible to do the course using `zsh` instead
of `bash`.

*Note*: Mac OS also comes with `bash` pre-installed, but `bash` is no longer
the default shell on Mac OS. Instead, the default shell is now `zsh` (since
Mac OS Catalina, released in 2019).

<br>

### Windows
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

### Linux
**No need to install anything**: virtually all Linux distribution come with a
recent version of `bash` installed out-of-the-box.

To check your version of `bash`, open a terminal and run:
```sh
bash --version
```
