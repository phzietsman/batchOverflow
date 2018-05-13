# batchOverflow

A fix for the [batchOverflow bug](https://medium.com/@peckshield/alert-new-batchoverflow-bug-in-multiple-erc20-smart-contracts-cve-2018-10299-511067db6536) found by the [PeckShield](https://peckshield.com/) team.

![execute](./README/buggy.png?raw=true)

## a fix
The original contract only did a check to ensure the sender has enough *whatever* to pay the total amount (input value x number of addresses). If an overflow ocurred this amount can be zero, which would allow  


![execute](./README/test.png?raw=true)


