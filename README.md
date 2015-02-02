# My docker host for Vagrant.

Uses chef zero to install docker and chef-dk on a centos 6.6 VM. Requires berkshelf for getting the cookbooks.


````
berks vendor
vagrant up
````

## Providers

This should work with virtualbox, vmware, and parallels, but I'm only running it on vmware.
