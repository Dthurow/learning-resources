# Danielle's notes (tl;dr of lecture)
Despite being high on the list when searching youtube for threat models, doesn't really talk about the process of threat modeling. Mainly an intro to a general Systems Security class (which you can watch for free and get lecture notes, etc. from MIT!). I stopped watching at 50:17 since it looks like he just goes into talking about buffer overflows for the rest of the class (based on the lecture notes). Good for some examples of how security can go wrong and some things to think about when securing a system. 

Video link: https://www.youtube.com/watch?v=GqmQg-cszw4
MIT course link: https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/


# Intro
Computer Systems Security, Threat Models video from MIT OpenCourseware 2014

Secure System: can do what it is supposed to do despite adversary

1. Policy - what you want your system to do, based on CIA (confidentiality, Integrity, Availability)
2. Threat Model - set of assumptions about adversary
3. Mechanisms - software/hardware/systems to enforce policy

Securing a system is an iterative process, requires you to update one or more of these points, then have to update security. 

All systems have breaking points, but that doesn't make them useless. Understand when breaking points are applicable to securing the system or not. 

Security mechanisisms can help improve functionality of the systems (e.g. running x86 native code in browser because it's fully sandboxed) 

# How Security Goes Wrong

## how to screw up systems policy

### Account recovery questions
E.g. if you forgot your email password, you can answer security questions to log in. (because you can't do an email with password link because you're locked out of your email). *Then policy changes*. Log in becomes either know password or know security question answers.

E.g. Multiple systems interacting with each other can cause issues. Matt honen was editor at wired.com. Bad guy got into his gmail account. 
*HOW* Gmail's reset password function sends a reset password link to old email (e.g. foo@me.com). Apple's me.com site allows reset password if you know your billing address and last 4 of credit card number. Amazon can add new credit card number to an account. Amazon's password reset requires you to provide a credit card number associated with the account. So you can get into the amazon account with that. Amazon will show last 4 numbers of credit cards. Then break into me.com, then get into gmail account. 

#### moral of the story
- Be conservative in policy
- Think hard

## How to screw up Threat models

### Human Factor
Don't assume humans will do certain security things cuz they'll mess up at some point

### Threat models change over time.
E.g. MIT in 1980s, made system Kerberos. Decided 56-bit DES size of keys for their crypto was good. Now, it's easy to enumerate all possible keys and it takes about a day. 

E.g. Hardware - used to assume physical hardware wasn't comprimised. But now we know Feds/Govt can comprimise it so that's not a good assumption anymore if you're trying to protect yourself from the Govt. 

E.g. SSL/TLS verifies a certificate against CA (certificate Authority). Originally assumed all CA's are trustworthy and never make a mistake. But over 300 CAs nowadays, can't really assume they're all great. 


### Other Examples
E.g. DARPA wanted to build secure OS. Got a bunch of examples from universities and then hired red team to try to break them. One example of red team breaking in: Instead of trying to hit server, accessed OS code on some dev server, added back door into code, so in the future researchers built the OS from the dev server and OS had back door. 

More in lecture notes https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/

## How to screw up Mechanisms

E.g. Apple's iCloud. Lets you store files, photosharing, and find your iPhone. Didn't enforce the same mechanism at all interfaces. On find my iphone interface it didn't track how many times you entered an invalid password. So vuln to brute forcing. There was a max password attempt on other interfaces, but they forgot to add it to the find my iphone. Once they guess on find my iphone, they have access to files and photos, etc.

E.g. Citibank website that allows you to look at credit card info. Got to site, login/pw, then go to new url (e.g. citi.com/acct?id=1234). Someone figured out if you change id in querystring, get other persons account. 

E.g. Android bitcoin. Android application were getting rand values to generate private keys from Java SecureRandom(). That function calls a pseudo random number generator(PRNG), but sometimes the java library forgets to seed the PRNG, so then you can access the private key for that bitcoin owner, steal their bitcoins.

*NOTE* to break the system, look to edge cases. 

E.g. SSL encoding scheme. SSL certificate has length of hostname, followed by hostname.(e.g. 10amazon.com) Browser null terminates the string(amazon.com\0). Could ask for certificate: amazon.com\0x.foo.com. Get certificate from CA and they'd be okay with that because it's a subdomain. Browser reads until null string, so displays amazon.com with valid certificate. 

*NOTE* disagreement on how storing data can lead to security issues

# Case Study: Buffer Overflows

Example system: Web server. Accepts requests, sends back replies, talks with database.

Policy: web server should do what the programmer wants it to do
Threat Model: adversary doesn't have physical access, but can send any request to the web server. 
Mechanism: mechanism is the web server software. 

Pulls up C function (from lecture notes)

*NOTE* stopped watching at this point. 