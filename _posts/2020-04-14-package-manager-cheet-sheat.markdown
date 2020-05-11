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
        <th class="description"></th>
        <th class="yum">rpm (yum/dnf) <em>(note 5)</em></th>
        <th class="apt">apt/dpkg</th>
        <th class="snap">snap</th>
        <th class="flatpak">flatpak</th>
    </tr>
</thead>
<tbody>
<tr>
    <th colspan="6">Information</th>
</tr>
<tr>
    <td class="description">Used in</td>
    <td class="yum">Fedora, CentOS</td>
    <td class="apt">Debian, Ubuntu</td>
    <td class="snap">Ubuntu ≥18</td>
    <td class="flatpak">User-added</td>
</tr>
<tr>
    <td class="description">Remote repository configuration</td>
    <td class="yum"><code>/etc/yum.conf</code> (or <code>/etc/dnf/dnf.conf</code>), <code>/etc/yum.repos.d/</code></td>
    <td class="apt"><code>/etc/apt/sources.list</code>, <code>/etc/apt/sources.list.d/</code></td>
    <td class="snap">?</td>
    <td class="flatpak">Via command line: <code>flatpak remote-add</code></td>
</tr>
<tr>
    <td class="description">Easy GUI</td>
    <td class="yum">apper</td>
    <td class="apt">synaptic</td>
    <td class="snap">?</td>
    <td class="flatpak">?</td>
</tr>

<tr>
    <th colspan="6">Installing software</th>
</tr>
<tr>
    <td class="description">Install a package by name</td>
    <td class="yum"><code>yum install PACKAGE</code></td>
    <td class="apt"><code>apt install PACKAGE</code></td>
    <td class="snap"><code>snap install PACKAGE</code></td>
    <td class="flatpak"><code>flatpak install REMOTENAME com.company.PACKAGE</code></td>
</tr>
<tr>
    <td class="description">Install a package from a file</td>
    <td class="yum"><code>yum install filename.rpm</code></td>
    <td class="apt"><code>apt install filename.deb</code></td>
    <td class="snap">?</td>
    <td class="flatpak">?</td>
</tr>
<tr>
    <td class="description">Uninstall a package</td>
    <td class="yum"><code>yum remove PACKAGE</code></td>
    <td class="apt"><code>apt remove PACKAGE</code></td>
    <td class="snap"><code>snap remove PACKAGE</code></td>
    <td class="flatpak"><code>flatpak uninstall com.company.App</code></td>
</tr>

<tr>
    <th colspan="6">Finding packages and files</th>
</tr>
<tr>
    <td class="description">List installed packages</td>
    <td class="yum"><code>yum list installed</code> or <code>rpm -qa</code></td>
    <td class="apt"><code>dpkg -l</code> <em>(lowercase L)</em></td>
    <td class="snap"><code>snap list</code></td>
    <td class="flatpak"><code>flatpak list</code></td>
</tr>
<tr>
    <td class="description">See files installed by a package</td>
    <td class="yum"><code>rpm -ql PACKAGE</code></td>
    <td class="apt"><code>dpkg-query -L PACKAGE</code></td>
    <td class="snap">N/A; see <code>/snap</code> <em>(note 3)</em></td>
    <td class="flatpak">N/A <em>(note 3)</em></td>
</tr>
<tr>
    <td class="description">Find what package installed a file</td>
    <td class="yum"><code>rpm -qf /path/to/file</code></td>
    <td class="apt"><code>dpkg-query -S /path/to/file</code> <em>(capital S)</em></td>
    <td class="snap">?</td>
    <td class="flatpak">?</td>
</tr>

<tr>
    <th colspan="6">Getting package information</th>
</tr>
<tr>
    <td class="description">Get information about an installed package</td>
    <td class="yum"><code>rpm -qi PACKAGE</code></td>
    <td class="apt">?</td>
    <td class="snap">?</td>
    <td class="flatpak"><code>flatpak info com.company.App</code></td>
</tr>
<tr>
    <td class="description">Get information about a package that may or may not be installed</td>
    <td class="yum"><code>yum info PACKAGE</code></td>
    <td class="apt"><code>apt show PACKAGE</code></td>
    <td class="snap"><code>snap info PACKAGE</code></td>
    <td class="flatpak">?</td>
</tr>
<tr>
    <td class="description">Find what package (that may or may not be installed) provides a file (pattern/glob)</td>
    <td class="yum"><code>yum provides PATTERN</code></td>
    <td class="apt"><code>apt-file search PATTERN</code> <em>(note 1)</em></td>
    <td class="snap">?</td>
    <td class="flatpak">?</td>
</tr>

<tr>
    <th colspan="6">Updating packages</th>
</tr>
<tr>
    <td class="description">Update list of available packages <em>(note 2)</em></td>
    <td class="yum"><code>yum check-update</code></td>
    <td class="apt"><code>apt update</code></td>
    <td class="snap">N/A</td>
    <td class="flatpak">N/A</td>
</tr>
<tr>
    <td class="description">Update installed packages to the latest version</td>
    <td class="yum"><code>yum update</code></td>
    <td class="apt"><code>apt upgrade</code></td>
    <td class="snap"><code>snap refresh</code> <em>(note 4)</em></td>
    <td class="flatpak"><code>flatpak update</code></td>
</tr>

</tbody>
</table>

Notes:

1. `apt-file` uses a separate file database than the other mentioned tools. You will need to run `apt-file update` before it can provide useful information.
2. `yum` always checks for updates to the list of available packages when you upgrade the packages installed on your system (which `yum` confusingly calls "updating"), so running `yum check-update` is optional. Conversely, `apt` has separate concepts for _updating_ the list of available packages, versus _upgrading_ your installed packages to the latest version. You need to update your packages before you can upgrade your system.
3. Snap and flatpak both work using a virtual container style model. Their files are contained in their respective images.
4. `snapd` updates its lists and packages automatically, four times a day, by default.
5. `dnf` was introduced as an alternative to `yum` in Fedora 22 and CentOS 7, and replaces `yum` in later versions. All the commands for `dnf` are the same as for `yum` (except that `yum list installed` becomes `dnf list --installed`).

Updated layout inspired by [this comprehensive PDF](http://johnmeister.com/linux/PDF-info/PackageManagementCheatSheet.pdf). I discovered that after creating this. Check it out if you're interested in openSUSE, Mandriva, Vector, Arch, or smart.
