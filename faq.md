---
layout: default
css_id: faq
---

### Frequently Asked Questions

**1. How difficult is it to integrate TUF?**

**2. Has there been a security audit of TUF?**
The [Security Audits](https://theupdateframework.github.io/audits.html) page
lists a few of the security assessments that have been publicly conducted by
others, such as the NCC group.  Papers on TUF have been reviewed by security
experts in academia, and published to security conferences like USENIX ATC and
NSDI, and CCS.

**3. Can TUF be used with weaker hardware, such as medical devices?**
Yes.  [Uptane](https://uptane.github.io/), a variant of TUF, is designed to
work with the Electronic Control Units found in automobiles.

**4. Can you combine Timestamp and Snapshot?**
There are a few reasons why the timestamp.json and snapshot.json files are not
combined.

* The timestamp.json file is downloaded very frequently and so should be kept
as small as possible, especially considering that the snapshot.json file grows
proportionally with the number of delegated target roles.

* As the Timestamp role’s key is an online key and thus at high risk,
separate keys should be used for signing the snapshot.json file so that the
Snapshot role’s keys can be kept offline, and thus more secure.

* Timestamp.json may be given to mirrors.

**5. What happens when you have to revoke a key?**

**6. Can I use the same keys for different roles?**

**7. How can I experiment with TUF?**
   The [Getting
   Started](https://github.com/theupdateframework/tuf/blob/develop/docs/GETTING_STARTED.rst)
   page contains instructions on how to install the reference implementation of
   TUF, including a quickstart guide and tutorial.  The CLI and client tools
   can be used to quickly create TUF repositories and experiment with software
   updates.  You can also experiment with
   [Notary](https://github.com/theupdateframework/notary) (based on TUF), which
   allows anyone to have trust over arbitrary collections of data.

**8. Can I use an online key to sign the Targets role?**

**9. What's the point of having the Root and Snapshot roles?**

**10. Is there a presentation or video about TUF?**
The [Videos](https://theupdateframework.github.io/videos.html) page contains
links to presentations that have been given by us and adopters.

**11. How often should role metadata expire?**

**12. How do you recover from a repository attack?**

**13. What happens if a key is compromised?**

**14. Why should I use delegations?**
