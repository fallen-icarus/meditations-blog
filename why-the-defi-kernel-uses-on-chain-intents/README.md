# Why the DeFi Kernel Uses On-Chain Intents

> [!TIP]
> Here is an AI-generated podcast giving a deep dive on this paper (audio-only).  
> Reload the page if there is a MIME error.

https://github.com/user-attachments/assets/8a39febd-ce84-4be4-8765-8fa7dd7dc29e

## Abstract

The DeFi Kernel is designed based on the layered philosophy described in "The DeFi Hypothesis". As
such, there are two critical requirements for the DeFi Kernel: 1) it must prioritize
censorship-resistance for both *read* and *write* operations, and 2) it must enable building layers
on top of it. These two requirements are extremely relevant when deciding whether to use on-chain
intents or off-chain intents for the DeFi Kernel, and the analysis strongly favors the use of
on-chain intents for this foundational DeFi layer. Exploring two questions is enough to highlight
the importance of using on-chain intents: 1) "how does Alice trustlessly view the current order book
when limit orders are off-chain?" and 2) "how hard is it for layer 2s like Midgard to be built on an
L1 where assets and their associated data are stored separately as with off-chain intents?". The
former requires the use of a data availability (DA) layer which effectively converts the off-chain
limit orders into on-chain limit orders, but with extra cost and complexity. The latter requires
Midgard to carefully match up the assets and data whenever the assets must be used; while this is
certainly possible, it adds significant complexity to Midgard that wouldn't be present if on-chain
intents were used to begin with. Imagine how must harder it would be to build Midgard if Cardano's
L1 UTxOs stored their datums in a separate DA layer.

## The DeFi Kernel's Mandate: Censorship-Resistance Above All

