# Bank-Marketing-Campaign

### Table of content
- [Project overview](#Project-overview)
- [Data sources](#Data-sources)
- [Tools](#Tools)
- [Data cleaning](#Data-cleaning)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Insights](#Insights) 
- [Recommendations](#Recommendations)

### Project overview
This dataset captures the outcomes of direct marketing campaigns conducted by a Portuguese banking institution. it is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict if the client will subscribe a term deposit (variable y). This is to find the best strategy to improve for the next marketing campaign .

### Data sources

### Tools
- excel
- python
- pandas
- matplotlib
- plotly express
-  Numpy
- seaborn

### Data cleaning
- Missing value
- Duplicate

### Exploratory Data Analysis
1. Which customers with Customer Demographics "age, job, marital and education" show the highest subscription "y"? 
2. How do financial attributes—such as average yearly balance, housing loans, or personal loans—correlate with a client's willingness to open a term deposit?
3. Do customers with existing credit defaults show significantly lower subscription rates?
4. What percentage of customers actually subscribed (yes vs. no), and how severe is the class imbalance?
5. Which communication channel works best? Does cellular contact yield higher conversion rates than telephone or unknown methods?
6. Which months or days of the month has the highest subscription rates?
7. How does the number of contacts (campaign) during the current drive affect client fatigue and refusal rates?
8. How does the duration of a phone call correlate with the term deposit subscription rate (y)?
9. Does the recency of communication impact a customer's willingness to subscribe?
10. Does higher historical familiarity with the bank increase conversion, or does it cause customer fatigue?
11. How does the conversion rate (percentage of 'yes' outcomes in the y column) change incrementally with each additional contact attempt recorded in the campaign column?"
12. How predictive is past customer behavior on current campaign success?

### Insights 

| **Demographics** |
| --- |
| **Age:** How old the customer is? |
|**Job:** The type of work they do |
|**Marital:** Their relationship status|
|**Education:** Their highest school level|

1. High-Volume vs. High-Conversion Groups: Clients working in management and blue-collar roles often make up the largest raw volume of contacts, but retired individuals and students consistently show higher relative conversion rates (propensity to subscribe to term deposits) despite smaller overall sample sizes.
2. Marital Impact: Married clients dominate the dataset (roughly 57%), representing the largest target block for fixed savings products, whereas single and divorced clients exhibit different risk and liquidity preferences. 
3. Education Correlation: Clients with secondary and tertiary education levels engage more reliably with long-term investment pitches, whereas primary or unknown education tiers correlate with lower or less predictable response rates.

<img width="900" height="400" alt="Customer Demographics" src="https://github.com/user-attachments/assets/e57b89ff-ded1-4bbb-b079-998be526c530" />

| **Financial History** |
| --- |
| **Default:** Do they already have a credit account that is in default (unpaid bills)? (yes/no). |
| **Housing:** Do they have a housing loan or mortgage with the bank? (yes/no). |
| **Loan:** Do they have a personal loan? (yes/no). |
| **Balance:** Average yearly account balance in Euros (numeric) |

1. Negative Balance Impact: Clients with credit in default (default=yes) rarely subscribe to term deposits.
2. Existing Debt Effect: Customers with active housing loans (housing=yes) are often less likely to lock funds into term deposits compared to non-borrowers.
3. Liquidity Correlation: Higher average yearly balance strongly correlates with a higher positive conversion rate for long-term investments.

<img width="800" height="600" alt="Financial History" src="https://github.com/user-attachments/assets/a4370ebd-f14e-4eb3-ac0a-4baebb69caf5" />

| **Campaign & Contact Details** |
| --- |
| **Contact, day, and month:** Capture the communication channel. How the bank reached them (cellular or telephone) and the specific date/month of the last contact. |
| **Duration:** Last contact duration in seconds. It heavily impacts the target variable but is unknown before a call, so it is often excluded for realistic modeling. |
| **Campaign:** Number of contacts performed during the current campaign. |
| **Pdays and previous:** Track the days since the last contact from a previous campaign and the total number of prior contacts, where -1 or 999 indicates no previous contact. |
| **Poutcome:** Outcome of the prior marketing campaign. What happened during the last campaign? (success, failure, other, unknown). |

1. Communication Channel Effectiveness: Unknown contact methods are highly inefficient, resulting in a 95% unsubscribe rate and only a 5% conversion rate. In contrast, direct outreach via telephone leads with a 15% subscription rate, closely followed by cellular at 14%.
2. Monthly Seasonality: December and March are peak months for conversions, yielding exceptional subscription rates of 45% and 42% respectively. Conversely, May is the worst-performing month, dragging success down to its lowest point of 6.7%.
3. Day-of-Month Timing: Timing within the month matters significantly. The 2nd and 10th days experience the highest conversion spikes at 37% and 28%. Marketing efficiency drops drastically toward the end of the month, hitting rock bottom on the 20th (5.8%) and 29th (5.7%).

<img width="800" height="800" alt="Campaign   Contact" src="https://github.com/user-attachments/assets/de688fe1-6e7a-401b-a7d2-4ca686d43b12" />

### Fatigue and Familiarity

1. Client Fatigue: Conversion Decay by Current Campaign Volume (campaign)- The variable campaign tracks the total number of contacts performed during the current marketing wave for a specific client. The data shows a strict diminishing marginal return that quickly devolves into severe client friction. 
 2. The Familiarity Effect: Conversion Rate by Historical Touchpoints (previous)
In stark contrast to current campaign volume, the variable previous (the number of contacts performed before the current campaign) reveals a positive correlation with success.
3. Historical Interactions (previous) - Prioritize warm leads. Filter dialing queues to prioritize clients who responded positively or engaged meaningfully in past quarters.

<img width="800" height="800" alt="Familiarity   fatig" src="https://github.com/user-attachments/assets/16b663ae-90ec-403f-9c1d-826fe1be919b" />

### Combating Class Imbalance

- The target variable y is heavily imbalanced, with only about 12% of clients subscription rate, a naive model could achieve 88% accuracy just by guessing "no" every time. 

<img width="948" height="500" alt="Imbalance" src="https://github.com/user-attachments/assets/4f42d29e-334d-412b-8d69-8dc8375f1614" />

### Recommendations

1. Target Previous Successes: Prioritize clients with a poutcome of "success" from past campaigns and recent prior contacts (pdays/previous) strongly signal a higher likelihood of subscription.
Conversion rates spike significantly for individuals who previously engaged.
2. Focus on Retirees and Students: Segment by job type; retirees and students show higher relative subscription rates to term deposits than blue-collar workers.
3. Clean the Contact Data: Stop wasting resources on "unknown" channels. Prioritize data-cleaning campaigns to capture valid cell phone or telephone numbers before launching a marketing push.
4. Shift Campaign Budgets: Allocate a larger portion of your annual marketing budget and agent hours to March and December. Scale back aggressive outbound calling in May, or use that month to test alternative, lower-cost digital offers.
5. Optimize Call Scheduling: Front-load your calling queues. Focus heavy sales pushes during the first half of the month—specifically targeting dates around the 2nd and 10th—and avoid aggressive outreach on the 20th and 29th when client receptiveness is lowest.
6. Engagement & Fatigue: Longer call durations correlate with higher conversions, whereas over-contacting within the same campaign (campaign) causes customer fatigue and lowers success rates.

