# Slow Blockchains are Better

*Why high-TPS chains are actually just L2s in denial — and why real wealth will always flee to the
"slow" lane.*

**Key Takeaways**

- **The Vanity of TPS:** The chase for 100,000+ TPS is a solution in search of a problem. The entire
crypto ecosystem's *actual* settlement demand today is less than **80 TPS**, revealing that most
high-speed activity is low-value noise, not economic signal.
- **Speed is Amnesia:** High-throughput blockchains generate data faster than they can sustainably
store it. By prioritizing speed, they force validators to aggressively prune history, effectively
destroying the "Hot History" (10-20 years) required for sovereign financial reputation.
- **The "Fast L1" is a Myth:** Any high-speed chain that relies on an external archive (like
Arweave) for long-term storage is not an L1; it is a high-performance **Sequencer**. The true L1 in
that stack is the archive, which must be slow to be secure.
- **The Jevons Trap:** Low fees do not create efficiency; they induce spam. "Cheap" block space
fills up with low-value bot noise, crowding out high-value economic settlement. Higher L1 fees act
as a necessary quality filter for global value.
- **Specialization Solves Fragmentation:** The current "bridging crisis" is a result of state
complexity in **General-Purpose L2s**. Interoperability is mathematically easier when bridging
between simple, specialized AppChains than between complex, Turing-complete environments.

---
Every few years, the crypto market falls for the same delusion: "Blockchain will get adopted if we
just make it faster."

We see charts showing Solana or Sui processing 100,000 transactions per second (TPS) while Bitcoin
and Ethereum crawl along at double digits. The conclusion seems obvious. The slow technology is the
dinosaur; the fast technology is the future.

