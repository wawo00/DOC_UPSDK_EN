
### Q: What should I do if there is no advertisement displayed correctly after embedding the SDK?

If you've set up an "placementid," please make sure you 've sent the correct placementid code to the technicist.

<br />


### Q: What advantages does UpLTV have over a single advertising platform , such as AdMob , Mobvista , Vungle, etc.?
 

1. UpLTV provides better ad fill rate and higher exhibition price ( eCPM ) than a single platform by integrating multiple ad resources. Usually, it will boost your monetization by 20 percent. 

2. UpLTV's one-stop access to multiple high-quality advertising platforms avoids the registration, docking and negotiation among multiple organizations. It makes the billing process simpler and the transfer faster.

3. Our professional technical support team and liquidation consultant team provide the 24/7 online support and even on-site service for key customers.


<br />
4.	我们更认为变现并不是简单的SDK对接，而是一种持续的服务。MaaS（Monetization as a Service） 。我们同样重视根据客户的游戏内容提供最佳的广告露出逻辑，这个更依赖于深度的机器学习和人工干预相结合的手段。

### Q: Why is UpLTV more efficient than other integration platforms such as YoMob , Heyzap , and Fyber ?
1. UPLTV has better loading strategies, traffic distribution and scheduling logic.

2. The goal of UPLTV is to optimize the life cycle value (LTV). It takes the short-term and long-term monetization into consideration and balances the monetization and retention.

3. UPLTV has a better back-end AI data analysis system and provides more room for improvement.

4. We believe that monetization should be an ongoing MaaS (Monetization as a Service) instead of a simple SDK docking. We also value the logic of providing the best advertising based on the customer's game content, which is more dependent on the combination of deep machine learning and manual intervention.
<br />

### Q: How long does it take to embed the SDK?

Based on our customer feedback, it takes only half a day to embed the SDK.

Please provide us with the test version after finishing the code embedding. We will promptly assist the test to confirm that the code embedding is correct.

When encountering, we are always providing 7/24 customized support for any problems occurred during the embedding process.

<br />


### Q: How can AI improve monetization based on integration? 

To further enhancing the efficiency of the monetization, the AI system analyzes each user's tolerance and conversion ratio for the ad and provides a fully personalized ad configuration for independent users, 


<br />

### Q: Can I check the benefits brought by each advertising platform in the background? 

There is no revenue data for each platform in the the background by default. However, if necessary, we can provide screenshots of the advertising platform individually, and at the monthly settlement, we can provide the accurate total revenue from each platform.

What we hope is to provide a whole set of optimization services instead of a tool. We hope that our AI can help developers pay attention the overall revenue, advertising ARPU, eCPM and LTV instead of any underlying details.


<br />

### Q: Can I choose to block ads from the competitors ?

For the advertising platform that supports blocking competing products, we can do it according to the developer's request.
<br />

### Q: Can I choose the certain type of advertisement, such as a rewarded video?

Of course, you can.
<br />

### Q: Can I check the data of rewarded video, interstitial, and banner separately?

Yes, you can.
<br />


### Q: Shall we re-embed the SDK after updating the game version?
No, you don’t have to.

However, we do recommend that you update the SDK to the latest version to ensure that you always have the best monetization efficiency.
<br />

### Q: Since the Chartboost has been embedded in the SDK , can you exchange the traffic?

It is not available temporarily. 

We use the advertising resources from Chartboost only as a general advertising platform.
<br />


### Q: What is the size of  the SDK currently? Is it related to the number of ad platforms integration?

The SDK size is less than 1M.
Its size depends on how many the third-party advertising platforms are integrated. Usually we recommend to choose three to five third-party advertising platforms, which increases the size to 2~3M.

<br />


### Q: If our game has embedded a single advertising platform such as vungle , unityads , and your SDK integrates the platform as well. Will there be any conflicts?

Usually there no conflicts. If there is a conflict, we will provide a customized solution.

Notes:

- We do not recommend re-integration among UPSDK and other third-party ad platforms, which may reduce revenue (repetitive ads).

- In addition, some third-party ad SDK might have compatibility problems.

