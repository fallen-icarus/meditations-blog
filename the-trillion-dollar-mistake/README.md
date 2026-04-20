# The Account Model: A Trillion Dollar Mistake

*The account model won mindshare because it's easier to build on. But ease of building is not the
same as capacity for what can be built — and the gap between them is measured in trillions.*

**Key Takeaways**

- **The Account Model Has a Low Utility Ceiling:** Storage access costs grow with adoption — every
new loan, order, and position deepens the trie that every subsequent user must traverse. Flat gas
pricing currently hides this behind a validator subsidy, but the subsidy is unsustainable. When it
ends, success becomes a drag. Dead state makes it worse: ~80% of Ethereum's state hasn't been
touched in over a year, cleanup is economically irrational, and every active user pays to traverse
this state graveyard.
- **eUTxO Has No Ceiling:** Each UTxO is independent state with effectively constant access cost
regardless of how many exist. Consuming state *is* deleting it, and the deposit mechanism means
cleaning up pays you. The common objection that eUTxO "has a contention problem" is a strawman —
contention is a property of scarce resources, not of ledger models, and eUTxO resolves it better: on
Ethereum, losers pay full gas while on eUTxO, losers pay nothing.
- **The Comfort Is the Trap:** The account model's DevEx advantage comes from putting everything in
shared, mutable, on-chain state — which is the same thing that causes the low utility ceiling.
- **The Flaw Cannot Be Hotfixed:** The account model's problems are not implementation gaps — they
are consequences of the data model itself. Better gas schedules, state expiry, L2s, and parallel
runtimes optimize within the utility ceiling but they cannot raise it.
- **The DeFi Kernel Lives Above the Ceiling:** The DeFi Kernel requires exactly the properties the
account model cannot provide: state costs that don't punish adoption, contention resolution that
doesn't waste gas or sacrifice censorship-resistance, and discoverability without shared-state
registries. The account model cannot host it, and the value it forfeits — the entire economy that
would grow from that seed — is measured in trillions.

---

## 1. The Comfortable Mistake

Ethereum won mindshare, and the reason is no mystery. The account model is comfortable. Mutable
state, sequential nonces, a global namespace where every contract has an address and every address
has a balance — it maps directly to the mental model most programmers already have. The learning
curve is short. The tooling is mature, and the developer experience is genuinely good.

*This post does not dispute any of that. The account model really is easier to build on.*

But ease of building is not the same as capacity for what can be built. A spreadsheet is easier to
use than a relational database. That does not mean you should run an exchange on a spreadsheet. The
account model has a **utility ceiling** — a hard upper bound on what it can do — and it reveals
itself when you try to build serious financial infrastructure on it. This ceiling shows up when a
credit market tries to serve thousands of concurrent borrowers, when an order book tries to handle
thousands of independent traders, and when the interaction between them needs to work at the scale a
real economy demands.

The DeFi Kernel — the minimum viable seed of a *productive* financial economy ([*The Seed of
DeFi*][seed-of-defi]) — lives above that ceiling. The account model cannot host it. And the value it forfeits
by not being able to host it is not small.

[seed-of-defi]: https://github.com/fallen-icarus/meditations-blog/blob/main/the-seed-of-defi/README.md

---

## 2. The Utility Ceiling

### The Growth Tax

Ethereum stores contract state in a trie data structure. Each storage access requires traversing
from root to leaf — roughly O(log(n)) database lookups where n is the number of entries. More
entries means deeper traversals and more disk I/O. **This is a growth tax and it is the root cause
of the account model's utility ceiling.**

> [!IMPORTANT]
> The trie is Ethereum's specific implementation, but the problem is general: **any shared data
> structure that indexes contract state grows with the number of entries, and every lookup pays for
> that growth.** Replace the trie with a B-tree, a skip list, or a Verkle tree — the O(log n)
> constant changes, but the scaling property doesn't. The cost is inherent to shared mutable state,
> not to Ethereum's choice of tree.

