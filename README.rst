Electrum - Lightweight Bitcoin client
=====================================

::

  Licence: MIT Licence
  Author: Thomas Voegtlin
  Language: Python (>= 3.6)
  Homepage: https://electrum.org/


.. image:: https://api.cirrus-ci.com/github/spesmilo/electrum.svg?branch=master
    :target: https://cirrus-ci.com/github/spesmilo/electrum
    :alt: Build Status
.. image:: https://coveralls.io/repos/github/spesmilo/electrum/badge.svg?branch=master
    :target: https://coveralls.io/github/spesmilo/electrum?branch=master
    :alt: Test coverage statistics
.. image:: https://d322cqt584bo4o.cloudfront.net/electrum/localized.svg
    :target: https://crowdin.com/project/electrum
    :alt: Help translate Electrum online





Getting started
===============

(*If you've come here looking to simply run Electrum,* `you may download it here`_.)

.. _you may download it here: https://electrum.org/#download

Electrum itself is pure Python, and so are most of the required dependencies,
but not everything. The following sections describe how to run from source, but here
is a TL;DR::

    sudo apt-get install libsecp256k1-0
    python3 -m pip install --user .[gui,crypto]


Biometric extension
-------------------

This works together with an `R503`_ fingerprint sensor. For communication with the sensor a linux device with a usable serial port is required. The preffered method of interaction is using a Raspberry Pi with `PiGpio`_ installed. Compile the necessary C library with::

    ./electrum/biometric-experiments/makesharedlib.sh
.. _R503: http://download.mikroe.com/documents/datasheets/R503_datasheet.pdf
.. _PiGpio: http://abyz.me.uk/rpi/pigpio/
For more info see :code:`electrum/biometric-experiments/README.md`.

*Premise:*
  * Tedious remembering and storing of various passwords. Mass adoption of crypto can't rely on "one-chance-only" potental life savings storage? You lose your wallet and seed words -> you're homeless, no one can recover your funds. Split funds into muliple wallets? -> Even harder to remember all the phrases. And a person won't always have time nor interest for research into smart techniques for wallet management. Will therefore resort to "trusted authorities" to manage their wallets anyway. What's the point then? -> "Not your keys, not your money" problem.
  * A bank will confirm my identity when I show up and prove it, and can recover my account. But no banks on the blockchain.
  * Try to generate wallets reliably tied to own biometric data? Fingers, retinas, face, voice, DNA???, etc. Then I can always recover my wallet just by "existing". No need to remember anything. Will still need a password for encryption.

*Problems:*
  * Is this a completely stupid idea?
  * If not, can this even preserve security of trusted algorithms?
  * If yes, then how to implement this robustly???
  * Is this feasable? No sensor will provide exactly the same deterministic data each time. But the generated seed must be identical.
  * Identity theft? Many companies (and banks) may already have samples of our biometric data. -> Futile?
  * What if I lose my finger(s), my voice changes, etc.?
  * A single fingerprint is used as entropy for the seed in this "demo". -> Defnitely NOT robust and ideal.

*How to implement?*
  * Better ways to interpret even the currently used fingerprint data?
  * Don't even use a wordlist? -> Use bio data (in binary form?) directly instead of words as seed?
  * Use the biometric data in some completely different way than as direct seeds? But don't give me phrases to remember!

Not pure-python dependencies
----------------------------

If you want to use the Qt interface, install the Qt dependencies::

    sudo apt-get install python3-pyqt5

For elliptic curve operations, `libsecp256k1`_ is a required dependency::

    sudo apt-get install libsecp256k1-0

Alternatively, when running from a cloned repository, a script is provided to build
libsecp256k1 yourself::

    sudo apt-get install automake libtool
    ./contrib/make_libsecp256k1.sh

Due to the need for fast symmetric ciphers, `cryptography`_ is required.
Install from your package manager (or from pip)::

    sudo apt-get install python3-cryptography


If you would like hardware wallet support, see `this`_.

.. _libsecp256k1: https://github.com/bitcoin-core/secp256k1
.. _pycryptodomex: https://github.com/Legrandin/pycryptodome
.. _cryptography: https://github.com/pyca/cryptography
.. _this: https://github.com/spesmilo/electrum-docs/blob/master/hardware-linux.rst

Running from tar.gz
-------------------

If you downloaded the official package (tar.gz), you can run
Electrum from its root directory without installing it on your
system; all the pure python dependencies are included in the 'packages'
directory. To run Electrum from its root directory, just do::

    ./run_electrum

You can also install Electrum on your system, by running this command::

    sudo apt-get install python3-setuptools python3-pip
    python3 -m pip install --user .

This will download and install the Python dependencies used by
Electrum instead of using the 'packages' directory.
It will also place an executable named :code:`electrum` in :code:`~/.local/bin`,
so make sure that is on your :code:`PATH` variable.


Development version (git clone)
-------------------------------

Check out the code from GitHub::

    git clone git://github.com/spesmilo/electrum.git
    cd electrum
    git submodule update --init

Run install (this should install dependencies)::

    python3 -m pip install --user -e .


Create translations (optional)::

    sudo apt-get install python-requests gettext
    ./contrib/pull_locale

Finally, to start Electrum::

    ./run_electrum



Creating Binaries
=================

Linux (tarball)
---------------

See :code:`contrib/build-linux/sdist/README.md`.


Linux (AppImage)
----------------

See :code:`contrib/build-linux/appimage/README.md`.


Mac OS X / macOS
----------------

See :code:`contrib/osx/README.md`.


Windows
-------

See :code:`contrib/build-wine/README.md`.


Android
-------

See :code:`contrib/android/Readme.md`.


Contributing
============

Any help testing the software, reporting or fixing bugs, reviewing pull requests
and recent changes, writing tests, or helping with outstanding issues is very welcome.
Implementing new features, or improving/refactoring the codebase, is of course
also welcome, but to avoid wasted effort, especially for larger changes,
we encourage discussing these on the issue tracker or IRC first.

Besides `GitHub`_, most communication about Electrum development happens on IRC, in the
:code:`#electrum` channel on Libera Chat. The easiest way to participate on IRC is
with the web client, `web.libera.chat`_.


.. _web.libera.chat: https://web.libera.chat/#electrum
.. _GitHub: https://github.com/spesmilo/electrum
