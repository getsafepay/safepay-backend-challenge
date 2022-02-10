# safepay-backend-challenge

## Overview

This is a takehome test for candidates applying for a back-end engineer
position at Safepay. It contains two sections: "Backend" and "Databases".

Feel free to solve these questions however you see fit, using whatever coding
style or third-party libraries you think are appropriate.

To start the test, simply create a repo and make your edits locally.

For the backend portion of the test, create a `/backend` folder. We'd like to write some code that achieves the following:

1. Create a JSON API (REST or GraphQL) (using any language + framework you're comfortable with) which will return which cryptocurrency exchange we should use to buy a given amount of Bitcoin to minimise the amount of USD or USDT we'll spend on this trade.

Example API call (for 1 BTC):

```
curl http://localhost:4000/exchange-routing?amount=1
```

Example API response (if Coinbase price of \$10,000 / BTC is the cheapest):

```
{
  "btcAmount": 1,
  "usdAmount": 10000,
  "exchange": "coinbase"
}
```

2. You'll need to compare Binance and Coinbase Prime order books and compute the best execution price for the given amount of Bitcoin we want to buy. (You can assume that 1 USDT = 1 USD at all time.)
3. [Bonus] Add a third exchange to compare with Binance and Coinbase Prime.

Feel free to structure the code however you prefer and use third-party libraries at your discretion.

### API Information & Documentation

- **Crypto Trading 101: How to Read an Exchange Order Book:** https://www.coindesk.com/crypto-trading-101-how-to-read-an-exchange-order-book
- **Binance API Documentation:** https://github.com/binance-exchange/binance-official-api-docs/blob/master/rest-api.md
- **Coinbase Prime API Documentation:** https://docs.cloud.coinbase.com/exchange/reference/exchangerestapi_getproductbook

### Explanation of the problem statement

The goal of the exercise is for the developer to fetch order books from all exchanges that they decide to integrate, iterate through each `ask` and find the lowest price that will facillitate the desired quantity of bitcoin to be purchased.

For example the order book from Coinbase for BTC-USD looks like this (truncated for brevity). The URL is https://api-public.sandbox.exchange.coinbase.com/products/BTC-USD/book?level=3

```json
{
   "bids":[
      [
         "39786.52",
         "0.01",
         "0bf6df12-4e53-40ea-81f8-ba3c5a67d7f6"
      ],
      [
         "39554.1",
         "0.00505",
         "0e4541b3-0850-4c8e-b974-b56bc91fa909"
      ],
      [
         "39447.3",
         "0.002",
         "2b583b5c-37cb-4520-80ce-76735589c6b7"
      ]
   ],
   "asks":[
      [
         "47520",
         "2.15537023",
         "738b9f96-f6b4-4095-9bb4-1d60eafe1371"
      ],
      [
         "47729.09",
         "0.000016",
         "ce1bd354-0ee0-438c-9928-3962aa638ce4"
      ],
      [
         "47781.36",
         "0.01077963",
         "50c2915c-670b-4c94-8c16-fc676dcbf454"
      ]
   ],
   "sequence":497720974,
   "auction_mode":false,
   "auction":null
}

```

In this response Coinbase is telling us that there are 3 offers of BTC for sale:
1. `2.15537023 BTC` is for sale at `$47520`
2. `0.000016 BTC` is for sale at `$47729.09`
3. `0.01077963 BTC` is for sale at `$47781.36`

Similarly the the order book from Binance for BTC-USD looks like this (truncated for brevity). The URL is https://api.binance.com/api/v3/depth?symbol=BTCUSDT
```json
{
  "lastUpdateId":16940096293,
  "bids":[
     [
        "43928.76000000",
        "0.33568000"
     ],
     [
        "43927.00000000",
        "0.02000000"
     ],
     [
        "43926.71000000",
        "0.00341000"
     ]
  ],
  "asks":[
     [
        "43928.77000000",
        "0.52573000"
     ],
     [
        "43928.78000000",
        "0.01706000"
     ],
     [
        "43928.93000000",
        "0.06714000"
     ]
  ]
}
```

In this response Binance is telling us that there are 3 offers of BTC for sale:
1. `0.52573000 BTC` is for sale at `$43928.77000000`
2. `0.01706000 BTC` is for sale at `$43928.78000000`
3. `0.06714000 BTC` is for sale at `$43928.93000000`

## Correctness

The goal of this challenge is to iterate through the `asks` for each exchange and find the lowest price that satisfies the purchase of the `amount` of BTC specified in the request.

For example if we wished to purchase `0.5 BTC` then the lowest price would be from Binance at `$43928.77` since there is an offer to sell `0.52573000 BTC` at that price. However if we wished to purchase `1 BTC` then the lowest price would be `$47520` from Coinbase since Binance cannot fulfill an order of 1BTC on the order book above.

## Databases

For the databases portion of the test, create a `/databases` folder.

Let's say you have two SQL tables: `users` and `transactions`.

The `users` dataset has 1M+ rows; here are the first three:
| id | email | country |
|--------|----------------------|-----|
| user_1 | user1@getsafepay.com | FRA |
| user_2 | user2@getsafepay.com | GBR |
| user_3 | user3@getsafepay.com | USA |

The `transactions` dataset has 1M+ rows; here are the first three:
| id | quote_currency | usd_amount | user_id |
|---------------|----------------|------------|---------|
| transaction_1 | btc | 100 | user_3 |
| transaction_2 | btc | 2000 | user_2 |
| transaction_3 | eth | 50 | user_1 |

1. Create a SQL query that shows the TOP 3 customers who spent the most.
2. Write an SQL query to find out how many users spent more than $1,000 but less than $2,000.
3. Print every country where the average lifetime spending per user is lower than \$500.


## Submitting Your Code

Once you've completed the test, please compress your files (via zip or tar) and
return them as a link or email attachment in reply to your test invite. We'd like the
code in your submission to remain private, so please avoid committing or pushing
the code publicly.

Once we receive it, a member of our team will review and we'll get back to you
as soon as possible.

Thanks!
