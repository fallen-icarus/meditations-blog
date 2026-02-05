# How to Bank the Unbanked and Bootstrap a DeFi Economy at the Same Time

> [!TIP]
> Here is an AI-generated podcast giving a deep dive on this paper (audio-only).  
> Reload the page if there is a MIME error.

https://github.com/user-attachments/assets/23e11c36-bd23-4eee-a8c8-6f0a169b12e6

## Table of Contents

- [Abstract](#abstract)
- [Unsecured loans are the initial economic spark](#unsecured-loans-are-the-initial-economic-spark)
- [Non-magin loans are more important than margin loans](#non-margin-loans-are-more-important-than-margin-loans)
- [Microloan-Backed Securities for DeFi](#microloan-backed-securities-for-defi)
    - [Example Business Model](#example-business-model)
- [Naturally Incentivized Honesty](#naturally-incentivized-honesty)

## Abstract

One of the primary goals of decentralized Finance (DeFi) is to bank the unbanked and provide
economic opportunities to under-served people, yet DeFi dApps are consistently **not** designed to
accomplish this. Within the DeFi space, it seems like 90% of all current lending/borrowing dApps
require borrowers to over-collateralize their loans. While some dApps offer the means of eventually
getting an under-collateralized loan after many successful loan repayments, this is not the right
approach for two reasons: 1\) the unbanked likely do not have any assets by virtue of being unbanked
and therefore have no way of even getting their first over-collateralized loan, and 2\) this is the
opposite direction that credit markets have developed. Credit markets have historically started with
small unsecured loans with high interest rates and evolved into exponentially larger collateralized
loans with lower interest rates. But starting with over-collateralized loans isn’t the only issue
with contemporary DeFi: most economic loans are non-margin loans (i.e., there is no liquidation
risk) while most DeFi loans today are margin loans. Margin loans are only ever used for asset
speculation; entrepreneurs don’t use them to fund startups since short-term market volatility can
wipe them out. So not only is contemporary DeFi taking the wrong approach to banking the unbanked,
but they are also trying to use the wrong type of loan to do it. Cardano-Loans is a DeFi protocol
built for Cardano that is specifically designed to to bank the unbanked: it has a built in credit
history system, and supports peer-to-peer loan negotiations and enforcement of non-margin loans.
Using Cardano-Loans, it becomes possible to create **internationally traded microloan-backed
securities** \- a killer DeFi application that could revolutionize the microfinance industry and
bank the unbanked at the same time.

## Unsecured loans are the initial economic spark

> [!IMPORTANT]
> This section is highly speculative in that it is largely untested. However, it logically follows
> from first principle reasoning, and is backed up by empirical evidence.

All economic growth, whether an individual starting to build wealth or a society starting to build
wealth, starts with unsecured loans (i.e., loans not backed by any collateral). If the unsecured
loans are used productively, they result in a compounding accumulation of wealth (a.k.a. assets).
However, due to the inherent risk of unsecured loans, lenders typically refuse to give large
unsecured loans \- you can’t buy a house with an unsecured loan. So borrowers, in order to access
greater amounts of debt and/or significantly better terms, are eventually incentivized to use their
newly accumulated wealth as collateral. The economic growth comes from the *virtuous cycle* this
creates:

- **Starting Point:** Borrowers begin with small unsecured microloans, which require no initial
  collateral.  
- **Productive Use:** When these loans are used effectively – say, to start a small business or
  invest in tools – borrowers can accumulate assets over time.  
- **Asset Growth:** These assets then serve as collateral, enabling borrowers to access larger
  loans.  
- **Infrastructure Development:** With bigger loans, entrepreneurs can fund projects like internet
  access or identity systems, which are foundational for economic participation.  
- **Systemic Benefit:** Improved infrastructure and asset ownership make lenders more confident,
  encouraging them to offer more loans, thus perpetuating the virtuous cycle.

The current DeFi zeitgeist believes that lenders will not lend unsecured loans because they are too
risky. Instead, lenders will require borrowers to start with secured loans, and only offer unsecured
loans once enough trust has been established. This is why nearly all DeFi lending/borrowing dApps
require over-collateralization. However, empirical evidence directly contradicts this stance.

In the developed world, it is commonly said that secured credit cards (i.e., fully collateralized
credit cards) are a good way for new borrowers to bootstrap a credit history for themselves.
However, they are actually rarely used. In the United States, a person must be at least 18 years old
to have a credit card in their name. According to [Sallie Mae's 2016
study](https://www.salliemae.com/content/dam/slm/writtencontent/Research/Majoring_in_Money.pdf),
only 5% of people aged 18-20 actually use a secured credit card for payments. Yet 43% use an
unsecured credit card for payments. This statistic is interesting for two reasons: 1\) it shows that
new borrowers overwhelmingly favor unsecured loans, and 2\) lenders don’t mind giving unsecured
loans even to new borrowers. This latter point is entirely missed by DeFi developers. 

As another example, consider [Kiva](https://www.kiva.org/) \- a microlending firm that lends to the
developing world. These loans are typically unsecured and have interest rates of about 35%
([source](https://www.cgaa.org/article/micro-loans-in-developing-countries#does-it-work)). And
despite these loans going to troubled jurisdictions, usually without good identity systems, Kiva’s
repayment rate is [reported to be \~95%](https://www.kiva.org/about/due-diligence/risk). Borrowers
benefit tremendously from these microloans. According to
[CGAA](https://www.cgaa.org/article/micro-loans-in-developing-countries#does-it-work): 

> Rural farmers in East Africa who received microloans through the One Acre Fund have seen their
> **incomes increase by 40-50 percent compared to a control group**.

If unsecured loans are so unsafe, why are they the number one type of loan for both new borrowers
and emerging economies? Granted, the amounts are small relative to collateralized loans in the
developed world. But if the current DeFi zeitgeist was correct, why are there any unsecured loans at
all and why do they have such a high repayment rate? Some scammers will take off with the principal;
but as long as lenders properly manage their risk they can safely lend unsecured loans.

> [!IMPORTANT]
> The fact that Kiva is successfully able to lend unsecured loans to the developing world is proof
> that it's also possible to vet borrowers in places lacking stable institutions and identity
> systems. **Kiva does not have a method for recovering assets in the case of a default**; there is
> no safety net for lenders ([section 1.6 of Kiva’s Terms of Service](https://www.kiva.org/legal/terms)).
> Yet this doesn’t stop Kiva from finding willing lenders for microloans.

There is an important point implied here that should be made explicit: **you cannot have a liquidity
pool that just gives an unsecured loan to anyone who asks**.

In order to safely conduct unsecured loans, they must be peer to peer. Lenders must vet the borrower
before agreeing to the loan. Any attempt to automate this vetting process will suffer from
[Goodhart’s law](https://en.wikipedia.org/wiki/Goodhart's_law). As a result, the best way to support
unsecured loans is through a DeFi/TradFi hybrid process: use a p2p DeFi lending protocol for the
actual loan enforcement and credit history database, but include TradFi background checks like proof
of employment. 

The biggest issue with TradFi microloans is the [high operational
costs](https://www.cgaa.org/article/micro-loans-in-developing-countries#improvement): getting the
money to the borrower requires going through several middlemen who each charge a fee. Kiva requires
at least two middlemen ([source](https://www.kiva.org/blog/changes-to-interest-rates)). Using the
hybrid approach enables microloans to have significantly cheaper operational costs and solves the
credit history database problem \- even borrowers in unstable regions will have a credit history
they can leverage next time. Developing nations don’t need to create their own expensive identity
databases.

> [!IMPORTANT]
> The blockchain’s transaction history is the database. The borrower's credit history and lender's
> reputation can be easily looked up using CIP-89's beacon tokens ([CIP source](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0089)).
> Just filter the transaction history using the beacons. Even the borrower's credit score can be trustlessly
> determined this way.

## Non-margin loans are more important than margin loans

Margin loans only comprise 5% of all household debt ([margin
source](https://www.finra.org/rules-guidance/key-topics/margin-accounts/margin-statistics),
[household debt source](https://www.newyorkfed.org/microeconomics/hhdc.html)). The reason for this
is that margin loans are too risky for most funding activities. If you used margin to fund a
business, short-term market volatility could wipe you out. Because of the downsides to margin loans,
they are typically only used to speculate on securities
([source](https://www.schwab.com/learn/story/what-every-trader-should-know-about-margin)). It isn’t
a coincidence that, to date, the only real use case for DeFi is speculation. DeFi developers are not
building economically useful credit markets. If we want DeFi to eventually support real economic
activity, we need to start supplying it with economically useful credit \- non-margin loans.

If you ask a DeFi developer why they are prioritizing margin loans, the response is usually along
the lines of: “Cryptocurrencies are too volatile to be used as collateral for non-margin loans so
there won’t be any lenders.” But this is the exact same fallacy as with the unsecured loans:

**DeFi developers don’t believe there is currently a market (i.e., willing lenders) for non-margin
loans when in fact there is\!** Just because you wouldn’t lend against volatile cryptocurrencies
doesn’t mean no one will… If a lender that properly vets a borrower is willing to offer unsecured
loans, why would they not also be willing to accept volatile assets as collateral? Isn’t some
collateral better than no collateral? This same argument (i.e., “there is no market for it”) was
also made for microloans, but Nobel Laureate Professor Mohammed Yunus proved this wrong:

> His concept of lending to \[the\] poor without any collateral, hitherto considered as impossible
> by many, was in fact a great success.  
> \- [Securitization of Microloans: An Indian Perspective of the Innovation in Microfinance
Industry](https://www.researchgate.net/publication/311649078_Securitization_of_Microloans_An_Indian_Perspective_of_the_Innovation_in_Microfinance_Industry) 

This belief \- that there is no market for non-margin DeFi loans \- is a self-limiting belief. If we
can get past it, DeFi can revolutionize the microfinance industry.

## Microloan-Backed Securities for DeFi

Asset-backed securities are a way of minimizing risk for general investors in the same way that
index funds minimize risk: *diversification*. If a mortgage-backed security is backed by 10
mortgages and one of the underlying mortgages goes into default, the other 9 are still paying the
principal and interest; the investor of the mortgage-backed security can still profit overall.
Consider Kiva’s 95% repayment rate. If you lent a single microloan through Kiva, there is a 5%
chance of you not getting paid. But if Kiva packaged up 10 of these loans and sold the package to
you, the chance of you not getting paid is astronomically small (0.05^10).

> [!WARNING]
> It may not always be safe to assume the loans are fully independent. For example, loan defaults
> are usually highly correlated during an economic recession. However, while this complicates the
> risk calculation, it does not change the underlying concept: *packaging microloans together
> dramatically decreases the overall risk*.

The other benefit of asset-backed securities, specifically loan-backed securities, is it allows
financial institutions to lend more
([source](https://www.financestrategists.com/wealth-management/investments/asset-backed-securities-abs/)).
Consider if Kiva lent out $1,000 for the 10 microloans ($100 each) and sold them as a
microloan-backed security for $1,050; Kiva made a $50 profit and can now make another 10 microloans
that it couldn’t before. The key takeaway here is that, by packaging microloans into securities,
**it lowers the overall risk of the microloans which attracts more capital for microloans**.

This is not just a theory. India first securitized microloans in 2009 and has since seen an
explosion in microloans: the microloan market has seen double digit growth over the past 20 years
and is showing no signs of slowing. It is expected to see a continued compounding growth rate of
about 12% through 2032\. This microloan lending is a huge contributor to India’s overall economic
growth ([source](https://www.marketsandata.com/industry-reports/india-micro-lending-market)). 

The issue with TradFi microloan-backed securities is one of scale. The idea is that, if you buy one
of these securities, future loan payments are supposed to be passed on to you. But if you live on
the other side of the world, how can this happen efficiently enough to be worth doing? Remittance
payments are expensive due to the operational costs of TradFi. If a microloan’s payment is only $10,
the TradFi fees required to pass this payment to someone in the United States takes pretty much all
of it. Many places even enforce a minimum transfer size to make the remittance payment worth it for
them (e.g., [Wells Fargo has a $25
minimum](https://www.wellsfargo.com/help/international-remittances-faqs/#howmuchmoneycanisendtomybeneficiary)).
This high cost fundamentally limits who can supply capital to fund these microloans.

On the flip side, consider Kiva. In order for Kiva to package its microloans for sale as a security,
it needs to digitize each microloan. But Kiva gives microloans to regions without reliable
infrastructure; India is stable enough to support digitizing microloans. Not only that, but Kiva
would need to pass on the loan payments to the new security owner every time it changes hands. This
is not an easy task when anyone in the world can buy/sell these securities.

**DeFi solves both of these problems**: it supports low-cost international payments and
automatically routes loan payments to the proper security owner. Cardano-Loans does nearly all of
the heavy lifting, and Cardano’s cheap international transactions do the rest. All that’s required
is an easy to use mobile app for borrowers to be able to pay the security owners directly, no matter
where they are in the world.

> [!IMPORTANT]
> Internationally traded microloan-backed securities is one of DeFi’s killer features, and is likely
> the most effective method for banking the unbanked.

### Example Business Model

1. A local lending shop opens in Argentina and offers microloans using the Cardano-Loans protocol as
the backend.  
2. A local borrower requests a loan and supplies TradFi information to back up their credibility
(e.g., proof of income).  
3. The lender agrees to the loan and gives the borrower the microloan which the borrower can pay
back through a mobile app. The lender gets a tradable loan bond (a Cardano NFT) from the
Cardano-Loans protocol for this loan.  
4. Repeat steps 2-3 several more times.  
5. Once the local lending shop has enough loans to package, they can offer the loan bonds for sale
as a microloan-backed security. Anyone in the world can buy them; the Cardano blockchain will
properly enforce the new ownership of the loan bonds.  
6. Once the sale goes through, the new owners can use the loan bonds to update the required payment
addresses for each loan in the package. This update can be done in the same transaction as the
purchase so there is no risk of missing future loan payments. Cardano-Loans will enforce all future
loan payments go to the new address.  
7. The lending shop can take the proceeds from the security sale and repeat steps 1-5.  
   
**The borrowers don't need to do anything.** The mobile app can easily abstract away the process of
finding the new securities owner whenever it changes hands.

Initially, international buyers of the securities may not trust the new lending shop. Some will be
willing to buy from them, but most will wait on the sidelines until the lending shop has proven it
can properly vet borrowers. Once the lending shop has a decent track record, more people will be
willing to buy microloan-backed securities from them.

One benefit of Cardano-Loans is that the lending shop’s reputation is trustlessly auditable. Every
lender for Cardano-Loans gets a unique on-chain identifier which can be used to actually see what
happens to all of the loans issued by this lender. **Selling the loan to investors does not break
the trustless link to the initial lender.** If the lender claims a 95% repayment rate, this can be
verified by looking at their on-chain lending history. This transparency adds confidence to
international buyers of these securities and incentivizes lenders to care what happens even after
they sell the microloans to investors.

> [!IMPORTANT]
> This business model effectively eliminates Kiva, the company. Its local partners are able to
> connect to the international market directly using DeFi and a smartphone.

Eventually, many lending shops could sell their securities to businesses that repackage them for
international buyers. For example, a business could buy microloans from a Nigerian shop and an
Argentine shop; then combine them to offer a “global” microloan-backed security. Combining
microloans from around the world further diversifies the risk of the securities (i.e., a recession
in Nigeria likely won’t impact Argentina) which will attract even more capital into microloans.

This business model could be highly lucrative for both local lenders and global investors; and by
using Cardano-Loans, borrowers get their own trustless credit history just for participating. This
is an extremely realistic way to bank the unbanked, and only DeFi is able to do it.

## Naturally Incentivized Honesty

Some critics might argue Kiva’s success is just luck; unsecured loans don’t work at scale because
the incentives favor running away with the loan. While this argument seems convincing, it is
logically flawed: **it completely ignores the long-term incentives which strongly favor paying back
the unsecured loan.**

Consider two borrowers: Alice and Bob. Both of them have the same starting income (e.g., $2/day) and
are both new borrowers who just got their first unsecured loan of $20 from their local lender. Alice
is malicious and keeps the money while Bob is honest and pays back the loan after using it
productively. Who is better off?

Alice got $20, but otherwise her situation is exactly the same as before the loan – her income is
still only $2/day. She is unable to get another unsecured loan because the local lender knows her.
It isn’t enough to just burn her on-chain identity; she needs to convince a local lender to give her
another loan using TradFi information again. Creating a brand new real world identity is
exponentially harder than just creating a new on-chain identity. Perhaps Alice is lucky and there
are a few other local lenders in her area. She might be able to get a $20 unsecured loan from these
lenders one-time each, but they too will stop lending to her after that. The main point is that
**Alice can only be malicious a finite number of times before she is effectively frozen out of the
credit market.**

> [!IMPORTANT]
> Government identity systems are helpful, but not necessary. Local lenders can keep their own
> records on the borrowers they do business with. This is how credit markets worked prior to
> institutional identity systems; credit reporting is actually only about 200 years old
> ([source](https://time.com/3961676/history-credit-scores/)). Yet credit markets go all the way
> back to at least Mesopotamia
> ([source](https://africame.factsanddetails.com/article/entry-1019.html#chapter-8)).

What about Bob? He used the loan productively and increased his income by 40-50% (e.g., from $2/day
to $3/day). He also paid back the loan which means the local lender trusts him enough to give him
another $20 loan. Once again, Bob uses the loan productively and his income increases by another
40-50% (e.g., $3/day to $4.50/day). Bob can repeat this process an infinite number of times because
the local lender trusts him. The local lender may even trust him enough to increase the loan amount
to $50 which Bob can use to increase his income by 100% (e.g., $4.50/day to $9/day). **Bob is
objectively better off than Alice simply because he still has access to the credit market.**

With Bob’s visibly rapid increase to his quality of life, his community members will get envious
which fuels the [keeping up with the
Joneses](https://en.wikipedia.org/wiki/Keeping_up_with_the_Joneses) psychological phenomenon. The
only way to keep up with Bob’s compounding quality of life is to also be honest and pay back
unsecured loans. As a result, Bob’s honesty is naturally contagious. **Most borrowers will be honest
because the long-term benefits of honesty dramatically outweigh the short-term benefits of
dishonesty.** Legal recourse for defaults help, but are not necessary.

> [!IMPORTANT]
> This is only true for the DeFi/TradFi hybrid approach because it makes it significantly harder for
> malicious borrowers to find new victims. The anonymous nature of the pure DeFi approach makes it
> way too easy to create new identities for new unsecured loans.
