GiveHope Core staging tree 1.0.0.0 
===================================

What is GiveHope?
----------------

GiveHope is an experimental digital currency that enables anonymous, instant
payments to anyone, anywhere in the world. GiveHope uses peer-to-peer technology
to operate with no central authority: managing transactions and issuing money
are carried out collectively by the network. GiveHope Core is the name of the open
source software which enables the use of this currency.


GiveHope Mission
----------------

GiveHope aims to increase the charitable giving through blockchain technology.
We all have charities that are close to our hearts, and they all need our help.
To that end, GiveHope aims to directly support voted upon charities with masternode
earnings, that shall be funded via Proof of Stake (PoS) mining.


License
-------

GiveHope Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is meant to be stable. Development is normally done in separate branches.
[Tags](https://github.com/givehopecoin/GiveHopeCore/tags) are created to indicate new official,
stable release versions of GiveHope Core.


Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`


### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.


### Coin Specs

• PoW Algorithm: Quark  
• Premine: (#0 Block) 450,000 HOPC  (2.5%)
• PoW Blocks: 1 - 500  
• PoS Blocks: Starting from 501  
• Block Time: 90 Seconds  
• PoW Ending: ~ ca. 1/2 Days (Estimated: Nov. 2018)  
• Masternode Requirements: 3000 HOPC  
• Maturity: 101 Confirmations  


# PoW Reward Distribution

![alt text](https://github.com/givehopecoin/GiveHopeCore/blob/master/doc/coin_specs.png)
