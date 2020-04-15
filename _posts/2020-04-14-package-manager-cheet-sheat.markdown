---
layout: post
title:  "Package Manager Cheat Sheet"
date:   2020-04-14 12:47:07 -0400
categories: package_management yum apt dpkg linux
---
If you've ever had to move from a RPM-based system to a deb-based one or vice versa, you know the feeling of typing the wrong command, and then trying to remember what the proper command is. I got tired of that feeling, so I created the following cheat sheet.

<table>
<thead>
    <tr>
        <th></th>
        <th>rpm/yum</th>
        <th>apt/dpkg</th>
    </tr>
</thead>
<tbody>
<tr>
    <th colspan="3">Information</th>
</tr>
<tr>
    <td>Used in</td>
    <td>Fedora, CentOS</td>
    <td>Debian, Ubuntu</td>
</tr>
<tr>
    <td>Remote repository configuration</td>
    <td><code>/etc/yum.conf</code>, <code>/etc/yum.repos.d/</code></td>
    <td><code>/etc/apt/sources.list</code>, <code>/etc/apt/sources.list.d/</code></td>
</tr>
<tr>
    <td>Easy GUI</td>
    <td>apper</td>
    <td>synaptic</td>
</tr>

<tr>
    <th colspan="3">Installing software</th>
</tr>
<tr>
    <td>Install a package by name</td>
    <td><code>yum install PACKAGE</code></td>
    <td><code>apt install PACKAGE</code></td>
</tr>
<tr>
    <td>Install a package from a file</td>
    <td><code>yum install filename.rpm</code></td>
    <td><code>apt install filename.deb</code></td>
</tr>
<tr>
    <td>Uninstall a package</td>
    <td><code>yum remove PACKAGE</code></td>
    <td><code>apt remove PACKAGE</code></td>
</tr>

<tr>
    <th colspan="3">Finding packages and files</th>
</tr>
<tr>
    <td>List installed packages</td>
    <td><code>yum list installed</code> or <code>rpm -qa</code></td>
    <td><code>dpkg -l</code> <em>(lowercase L)</em></td>
</tr>
<tr>
    <td>See files installed by a package</td>
    <td><code>rpm -ql PACKAGE</code></td>
    <td><code>dpkg-query -L PACKAGE</code></td>
</tr>
<tr>
    <td>Find what package installed a file</td>
    <td><code>rpm -qf /path/to/file</code></td>
    <td><code>dpkg-query -S /path/to/file</code> <em>(capital S)</em></td>
</tr>

<tr>
    <th colspan="3">Getting package information</th>
</tr>
<tr>
    <td>Get information about an installed package</td>
    <td><code>rpm -qi PACKAGE</code></td>
    <td>?</td>
</tr>
<tr>
    <td>Get information about a package that may or may not be installed</td>
    <td><code>yum info PACKAGE</code></td>
    <td><code>apt show PACKAGE</code></td>
</tr>
<tr>
    <td>Find what package (that may or may not be installed) provides a file (pattern/glob)</td>
    <td><code>yum provides PATTERN</code></td>
    <td><code>apt-file search PATTERN</code> <em>(note 1)</em></td>
</tr>

<tr>
    <th colspan="3">Updating packages</th>
</tr>
<tr>
    <td>Update list of available packages <em>(note 2)</em></td>
    <td><code>yum check-update</code></td>
    <td><code>apt update</code></td>
</tr>
<tr>
    <td>Update installed packages to the latest version</td>
    <td><code>yum update</code></td>
    <td><code>apt upgrade</code></td>
</tr>

</tbody>
</table>

Notes:

1. `apt-file` uses a separate file database than the other mentioned tools. You will need to run `apt-file update` before it can provide useful information.
2.  `yum` always checks for updates to the list of available packages when you upgrade the packages installed on your system (which `yum` confusingly calls "updating"), so running `yum check-update` is optional. Conversely, `apt` has separate concepts for _updating_ the list of available packages, versus _upgrading_ your installed packages to the latest version. You need to update your packages before you can upgrade your system.

Updated layout inspired by [this comprehensive PDF](http://johnmeister.com/linux/PDF-info/PackageManagementCheatSheet.pdf). I discovered that after creating this. Check it out if you're interested in openSUSE, Mandriva, Vector, Arch, or smart.
