MaNo Core staging tree 0.12.2
===============================


What is MaNo?
----------------

MaNo is an experimental new digital currency that enables anonymous, instant
payments to anyone, anywhere in the world. MaNo uses peer-to-peer technology
to operate with no central authority: managing transactions and issuing money
are carried out collectively by the network. MaNo Core is the name of the open
source software which enables the use of this currency.


License
-------

MaNo Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

<<<<<<< HEAD
A Linux bash script that will set up traffic control (tc) to limit the outgoing bandwidth for connections to the Mano network. This means one can have an always-on manod instance running, and another local manod/mano-qt instance which connects to this node and receives blocks from it.
=======
The `master` branch is meant to be stable. Development is normally done in separate branches.
[Tags](https://github.com/MaNodev-the-man/MaNo/tags) are created to indicate new official,
stable release versions of MaNo Core.
>>>>>>> master

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

Testing
-------

<<<<<<< HEAD
### [Debian](/contrib/debian) ###
Contains files used to package manod/mano-qt
for Debian-based Linux systems. If you compile manod/mano-qt yourself, there are some useful files here.
=======
Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.
>>>>>>> master

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

The Travis CI system makes sure that every pull request is built for Windows
and Linux, OS X, and that unit and sanity tests are automatically run.

<<<<<<< HEAD
### [TestGen](/contrib/testgen) ###
Utilities to generate test vectors for the data-driven Mano tests.
=======
### Manual Quality Assurance (QA) Testing
>>>>>>> master

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

