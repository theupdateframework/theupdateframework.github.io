---
layout: default
css_id: faq
---

### Frequently Asked Questions

**1. How difficult is it to integrate TUF?**


**2. Has there been a security audit of TUF?**
  The [Security Audits](https://theupdateframework.github.io/audits.html) page
  links to a few of the security audits done by the NCC group.  A security
  audit by [Cure53](https://cure53.de/) is anticipated in June 2018.

**3. Can TUF be used with weaker devices?**
  At a minimum, a client device must verify the hashes and signatures on
  metadata.  If a device isn't powerful enough to perform cryptographic
  operations or has limited memory, it can delegate verification of hashes and
  signatures to another device.  For instance, a weaker device can rely on
  another device on the network to verify the signatures on top-level metadata.
  Delegating to another device is not built into the framework but
  [Uptane](https://uptane.github.io/), a variant of TUF, is designed to work
  with weaker devices like the Electronic Control Units found in automobiles.

**4. Can you combine Timestamp and Snapshot?**
  There are a few reasons why the timestamp.json and snapshot.json files are
  not combined:

  * The timestamp.json file is downloaded very frequently and so should be kept
  as small as possible, especially considering that the snapshot.json file
  grows proportionally with the number of delegated target roles.

  * As the Timestamp role’s key is an online key and thus at high risk,
  separate keys should be used for signing the snapshot.json file so that the
  Snapshot role’s keys can be kept offline, and thus more secure.

  * Timestamp.json may be given to mirrors.

**5. What happens if the server and keys are compromised?**

**6. Can I use the same keys for different roles?**

**7. How can I try TUF?**
   The [Getting
   Started](https://github.com/theupdateframework/tuf/blob/develop/docs/GETTING_STARTED.rst)
   page contains instructions to install and run the reference implemention.
   The client and repo tools can be used to quickly create TUF repositories and
   experiment with software updates.

**8. Can I use an online key to sign the Targets role?**

**9. What's the point of having the Root and Snapshot roles?**

**10. Is there a presentation or video about TUF?**
  The [Videos](https://theupdateframework.github.io/videos.html) page contains
  links to presentations that have been given by us and adopters.

**11. How often should metadata expire?**

**12. Why should I use delegations?**