Most people are not aware of this growth tax because gas pricing is currently flat: a storage read
costs the same whether the contract has 1,000 or 1,000,000 entries. The real I/O cost grows, but the
price charged to users does not. Validators are currently forced to subsidize the difference by
using extra compute they aren't compensated for.

This subsidy is unsustainable because it creates a death spiral: as state grows, validators need
increasingly powerful hardware to keep up, which raises the barrier to entry, which centralizes the
validator set. A decentralized blockchain that centralizes its validators to subsidize cheap storage
access has defeated its own reason for existing. So the subsidy either ends (i.e., access costs are
repriced honestly) or the chain quietly centralizes. Either way, DeFi protocols built on flat-priced
storage lose.

Once the subsidy is corrected, the Nth user of a protocol makes it more expensive for users N+1
through infinity. The more successful a lending protocol or order book becomes, the more expensive
each interaction gets. *Growth creates drag.* The architecture punishes exactly the thing you need:
adoption. The more the economy tries to grow, the harder the soil pushes back.

> [!IMPORTANT]
> It is actually worse than this because a single user could have multiple intents: a trader with 50
> open orders has 50 entries in the trie. So the growth tax actually scales with the number of
> intents which grows faster than the number of users in the system.

### The Dead State Trap

The growth tax on its own is bad enough, but the account model also has a dead state problem which
increases the tax — and further lowers the utility ceiling.

On the account model, every storage entry persists unless explicitly deleted. Completed loans,
filled orders, and expired positions all remain in the trie forever by default. Deletion is
economically irrational: the person who deletes an entry has to pay gas upfront while the benefit (a
smaller trie) accrues to the network. *Classic tragedy of the commons.*

Ethereum tried generous cleanup refunds, but the mechanism was gamed into "gas tokens."
[EIP-3529][eip-3529] capped refunds to kill the exploit, but it also killed any meaningful incentive
to clean up. Dead state continues to accumulate, the trie keeps growing, and the real cost of every
state access keeps rising — all hidden behind flat gas pricing.

This is not a hypothetical future concern: [roughly 80%][dead-state] of Ethereum's total state has
not been accessed in over a year. The trie is dominated by dead weight that every living access must
traverse. Ethereum's own community acknowledges as much: [EIP-8032][eip-8032] proposes making gas
scale with a contract's storage count. *Its existence is an admission that flat pricing is a
subsidy, not a reflection of real cost.* 

The question is not *whether* the subsidy ends, but *when* — and what happens to every DeFi protocol
built on the assumption that storage is flat-priced.

### The Off-Chain Escape Hatch

An account developer could argue that state should just move off-chain. If too much state is the
problem, just store the state off-chain and only use the L1 for settlement.

At first glance, this might make sense. But the reality is that this kills *read*
censorship-resistance. If limit orders live off-chain, Alice can't trustlessly view the order book,
and price discovery itself becomes censorable. **A censorable order book with decentralized
settlement is still a censorable order book.**

If blockchain is meant to one day resist corrupt governments, the core financial primitives must
exist directly on-chain where there is the most censorship-resistance.

[eip-8032]: https://eips.ethereum.org/EIPS/eip-8032
[eip-3529]: https://eips.ethereum.org/EIPS/eip-3529
[dead-state]: https://blog.ethereum.org/en/2025/12/16/future-of-state

---

## 3. eUTxO Has No Utility Ceiling

**The growth tax — and the low utility ceiling it causes — are not inherent to blockchains.** It is
a consequence of *where* computation happens.

The account model runs everything on-chain: even just checking if an order still exists requires a
runtime trie traversal. This runtime lookup step is the root cause of its growth tax.

eUTxO separates concerns: most computation happens off-chain during transaction construction. The
validator's only job is to validate the result. The bulk of the cost moves to where it is cheap,
unmetered, and borne only by the transaction builder.

### No Growth Tax

*All UTxOs are stored in a flat map.*

When you specify a UTxO as input to a transaction, you are telling the validator exactly where your
data is located. This means there is no need for a runtime lookup step; an O(log N) operation
effectively becomes constant-cost. This means flat access costs for UTxOs actually make sense
because the real world costs are also flat. **No subsidy needed.**

