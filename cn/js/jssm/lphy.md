---
description: 流动性池
---

# LendingPool 合约

## 1. Deposit

FIL持有者将FIL存入池子中赚取收益，用户存入FIL将返回相同数量的rSFT，随着借款用户偿还利息，用户rSFT的余额将自动增加。核心公式为：

{% hint style="success" %}
amount = shares \* (totalPooledFIL / totalShares)
{% endhint %}

其中，totalPooledFIL表示池子所控制的FIL的总量（包括用户存入的FIL + 借款者偿还的利息）, shares可以理解为用户占totalPooledFIL的一个股份。

> 举个例子：
>
> 在池子刚启动时（此时池子FIL余额为0，存入的FIL数量等于shares数量），用户A存入100FIL，sharesOf(A) = 100；
>
> 随后用户B存入200FIL，此时 amount = 200， totalPooledFIL = 100， totalShares = 100, 则sharesOf(B) = 200；
>
> 假设随后有用户借款并产生了600FIL的利息，则此时totalPooledFIL = 900，totalShares = 300，用户A的rSFT余额为amountOf(A) = 100 \* 900 / 300 = 300；
>
> 用户B的rSFT余额为amountOf(B) = 200 \* 900 / 300 = 600；
>
> 若此时用C存入300FIL，sharesOf(C) = amountOf(C) \* (totalShares / totalPooledFIL) = 300 \* (300 / 900) = 100。 &#x20;

## 2. Withdraw

用户可以将rSFT 1:1换回FIL。

## 3. StakingOrder

用户抵押SFT的定期存款订单以获得借款能力。例如，用户抵押了一张10000个FIL的6个月定期存款订单，LTV(贷款比例)被设置60%，则用户最大可以借出6000个FIL。

## 4. unStakingOrder

用户在还清借款后，可以解抵押订单。

## 5. Borrow

用户可以使用抵押的订单来借出一定数量的FIL,最大的比例是60%。

## 6. Repay

用户根据订单来偿还其借出的FIL，用户不需要额外偿还借款利息，其借款利息由订单产生的收益每天自动偿还。每天偿还的利息计算公式为：

{% hint style="success" %}
interest = applyBorrowAmount \* rewardPerSFT \* multipiler
{% endhint %}

其中，applyBorrowAmount代表用户当天借款的最大数量，例如，用户在借了1000FIL后随后马上偿还了500FIL，applyBorrowAmount仍为1000；

rewardPerSFT代币当日单个SFT的收益；

multipiler是一个随着池子的资金利用率变化而变化的乘数，记U代表资金利用率；

U\<sub>low\</sub>代表低资金利用率阈值（当前为20%）， U\<sub>opt\</sub>代表最佳资金利用率（当前为80%），minMultipiler代表最小乘数（当前为0.5）；

slope1代表斜率1（当前为0.5），slope2代表斜率2（当前为0.66）。则有：

* 当U <= U\<sub>low\</sub> 时，multipiler = minMultipiler；
* 当 U\<sub>low\</sub> < U <=U\<sub>opt\</sub>时，multipiler = minMultipiler + slope1 \* (U -  U\<sub>low\</sub>) / (U\<sub>opt\</sub> -  U\<sub>low\</sub>)；
* 当 U\<sub>opt\</sub> < U <= 1时, multipiler = minMultipiler + slope1 + slope2 \* (U -  U\<sub>opt\</sub>) / (1 -  U\<sub>opt\</sub>)。

## 7. BorrowLiquidity

​该方法只有合约能调用，当普通用户进行赎回操作时，如果赎回池中FIL余额不足，并且当前借贷池的资金使用率低于最佳资金利用率时，合约将使用SFT作为抵押 1:1从借贷池中借走FIL。

## 8. DistributeReward

根据池子中SFT的数量发放收益。
