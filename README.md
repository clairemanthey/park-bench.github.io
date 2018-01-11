# Organization Description
This is a collection of software built as a support system for a SecureDrop
instance. It contains four primary components: 

* gpgmailer sends encrypted email
* torwatchdog discreetly monitors the status of a hidden service
* watchman monitors a physical location with a camera
* netcheck attempts to keep Internet access

torwatchdog, watchman, and netcheck can all be used independently of each
other, but require gpgmailer.

These programs are still in development and may not be production-ready.
However, if you do use our software, please let us know. Any feedback is
extremely helpful.

# Motivation
We initially developed these applications while planning a local SecureDrop
instance, but chose to only continue developing the supporting monitoring
software.

# Detailed Descriptions

## [Gpgmailer](https://github.com/park-bench/gpgmailer)
Gpgmailer is a daemon that sends encrypted email and includes a Python library
to add messages to its' queue.  The Python library, gpgmailqueue, accepts a
subject, body, and an arbitrary number of attachments, then writes the
unencrypted message to a file defined in the configuration file. The daemon
reads the file, builds the email, signs, encrypts, and sends a
properly-formatted PGP/MIME email to each configured recipient.

## [Torwatchdog](https://github.com/park-bench/torwatchdog)
Torwatchdog is a relatively simple URL checking daemon that uses Tor and times
each request randomly. It starts its own Tor instance and randomly selects from
a specified list of nameservers. When the daemon detects a state change, either
up or down, it sends an encrypted email notification via Gpgmailer.

## [Watchman](https://github.com/park-bench/watchman)
Watchman is a daemon that monitors a camera for motion and responds by taking
several pictures. Those pictures are then sent in an encrypted email via
Gpgmailer. It detects and properly ignores background changes.

## [Netcheck](https://github.com/park-bench/netcheck)
Netcheck is a daemon that attempts to keep a working Internet connection at all
times. It first checks the wired network for an address and for DNS capability.
If that fails, it does the same with the backup wifi network, and if that
fails, it checks a list of supplemental wifi networks. If all of that fails, it
just keeps trying.

## [Confighelper](https://github.com/park-bench/confighelper)
Confighelper is a class with a collection of helper methods for parsing
configuration files, performing very basic value-checking, and setting up
logging in a particular way. All of our projects depend on this library.


# Build/Install Instructions
Each package can be built in any order, but Confighelper must be installed
first, Gpgmailer must be installed second, and then Torwatchdog, Watchman, and
Netcheck may be installed in any order. Each of these projects has specific
build instructions on their respective project pages.


# Contact
We would love to know if you are using any of our projects! Even one user is a
strong motivator for us, so please contact us with any questions or comments,
either through Github or email.

* eviljoel: eviljoel (at) linux (dot) com, PGP fingerprint: A2BE 2D12 24D1 67CA 8830  DDE7 DFB3 676B 196D 6430
* andklapp: andklapp (at) null (dot) net, PGP fingerprint: C5FB D515 CE2C 67B0 088D  BD5E D78A DB07 F66B 6AE4
* brittdog: bkscaccia (at) gmail (dot) com, PGP fingerprint: 31C4 04D0 5658 35D7 F469  55DF 05FF 70C5 3851 1342

# License
These projects are all licensed under the Gnu Public License version 3.  This
description project is licensed under the Creative Commons
Attribution-ShareAlike 4.0 International license.

# Special Thanks
We'd like to thank to the now defunct [CivicLab](http://www.civiclab.us/) and it former operators, Benjamin Sugar and [Tom Tresser](http://www.tresser.com/). CivicLab provided some early support for our project by providing regular meeting and storage space.

Mr. Tresser is an especially vocal community activist. As a thank you to him, we would like to bring your attention to his book, [Chicago Is Not Broke](http://wearenotbroke.org/).