### No Dead State

On the account model, state persists until someone pays to delete it — and no one ever does. On
eUTxO, state cleans itself up.

Spending a UTxO removes it from the active set. This is not a separate cleanup operation that
someone must be incentivized to perform. It is the transaction itself. The spend *is* the deletion.
When a loan is repaid, the UTxO representing that loan is consumed as an input to the repayment
transaction which removes it from the on-chain state. *The active set naturally shrinks as state is
used.*

The incentives reinforce this. Every UTxO on Cardano holds a minimum ADA deposit proportional to its
storage size. Creating state costs a deposit. Consuming state releases the deposit back to the
consumer. The person who cleans up *profits* — they recover the locked ADA.

The active UTxO set trends toward containing only the state that matters. Everything else has
already been consumed and removed.

---

## 4. The Contention Strawman

The most common objection to eUTxO is contention: only one transaction can spend a given UTxO per
block, so popular UTxOs become bottlenecks. This is real but the implied conclusion — that Ethereum
doesn't have this problem — is wrong. Contention is a property of scarce resources, not of ledger
models. **All financial markets have contention.** The difference is where it's resolved and who
pays.

### On Ethereum, Losers Pay

Competing transactions all enter the mempool, all get included in a block, and all pay gas —
regardless of their outcomes. **Losers discover they lost only after execution, and they still pay
full gas for the failed attempt.** During the Otherside NFT mint, users [lost over $4
million][otherside] in gas on thousands of failed transactions. The contention was real — Ethereum
just made each of them pay to discover they'd lost.

> [!IMPORTANT]
> Paying for failed attempts is required with the account model because it checks for the existence
> of state at runtime instead of during transaction construction.

Worse, the block producer's power to *order* competing transactions allows them to monetize this
contention. Searchers and builders exploit this ordering power to extract value — frontrunning,
backrunning, sandwiching. This is not a bug in specific protocols; it is a structural consequence of
resolving contention at execution time.

### On eUTxO, Losers Pay Nothing

The eUTxO model breaks transaction validation into two phases:
1. **Phase 1:** Do all the required UTxOs still exist?
2. **Phase 2:** Do the smart contracts return true?

Phase 1 validation is extremely cheap which means it can be done at scale without having to charge
users for its computational burden. Phase 2 validation is the expensive check, but it only happens
if the transaction passes Phase 1 validation.

If two transactions attempt to spend the same UTxO, only one can actually pass Phase 1 validation
when the block producer gets them. The other is cheaply rejected without having to charge the loser
fees. The Otherside disaster is not possible on an eUTxO blockchain.

When contention is explicit (you can see whether a UTxO still exists), participants can route around
it naturally. Consider an order book like [cardano-swaps][cardano-swaps]: a trader can deliberately
choose a slightly worse-priced order rather than competing for the best one. The most contested
order goes to whoever gets there first; everyone else disperses across the book. The more you pay
up, the higher your chance of success. This is exactly how the real economy handles contention: with
price. With this method, there is no wasted on-chain computation which means there is no reason to
charge losers fees.

> [!NOTE]
> Even shared liquidity pools (e.g., AMMs using a constant-product formula) do not require batchers
> on eUTxO. Cardano's [CIP-159][cip-159] account address enhancement enables storing pool liquidity
> in an account address where deposits and withdrawals can be processed in parallel. The same
> principle applies: a trader sets a price tolerance that determines how much slippage they'll accept
> from concurrent swaps — a wider tolerance accepts a worse price but is more likely to succeed.
> The more you pay up, the higher your chance of success. Some AMMs may still choose batchers to
> enforce FIFO ordering, but it is a design choice, not a necessity.

[otherside]: https://nftplazas.com/backlash-as-otherside-nft-mint-gas-fees/
[cardano-swaps]: https://github.com/fallen-icarus/cardano-swaps
[cip-159]: https://github.com/cardano-foundation/CIPs/tree/master/CIP-0159

