+++
title = "Introduction to plain text accounting"
date = 2019-09-14
template = "post.html"
+++

Being too broke until yesterday, I decided it's high time to get on top of my financial situation.

This, among others, involves keeping close track of how much money I have and spend. But, how do this? It would unequivocally be a shame to miss this chance to use something hacker-worthy.

## Enter plain text accounting

In the past, I have tried numerous times to keep track of my personal finances. All those times, after one or two months, I gave up. It would be too tedious to keep track or even care how much money I spend when I am not broke.

Attempted methods include simple spreadsheets, multiple web and/or mobile apps, even spending only from one bank account so as to have everything centralized and easily analyzable. For some reason or another all of them stopped working.

But now I'm sure I have found the pinnacle of accounting: plain text accounting!

It is of undeniable certainty that this method too, will fail. Until then, here is its story.

## Ledger-cli, hledger, beancount, abandon

All those are names of super cool software that does plain text accounting. But first, a definition:

> Plain text accounting is accounting software with database a plain text file.

So no database of the SQL kind. Instead, old school paper accounting with new school digital digits.

The first obstacle I faced in my Plain Text Accouting Journey (PTAJ from now on) was the decision of which software I should choose. Ledger-cli is the historically first PTA software, appearing in 2003 and written in C++; but hledger is written in cool Haskell. And beancount is written in Python, with easily pluggable web interface and nice charts and visualizations. Deadlock.

After several minutes I settled on ledger-cli. The documentation and the input method was seemingly the simplest to get started. Furthermore, it seems data can easily be exchanged between each other of those, so I can switch easily if need be.

## Getting started

