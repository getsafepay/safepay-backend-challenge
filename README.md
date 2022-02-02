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
- **Coinbase Prime API Documentation:** https://docs.prime.coinbase.com/

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
