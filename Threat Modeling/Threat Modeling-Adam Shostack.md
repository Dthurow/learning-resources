

Threat Modeling by Adam Shostack
https://www.goodreads.com/book/show/18379732-threat-modeling

# Chapter One - Dive In and Threat Model!

Basic questions during threat modeling:
* What are you building?
* What can go wrong?
* What should you do about those things that can go wrong?
* Did you do a decent job of analysis?

**Vocab** - Trust boundaries

Boundaries wherever different people control different things. Good examples of this include the following:

* Accounts (UIDs on unix systems, or SIDS on Windows)
* Network interfaces
* Different physical computers
* Virtual machines
* Organizational boundaries
* Almost anywhere you can argue for different privileges

**Vocab** - Attack Surface

Attack surface is the parts of a system that are exposed to attackers. So a company with lots of APIs and externally facing websites has a larger attack surface than a company with a single website. An attack surface is a trust boundary and a direction from which an attacker could launch an attack

## What are you building?

* Build diagram of discrete parts in system (Can use data flow), diagram on whiteboard/Visio/etc.
* Draw out known trust boundaries

## What can go wrong?

Suggests playing Elevation of Privilege game. Link in book is broken, correct link now: https://www.microsoft.com/en-us/download/details.aspx?id=20303

**Vocab** - STRIDE 

STRIDE is a mnemonic to help determine what can go wrong

* **Spoofing** is pretending to be someone/thing you're not.
* **Tampering** is messing with data you're not supposed to be messing with
* **Repudiation** means claiming you didn't do something (regardless of whether you did or not).
* **Information Disclosure** giving out more info than you mean to
* **Denial of Service** are attacks designed to prevent a system from providing service, including by crashing it, making it unusably slow, or filling all its storage.
* **Elevation of Privilege** is when a program or user is technically able to do things that they're not supposed to do.



## What should you do about those things that can go wrong?

Ways to deal with discovered threats:
* Mitigate - changing how things are done in order to make it harder to actually exploit the issue that was found
* Eliminate - completely remove the ability to exploit the issue found (NOTE: can often easiest be done by removing functionality, which has potentially negative business impact)
* Transfer - make the threat someone else's issue by, e.g., buying a product to support login functionality and assume they're making authentication secure. Note that this doesn't guarentee the issue is no longer something that can happen, it's just something you can't do anything about anymore.
* Accept the risk - If all options to mitigate a risk have too high a cost, or the issue is very unlikely to happen, may make sense to simply accept the risk and not worry about it. E.g. not trying to make your software NSA-proof because the cost of doing that is way too much.

Mitigation is normally the best option for the business and clients (minimize risks while maximizing functionality for clients)

### General Mitigation strategies
* Leverage Operating Systems defaults
    * ACLs
    * private directory structures
    * application identifier that the OS will enforce
    * OS memory protection
* Crypto
    * DNSSEC
    * SSL
    * IPsec
    * File Encryption
    * Disk Encryption
* Logs
* Use Type-safe Languages
* Structure systems for resiliency
* Sandbox
* Validate data from outside trust boundaries before using. NOTE: trying to sanitize isn't recommended, instead put the burden of correct data on external entities to avoid subtle bugs in sanitization functions

### File Bugs
Now that there's a list of issues and ways to fix them, create bug reports for them!

Prioritize them so the largest threats get taken care of first. Presumably the book later talks about how to prioritize?

## Checking your work
Steps for checking your work are
* checking the model
* checking that you've looked for each threat
* checking your tests

### Check the model
Make sure it actually matches with what was built. Complete, accurate, etc. If needed, update and check for threats as more info comes in. Try to balance completeness with usability. If you gotta squint or its a mass of lines, maybe simplify or break out into different diagrams.

### Check each threat
Make sure you've dealt with each found threat: mitigate, eliminate, transfer, or accept it. 

### Check your tests
For each threat, build out tests that detect the problem. Either manual or automatic, and included with standard software tests, so the security issues don't come back in future releases.

## Chapter One Key Conclusions
Basics of threat modeling are
1. Build a diagram of your system as complete as possible w/o confusion
2. Work through, in an organized manner, all parts of the diagram, (can use STRIDE or Elevation of Privilege game) to create a list of threats/issues to deal with
3. For each issue, create a mitigation plan, file a bug, and create tests to validate when the issue is fixed, it stays fixed
4. Review diagram, check your work, and fix any new threats/issues as needed