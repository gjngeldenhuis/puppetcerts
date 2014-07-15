# Puppet Certificate Management
An attempt at explaining certificate usage in Puppet and how to use an external CA like Thawte, Verisign, etc.

## PuppetDB
/opt/puppet/sbin/puppetdb-ssl-setup

## MCollective

## General
A list of all certificates ever issued by Puppet’s CA can be found in the file $cadir/inventory.txt.


## List of certificates:
* master.puppetlabs.vm
* pe-internal-broker
* pe-internal-dashboard
* pe-internal-mcollective-servers
* pe-internal-peadmin-mcollective-client
* pe-internal-puppet-console-mcollective-client

## Usefull commands
Run this command in bash to create a shortcut to view certificates with.
```bash
function viewcert { openssl x509 -in $1 -noout -text; }
```
