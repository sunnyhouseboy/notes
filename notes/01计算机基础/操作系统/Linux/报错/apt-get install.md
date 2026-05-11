apt-get install <packagename>
Reading package lists... Done
Building dependency tree... Done
Package aptitude is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
E: Package <packagename> has no installation candidate

解决办法：
 apt-get update
apt-get upgrade
apt-get install <packagename>