This is false, and it is based on a fundamentally flawed understanding of the problem. The entire
premise is a solution in search of a problem, anchored to vanity metrics that have been detached
from reality. To put these numbers in perspective: **the total settlement demand for the entire
global TradFi system today is estimated to be ~8,000 TPS, which includes stock market trading** (see
[Appendix](#appendix-a-back-of-the-envelope-calculation-of-global-settlement-demand)). The demand
required to support every economically significant settlement transaction in the entire crypto
ecosystem is less than 1% of that — roughly 80 TPS. 

The 100,000 TPS figure isn't a sign of efficiency; it's a signal of induced demand, where nearly all
of the activity is low-value noise crowding out the signal.

Speed in an L1 blockchain is not a feature; it is a leak. It is a leak of **history, auditability,
and sovereignty**.

When an L1 blockchain runs at the speed of a centralized server, it bloats at the speed of a
centralized server. To keep the network alive, validators are forced to aggressively "prune"
(delete) old data. The result? An L1 blockchain that has the memory of a goldfish.

To access your own transaction history from three years ago on a high-TPS chain, you often can't ask
the blockchain itself. You have to ask a centralized archival node or a completely separate storage
network. This reveals the uncomfortable truth that high-speed "L1s" are desperate to hide: **They
aren't L1s at all**.

Here is why the world’s high-value economic activity will always flock to the slow lane — and why the
"fast" chains are destined to become amnesiac execution L2s.

### The Amnesiac Blockchain: Speed Kills Sovereignty

We often talk about "censorship resistance" as the ability to *send* a transaction. But real
sovereignty is the ability to *prove* a transaction happened years later.

Consider your credit history. In the traditional financial world, a credit score is built on 7–10
years of consistent behavior. This is **"Hot History"** — data that is technically "old" but
economically "active" because it proves your reputation, solvency, and ownership.

On a slow blockchain like Bitcoin or Ethereum, a user running a node on a standard laptop can store
and verify this history independently. The "Hot History" remains trustlessly accessible.

On a high-TPS chain, this is impossible. The sheer volume of data — often petabytes of state bloat
over a few years — forces the network to prune history rapidly.

- **The Trust Cliff:** If the L1 prunes data after 6 months to maintain performance, you fall off a
  cliff. To prove you paid a debt 2 years ago, you must query a centralized "Archive Service" or a
third-party protocol.
- **The Dystopia:** If you cannot verify your own history without asking permission from a massive
data center, you are at the mercy of that data center.

> [!IMPORTANT]
> Storing merkle roots on-chain is not enough because they are just hashes. If you need to get the
> original data from a centralized service, what happens if they refuse to give it to you? The
> merkle root proves nothing by itself. The same applies to ZK-proof based settlement. An on-chain
> hash is economically worthless without the data it corresponds to.

True financial sovereignty requires that the base layer (L1) serves as the **Judge of Truth** for a
relevant human timeframe (a generation), not a machine timeframe (a few milliseconds).

### The "L1" Lie: Physics of the Weakest Link

Proponents of fast chains will argue: "*We don't delete the history; we offload it to Arweave or
specialized archival nodes.*"

This defense is actually an admission of defeat because it misunderstands the definition of a Layer 1. 
**The L1 is the Root of Trust.** It is the final backstop where *economic truth* is determined.

If Solana relies on Arweave to store its long-term history, then **Solana is not the L1**. Arweave is
the L1. Solana is simply a high-speed Execution Layer (a decentralized Sequencer) settling to
Arweave’s Storage Layer.

Fast chains still have tremendous value, *but only as L2s*. We see this today in traditional
finance: the Visa and Mastercard networks process billions of high-speed, low-value consumer
payments as a Layer 2, while the final, net settlement of large balances between financial
institutions occurs on the FedWire system — a slow, secure, and deliberate Layer 1. The TradFi
industry has already learned that you separate the fast, noisy execution from the slow,
authoritative settlement.

*Yet for some reason, the blockchain industry refuses to accept this lesson.* Some people argue "we
just need the right technology" but this is a fundamental denial of physics.

This brings us back to the **Blockchain Trilemma**. For Arweave to be a secure, decentralized, and
permanent hard drive for the world, it cannot be fast. It must be redundant, verifiable, and likely
"slow."

The system self-organizes around physics:

1. **The RAM (Solana):** Fast, ephemeral, clears cache often.
2. **The Hard Drive (Arweave):** Slow, permanent, remembers everything.

You cannot cheat the trade-off. You can only move the bottleneck. A "fast" system that relies on a
"slow" archive for its integrity is, by definition, a system limited by the security properties of
the slow layer.

> [!IMPORTANT]
> Blockchains like Solana and Sui can try to fight this reality, but the outcome (playing out over
> decades) is inevitable. They are destined to be a fast L2 to a slower L1.

### The Jevons Trap: Why High Fees are a Feature

There is a widely held belief that expensive transactions are a sign of failure. But there is a
massive difference between 'expensive' to a human and 'expensive' to a machine.

An L1 does not need to cost $50 to be secure, but it *cannot* cost $0.001. There is a *minimum
economic threshold* — roughly $0.05/intent — that acts as a digital postage stamp.

At $0.05, the fee is invisible to a human settling a meaningful transaction. But to a bot attempting
high-frequency spam or arbitrage, that cost is fatal. By enforcing this minimum threshold, the L1
filters out the noise without punishing the user. It ensures the chain remains a ledger of human
intent, not a log of algorithmic waste.

Any argument for fees significantly cheaper than $0.05 ignores **Jevons Paradox**: As technology
increases the efficiency of a resource, total consumption increases rather than decreases.

- **On a "Slow" Chain:** Block space is scarce and expensive. This forces an economic filter. You
don't put coffee purchases or spam bots on the main chain. You reserve the L1 for high-value
settlements and L2 proofs. The chain remains small, auditable, and **signal-dense**.
- **On a "Fast" Chain:** Block space is cheap. This invites infinite demand from bots. The chain is
flooded with millions of low-value, zero-sum transactions (arbitrage spam, failed mints, etc.) that
clog the network and bloat the history.

By chasing speed, fast L1s allow the "noise" (spam) to crowd out the "signal" (wealth). A global
bank settling a $1B bond issuance requires 100-year durability, not 400ms finality. They will always
choose the Vault (L1) over the Twitter Feed (Fast Chain).

### The Complexity Trap: Solving the Bridging Crisis

The final argument against slow L1s is the "User Experience" argument: "*Users hate bridging to L2s.
Fragmentation is bad.*"

This is a misunderstanding of the problem. Users don't hate L2s; they hate **General-Purpose L2s**.

We currently have dozens of "Mini-Ethereums" (Arbitrum, Base, Optimism) that are all walled gardens.
They trap liquidity. Because they are all Turing-complete and complex, bridging between them is
dangerous and difficult. *The fact they are attached to a global state L1 makes the bridging problem
exponentially worse*.

The solution is not to abandon L2s, but to embrace **Specialized AppChains** on a local state L1
(e.g., eUTxO).

- **First Principles:** Connecting two complex Operating Systems is hard (General Purpose L2s).
Connecting two simple APIs is easy (Specialized L2s).
- **Hub-and-Spoke:** The overwhelming majority of economic activity is vertical (L2 -> L1
Settlement), not lateral (L2 -> L2). When the L1 uses local state, atomically composing actions
between layers is computationally efficient.
- **The Fix:** When L2s are specialized (e.g., a dedicated Payments Chain or Perps Chain), their
state is bounded and simple. This makes them highly interoperable with the L1 Hub.

We don't need a faster/cheaper L1 to solve fragmentation. We need simpler L2s on a local state L1.

Developers consistently tout global state blockchains (e.g., Ethereum) as being easier to program
for than local state blockchains (e.g., Cardano). *They are correct*. But what gets consistently
missed is that global state blockchains have a low "utility ceiling" — their economic potential is
exponentially lower than that of a local state blockchain. This potential is a product of physics:
updating global state is exponentially more compute intensive than updating local state. Most
economic activity happens at the local (i.e., individual) level which means global state is a
terrible product-market-fit for a DeFi economy.

> [!IMPORTANT] 
> The low utility ceiling of global state is why local state blockchains will inevitably dominate in
> the future despite being harder to program for.

### The World Computer Fallacy: The Casino vs. The Castle

If slow blockchains are superior, why do high-speed chains currently dominate the narrative and user
activity?

The answer lies in who is currently using crypto. Today, the crypto ecosystem is largely a
hermetically sealed echo chamber of day-traders and speculators. For them, **speed is the product**.
A day-trader does not care about the auditability of the ledger in ten years; they care about the
execution of the trade in ten milliseconds.

This selection bias has birthed the delusion: "Users only care about speed." But these speculators
do not represent the perspective of the rest of the world!

The rest of the world — the 99% of global wealth that has yet to enter crypto — does not want a
casino. They want a Castle.

- **Wealth values auditability over latency.** A sovereign wealth fund, a central bank, or a
property title registry cares infinitely more about whether the record is retrievable in 20 years
than whether it settled in 400 milliseconds.
- **Wealth aggregates to the Slow Lane.** History shows that settlement layers always gravitate
toward security and stability, while execution layers gravitate toward speed.

We are currently witnessing a bifurcation that the market has not yet priced in:

- **End-Users** will aggregate to the **Fast L2s** (the Checkout Counters) for convenience.
- **Global Wealth** will aggregate to the **Slow L1s** (the Vaults) for preservation.

The idea that the world will choose a "fast" L1 for its savings is absurd! You do not store gold in
a high-frequency trading platform; you store it in a vault.

### First Principles: The Non-Negotiable Laws of a Trustworthy Ledger

Some will read this and think, "*This is a temporary problem. Technology will solve it. ZK-proofs,
data availability sampling, or some future innovation will let us have speed without sacrificing
history.*"

This is a dangerous delusion. It mistakes a fundamental limitation for a simple engineering hurdle.
The trade-offs we face are not rooted in software, but in the unyielding laws of physics, economics,
and sovereignty. To build a lasting financial system, these three laws are non-negotiable.

#### 1. The Law of Physics (The Law of Storage)

A blockchain's history is like a physical library. For that library to be a truly public good, any
motivated citizen must be able to afford to house a complete copy. A "slow" chain adds a few new
books each day — a manageable burden for a serious librarian.

A "fast" chain, however, is trying to add a new book every single second. Within a few years, the
library has grown to the size of a city. Soon, only the wealthiest corporations on Earth can afford
to build a warehouse big enough to hold all the books and keep it updated. Everyone else, from
individuals to universities, must ask these corporations for permission to read.

At that point, it is no longer a public library; it is a private collection. This is centralization
through physics, and it is an unavoidable dead end for any system claiming to be trustless.

#### 2. The Law of Economics (The Law of Trust)

Proponents of fast chains argue that storing a cryptographic "hash" or "proof" of the history
on-chain is good enough. This is a fatal misunderstanding of value.

Placing a hash on-chain without the corresponding data is like putting a photo of a gold bar's
serial number in a vault, while leaving the actual gold bar with a stranger.

The serial number proves the gold bar existed, but it proves nothing about your current ownership or
the bar's existence. The value is in the asset (the gold bar), not its fingerprint (the serial
number). To settle any meaningful economic dispute, you need access to the asset itself. If you have
to ask the stranger to see your gold bar, you are no longer its owner; you are a supplicant.

#### 3. The Law of Sovereignty (The Law of Proof)

This is the ultimate reason why the first two laws matter.

Imagine in 15 years, a malicious government accuses you of tax evasion based on its analysis of the
public ledger. To prove your innocence, you must present your complete, unabridged transaction
history.

On a "slow" chain, you run your own node. You hold your own history. You can produce the proof
independently, without asking anyone for permission. Your sovereignty is intact.

But on a "fast" chain, that data from 15 years ago was pruned to keep the network performant. To
retrieve your own history, you must ask a centralized "archive node" provider. What if that company
has gone out of business? What if it has been acquired by a competitor? What if it is legally
compelled by that same government to deny you service?

Your on-chain hash is worthless. You have no data to compare against it. You are defenseless.

This is the endgame that "slow" chains are meticulously designed to prevent. Their slowness is not a
bug. It is the very price of permanent, independent, and sovereign proof.

> [!IMPORTANT]
> The vast majority of wealth in the world is willing to sacrifice speed for this sovereignty, even
> if contemporary crypto-enthusiasts are not.

### Conclusion: The Future Belongs to the Slow

We must stop apologizing for the slowness of our L1s. It is not a bug; it is the immune system that
protects our trustless history.

The industry is currently intoxicated by throughput. We are building "fast" chains that are destined
to become amnesiac execution layers, overrun by bot spam, and forced to delete their own pasts just
to survive the present. **They are engineering marvels, but they are economic dead ends as L1s.**

True financial sovereignty requires a different path. It requires an L1 that is proudly slow,
expensive, and unwieldy — because it refuses to compromise on the auditability of the last twenty
years for the convenience of the next twenty milliseconds. The fast chains will then settle against
this slow L1 in the same way that Visa and Mastercard settle against FedWire. Even global stock
markets are built this way where high-frequency trading eventually settles down through the DTCC.

The next generation of core financial infrastructure (L1s) won't be defined by how fast it can move;
it will be defined by how much it can remember.

If you want speed, use a centralized database. If you want truth, use a slow blockchain.

### Appendix: A Back-of-the-Envelope Calculation of Global Settlement Demand

The ~8,000 TPS figure used in this post is a conservative estimate of the *peak settlement* load
required to run the core U.S. financial system, which serves as a proxy for global demand. It is not
an arbitrary number. This calculation is based on publicly available data from the primary
settlement infrastructures.

> [!NOTE] 
> These figures represent the average daily settlement load. While peak demand can be 2-3x higher,
> this analysis does not assume that a blockchain L1 must process peak demand instantaneously. A key
> architectural advantage of a blockchain is its ability to absorb demand spikes into a temporary
> backlog (an economically-sorted queue) that can be cleared over minutes or hours without systemic
> risk, a feature traditional 9-to-5 settlement systems lack.

- **FedWire**
    - **Source Data:** FedWire processed 209 million transactions in 2024 ([link][1]).
    - **Average Daily Volume:** 209M / 252 ≈ 830,000 transactions/day
    - **Required TPS:** 830,000 / 86,400 ≈ **10 TPS**
- **ACH**
    - **Source Data:** Nacha reported 31.5 billion payments in 2023 ([link][2]).
    - **Average Daily Volume:** 31.5 billion / 252 business days ≈ 125 million transactions/day
    - **Required TPS:** 125,000,000 / 86,400 seconds (24 hours) ≈ **1,450 TPS**.
- **CHIPS**
    - **Source Data:** In 2024, CHIPS processed 141 million transactions ([link][3]).
    - **Average Daily Volume:** 141,000,000 / 251 business days ≈ 561,000 transactions/day
    - **Required TPS:** 561,000 / 32,400 ≈ **17 TPS**
- **DTCC**
    - **Source Data:** The NSCC subsidiary of the DTCC processed an average of 220 million
    transactions per day ([link][4]). This number is *before* netting which decreases the actual
    number of transactions executed.
    - **Average Daily Volume:** 220 million transactions/day
    - **Required TPS:** 220,000,000 / 32,400 ≈ **6,790 TPS**

> [!NOTE]
> Visa and Mastercard are *not* part of the core settlement layer because they themselves settle
> using FedWire.

As these numbers highlight, current global demand is satisfied by ~8,000 TPS. Blockchain currently
handles less than 1% of TradFi's activity which means a contemporary layered blockchain system
theoretically only needs ~80 TPS on the L1. Its TPS can be slowly scaled up to 8,000 TPS as it grows
in adoption over decades.

Even if blockchain enables new use cases that belong on the settlement layer where we need 2-3x the
throughput, that is still *decades* away from being necessary.

[1]: https://www.frbservices.org/resources/financial-services/wires/volume-value-stats/annual-stats.html
[2]: https://www.nacha.org/news/ach-network-records-strong-growth-2023-same-day-ach-surpasses-3-billion-payments-inception
[3]: https://www.theclearinghouse.org/-/media/New/TCH/Documents/Payment-Systems/CHIPS-VOLUME-AND-VALUE-through-August-2025.pdf?rev=33ce7a4f987144a99a6637939b192c3f
[4]: https://www.dtcc.com/annuals/2024/value/national-securities-clearing-corporation