---

## 5. The Foundation Cannot Be Swapped

The data model — independent objects (eUTxO) vs. a shared growing data structure (account) — is the
load-bearing difference. You can bolt optimizations onto the account model: better gas schedules,
state expiry schemes, or parallel runtimes. But you cannot make state *independent* after the fact.

State expiry removes dead state, but it does not help with live state. A lending protocol with
10,000 concurrent active loans still stores all 10,000 in the same contract trie, and each access
still traverses a trie that grows with the number of active entries. The more successful the
protocol is *right now*, the more expensive it is to use *right now*. State expiry solves the dead
state problem, not the growth tax problem.

Better gas schedules make the cost honest, but they don't make it smaller. They just make end-users
actually feel the growth tax.

Parallel runtimes increase throughput, but they don't reduce per-operation cost. A trie with
1,000,000 entries still requires O(log n) cost per access, whether those happen sequentially or in
parallel is irrelevant.

> [!NOTE]
> Verkle Trees and statelessness — two pillars of Ethereum's current roadmap — also optimize within
> the ceiling. As noted above, swapping the data structure changes the constant but not the scaling
> property. Statelessness shifts *who* stores the state, not *how much* state there is. Neither
> changes the data model, and the data model is the problem.

Nor can you escape to L2s. The DeFi Kernel demands L1 censorship-resistance — the foundational DeFi
layer must run on the base layer (see [*The DeFi Hypothesis*][defi-hypothesis] for more details).
And an L2 built on the EVM still uses the account model — same trie, same growth tax. The same L2
built on an eUTxO chain would be dramatically cheaper.

### Just Shard the State!

The natural account model response to the state access problem is to deploy one contract per loan or
per order. But on the account model, separating state also separates *identity*. How does a lender
discover all open loan requests? How does a borrower prove their repayment history across dozens of
past loans? How does a trader find resting limit orders across thousands of isolated contracts?

In order to support peer-to-peer discovery, you need a registry — a contract that indexes all the
individual contracts. But a registry is shared state! The solution to the discovery problem
reintroduces the growth problem you just escaped! The only alternative is to rely on an off-chain
indexer which introduces centralization.

> [!NOTE]
> Solana illustrates this tradeoff directly. Its dApps shard state across individual accounts, but
> discovering those accounts requires RPC nodes powerful enough to index and scan the entire account
> set. The result is a reliance on centralized high-powered infrastructure operators.

On eUTxO, state and logic are separated by design. Each loan is its own UTxO, but all loans share
the same validator hash (same smart contract). [CIP-89][cip-89] beacon tokens exploit this — any
participant can discover every open offer, every active loan, and every historical repayment by
querying a single known identifier: the smart contract's hash. This discovery happens off-chain
without relying on a centralized indexer and where the cost is borne only by the user that needs it. 

Every attempt to fix the account model's data model problem exposes the next problem of the data
model. **Account model chains can optimize within their ceiling, but they cannot raise it.**

[defi-hypothesis]: https://github.com/fallen-icarus/meditations-blog/blob/main/the-defi-hypothesis/README.md
[cip-89]: https://github.com/cardano-foundation/CIPs/tree/master/CIP-0089

---

## 6. "But the DevEx..."

"Fine. eUTxO is great on paper, but nobody wants to build on eUTxO. The programming model is alien.
The tooling is immature, and you can't hire developers."

Fair enough. The complaint is real. But consider an analogy.

**The assembly language is a terrible developer experience!** Most people don't write it by choice.
Every mainstream language that followed was invented, at least in part, to escape from it. *Yet
every computer on Earth executes assembly.* Nobody replaced assembly with something "easier" at the
hardware level. They built better tools *on top* of it. Assembly persists because it maps faithfully
to what the processor actually does.

Assembly wasn't hard because the instruction set was hard. It was hard because the programmer has to
manage everything manually: register allocation, memory layout, calling conventions, etc. The
industry didn't fix this by replacing the hardware or the assembly language. It built compilers.

