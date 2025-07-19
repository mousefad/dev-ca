Minimal Certificate Authority
=============================

Implements some scripts that can create a certificate authority (CA), CSRs
and mint certificates.

The generated CA has a form that is common - a root CA certificate with a
very long life-time, and an intermediate (issuing) CA certioficate derived
from the root certificate.

The intermediate CA certificate is then used to sign CSRs for general use.


Dependencies 
------------

* `bash`
* `openssl` command-line tool


Usage
-----

#. Edit details in `config.env`
#. Execute `x509-ca` to generate a CA
#. Create certificate signing requests for your servers with `x509-csr`.
   To be secure this should be done on the servers where the certificates 
   are to be used so that the generated private key never leaves the 
   machine. The .csr file does not conrain any sensitive data and can be
   copied safely to the CA machine
#. Use `x509-sign`  to sign a CSR with the CA certificates, and copy the
   resulting certificate to the host where it will be used


