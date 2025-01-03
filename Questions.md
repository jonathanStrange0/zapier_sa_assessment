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

If you have a table of orders for an e-commerce business, and you wanted a summary of the past week's orders, the query you use might be something like:

```SQL
SELECT
    COUNT(*) AS total_orders,
    COALESCE(SUM(order_amount), 0) AS total_order_value
FROM orders
WHERE order_date >= NOW() - INTERVAL '7 days';
```

By default, Zapier polls for new information at a 15-minute interval. If you only want this data sent to Slack once a week, you can schedule that message in the Slack configuration in the `Schedule At` input box.

![schedule_at](https://github.com/jonathanStrange0/zapier_sa_assessment/blob/main/schedule_at.png)

When this Zap runs, you will see output to your selected slack recipients (channels or individual users), and it will look something like this:

![report](https://github.com/jonathanStrange0/zapier_sa_assessment/blob/main/zap_report.png)

Of course, you can customize the data in the Slack report according to your needs and the content of the data returned in your custom query. More details on how to customize the look of slack messages can be found [here](https://help.zapier.com/hc/en-us/articles/8496025607181-Tips-for-formatting-Slack-messages#text-0-0).

This should get you started automating a report from your Postgres database and delivering that report via Slack. Thank you so much for reaching out to us! If you have any further questions, we would love to help. Please feel free to reply to this email with any other questions you may have. 

Thank you,

Jonathan Mucha.

## Question 2:  **Customization Request**
```
Unless Zapier can come with the ability to run code steps on my own infrastructure, it looks like we may have to take our business elsewhere. What can you do to make this happen?
```

## Author's Notes (not part of the email):
This customer is not the friendliest or happiest. The order in which I make the following suggestions would depend on the previous context with this particular customer. For instance, if we had already had conversations about their security requirements and ruled out the Code by Zapier route, I wouldn't suggest it here. I may also ask some questions to clarify the situation's requirements if there is no history of interaction with them.

## Answer:
Hello! Thank you for reaching out. I understand that running custom code on your infra is essential to your desired workflows. While Zapier cannot currently run completely on-prem for our clients, you can run custom code in several ways in your Zaps. Here are a few suggestions in order of level of complexity and effort:

### 1. Use Code by Zapier
Zapier does offer a workflow step that allows you to run custom code, complete with an AI assistant, to speed up the process. This works well for custom data transformations, string manipulations, or API requests. 

Code by Zapier is best suited for small scripts with limited dependencies and runtime requirements rather than large-scale custom app logic.

You can find some more information on Code by Zapier [here](https://zapier.com/blog/code-by-zapier-guide/)

---
### 2. Serverless Functions in the Cloud
If you have more complicated logic you would like to implement, you could use a serverless function like AWS Lambda that is accessible using the [webhook](https://help.zapier.com/hc/en-us/articles/8496083355661-How-to-get-started-with-Webhooks-by-Zapier) or [HTTP](https://help.zapier.com/hc/en-us/articles/12899607716493-Set-up-an-API-Request-action#h_01JD2EG7QP773YVQ8D371878BJ) Zap actions to send a request to your function for data processing. 

Serverless functions are a good option if you anticipate high request volumes through this Zap as they scale well. However, it is essential to remember that you will have to manage this environment outside of Zapier and be responsible for managing the security around these functions as well. 

---
### 3. Build a Webhook Interface for Your Existing Code
If you already have code you would like to access, another way to connect your Zap to this code would be to build a webhook interface in front of the code in question and allow the Zap access through the webhook or HTTP actions mentioned above. 

This approach gives you the ultimate flexibility to run your code on your servers. It is possible to set up a robust workflow here, even if processing the data sent by Zapier takes a while. The output of your function(s), if there is any, can be pushed back to Zapier with an incoming webhook trigger if you need it. More information on triggering Zaps from a webhook can be found [here](https://help.zapier.com/hc/en-us/articles/8496288690317-Trigger-Zaps-from-webhooks). 

---
### 4. Build a Custom Zapier App Integration
The [Zapier developer platform](https://docs.zapier.com/platform/home) allows businesses to build custom integrations into Zapier to allow access to their apps. These app integrations can be public or private, and you can define the authentication, triggers, searches, and actions a Zap may use to interact with your app. 

This approach allows you to tailor the app integration as needed and build multi-step logic inside your Zap where necessary. Of course, you will also need to become familiar with the developer platform if you are not already, and it may be overkill for what you are trying to accomplish.

--- 

Given the number of ways to achieve your goal and the potentially tricky integration here, I would love to discuss your options and intended outcomes. Please let me know your availability to discuss your challenges, and I'll schedule a call.

I hope you have a great week! I look forward to speaking with you soon.

Thank you so much for reaching out,

Jonathan Mucha.

## Q3 - Team vs Enterprise

```
We have a handful of people within our company who want to create automations for their teams. Which plan is the better choice for me to present to management - Team or Enterprise?
```
## Author's Notes:
Again, context matters a lot here. If we know anything about the customer/prospect, my approach changes based on that. If this were a fresh contact from an unknown user, my approach would be as follows:

## Answer
Thank you for reaching out! This is a great question, and it can be challenging to recommend a plan without more insight into your specific needs. Generally, the decision between our Team and Enterprise plans hinges on factors such as how many teams will be using Zapier, the level of security you require, and the depth of user-permission controls needed.

Since you mentioned multiple teams are interested in automations, it might be beneficial to explore the Enterprise plan. Its advanced features—like enhanced admin permissions, greater observability, and a dedicated Technical Account Manager—often provide stronger oversight and support for organizations with diverse or growing needs.

However, before making a final recommendation, I’d love to connect with you and other relevant stakeholders. I’ll bring one of our Enterprise Account Executives into the conversation so we can cover any questions about pricing, features, and how each plan aligns with your goals. By the end of that discussion, we’ll have a clearer idea of which plan best fits.

Would you be available for a brief call next week? Please let me know a few times that might work for you and your team, and I’ll set it up.

In the meantime, a breakdown of the features for each plan can be found [here](https://zapier.com/app/planbuilder/pricing). This will help you understand the details of the differences between the plans and prepare for our call.

Thank you again for reaching out, and I look forward to speaking with you!

Jonathan Mucha.
    
