# Zapier tech assessment

## Q1 - On-Premis Postgres
## Question:
```
Is there an integration with Postgres? We have an on-premises database that I need to pull data from on a regular basis and use it to post a weekly summary to Slack.  How would I go about doing that?
```
## Answer:
Hello, thank you for reaching out regarding your Postgres database connection. Zapier does offer a connection to Postgres as a database, either on-prem or cloud-hosted, as long as you can connect to the database using a standard connection protocol.

You can find details on how to make the connection [here](https://help.zapier.com/hc/en-us/articles/8495937482253-How-to-Get-Started-with-PostgreSQL) and a quick primer on how to connect it to Slack [here](https://zapier.com/apps/postgresql/integrations/slack). 

So that you know, you must upgrade your plan to allow access to Zapier's static IP addresses to connect to your DB. You can test this in a trial of the Zapier Pro Plan, however, so there's no need for a commitment upfront. If you see the error `AppVersions using SQL Zero require static-ip pool types` when you attempt to connect to your database, it is because the static IP address is required, and you'll need the pro plan.

The query you use might be something like:
```SQL
SELECT
    COUNT(*) AS total_orders,
    COALESCE(SUM(order_amount), 0) AS total_order_value
FROM orders
WHERE order_date >= NOW() - INTERVAL '7 days';
```
By default, Zapier polls for new information on a 15-minute interval. If you're only looking to have this data sent to Slack once a week, you can schedule that message in the Slack configuration in the `Schedule At` input box.
![[Pasted image 20241227111439.png]]

When this Zap runs, you will see output to your selected slack recipients (channels or individual users), and it will look something like this:
![[Pasted image 20241227111802.png]]
Of course, you can customize the data in the Slack report according to your needs and the content of the data returned in your custom query. 

Thank you so much for reaching out to us! If you have any further questions, we would love to help. Please feel free to send over any other further questions you may have. 

Thank you,

Jonathan Mucha.
