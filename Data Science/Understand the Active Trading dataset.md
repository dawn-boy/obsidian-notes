We have two datasets, 
## 1. `fear_greed_index.csv`
This dataset tells us about the emotional wind of the market on any given day from ==*1st Feb 2018* to *2nd May 2025*==

### Columns:
- `timestamp / date`: Tells us the date. This is the key column to merge this dataset with other datasets.
- `value` (0 - 100): The core metric
	- 0 - 24 (Extreme Fear)
	- 25 - 49 (Fear)
	- 50 (Neutral)
	- 51 - 74 (Greed)
	- 75 - 100 (Extreme Greed)
- `classification`: A human-readable label for the given score

# 2. `historical_data.csv`
This dataset is a log of all individual actions taken by traders. Its like a bank statement from a lots of trader accounts. This dataset contains data from ==*May of 2023* to *May of 2025*==

### Columns
- `Account`: An anonymized ID of the trader
- `Coin`: The asset they've traded
- `Execution Price`: The price they got per token
- `Size Tokens`: Number of tokens they've traded
- `Size USD`: The total price for the tokens
- `Timestamp IST`: The Date column. We'll use this to merge with other datasets
- `Start Position`: Tells us how many tokens of that specific coin a user held in their wallet immediately before that trade took place
- `Direction`: Describes the intent of the trade more specifically than `Side`
	- `Open long`: Entering a BUY position betting that the prices would rise
	- `Close Long`: Exiting a position thinking that the rising trend is over. ==Selling the Tokens==.
	- `Open Short`: Entering a SELL position betting that the prices would fall
	- `Close Short`: Exiting a position thinking the the dropping tread is over. ==Buying back the tokens.==
- `Closed PnL`: The Realized profit and loss. A value of `0` says a position is opened rather than closing
- `Transaction Hash`: The digital fingerprint acting as a proof that the transaction actually happened.
- `Order ID`: Internal system identifier
- `Crossed`: Tells us if the order was a "Maker" or a "Taker"
		Taker: We wanted the trade to happen immediately, so we accepted the current market price
		Maker: We set a specific price limit and waited for someone else to match it.
- `Fee`: Margin levied by the brokerage for the trade
- `Trade ID`: A unique identifier for that trade
- `Timestamp`: A raw unix timestamp that is very precise than `Timestamp IST`
***
## Pre-Processing our data
We have a common `date` field in both of our datasets, using which we'll merge them together.

But the `date` field is not properly formatted and not in `datetime` type as required. So here comes our preprocessing.

```python
import pandas as pd

historical_df = pd.read_csv("historical_data.csv")
sentimental_df = pd.read_csv("fear_greed_index.csv")

## Preprocessing
historical_df['datetime'] = pd.to_datetime(historical_df['Timestamp IST'], dayfirst=True)
historical_df['date'] = historical_df['datetime'].dt.floor("D")
sentimental_df['date'] = pd.to_datetime(sentimental_df['date'])

## Merging
merged_df = pd.merge(historical_df, sentimental_df[['date', 'classification', 'value']], on='date', how='left')

## Renaming
merged_df.rename(columns={'value': 'fear_greed_score', 'classification': 'sentiment_class'}, inplace=True)
print("Merged dataframes on 'date' column:")
print(merged_df.head())
```

***
# Testing our Hypothesis

Here we'll question a set of beliefs and trends and use mathematical evidence as our compass towards reaching the truth. Numbers and charts are our allies here, unless I screw up and pre-process the data bad. In that case, we're screwed.

## 1. Do Traders make significantly more money when they buy during ==*Extreme Fear*== compared to ==*Extreme Greed*==

There's this belief that the crowd is wrong. When the index is at 80+ (Extreme Greed), prices are likely peaking and so buying then is actually buying the top, which is bad.

When the index is <20 (Extreme Fear), prices are crashing, so buying then would mean catching the bottom, which could be very profitable later when the prices soar again.

Data Says,
![[Pasted image 20260102163940.png]]
Traders bought during *Fear market**  times experienced more *Average Profit* compared to other market sentiments.
One might think why *Extreme Fear* market would cash in more profits but this is expected as *Extreme Fear markets* has a high risk of further downside, often triggering fixed exits (Stops, risk rules, psychology).
But *Fear* market indicates that a temporary equilibrium has formed, so buying there has a higher probability of a near-term rise and relatively lower probability of a dip compared to *Extreme Fear* markets.

***So this proves a signal to make relatively more money with Fear markets than other market sentiments.***

## 2. 