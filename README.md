# batchOverflow
[![Build Status](https://travis-ci.org/phzietsman/batchOverflow.svg?branch=master)](https://travis-ci.org/phzietsman/batchOverflow)

A fix for the [batchOverflow bug](https://medium.com/@peckshield/alert-new-batchoverflow-bug-in-multiple-erc20-smart-contracts-cve-2018-10299-511067db6536) found by the [PeckShield](https://peckshield.com/) team.


## a fix
The original contract only did a check to ensure the sender has enough *whatever* to pay the total amount (input value x number of addresses). If an overflow ocurred this amount can be zero, which would allow the test on `line 12` to pass. 

![execute](./README/buggy.png?raw=true)

One possible fix is to add another test to check if the sender's balance minus the amount is less than his current balance. If a overflow ocurred the balances would be same, making it an invalid transaction. This however will still not fix the problem. If the attacker has a small balance, say 10 whatever, the attacker could craft _value to overflow to some amount smaller than the current balance they currently hold and thereby passing this gate.

Better fix would be to simply check if the total amount that transferred is greater or equal that _value. If an overflow occurred, this test would not pass. For an attacker to get past this gate they would need a minimum of a that magical number / 20, which is still a very large amount and probably impossible to get without exploiting another bug.

## test it
Ensure that you have truffle installed and run the `truffle test` command from the root of your project. It should look something like this.

![execute](./README/test.png?raw=true)


