Minimal Certificate Authority
=============================

Implements some scripts that can create a certificate authority (CA),
CSRs and mint certificates.

The generated CA has a form that is common - a root CA certificate with
a very long life-time, and an intermediate (issuing) CA certioficate
derived from the root certificate.

The intermediate CA certificate is then used to sign CSRs for general use.


Dependencies 
------------

* `bash`
* `openssl` command-line tool


Usage
-----

#. Edit details in `config.env`
#. Execute `x509-ca` to generate a CA
#. Create certificate signing requests for your servers with `x509-req`.
#. Use `x509-sign`  to sign a CSR with the CA certificates.


Security
--------

The goal here is not high security - it's to make something quick and
easy to use for development and testing purposes. The biggest issue is
probably that the root and intermediate CA files are all in the same
directory - the only thing protecting the root cert is the password on 
the root key.  In a real CA, the root key would be on an air-gapped
system and only ever unlocked for signing intermediate certs.  

There's no support for hardware security modules (HSMs) here either -
the only thing protecting the private keys is the pass-phrases that
encrypt them.

Within these limitations, the following practises are probably advisable:

* Don't set `CA_ROOT_PASS`, `CA_INT_PASS` or `PASS` environment
  variables in the config file (or your `~/.profile`) - use interactive
  prompting instead.
* Generate CSRs on the servers where the certificate will be used, and
  never copy the private key to any other system.
* Good pass phrases!


Still To Do
-----------

* `x509-rev`: certificate revokation
* `x509-crl`: generate certificate revocation lists
* `x509-ca`: options for CA cert lifetimes


License
-------

This is Free software, released under the terms of the GNU GPL v3. See
the `LICENSE` file for more details.

