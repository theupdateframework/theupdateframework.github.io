---
layout: default
css_id: faq
---

### Frequently Asked Questions

**1. How difficult is it to integrate TUF?**
  At a high level, an adopter only needs to (1) add TUF metadata to its
  software repository and (2) arrange for clients to use a TUF library to fetch
  files from the repository.

  In practice, (1) will also require management of the keys needed to sign TUF
  metadata, code to periodically update and re-sign metadata, and the initial
  task of deciding how to organize the metadata and delegations available to
  clients.  For (2), the adopter has to figure out how to ship the initial Root
  file, andn implement TUF in their language of choice if one of the existing
  implementations is insufficient.

**2. Has there been a security audit of TUF?**
  The [Security Audits](https://theupdateframework.github.io/audits.html) page
  links to a few of the security audits provided by the NCC group.  A security
  audit by [Cure53](https://cure53.de/) is anticipated in June 2018.

**3. Can TUF be used with weaker devices?**
  At a minimum, a client device must verify the hashes and signatures on TUF
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
  The repo maintainer must revoke and replace compromised keys.  If a
  Timestamp, Snapshot, Targets, or Root key is compromised, the Root role must
  re-sign its metadata to replace the compromised key.  If a threshold of Root
  keys are compromised, the Root file must be re-issued out of band.  It is
  advised that a threshold number of offline keys be used to make a full
  compromise of the repo unlikely.  For a more in-depth discussion on the steps
  to follow in the event of a key compromise, see [PEP
  458](https://www.python.org/dev/peps/pep-0458/#in-the-event-of-a-key-compromise),
  which covers one way to deal with compromised keys on a community repo such
  as PyPI.

**6. Can I use the same keys for different roles?**
  In general, you shouldn't share keys.  In certain cases, even sharing online
  keys (e.g., between the Timestamp and Snapshot roles) is not advised.  As we
  recommend for the PyPI community, "different keys for online roles allow for
  each of the keys to be placed on separate servers if need be, and prevents
  side channel attacks that compromise one key from automatically compromising
  the rest of the keys."

**7. How can I try TUF?**
   The [Getting
   Started](https://github.com/theupdateframework/tuf/blob/develop/docs/GETTING_STARTED.rst)
   page contains instructions to install and run the reference implemention.
   The client and repo tools can be used to quickly create TUF repositories and
   experiment with software updates.

**8. Which roles can use online keys?**
  The Timestamp and Snapshot roles can use online keys to facilitate continuous
  delivery of updates on the typically repository.  All other roles should rely
  on offline keys to prevent attackers from signing for malicious packages in
  the event of a repo compromise.

**9. What's the point of having the Root and Snapshot roles?**
  The Root role keeps track of the trusted public keys of the top-level roles,
  removing or adding keys when needed.  Its metadata is rarely updated and its
  signing keys protected the most.  In contrast, the Snapshot role is updated
  often, signed with an online key, and provides a consistent view of the
  metadata available on a repo.  The Snapshot and Root role are responsible for
  different tasks that differ in level of importance.  Responsibility
  separation is one of TUF's design choices.

**10. Is there a presentation or video about TUF?**
  The [Videos](https://theupdateframework.github.io/videos.html) page contains
  links to presentations that have been given by us and adopters.

**11. How often should metadata expire?**
  The Timestamp and Snapshot metadata should normally have a short expiration
  (1 day), whereas the Root and Targets metadata should expire less often (1
  year).  A good rule of thumb is that metadata should expire sooner the more
  often it changes.

**12. Why should I use delegations?**
  As we state in the specification: "Delegated roles can further delegate trust
  to other delegated roles. This provides for multiple levels of trust
  delegation where each role can delegate full or partial trust for the target
  files they are trusted for."  You should use delegations because they provide
  more security.  For instance, in a community repository like PyPI, delegating
  trust of target files to a project developer is recommended to achieve
  compromise resilience.  An attacker cannot serve malicious files for the
  developer's project because they don't have access to the developer's project
  keys.