The concept of a "DeFi Kernel" emerges directly from [The DeFi
Hypothesis](https://github.com/fallen-icarus/meditations-blog/blob/main/The%20DeFi%20Hypothesis/README.md),
which posits that the globally adopted blockchain will feature a foundational DeFi layer built
directly onto its Layer 1. This Kernel is not envisioned as an all-encompassing DeFi platform
attempting to cater to every conceivable use case with maximum speed. Instead, its primary,
non-negotiable mandate is to provide an unwavering bedrock of censorship-resistance for its core
financial primitives.

This prioritization is not arbitrary; it is the cornerstone of the Kernel's value proposition and
its potential to offer a true alternative to traditional financial systems. As outlined in "The DeFi
Hypothesis," the blockchain trilemma – which dictates that a single system cannot simultaneously
maximize decentralization (and thus censorship-resistance), security, and throughput – only applies
to specific applications. By building DeFi with composable layers, the DeFi ecosystem as a whole can
entirely sidestep the blockchain trilemma: it can support both censorship-resistance and
high-throughput. With security being an absolute prerequisite, the DeFi Kernel consciously chooses
to optimize for censorship-resistance so that it can be the bedrock for the entire DeFi ecosystem.
DeFi L2s and other entities can build on top of the DeFi Kernel to provide missing features and
throughput.

This commitment to censorship-resistance must extend to both write operations (e.g., submitting a
transaction) and read operations (e.g., observing and verifying the current state of financial
instruments). If users cannot reliably and freely access and verify the state of the Kernel without
fear of interference or manipulation, its claim to censorship-resistance becomes hollow. For
example, if Alice must go through a centralized service just to view the current order book for a
specific trading pair, the DeFi order book is effectively centralized and censorable. The whole is
only as strong as its weakest link.

> [!IMPORTANT]
> Efficient markets **require** public prices. This is a key concept often overlooked by privacy
> focused DeFi applications. If you want to sell your house, how do you know what price to ask for?
> You need to see what similar houses are selling for. This is why the read step must also be
> censorship-resistant.

Therefore, any architectural decision for the DeFi Kernel, including the handling of user intents,
must be evaluated first and foremost through this lens: does it uphold and strengthen
censorship-resistance, or does it introduce potential vulnerabilities or dependencies that could
compromise this core tenet? Features, speed, and even cost-efficiency, while important for the
broader ecosystem built atop the Kernel, are secondary considerations for the Kernel itself. Its
role is to be the maximally resilient, trust-minimized foundation upon which more specialized,
higher-throughput applications can later be built.

> [!IMPORTANT]
> Obviously, if censorship-resitance is too slow and expensive, no one will use it. A minimum
> threshold is required for both. However, Cardano already satisfies them today and upgrades like
> Leios will guarantee it is able to continue satisfying them in the future. Large institutions
> would gladly pay an extra $0.30 for censorship-resistance! This cost only adds up for
> high-frequency traders who likely shouldn't be using the DeFi Kernel directly anyway. The layer 1
> should be reserved for activity that **requires** global accessibility and auditability.

## The Intent Dilemma: Why Off-Chain Solutions Fall Short

Having established the DeFi Kernel's unwavering commitment to censorship-resistance, the question
arises: how should user intents be architected within this foundational layer? For the Kernel,
"intents" primarily refer to the explicit expressions required to interact with its core financial
primitives, such as placing or canceling a limit order or loan request. The crucial architectural
question is whether these intents, and the state they generate, should reside directly on-chain or
be managed off-chain.

At first glance, handling intents off-chain seems attractive, often promising greater scalability,
lower costs, and enhanced privacy for more complex applications. Indeed, for many Layer 2 solutions
or specialized applications built atop the Kernel, an off-chain intent model coupled with on-chain
settlement might be perfectly appropriate. However, when applied to the core primitives of the DeFi
Kernel itself, this approach introduces a fundamental dilemma that clashes directly with its
mandate.

The central issue, as foreshadowed, is one of read censorship-resistance. If Alice wishes to
interact with the Kernel's foundational order book, and the limit orders are stored off-chain, how
can she trustlessly view the current prices? She needs to see the current prices to know how to
price her own assets. But when the limit orders are off-chain, she cannot trustlessly view the
prices. Her view of the market becomes dependent on an external system to provide her with that
off-chain data.

The commonly proposed solution to this problem is the introduction of a Data Availability (DA)
layer. The idea is that off-chain intents are posted to this DA layer, which then somehow guarantees
their availability for verification. While DA layers are a valuable innovation for scaling
general-purpose blockchains or Layer 2s, relying on them for the integrity of the DeFi Kernel's own
foundational state presents critical flaws:

1. **Compromised Censorship-Resistance:** If the DA layer is not as decentralized and
   censorship-resistant as the DeFi Kernel's Layer 1, it becomes the "weakest link." The overall
censorship-resistance of the Kernel's order book is now reduced to that of the DA layer. If
this external DA layer can be censored, coerced, or simply becomes unavailable, then access to the
true state of the Kernel's financial primitives is jeopardized.
2. **Redundant Complexity for Foundational State:** If, conversely, the DA layer does achieve the same
   level of censorship-resistance and decentralization as the Layer 1, it effectively becomes a more
complex, potentially less efficient, and less integrated way of achieving what direct on-chain
storage of these intents would provide. In essence, it's an attempt to convert off-chain intents
into on-chain intents via a detour, rather than directly leveraging the inherent capabilities of the
Layer 1. This extra complexity only makes it harder to build on top of the DeFi Kernel.

> [!IMPORTANT]
> On-chain intents are best for data that is small and directly necessary for smart contract
> execution. Limit orders and loan requests fit this requirement perfectly since they are each only
> a few hundred bytes and their data (e.g., limit price) is necessary to validate spending of the
> UTxOs. However, larger data may best be served by a DA layer (e.g., L2 state) since storing the
> data inside UTxOs may become unwieldy.

Therefore, using off-chain intents with a DA layer for the DeFi Kernel either introduces
unacceptable compromises to its censorship-resistance or adds unnecessary complexity which
undermines its role as a foundational DeFi layer. The off-chain intent approach fundamentally
conflicts with the Kernel's design philosophy and purpose.

## On-Chain Intents: The Uncompromised Foundation for the DeFi Kernel

Given the compromises inherent in off-chain solutions for a foundational DeFi layer, the DeFi Kernel
must manage its core financial intents directly on the blockchain Layer 1. This on-chain approach is
crucial for upholding its primary mandate of unwavering censorship-resistance and fulfilling its
role as a foundational DeFi layer.

Storing intents, such as limit orders or loan requests, directly on-chain offers several
indispensable advantages that align perfectly with the Kernel's requirements:

- **Intrinsic Censorship-Resistance and Trustless Verifiability:** By residing on Layer 1, intents
inherit the blockchain's core censorship-resistance for both submission (*write*) and, crucially,
observation (*read*). Users and smart contracts can directly and trustlessly query the Kernel's state
(e.g., order books) from the L1 itself as the single source of truth. This ensures reliable price
discovery and market access without reliance on intermediaries.
- **Unimpeachable Data Integrity and Provenance:** The blockchain's immutability guarantees a
permanent, transparent, and auditable record of all intents and their resulting state changes. This
fosters profound trust and predictability in the Kernel's foundational operations because the
history of financial activities is clear and unalterable.
- **Seamless Composability:** With intents and their resulting state (e.g., order books)
existing directly on L1, other L1 smart contracts can efficiently and trustlessly interact with them.
This unlocks powerful on-chain financial engineering and allows for the creation of sophisticated
financial instruments that build directly upon the Kernel's primitives, without requiring complex
cross-layer communication (e.g., Oracles) or additional trust assumptions. To put it more
concretely, this tighter integration between the data and the associated assets in the UTxOs makes
it significantly easier for L2s to interoperate with the DeFi Kernel (e.g., a high-frequency trading
L2 can more easily settle against the L1 order book).

The common concerns regarding scalability and transaction costs of on-chain intents are secondary
for the DeFi Kernel. As "The DeFi Hypothesis" posits, this foundational layer deliberately
prioritizes censorship-resistance and security. The required throughput for core settlement and
liquidity is achievable on a well-designed blockchain L1, with higher-volume activities deferred to
Layer 2 solutions that build upon the Kernel. This layered architecture allows the ecosystem to
enjoy both foundational resilience and application-layer scalability.

In essence, for the DeFi Kernel to be the truly censorship-resistant and trust-minimized bedrock
envisioned, its intrinsic financial intents must reside on-chain. This is not merely a preference
but a direct consequence of its core mission to provide an uncompromised foundation for the broader
DeFi ecosystem.

## Appendix

### TradFi Stock Markets Use Off-chain Intents

Technically, the DTCC is only for settlement of trades while a stock exchange is used for
broadcasting open orders to everyone. This architecture mirrors the off-chain intents approach.
However, **TradFi is censorable**. End-users are not able to interact with the DTCC directly, they
*must* go through intermediaries. In order to ensure censorship-resistance, the DeFi Kernel
*deliberately merges the functionality of the DTCC and the stock exchange*. Layer 2s built on top
(e.g., DeltaDeFi) could separate the two functionalities again in order to gain increased
throughput.
