# Deb Flavors
## dpkg - local packages
 * --install // -i \*.deb
 * --remove // -r \*.deb
 * --purge // -P \*.deb
 **also remove config files
 * --force-depends \*.deb
 * --info
 * --status // -s
 **abbreviated form of info
 * --list // -l
 **(installed files)
 * --list-files // -L
 **(files from installed packages)
 * --search // -S
 **(installed packages)
 * dpkg-reconfigure \*.deb
## apt-* - remote packages (managed w/dpkg)
* apt-get install <package-name>
* apt-get update
**update info at repositories
* apt-get --only-upgrade
**upgrade only if installed
* apt-get \[dist-\]upgrade
**upgrade \*all\*
* apt-get remove
**same as above
* apt-get purge
**same as above
* apt-cache search \*
**package existent in repositories?
* apt-cache show \*
**package information
* apt-cache showpkg \*
**technical information
### config
 * repositories: /etc/apt/sources.list
 * files: /etc/apt/sources.list.d/
 ** deb = binary
 ** deb-src = source

# RPM Flavors
## rpm - local packages
 * --install // -ivh
 ****i**nstall, **v**erbosely, with **h**ashmarks
 * --nodeps
 **ignore dependent packages
 * --replacefiles
 **duplicate files
 * --force
 **truly forced
 * --rebuilddb
 **see below
 * --checksig // -K \*.rpm
 * --import \*site\*
 **get gpg key
 * --verify // -Va
 ****V**erify **a**llInstalled
 * --upgrade // -U
 * --freshen // -F
 * --erase // -e pkg[.rpm]
 **\[--allmatches\] \[--nodeps\]
 * -q\[i\]\[l\]\[p\] \[--changelog\]
 ****q**uery **i**nfo **l**istItsFiles **p**ackageOnDisk
 **show revision history, not database
 * -qc
 **show only configuration files
 * -qRp
 ****q**uery **R**equirements of **p**ackagesOnDisk
 * -qf
 ****q**uery package owning **f**ile
## yum
 * \[-y\] install
 **\[skip confirmation\]
 * install --download only
 **do not install
 * yumdownloader --source --urls
 **yum install --resolve --destdir
 * \[check-\]update \[*\] // upgrade \[\*\]
 * list \[package\]
 **search repositories
 * search \*string\*
 **in package info
### config
 * /etc/yum.conf
 * /var/cache/yum
 * /var/log/yum.log
 * /etc/yum.repos.d/
 * --enablerepo \*reponame\*