eUTxO is the assembly language of financial infrastructure. It maps faithfully to economic reality:
independent transactions are independent. The eUTxO model is less intuitive than the account model
for the same reason assembly is less intuitive than Python — it exposes the underlying reality
rather than abstracting it away. *But the underlying reality is the thing that matters when you're
building infrastructure that must actually work under load.*

The DevEx complaint is a **tooling problem**, not a **foundation problem**. You solve it the same
way the software industry solved assembly: by building better "compilers", better frameworks, better
abstractions *on top of* the correct foundation. You don't swap out the foundation for one with a
lower utility ceiling just because the current tools are immature...

---

## 7. The Trillion Dollar Mistake

*The account model cannot host the DeFi Kernel.*

Not because of a missing feature, but because the architecture punishes the Kernel's success. A
credit market serving thousands of concurrent intents triggers the growth tax maximally. An order
book handling thousands of independent traders wastes gas on every failed contention attempt. The
more the Kernel succeeds, the harder the account model pushes back.

The DeFi Kernel is not an incremental improvement. It is the seed of a real financial economy that
compounds in two directions:

- **Credit compounds upward.** Each non-margin loan is an individual bond. Because lending is
peer-to-peer, these bonds naturally span a range of risk profiles — different borrowers, different
collateral, different terms. That diversity is exactly what securitization needs: pools of loans
with varied risk can be packaged into loan-backed securities, and those securities can be tranched
to match different investor risk appetites. Tranched products attract institutional capital that
would never touch individual loans. That capital funds more loans, which creates more bonds, which
enables more securities. Each layer multiplies the value of the one below it. Kill the base layer
and none of the layers above it ever exist. (See [Layered Architecture of Credit][credit-layers] for
more details.)
- **Settlement compounds outward.** A trustless DTCC (the order book) enables L2 order books that
tap into a shared liquidity layer. More liquidity attracts more traders. More traders generate more
fee revenue. More revenue attracts more liquidity. 

The account model doesn't forfeit a single protocol. It forfeits every layer that would have grown
from the Kernel.

A non-margin credit market requires a negotiation phase: a single loan might pass through 5 or more
entries (a request + offers) before it becomes one active loan position. The growth tax hits hardest
during exactly this phase, when state is most plentiful and most transient. And unlike eUTxO, where
finished loans are consumed and their deposits recovered, the account model leaves every expired
entry in the trie permanently.

The order book fails differently. An efficient order book depends on arbitrageurs correcting
mispriced trading pairs — and arbitrage is inherently competitive. When contention resolution
charges losers full gas, the cost of a failed arbitrage attempt becomes a tax on price correction
itself. Arbitrageurs widen their margins to compensate, which means prices stay mispriced longer and
users get worse fills. **The account model doesn't just make the order book expensive — it makes it
less accurate.**

*Stock (a.k.a. TVL) follows flow.* The total value held in a layered credit market is a function of
how efficiently new loans can be originated, serviced, packaged, and settled. A growth tax on every
interaction doesn't just make individual transactions expensive — it caps the flow, which caps every
layer that depends on it. In TradFi, [private sector non-margin debt alone is ~$42
trillion][fed-debt] and the securities settlement infrastructure represents [another ~$100 trillion
in assets under custody][dtcc]. That $150 trillion of TVL exists *because* the underlying flow works
efficiently. The account model cannot sustain that flow. Whatever economy would have grown from the
DeFi Kernel — whatever fraction of that stock it would have generated — is forfeited entirely.

[credit-layers]: https://github.com/fallen-icarus/meditations-blog/blob/main/layered-architecture-of-credit/README.md
[fed-debt]: https://www.federalreserve.gov/releases/z1/dataviz/z1/nonfinancial_debt/chart/
[dtcc]: https://www.dtcc.com/news/2025/june/18/dtcc-central-securities-depository-subsidiary-surpasses-100-trillion-in-assets-under-custody

---

*What the account model forfeits is not a feature or an optimization. It is the seed of a real
economy.*
