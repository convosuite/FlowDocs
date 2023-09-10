# Custom Tool



## Problem

Function usually takes in structured input data. Let's say you want the LLM to be able to call Airtable Create Record [API](https://airtable.com/developers/web/api/create-records), the body parameters has to be structured in a specific way.&#x20;

Let's say you want the LLM to be able to call Slack or Teams to collect leads from customer support chatbot.&#x20;



## Use case

**Goal**: Have the agent automatically get the stock price movement, retrieve related stock news, and add a new record to Airtable.

Goal: Let the customer support chatbot ask the leads for them name , email, phone number and send to slack or Teams App or salesforce.



<figure><img src="../.gitbook/assets/collect leads.gif" alt=""><figcaption><p>A customer support chatbot asks visitors for their contact details and sends the information to Slack using the OpenAI call function</p></figcaption></figure>









Custom Tools example:

## ![](<../.gitbook/assets/image (50).png>)

<figure><img src="../.gitbook/assets/image (3) (3) (1).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:blue;">What are the latest news about this stock that might cause the price movement?</mark>_

_<mark style="color:orange;">Here are the latest news about Overstock.com (OSTK) that might have caused the price movement:</mark>_

1. _<mark style="color:orange;">Title: "Overstock's shares soar on successful 21.5 million bid for Bed Bath & Beyond assets" Source: MarketWatch Published Date: June 22, 2023 Summary: Overstock.com's shares experienced a significant increase after successfully winning a bid for Bed Bath & Beyond assets worth 21.5 million.</mark>_
2. _<mark style="color:orange;">Title: "Thinking about trading options or stock in Meta Platforms, Overstock.com, Walmart, Home Depot, or United Parcel Service?" Source: PR Newswire Published Date: June 22, 2023 Summary: This news article discusses the potential trading options and stocks, including Overstock.com, that investors may consider.</mark>_

_<mark style="color:orange;">Please note that these news articles are for informational purposes only and may not be the sole reason for the price movement. It is always recommended to conduct thorough research and analysis before making any investment decisions.</mark>_

Lastly, you can ask ChatGPT to add a new record to Airtable:

_<mark style="color:blue;">Can you add a record to Airtable with the stock ticker, price move and news summary?</mark>_

_<mark style="color:orange;">I have added a record to Airtable with the following details:</mark>_

_<mark style="color:orange;">Stock Ticker: OSTK Price Move: 17.47% News Summary: Overstock.com's shares experienced a significant increase after successfully winning a bid for Bed Bath & Beyond assets worth $21.5 million.</mark>_

You can create your own custom tool and use it with the OpenAI Function Agent!





####

