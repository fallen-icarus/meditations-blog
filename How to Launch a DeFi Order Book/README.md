# **How to Launch a DeFi Order Book**

> [!TIP]
> Here is an AI-generated podcast giving a deep dive on this paper (audio-only).  
> Reload the page if there is a MIME error.

https://github.com/user-attachments/assets/09ad2123-fdda-4907-8ca3-2fd0bb51b491

## Table of Contents

- [Abstract](#abstract)
- [Motivation - The World Needs a DeFi Order Book](#motivation---the-world-needs-a-defi-order-book)
- [Initial Liquidity](#initial-liquidity)
- [Order Book UTxO Contention and Sharing Liquidity](#order-book-utxo-contention-and-sharing-liquidity)
- [The Future of DEXs](#the-future-of-dexs)
- [Conclusion](#conclusion)

## Abstract

Launching a Cardano DeFi order book has proven to be a difficult problem for two reasons: 1\) it is
difficult to incentivize initial liquidity and 2\) it suffers from UTxO contention. Automated Market
Maker (AMM) DEXs have remained dominant precisely because no contemporary DeFi order book has found
adequate solutions to these problems. Since DeFi order books are significantly more capital
efficient and offer better risk management over AMMs, figuring out how to launch a DeFi order book
is an existential problem for DeFi in general – TradFi will never take DeFi seriously if all it has
to offer the world are AMMs. Motivated by this belief, this paper offers plausible solutions to both
of the aforementioned problems. Solving the early liquidity problem involves initially positioning
the order book to **complement** the current AMMs; it should not try competing against them. By
doing this, the order book will be able to **permissionlessly** tap into the liquidity already
present in the AMMs. The trick is to target a niche that is currently unsatisfied by contemporary
AMMs: swing traders and position traders. These traders will place limit orders on the open order
book; and when AMM prices overlap with these orders, arbitrage bots can trustlessly and
permissionlessly execute the limit orders *against* the AMMs – ensuring execution once the limit
prices are hit. The solution to UTxO contention involves letting the free market handle it: users
that want to interact with the order book directly can either deliberately choose a more expensive
limit order to face less UTxO contention or deliberately create a negative spread to incentivize
bots to compete for the UTxO on their behalf. A consequence of this free market approach is that the
order book will be able to share its liquidity with other dApps and liquidity providers can get paid
a real yield when it does. These two solutions together are how Cardano can successfully bootstrap a
user-friendly DeFi order book. Once launched, the DeFi order book will revolutionize Cardano’s DeFi.

## Motivation \- The World Needs a DeFi Order Book

The problem with Automated Market Maker (AMM) DEXs stem from how they determine price \- they base
it off the ratio of the assets in the liquidity pool. As an extremely basic example, a liquidity
pool with equal amounts of ADA and DJED would have a price of 1 ADA/DJED. If someone removed half
the ADA, the price would become 0.5 ADA/DJED. The issue with this is that it results in excessive
slippage.

Unlike limit orders, AMMs are constantly repricing, even in the middle of a trade execution. So if
the AMM initially had 1,000 ADA and 1,000 DJED priced at 1 ADA/DJED, and Alice wanted to trade 200
ADA for DJED, her trade would *not* be executed entirely at 1 ADA/DJED. Every AMM is different, but
they all effectively reprice every few units. So the first 5 ADA could be priced at 1 ADA/DJED. But
then the AMM will reprice and fill the next 5 ADA at the new price. Then reprice again for the next
5 ADA, and so on. The price “slips” during the trade. In order to not experience any slippage, the
AMM would effectively need an equally infinite amount of ADA and DJED. It is an interesting exercise
to calculate how much liquidity is needed in an AMM for it to execute a trade of $1,000 without
experiencing more than 1% of slippage. For many AMMs, they would likely need 50-100 times that
amount in liquidity (i.e., $50k-$100k of liquidity) just to process a $1,000 trade without much
slippage. **This is absurdly inefficient.** An order book only needs $1,000 worth of liquidity at
the specified price to be able to process a $1,000 trade without slippage. **An AMM can never have
zero slippage by design.**

Slippage is not just an annoyance; **it is an existential problem**. Imagine if a stablecoin issuer
has a treasury of $500k ready to defend the peg. If defending the peg requires trading using an AMM,
the AMM would need to have $25m-$50m worth of liquidity to be able to absorb this trade without much
slippage. **No Cardano AMM currently has this much liquidity**
([source](https://www.geckoterminal.com/cardano/pools?sort=-24h_trend_score)). That means *a
significant portion of the stablecoin treasury will be lost to slippage* instead of defending the
peg. Effectively defending stablecoin pegs **requires** the use of capital efficient order books.
The same also applies to corporations and institutions: if a central bank wants to convert $50m
worth of ADA to DJED without much slippage, this would require an absurd amount of liquidity in the
AMM. **Central banks will not even try this due to the risk of slippage**.

> [!IMPORTANT]
> It is not possible for DeFi to be mass adopted without a working DeFi order book because it will
> be too capital inefficient.

As you’ll see in this paper, a DeFi order book is not meant to compete against AMMs; it is meant to
compliment them. If AMMs relied on the DeFi order book for their prices (using oracles), the
slippage problem goes away. Likewise, the secret to actually launching a DeFi order book is to rely
on AMMs. *They stabilize each other.*

## Initial Liquidity

There is no quick way to attract liquidity to an order book. TradFi’s order books took decades to
liquify enough for more complicated features like options trading and short selling. However, order
books can become stable long before they have enough liquidity to support these more advanced types
of trades. The trick is to identify a niche that can’t be satisfied without the order book: swing
traders and position traders.

The main feature satisfied by AMMs are market orders \- orders meant for immediate execution. This
type of order requires instant liquidity. But limit orders serve a different niche. Imagine if the
current price for ADA is $0.70, and Alice thinks it will retrace to $0.50 within the next month. In
TradFi, she would just create a limit order to buy ADA at $0.50. She doesn't care if it takes a week
or a full month; she will just leave it there. Limit orders are great because it means Alice doesn’t
need to be online at the moment the price hits $0.50. Market orders will never be able to serve this
niche because they fundamentally require Alice to be online at the moment of execution, but she has
no idea when the price will actually hit $0.50. She would have to be available 24/7.

Some AMMs recognize the value of limit orders for this niche and have built their own
implementations. However, this results in siloed limit orders. Limit orders set for Minswap will not
execute against SundaeSwap even if SundaeSwap’s liquidity pool hit the target price. As a result,
limit order liquidity is just as fractured as the AMMs themselves.

A universal order book can fix this: instead of users creating limit orders for a specific AMM,
they will create the limit orders on an open order book. Then, when the price of an AMM overlaps
with the limit order’s price, an arbitrage bot can trustlessly execute the limit order against the
target AMM. The arbitrage bot would get to keep the arbitrage amount from this trade which naturally
incentivizes them to perform this service. The arbitrage bot can be thought of as a DexHunter
service that is constantly running in the background, comparing limit orders to the current AMMs’
prices. 

> [!IMPORTANT]
> MEV will always be a risk for arbitrage bots. However, as long as Cardano succeeds at having
> decentralized block production, this risk is mitigated (not all SPOs will care to do this).

The DeFi order book effectively starts out as an “order book for AMMs” \- standardizing the limit
order implementations and sharing the limit orders across all AMMs. AMMs also benefit from this
service since it makes it easier to sync the prices offered across the different AMMs. All that is
required for this synergy is a wallet with a user-friendly UI/UX for creating and managing limit
orders, and at least one arbitrage bot constantly running behind the scenes.

> [!IMPORTANT]
> The openness of the DeFi order book and the permissionlessness of becoming an AMM batcher means
> anyone could start and run an arbitrage bot.

Past DeFi order books for Cardano have all had some kind of problem that prevented them from serving
this “order book for AMMs” role:

- ***No support for partial order fulfillment.*** Without partial fulfillment, the order book will
suffer from the [double coincidence of wants
problem](https://en.wikipedia.org/wiki/Coincidence_of_wants), effectively making it useless.  
- ***Forced users to sacrifice custody and delegation control.*** Large entities like the Cardano
Foundation are reluctant to use their ADA in DeFi because it effectively forces them to pick winners
and losers for dApps, stake pools, and dReps. To attract their liquidity, the order book **must**
allow users to keep custody and delegation control.  
- ***They have not marketed themselves as complementary to the current AMM DEXs.*** They have all
tried to compete against them and made it difficult to tap into the liquidity already present in the
AMMs.

The DeFi Kernel’s [order book](https://github.com/fallen-icarus/cardano-swaps) solves the first two
problems (using [CIP-89](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0089) to solve
the second problem) and its marketing strategy will solve the third problem.

## Order Book UTxO Contention and Sharing Liquidity

> [!NOTE]
> This section goes over the concepts discussed in the following youtube video from 17:55-32:59. If
> you’ve already seen the video, feel free to skip this section.  
> [Presenting P2P-DeFi to the Cardano Foundation](https://youtu.be/Pk6eNMLNDps?si=VsdiwaTSzTJRfmGa&t=1075)

Solving UTxO contention is critically important for creating a useful DeFi order book. UTxO
contention is when two entities race to spend a one-time use UTxO. If both entities submit their
transactions at the same time, only one transaction will actually get processed by the blockchain.
Since order book limit orders are each separate UTxOs, DeFi order book critics believe end-users
will be forced to race each other to use limit orders. They argue order books will have a terrible
user experience since end-users will need to keep resubmitting transactions, hoping one will go
through. This fear is why even DeFi order books tend to enforce some kind of batching system.

But if end-users are allowed to interact with limit orders directly, **this is not what will
actually happen**. By deliberately choosing a more expensive limit order, end-users can minimize the
chance of someone else competing for the same limit order. The insight comes from the realization
that, if you choose to use the worst price limit order, you would likely be the only person in the
world trying to use that UTxO \- there would be no UTxO contention. Consider the following table:

| Amount Paid Above Market Price | Users/Bots Competing | Tx Success Rate |
| :---: | :---: | :---: |
| 1% | 70% | 20% |
| 2% | 20% | 65% |
| 3% | \<1% | 99% |

**Table 1:** Paying a premium to avoid UTxO contention

The table gives some estimates of what a user could expect: choosing a limit order 3% more expensive
than the current market price could be enough for the user to get the UTxO all to themselves.

> [!IMPORTANT]
> **The wealthy cannot price out poorer users by paying up.** The order book segments liquidity into
> different price levels. Imagine if 100 ADA is priced at $0.70/ADA and another 100 ADA is priced at
> $0.75/ADA. If a wealthy entity chose to use the 100 ADA at $0.75/ADA, the other 100 ADA is still
> available for other users.

Paying up is for when the end-user wants an asset conversion immediately; but if the user is willing
to wait, they could get a better price by hiring a bot. The insight for this comes from recognizing
that arbitrage bots are constantly scanning the open limit orders, looking for arbitrage
opportunities. If the end-user creates a new limit order that deliberately causes a negative spread
for the order book, the negative spread will attract these arbitrage bots because a negative spread
is an arbitrage opportunity. For this approach, the end-user can control how much they are willing
to pay for the asset swap by controlling how negative to make the spread. Consider the following
table:

| Negative Spread (%) | Fulfillment Time |
| :---: | :---: |
| 0.1% | 3-4 hours |
| 0.2% | 30-60 minutes |
| 0.5% | 1-5 minutes |

**Table 2:** Hiring an arbitrage bot. The table assumes a trade to convert 100 ADA.

Once again, the table only gives estimates. If the user wants to convert 100 ADA, a 0.1% overlap
gives the arbitrage bot a profit of 0.1 ADA. This amount is less than the expected transaction fee
for the arbitrage bot so it will need to batch this user’s order with other arbitrage trades.
Finding these other trades is why it could take 3-4 hours. However, if the user gave a 0.5% overlap,
that’s a profit of 0.5 ADA for the arbitrage bot; this more than covers the transaction fee which
means the arbitrage bot can submit this user’s order immediately. Hiring a bot is nice for two
reasons: 1\) the user’s order is guaranteed to be filled eventually as long as the negative spread
persists, and 2\) it enables using arbitrage bots as batchers despite the order book not having an
official batching system. The end-user effectively transfers the burden of UTxO contention to the
bots (who largely don’t care about it) and pays them for providing this service.

> [!IMPORTANT]
> It is not possible to eliminate UTxO contention entirely without causing other, more serious
> consequences. Limit orders are fundamentally scarce resources which means there will always be
> contention (even in TradFi). Pretending like they are not scarce resources will only result in
> inefficient markets.

The order book’s first solution to UTxO contention (paying up for a limit order), is a DeFi game
changer. Imagine if you see an NFT on sale for ADA but you only have DJED. You are expecting a
market correction in ADA so you have converted most of your money to DJED. Without the option to pay
up on the asset conversion, you would need to use two separate transactions to buy this NFT:

1. Convert the DJED to ADA in the first transaction.  
2. Try to buy the NFT with the new ADA in the second transaction.

What if the NFT is purchased by someone else after the first transaction, but before the second one?
You would need to rush to convert your ADA back to DJED before the market correction happens\! If
you’re lucky, you only had to cover the fees for two transactions. But if you got caught in the
market correction, you could have easily lost 20% of your original DJED. This is an extremely risky
gamble just to try buying this NFT.

But what if you could merge the asset conversion transaction and the purchase transaction into just
a single transaction? If you did, a failed purchase will also cause the asset conversion to fail.
This means: **your DJED will only ever be converted to ADA if it is immediately used to purchase the
NFT**. The risk of the market correction is entirely eliminated in this scenario\!

This n-in-1 transaction (i.e., multiple actions performed in one transaction) has tremendous
benefits for DeFi:

- ***It makes all native assets fungible for a slight fee (i.e., Babel Fees)*** – At a transaction level, you were able
to use DJED to buy an NFT on sale for ADA.
- ***It eliminates a lot of DeFi risk*** – You completely eliminated the risk of market volatility.  
- ***It enables dApps to share liquidity*** – Even though the NFT marketplace didn’t have any
liquidity pools, you were still able to use DJED to buy the NFT.

Given how many Cardano native assets there are, the n-in-1 transaction will make corporations much
more comfortable to hold different native assets and use them in DeFi. They have entire departments
dedicated to risk-management so they will naturally appreciate the n-in-1 transaction, and they will
likely be more than willing to pay up 3% on an asset conversion to avoid a potential loss from
market volatility.

> [!IMPORTANT]
> Behavioral economics has shown that people would rather pay up a little now to avoid the risk of a
> large loss later. The entire insurance industry is based on this idea \- people pay a small
> monthly premium to avoid a large loss if disaster strikes.

As for sharing liquidity, dApps would no longer need to bootstrap their own liquidity. An options
trading dApp or a credit market dApp can just tap into the order books liquidity immediately. This
makes it significantly easier to launch new DeFi dApps.

While some liquidity will already be present on the order book due to the demand from swing traders
and position traders, being able to share liquidity adds new incentives to provide more liquidity.
Because the n-in-1 transaction is so useful, it will generate its own type of demand for the order
book. And since what makes the n-in-1 transaction work is paying up for limit orders, it provides
natural incentives for people to create limit orders specifically for these transactions. **This
means there is a natural incentive to fill the gaps typically found in DeFi order books which
naturally increases overall market depth.**

## The Future of DEXs

DeFi order books aren’t perfect. One of the biggest draws to AMMs is the fact that users can “set it
and forget it”. Remember that the main problem with AMMs (i.e., excessive slippage) stems from how
they determine the price of their liquidity. What if the AMMs used the order book to determine their
prices just like how TradFi market makers determine their prices based off of the TradFi order book?
The AMMs could use oracles that constantly tell them what the current bid/ask spread is for the
order book; the oracles could even tell them the order book’s current market depth. By outsourcing
price determination to the order book, most of the AMM’s slippage should go away. For example, users
could deposit their liquidity into an AMM that always provides liquidity within a 5% range around
the order book’s current mid price. AMMs don’t go away; they just evolve.

The DeFi order book will eventually also have another method of providing market orders:
[Nested Transactions](https://github.com/cardano-foundation/CIPs/pull/862). The flow for
a nested transaction market order is outlined below:

1. An off-chain market maker looks at the current on-chain order book to determine its desired
   market order prices for a given trading pair.  
2. The off-chain market maker tells a wallet these prices. **These prices are not posted on-chain.**
   Instead, they are communicated using a traditional server-client architecture.  
3. A user of the wallet agrees to the market order price, and creates and signs an unbalanced
   transaction. This unbalanced transaction effectively hard-codes the required swap; no smart
contracts are needed for trustless enforcement.  
4. The wallet sends the signed, unbalanced transaction to the off-chain market maker.  
5. The market maker batchers this user’s unbalanced transaction with unbalanced transactions from
   other users. In the top-level transaction, the market maker will supply their own liquidity
UTxOs.  
6. The nested transaction will be submitted to the chain, fulfilling all of the market orders in one
   transaction.

While AMMs will be more convenient for *passive* market making, the *active* nested transactions
approach to market orders has some advantages:

- Market order prices can be updated as fast as the server-client connection allows. Their prices
will be based on the on-chain order book’s prices; but by keeping prices off-chain, their prices can
be updated even faster than AMMs using oracles tied to the on-chain order book.  
- The same liquidity pool is able to satisfy market orders for many different trading pairs. In
other words, instead of having separate liquidity pools for ADA/SNEK and ADA/HOSKY, a single ADA
liquidity pool is able to serve as liquidity for both pairs.  
- Significantly lower fees: no batcher fees, pool fees, DAO fees, or oracle fees. There is only the
market maker’s spread (and possibly a wallet fee).

So while some liquidity providers will still prefer the “set it and forget it” ability of (order
book priced) AMMs, professional market making businesses will become possible thanks to the Nested
Transactions CIP.

## Conclusion

Successfully launching a DeFi order book involves initially positioning itself as the “order book
for AMMs” by targeting swing traders and position traders, and enabling the n-in-1 transaction. These
two niches will provide the necessary demand for liquidity to start forming on the DeFi order book.
By trying to complement AMMs instead of competing with them, the order book can be useful
immediately after launch, despite having very little of its own liquidity. Over time, the DEX
landscape will evolve: AMMs will adapt to use the on-chain order book for their prices which
eliminates their slippage problem, and the Nested Transaction CIP will make professional market
making possible. All that’s required for this is a good UI/UX for managing limit orders and building
n-in-1 transactions, some arbitrage bots willing to connect the order book to the current AMMs, and
a bit of patience.
