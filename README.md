# Puppet Certificate Management
An attempt at explaining certificate usage in Puppet and how to use an external CA like Thawte, Verisign, etc.

## RTFM list
[X.509](http://en.wikipedia.org/wiki/X.509)


## PuppetDB
/opt/puppet/sbin/puppetdb-ssl-setup

## MCollective

## General
A list of all certificates ever issued by Puppet’s CA can be found in the file $cadir/inventory.txt.


## List of internall generated certificates:
* master.puppetlabs.vm
* pe-internal-broker
* pe-internal-dashboard
* pe-internal-mcollective-servers
* pe-internal-peadmin-mcollective-client
* pe-internal-puppet-console-mcollective-client

## Usefull commands
Run these commands in bash to create a shortcut to view certificates with.
```bash
function viewcert { openssl x509 -in $1 -noout -text; }
function certcompare { vimdiff <(viewcert $1) <(viewcert $2); }
```

## CA Directory disection
Where not specified, just use the viewcert bash function to view a certificate. Anything else is not going to be a certificat and will need a different command.
```bash
tree  $(puppet config print ssldir)
/etc/puppetlabs/puppet/ssl
├── ca
│   ├── ca_crl.pem
│   ├── ca_crt.pem
│   ├── ca_key.pem
│   ├── ca_pub.pem
│   ├── inventory.txt
│   ├── private
│   │   └── ca.pass
│   ├── requests
│   ├── serial
│   └── signed
│       ├── master.puppetlabs.vm.pem
│       ├── pe-internal-broker.pem
│       ├── pe-internal-dashboard.pem
│       ├── pe-internal-mcollective-servers.pem
│       ├── pe-internal-peadmin-mcollective-client.pem
│       └── pe-internal-puppet-console-mcollective-client.pem
├── certificate_requests
├── certs
│   ├── ca.pem
│   ├── master.puppetlabs.vm.pem
│   ├── pe-internal-broker.pem
│   ├── pe-internal-mcollective-servers.pem
│   ├── pe-internal-peadmin-mcollective-client.pem
│   └── pe-internal-puppet-console-mcollective-client.pem
├── crl.pem
├── private
├── private_keys
│   ├── master.puppetlabs.vm.pem
│   ├── pe-internal-broker.pem
│   ├── pe-internal-mcollective-servers.pem
│   ├── pe-internal-peadmin-mcollective-client.pem
│   └── pe-internal-puppet-console-mcollective-client.pem
└── public_keys
    ├── master.puppetlabs.vm.pem
    ├── pe-internal-broker.pem
    ├── pe-internal-mcollective-servers.pem
    ├── pe-internal-peadmin-mcollective-client.pem
    └── pe-internal-puppet-console-mcollective-client.pem
```

```bash
ca/ca_crl.pem
```
Certificate revocation list, to view this file run:
```bash
openssl crl -in ca/ca_crl.pem -noout -text
```

```bash
ca/ca_crt.pem
```
The CA certificate

```bash
ca/ca_key.pem
```
The CA private key. For the sake of completeness the command to view it is:
```bash
openssl rsa -in ca/ca_key.pem -noout -text
```


