---
description: Liquidity Pool
---

# LendingPool Contract

## 1. Deposit

FIL holders deposit FIL into the pool to earn profits. Users who deposit FIL will receive an equal amount of rSFT. As borrowing users repay interest, the balance of rSFT will automatically increase. The core formula is:

{% hint style="success" %}
amount = shares \* (totalPooledFIL / totalShares)
{% endhint %}

where totalPooledFIL represents the total amount of FIL controlled by the pool (including the FIL deposited by users and the interest repaid by borrowers), shares can be understood as the share of users in totalPooledFIL.&#x20;

> For example:
>
> Where totalPooledFIL represents the total amount of FIL controlled by the pool (including the FIL deposited by users and the interest repaid by borrowers), shares can be understood as the share of users in totalPooledFIL. For example:
>
> When the pool is just launched (at this time, the pool FIL balance is 0, and the number of FIL deposits is equal to the number of shares), user A deposits 100 FIL, and sharesOf(A) = 100;
>
> Then user B deposits 200 FIL. At this time, amount = 200, totalPooledFIL = 100, totalShares = 100, then sharesOf(B) = 200;
>
> Suppose a borrower borrows and generates 600 FIL in interest, then totalPooledFIL = 900, totalShares = 300, and the rSFT balance of user A is amountOf(A) = 100 \* 900 / 300 = 300,
>
> The rSFT balance of user B is amountOf(B) = 200 \* 900 / 300 = 600;
>
> If user C deposits 300 FIL, sharesOf(C) = amountOf(C) \* (totalShares / totalPooledFIL) = 300 \* (300 / 900) = 100.

## 2. Withdraw

Users can exchange rSFT for FIL at a 1:1 ratio.

## 3. StakingOrder

Users can mortgage SFT to obtain borrowing capacity. For example, if a user mortgages a 6-month fixed deposit order of 10,000 FIL, and the LTV (loan-to-value ratio) is set to 60%, then the user can borrow up to 6,000 FIL.

## 4. unStakingOrder

Users can un-mortgage orders after repaying the loan.

## 5. Borrow

Users can borrow a certain amount of FIL using the mortgaged order, and the maximum ratio is 60%.

## 6. Repay

Users can repay their borrowed FIL based on the order, and they do not need to repay the interest separately. Their loan interest is automatically repaid by the income generated by the order each day. The daily interest calculation formula is:

{% hint style="success" %}
interest = applyBorrowAmount \* rewardPerSFT \* multipiler
{% endhint %}

where applyBorrowAmount represents the maximum amount borrowed by the user on that day. For example, if the user borrowed 1,000 FIL and then immediately repaid 500 FIL, applyBorrowAmount is still 1,000;

rewardPerSFT is the daily income of a single SFT token;

multipiler is a multiplier that varies with the pool's capital utilization rate. Let U represent the capital utilization rate;

U\<sub>low\</sub> is the low capital utilization rate threshold (currently 20%), U\<sub>opt\</sub> is the optimal capital utilization rate (currently 80%), minMultipiler is the minimum multiplier (currently 0.5);

slope1 represents slope 1 (currently 0.5), slope2 represents slope 2 (currently 0.66), then:

* When U <= U\<sub>low\</sub>, multipiler = minMultipiler;
* When U\<sub>low\</sub> < U <=U\<sub>opt\</sub>, multipiler = minMultipiler + slope1 \* (U - U\<sub>low\</sub>) / (U\<sub>opt\</sub> - U\<sub>low\</sub>);
* When U\<sub>opt\</sub> < U <= 1, multipiler = minMultipiler + slope1 + slope2 \* (U - U\<sub>opt\</sub>) / (1 - U\<sub>opt\</sub>).

## 7. BorrowLiquidity

This method can only be called by the contract. When ordinary users redeem their holdings, if the FIL balance in the redemption pool is insufficient and the fund utilization rate of the current borrowing pool is lower than the optimal utilization rate, the contract will borrow FIL from the borrowing pool at a 1:1 ratio using SFT as collateral.

## 8. DistributeReward

Distribute profits based on the number of SFT tokens in the pool.
