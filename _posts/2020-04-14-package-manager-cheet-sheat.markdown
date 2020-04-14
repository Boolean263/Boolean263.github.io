---
layout: post
title:  "Package Manager Cheat Sheet"
date:   2020-04-14 12:47:07 -0400
categories: package_management yum apt dpkg linux
---
If you've ever had to move from a RPM-based system to a deb-based one or vice versa, you know the feeling of typing the wrong command, and then trying to remember what the proper command is. I got tired of that feeling, so I created the following cheat sheet.

| Task                              | yum/rpm               | apt/dpkg                  |
| ---                               | ---                   | ---                       |
| Install a package by name         | `yum install PACKAGE`     | `apt-get install PACKAGE`     |
| Uninstall a package               | `yum remove PACKAGE`      | `apt-get remove PACKAGE`      |
| See files installed by a package  | `rpm -ql PACKAGE`         | `dpkg-query -L PACKAGE`       |
| Find which package installed a file | `rpm -qf /path/to/file` | `dpkg-query -S /path/to/file` |
| Get information about a package that may or may not be installed | `yum info PACKAGE` | `apt show PACKAGE` |
| Find what package (that may or may not be installed) provides a file (pattern/glob) | `yum proivdes PATTERN` | `apt-file search PATTERN` (note 1) |
| Update your system's list of packages from your remotes | N/A (note 2) | `apt-get update`      |
| Upgrade all installed packages to the latest version | `yum update` | `apt-get upgrade` |
| GUI package management program    | `synaptic`            | `apper`                   |

Notes:

1. `apt-file` uses a separate file database than the other mentioned tools. You will need to run `apt-file update` before it can provide useful information.
2.  `apt` has separate concepts for _updating_ the list of available packages, versus _upgrading_ your installed packages to the latest version. `yum` always checks for updates to the list of available packages when you upgrade the packages installed on your system (which `yum` confusingly calls "updating").
