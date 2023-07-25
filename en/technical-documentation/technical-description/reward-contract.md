# Reward Contract

## 1. DistributeReward

This method is the entry point for distributing profits to users who pledge SFT each day. The profit distribution unit is the order of pledged SFT. In version V2, the following additions have been made when distributing profits:

① Check whether the order has a mortgage loan in the borrowing pool. If so, calculate the loan interest according to the rules described in the repay method above and repay it;

②  Check whether the order's pledge time has expired and is still in the pledged state. If so, the order will be automatically renewed.

## 2. Unstake

Users can unpledge SFT orders after they expire. In version V2, there is a new restriction: orders in the pledged state cannot be unpledged.
