
**CIA** - Confidentiality, Integrity, Availability. Each of these are important to a different extent for a system you're securing.

**Trust boundaries** - boundaries wherever different people control different things. E.g. a webserver w/ business logic is in a corporate data center, while the database is in an offsite web storage location (say in the cloud)

**Attack Surface** - An attack surface is a trust boundary and a direction from which an attacker could launch an attack

**STRIDE** - a mnemonic to help determine what can go wrong. Stands for Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, and Elevation of privilege. 

**Spoofing** - pretending to be someone/thing you're not.

**Tampering** - messing with data you're not supposed to be messing with

**Repudiation** - means claiming you didn't do something (regardless of whether you did or not)

**Information Disclosure** - giving out more info than you mean to

**Denial of Service** - attacks designed to prevent a system from providing service, including by crashing it, making it unusably slow, or filling all its storage

**Elevation of Privilege** - when a program or user is technically able to do things that they're not supposed to do

**ACL** - Access Control List, a list of permissions associated with a system resource (object). An ACL specifies which users or system processes are granted access to objects, as well as what operations are allowed on given objects

**DNSSEC** - Domain Name System Security Extensions. designed to protect applications from using forged or manipulated DNS data. I.e. protect from DNS cache poisoning. Also protects IP addresses

**IPsec** -  Internet Protocol Security. Authenticates and encrypts the packets of data to provide secure encrypted communication between two computers over an Internet Protocol network. It is used in virtual private networks (VPNs).