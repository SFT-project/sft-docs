---
description: Minting Pool and Redemption Pool for Ordinary Users.
---

# Swap Contract

## 1. swapFil

Users use SFT to exchange FIL, that is, a redemption operation. When the FIL balance in the contract is insufficient, the contract borrows FIL from the borrowing pool to meet the user's redemption needs (see the above [**7. borrowLiquidity**](lendingpool-contract.md#7.-borrowliquidity) method for details).
