---
layout: post
title:  "Ensuring Bitcoin's growth"
date:   2014-08-22 14:38:00 +0100
categories: bitcoin
---
![image](https://68.media.tumblr.com/7ea132c609f79906ea48345e3469476f/tumblr_inline_naplp22cO21sia8s8.jpg)

If we want bitcoin to be used as the number one currency in the world, it must support all the use-cases of todays currencies. The transaction time and fee should be, and stay, as low as virtually possible. Two very important features of todays currencies are the non-existent transaction fee and instant transaction time if you choose to pay with cash. If we truly want bitcoin to be the number one currency, we must make paying with bitcoin just as easy and fast as paying with cash. Therefore, two things must be improved: the transaction time and the transaction fee.&nbsp;

Bitcoin is growing a lot, and with growth comes potential scaling issues. Potentially the biggest one:&nbsp;reaching the limit of transactions per second the network can handle which would result in higher transaction fees and slower transaction times. Miners would need to choose which transactions they’re going to include in their blocks (blocks are several transactions grouped together) and it is only logical that they would include the transactions with the highest transaction fees, because these generate the most money. The transactions with the lowest fees aren’t going to be included in any blocks anymore, which means they’ll be carried out extremely late, or not at all. To ensure that a transaction is going to be carried out, people would need to pay a transaction fee that is high enough to be included in a block. This means that the average transaction fee is going to be higher, with the potential of rising indefinite.

If transaction fees would rise, it would be bad for the adoption and usage of bitcoin. One of the advantages bitcoin currently has over traditional payment networks is the fact that it has low transaction fees. If transaction fees become higher, that advantage is lost, giving people one less reason to switch.

Gavin Andresen, the chief scientist of the Bitcoin Foundation, has recently published a proposal that would increase the amount of transactions per second (tps) the Bitcoin network can handle. This proposal would make sure that the Bitcoin network can handle around 15,000 transactions per second, which is almost 8 times more than the amount of transactions Visa handles on average ([link](http://usa.visa.com/merchants/industry-solutions/retail-visa-acceptance.jsp)). By solving this problem now, Andresen prevents any problems with transaction speeds and transaction fees going forward, and makes sure Bitcoin doesn’t encounter the problem described above.

**Andresen’s proposal**

As Andresen described, “Bitcoin miners want their newly-found blocks to propagate across the network as quickly as possible, because every millisecond of delay increases the chances that another block, found at about the same time, wins the block race.”

Bitcoin miners get a reward for their efforts, which is currently 25 bitcoin, so they want to want to&nbsp;report their efforts as quickly as possible to the network. If they are the first to report about their efforts, then they receive the 25 bitcoin reward. Of course, the same block can be solved by other miners as well, so it is very important If they are slower than another miner, they lose their 25 bitcoin. Making sure that they are faster than other miners is what we call the ‘block race’.

The amount of time it takes for a solved block to be reported to the network depends on the size of the block. The size of the block is in turn determined by the number of transactions that are in the block. This creates an incentive for miners to keep their block sizes as small as possible, thus not including the maximum amount of transactions possible. If they included the maximum amount of transactions, it would probably mean that their block propagated slower than other blocks, in which case they would lose their miners fee.

Because of this, transactions with a higher miners fee are included in the blocks much faster than transactions with a relatively low miners fee. However, we make a lot of small payments where a relatively high miners fee isn’t worth it (let’s say that I want to buy some drinks in a store, if I must pay $.05 miners fee for a $2 bottle of cola, using bitcoin has zero advantage over cash in that case).

A commenter on Reddit made the following great comparison: “Picture a whisper game among 100 5-year olds standing in a circle. You and Billy, who is next to you, whisper different messages to the people next to you - you whisper the word "Bitcoin" to the person to your right, while Billy recites the Preamble to the Declaration of Independence to the person to his left. The two messages transmit around the circle until everyone has one of the two messages. So which message is more prevalent? The shorter one. So Bitcoin miners currently have incentive to pass short messages, which means small blocks, which means few transactions.”

Andresen’s solution is very simple: no matter the amount of transactions included in each block, each block must be equally big in size. This means that each block transfers equally fast, removing the need to be faster. This would eliminate the ‘block race’ and the discrimination between transactions with a high and low miners fee.

Because the size of the blocks will be also smaller than the size of the blocks used today, the time before a transaction will be confirmed will also be a lot shorter.

**How does it work**

The technical aspects of Andresen’s proposal are somewhat difficult to understand, but I’ll try to explain it as simply as possible.

In order to make every block equally big, you need to carry out some functions. Functions are just a combination of different steps or calculations.

Functions have an input and an output. You can compare this function with a recipe. You enter the input into the function, and then several calculations or steps are taken to reach the output. If you want to know more about functions you can view [this](http://www.mathsisfun.com/sets/function.html) page.

The goal is to construct a series of functions that if executed, no matter what the input is, the size of the outcome is always the same. In this case, the input would be the amount of transactions and the outcome is the size of the block that needs to be transferred. If you want to know how things work exactly, you should really read Andresen’s proposal.

It is a simple idea, but it has great advantages, as it would remove the incentive to not include all transactions in a block because of the ‘block race’. It also limits the amount of bandwidth the network uses.

**The future**

Increasing the amount of transactions per second was something many in the Bitcoin community pushed for and thought about lately.

The rollout of this solution could easily take more than a year, because it needs to be thoroughly tested and tweaked, as Andresen pointed out.

But, if it finally is working, the benefits for users of bitcoin are huge. Transaction fees would go down and transactions are going to be confirmed faster. Cryptocurrencies that were designed to solve this problem will vanish and more people will start using Bitcoin.

This is especially great news for people in third world countries. A transaction fee of about $.05 is quite a lot of money for them. If you take South Africa as an example: 1 ZAR (South African Rand) is equal to $.094. If we convert that to the transaction fee they would pay, it’s around 0.5 ZAR. If the transaction fee would go down, using bitcoin for their payments becomes more interesting. We already see a huge growth of bitcoin users in third world countries, and this would stimulate that growth even more.

It also enables bitcoin to be used for In App Purchases (IAP). If you need to pay $.99 for an IAP with today’s transaction fee, the transaction fee is relatively high compared with the price of the IAP. IAP’s mostly cost between $.50 and $10. A lot of money is spent on IAP’s, and if bitcoin could be used to pay them, it would increase the amount of bitcoin users.

Reducing the transaction fee could mean that companies like Apple and Google (who both don’t accept bitcoin for transactions made on their respective mobile platforms) are going to think about accepting bitcoin, which would make bitcoin viable for another use-case. &nbsp;

The minimum transaction fee could be as low as $.005 (half a cent), which would make it virtually free to transfer money. If this proposal is finally working it also means that Bitcoin can grow for quite some time before it experiences any major issues such as hard forks. If the network reaches its limit, it would require several hardware upgrades and possibly a hard fork of the Bitcoin technology (basically this means that a new upgrade isn’t backwards compatible: if not 100% of Bitcoin users upgrade, you would have two blockchains (one with the upgrade and another one for users that didn’t upgrade).

All of this means that Bitcoin is maturing as a technology and is becoming more viable for even more use cases, like micropayments. If we combine this with third-parties making using bitcoin even [easier](http://andrewoons.com/post/93339555434/how-to-get-bitcoin-from-the-early-adopters-to-the-early), we can experience an even bigger growth in bitcoin usage. Andresen's proposal makes sure that we can handle this growth.

If you’re interested in reading Gavin Andresen’s proposal, click here ([link](https://gist.github.com/gavinandresen/e20c3b5a1d4b97f79ac2)).

You can follow me on Twitter: [@andrewoons](https://twitter.com/andrewoons)