# FMM_Sol

Attempts:

**Deligate_1 and Deligate_2**

Goal: Have Users Local Wallet Make Initial Call ==> Hit Proxy Contract ==> Hit FixedProductMarketMaker

Results:

On Deligate_1 I kept receiving "You don't have enough EC20 tokens" style responses.  My thought was that this was because, even though I wanted the final FPMM contract to use the local wallets funds, this wasn't the case because my marketMaker.addFunding call wasn't actually a deligate call, it was expecting to take funds from the Proxy contract.


On Deligate_2 I tried to solve that problem by replacing the direct addFunding call with a low level deligate style call.  With the hope that this would use Local wallet funds. 
Upon researching deligate calls I learned I needed to have all the local variables in place in order for the deligate call to work correctly, so I attempted to place all these variables in the contract before making the add funding call.  This produced mosty "Execution Reverted" failures and I was never able to make a successfull Buy / Add Funding call.

**NonDeligate_1**

Goal: Have Users Local Wallet Make Initial Call ==> Hit Proxy Contract ==> Hit FixedProductMarketMaker

Results:

On NonDeligate_1 I decided to give up on using a local wallet / proxy contract and to simply try and load up a Smart Contract with some funds and call the Buy / Add Funding calls normally. I am able to get the contract loaded with USDC + MATIC and approved for sending, getting passed the first few checks, but it always reverts when hitting transferFrom (line 308 here: https://github.com/gnosis/conditional-tokens-market-makers/blob/master/contracts/FixedProductMarketMaker.sol)