Our recommendation is to take over the provisioning strategy directly from the UPSDK in the top-level logic .

If you are concerned about the decline in revenue due to our SDK, we can provide the corresponding claims protection clause in the contract.

<br />

### Q: How do you get priority to show the relatively high price Offer of advertising? Is it a real-time bid?

1.	UpLTV has integrated the data API for every third-party advertising platform, so that it can access to the product information such as the sub-national rate, click-through rate per hour filling rate etc..

2.  Then the more efficient advertising platform will come first through comprehensive calculations.

Currently, real-time bidding is not mainstream in the industry for mobile In-App advertising . We are still using a strategy-based collation.

But it is worth mentioning what we have done. 

- The data provided by the advertising platform will be revised according to our own statistics.

-  Full consideration is given to the impact of the ranking itself on prices and CTR, which is corrected by the model.

- Add additional scheduling strategies to capture short-term opportunities for short-term premium offers in some regions.

- Different federation and ad slot combinations are used based on the grouping pattern of user portraits.


<br />

### Q: Will your SDK be added to your own interactive advertising platform?

Already joined.

<br />

### Q: Can you set up the horizontal or vertical screen ads display?

Most ad networks support automatic adaptation of resources, and developers don't need to care about adaptation issues.

-  If the advertising system is poor due to poor adaptability of the horizontal and vertical screens of an advertising platform, it will be quickly reduced by our automatic algorithm.

-	If the revenue (LTV) is good enough, the developers do not need to care about whether the horizontal and vertical screens are adapted.
<br />

### Q: Is it enough to access your SDK and API only? Is it still necessary to access our own data platform for you to collect data?

No need.

 
Our SDK has built-in collection and reporting of ad-related events to help game developers optimize revenue. In addition to accessing the SDK, game developers do not need to open up the data platform for us.

However, in order to support the A/B Testing function of the advertisement , we may need to pass the information of “whether it is a paid user” or “whether it has passed the novice tutorial” to the game developer to help us optimize. Specific information has different options depending on the game.

In fact, we provide three levels of access services based on customer needs:

-  SDK - integrated into the game concurrent version, relatively junior docking, suitable for small CP, customers who have little or no experience in advertising cash.

- API - Need to pass a small amount of data through the interface (whether it is a paid user), large and medium-sized CP, full awareness of advertising.

- AI - Need to pass more in-game events through the interface (clearance, failure, resurrection, new records, etc.), deep cooperation customers, fully aware of the value of advertising cash.

All of the above are SDK-based and do not require a CP open data platform.

<br />


### Q: Can eCPM set a low price?

It’s not available.

In fact, we will use Floor eCPM to limit the price of third-party platforms to optimize overall revenue.
However, in order to improve the LTV, we will not provide the function of limiting eCPM .
<br />


### Q: To what extent can user tags be refined after API access?

There are three main dimensions of UPLTV's attention:

-  Willingness to pay

-  Retention viscosity

-  Active advertising


Our AI system will roughly group the high, medium and low groups based on the above three dimensions based on the user's events in the game. Then it will provide personalized advertising display strategies based on groupings.

<br />

### Q: How to avoid the tax generated by the payment ?

Our payment account is a Hong Kong company identity. And we will assist mainland developers to complete tax deductions (similar to Google and Facebook).
<br />

### Q: How do you distinguish between subscribers and non-paying users to targeted delivery group ?

Analyze user behavior and predict its potential payment probability (based on AI technology).
Grouping for willingness to pay. Under the premise of not affecting the retention of users , the upper limit of the number of daily viewing advertisements of low- paying users is increased .
<br />

### Q: Will accessing two CPs at the same time increase the package size?

When we connect with other platforms at the same time, the alliances we support together do not need to re-access. We need to access the alliances that we have but another aggregation does not need. It will not increase the size of the package.
<br />



### Q: What is the current price of eCPM in North America for words game?

- Android incentive video is about $8, Interstitial$5-6;

- iOS reward video $10, Interstitial 6-8.

Different types of products fluctuate greatly, the above data is for reference only.