I loved the brutal simplicity of [ledger-cli's website](https://www.ledger-cli.org/) and at the same time shocked with the abundance of information on their [docs](https://www.ledger-cli.org/3.0/doc/ledger3.html). However, I had already realized that I had learned enough (in the software comparison phase) to be able to cover my bookkeeping needs, so who cares about reading any more docs.

To get started in your PTAJ, you need to reflect your current financial state in a plain text file. I created a file named `ledger.txt` with the following content:

```
2019/09/14 * Opening Balance
    Assets:Checking             $1000.73
    Liabilities:MasterCard      -$200.60
    Equity:Opening Balances
```

This means I have 1000 dollars in my checking bank account and I owe 200 dollars for my credit card borrowing performance. And this is all the money I have and owe.

I later learned what `Equity:Opening Balances` meant. It was the most rocky part of my PTAJ, and I believe everyone's, so I'll leave it for now.

Let's see the results of our work so far. Running in the command line:

```
$ ledger -f ledger.txt balance
            $1000.73  Assets:Checking
            $-800.13  Equity:Opening Balances
            $-200.60  Liabilities:MasterCard
--------------------
                   0
```

Not much. Let's say you go out for a pizza and add this entry in your file:

```
2019/09/10 * Pizza
    Expenses:Food             $10.00
    Assets:Checking          -$10.00
```

Running:

```
$ ledger -f ledger.txt balance checking
             $990.73  Assets:Checking
```

As you can see, we spent 10 dollars in a pizza, and our clever software knew what to subtract and is kind enough to let us know of the result. `Expenses:Food` is a sub-account of the `Expenses` top-level account. [According to the ledger-cli docs](https://www.ledger-cli.org/3.0/doc/ledger3.html#Structuring-your-Accounts), there are five top-level accounts:

* Expenses: where money goes
* Assets: where money sits
* Income: where money comes from
* Liabilities: money you owe
* Equity: the real value of your property (*confusing*)

Another example:

```
2019/09/10 * Amazon frenzy
    Expenses                     $350.00
    Liabilities:MasterCard      -$350.00
```

I used my credit card to pay at Amazon, which I sorted that under the `Liabilities` account - it's money that I now owe.

You have now learned basics of ledger-cli. I did think this was enough knowledge to enable my future affluence, but the PTAJ was too fun to stop. For instance, the following entry is equivalent to the above:

```
2019/09/10 * Amazon frenzy
    Expenses                     $350.00
    Liabilities:MasterCard
```

Every entry needs to be balanced (as in sum equals zero). Thus, if you omit an obvious part, the software will fill it for you. Though, only in its mind, it will never alter the text file.

## Single-entry vs double-entry accounting

Single-entry accounting is the obvious, straight-forward way someone would keep track of expenses. e.g.:

1. I have 100 dollars in my wallet
2. I paid 10 dollars for a pizza
3. I now have 90 dollars in my wallet

All records follow one thread, keeping track of one number.

Double-entry accounting keeps track of multiple numbers. Also, it always keeps track of the source and the destination of the money being transfered. The accounting lingo is `credit` and `debit`. Now, every time there is a change in the numbers we keep track of, we update them. Since a change is a transfer from one to another, we will always update (at least) two accounts. However, every entry must be balanced - equal amount of money needs to be at the source and at the destination. We can neither create money out of thin air, nor make it disappear. Money has to come from somewhere and go somewhere.

This is the point of the `Equity:Opening Balances` account. It is a sub-account of our `equity`, "the real value of our property", useful for explaining from where our money comes from when we start our bookkeeping records.

## More PTAJ fun

[John Wiegley](https://github.com/jwiegley) et al have been developing ledger-cli for 16 years. Unsurprisingly, it has many tricks up its sleeve. Let's explore a few.

### Cleared and pending transactions

You may have noticed an asterisk (`*`) between the date and the name of the entry in the examples. It's purpose is not to separate the two, it could be omitted. It's meaning in the ledger-cli system is signifying a cleared transaction. There is also the exclamation mark (`!`), which signifies a pending transaction. [According to the documentation](https://www.ledger-cli.org/3.0/doc/ledger3.html#Transactions-and-Comments) you have to choose for yourself what "cleared" and "pending" transactions mean. I found no value and ignored for the first hours of my PTAJ, but later I realized I can use them for payments that I will do in the near future and thus don't want these money to appear as available for spending.

### Unit price

Another enjoyable trick is setting a unit price. Let's say you buy a few apples, and pay per apple:

```
2019/09/11 * Farmer's Market
    Expenses:Food       10 apples @ $0.30
    Assets:Checking
```

Ledger-cli can calculate how much you paid, and subtract it from the checking account.

Maybe though, you know the final price but not the unit price. In that case, you can do that:

```
2019/09/11 * Farmer's Market
    Expenses:Food           10 apples @@ $3.00
    Assets:Checking
```

### Stock

Ledger-cli supports a concept called commodities, which enables us to record [buying and selling stock](https://www.ledger-cli.org/3.0/doc/ledger3.html#Buying-and-Selling-Stock). Let's buy some Apple shares:

```
2019/09/13 Stock purchase
    Assets:Broker                     10 AAPL @ $218.75
    Expenses:Broker:Commissions        $20.00
    Assets:Broker                  $-2,207.50
```

### Strict mode

One day you write this entry:

```
2019/09/10 * Supermarket
    Expenses                     $50.00
    Liabilities:MatserCard
```

As you may have noticed, there is a typo.

Unfortunately, no one will complain. Ledger-cli will consider MatserCard a brand new account. Hence, leaving your balance completely off.

Thankfully, there is a way to prevent this. Firstly, you need to statically define all your accounts like this, in the beginning of your text file:

```
account Equity:Opening Balances
account Assets:Checking
account Income:Salary
account Liabilities:MasterCard
account Expenses:Food
```

And secondly, you need to use the `--strict` in your cli commands. E.g. `ledger -f ledger.txt balance checking --strict`. Consequently, if there is an undefined account [ledger-cli will complain](https://www.ledger-cli.org/3.0/doc/ledger3.html#Keeping-it-Consistent).

### BitBar Plugin

Here is a tiny [BitBar](https://getbitbar.com/) plugin, in case you want to be reminded all the time how much money you have.

```sh
#!/bin/bash

# Display balance of accounts, using ledger-cli

CASH=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b cash --strict | awk '{print $1}')
CHECKING=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b checking --strict | awk '{print $1}')
SAVINGS=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b savings --strict | awk '{print $1}')
PENDING=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b assets --pending --strict | awk '{print $1}')
LIABILITIES=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b liabilities --strict | awk '{print $1}')
STOCK=$(/usr/local/bin/ledger -f /Users/sirodoht/ledger.txt b stocks --strict | awk '{print $1 " " $2}')
OVERVIEW=$((CASH+$CHECKING))
echo "💸 $OVERVIEW"
echo "---"
echo "Cash $CASH"
echo "Checking $CHECKING"
echo "Savings $Savings"
echo "Pending $PENDING"
echo "Liabilities $LIABILITIES"
echo "Stock $STOCK"
```

## Epilogue

Ledger-cli accounting is more entertaining than expected :P

The [Ledger-cli docs](https://www.ledger-cli.org/3.0/doc/ledger3.html) are a great resource to learn, despite initial trauma due to magnitude. Additionally, [plaintextaccounting.org](https://plaintextaccounting.org/) is everything PTA.
