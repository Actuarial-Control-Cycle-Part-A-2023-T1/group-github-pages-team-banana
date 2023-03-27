# ACTL4001 Project - SOA Research Relocation Social Insurance Case Study

## Executive Summary
This report details the structure and implementation on the social insurance program designed to help the citizens of Storslysia. Due to climate-related catastrophes, individuals from Storslysia are prone to involuntary displacement, as well as voluntary relocation. This report highlights the strategies behind managing exposure to displacement risk financially due to climate-related events. 

This report outlines the main objectives of the social insurance program, the program design with key features, and the pricing costs to fund the mitigation of displacement risk. More specifically, a gradient boosting model XGBoost in conjunction with a gamma regression objective link is used to model likelihood of claims from the highly volatile hazard data and hazard events. This program ensures the key criterias are met: 
- Reducing Storslysia’s financial commitments from climate catastrophe-related displacement
- Prevent costs of relocation from exceed 10% of Storslysia’s GDP each year
- Coverage of all Storslysia’s population

Assumptions used in our financial modeling are listed in the report, along with the risks and risk mitigation strategies for the implementation of the social insurance program. Finally, data used and limitations in the data is stated in the final section of the report. 

## Objectives
The residents of Storslysia are threatened by the impact of the climate-related catastrophes and are becoming more exposed to displacement risks that arise from these perils. As a consulting firm, we have been hired to design a social insurance program, with the objective to mitigate negative financial impacts of the displacement and relocation on the Storslysia residents that have been adversely impacted by the catastrophes. 

The designed program aims to help manage the exposure to displacement risks.This is achieved through incentivising residents of Storlysia to move out of the high catastrophe areas as well as helping them resettle into new locations. Taking into account the diverse geographic regions and demographics of Strorslysia, the designed program aims to provide benefits to the affected victims which vary based on their current geographic risk. Relocation out of high risk areas helps reduce disaster risk and property claims costs, therefore a program that encourages such displacement will greatly reduce natural perils related claims and serve as a risk mitigation method that can help minimize exposure. With those that are unfortunately affected, the program still aims to help maintain the victim’s quality of life by assisting in their relocation by considering several factors such as the victim’s socio-economic background.

The program will reduce Storlysia’s cost arising from climate catastrophe and prevent arising costs from both voluntary and involuntary displacement from exceeding 10% of Stroslysia’s gross domestic product (GDP). As a social insurance program, the entirety of Storyslysia is taken into consideration and covered. 

### Monitoring and Key metrics
In order to make sure our program has been designed appropriately we will monitor the performance that has been achieved on a quarterly basis. We will review and monitor the social insurance program’s success using the following metrics: 
| Metric | Review |
| --- | ----------- |
|Claims frequency | A reduction in claims frequency from the last reporting date relative to the catastrophic events that has occurred. As the program aims to incentivise the relocation to safer regions, the program should decrease the amounts of claims due to more participants being in areas of lower geographic risk in future periods - if this is not achieved a re-evaluation should be done.|
|Average cost per claim (severity) | Decrease in claims severity as people relocate to safer areas, supported by the program’s scheme. Similar to claims frequency, a re-evaluation is required if a downward trend is not observed.|
|Loss Ratio |With a reduction in claims costs, the loss ratio would give a good indication of how our product is performing and give insight into the profitability of the scheme which is a useful metric to convey to stakeholders. <br/> <br/> In order to ensure that the program is meeting the current financial and profit margins, a re-evaluation of the program will need to be performed quarterly to ensure that a downward loss-ratio trend is achieved. |
|Satisfaction rate | Although the scheme is designed to cover all Storlysia’s residents, the satisfaction of policy holders can indicate how the program is faring and whether it is in fact benefiting the residents as intended.|

## Program Design
The requirements that must be satisfied for a citizen of Storslysia to file a claim under the program are listed below: 

- Address of current location and new location are required. Individual’s filing a claim are required to relocate from a higher to lower risk region. 
- Total property damage costs that arise from voluntary relocation must exceed the median value of owner-occupied housing units in the respective region in order to be eligible for a claim.
- Total property damage costs that arise from involuntary relocation must exceed Ꝕ500,000 in order to be eligible for a claim. 
- Medical reports and test results may be requested as supporting documents in the case of psychological claims.

The design of this social insurance program incentivises the individuals of Storslysia to relocate to areas of lower risk and covers the losses resulting from displacement. It addresses both voluntary and involuntary relocation as a result of a catastrophic event. Relocation tends to include expenses such as building accommodation, replacing lost household items, and addressing psychological challenges that may arise after the event. With these factors in mind, the designed program will aim to help the victims resettle. 

The cost of coverage for voluntary relocation is lower than that of involuntary displacement, which includes expenses such as building accommodation, replacing lost household items, and addressing psychological challenges that may arise after the event. To reduce these costs to a high degree of certainty, efforts must be made to ensure that the costs of both voluntary and involuntary relocation do not exceed 10% of Storslysia's GDP per year. It is essential to provide complete coverage to Storslysia to ensure that everyone affected by the catastrophe is protected and assisted in their relocation.

In the event of a claim, the following is under coverage from this program:

- Finding accommodation 
- Building accommodation 
- Replacing damaged household items
- Replacing lost household items
- Managing psychological challenges associated with the climate catastrophe causing relocation, including but not limited to trauma, mental illness and stress

### Key program features
- In the case of voluntary relocation, a discount is given due to the smaller cost associated with finding and building accommodation, and replacing lost/damaged household items.
- In the case of involuntary relocation, no discount is given, due to the circumstances of the program covering costs associated with damaged household and items, along with finding and building accommodation.

## Pricing/ Cost

### Modelling Claims

To price and find the cost of our program, we first look to model the probability of a claim as well as the amount claimed using historical hazard data given. Due to the high variability of the historical data and hazard event, we have decided to use a gradient boosting model, XGBoost with a gamma regression objective link. 

We split the historical data into 70% training data and 30% testing data, and created the XGBoost model and predicted results using the testing data. The results of the predicted and actual density of results are presented below:
<p align="center">
<img src="https://user-images.githubusercontent.com/87253028/227770798-9bfa73e1-37f7-4f93-bc4a-5e2d8646ed36.png"> 
</p>

The XGBoost model is a good fit when predicting the likelihood for a claim, as the predicted and actual curves are relatively close to one another.

Also the summary of model features are presented to the right, showing the significance of each feature to the model.

<p align="center">
<img src="https://user-images.githubusercontent.com/87253028/227771015-c7c4a3e2-e8f3-466b-8e16-83b2c41321f1.png"> 
</p>

### Test Mean-Squared Error

Running the model - get a really high mse due to the variability of the hazard event and claim magnitude, thus the high mse is reasonable for our case as claim amounts fluctuate between high numbers.

### Results of XGBoost Model (with projected data)

#### Test Mean-Squared Error
The MSE that the model produced for the test dataset came in at around twenty million, which gave more consistent and accurate results after hyper-tuning the parameters of our XGBoosting model using a grid search. Given the high variability of the hazard and claims (fluctuating in the millions) the test MSE for the model is acceptable.

#### Modeling Relocation
For the modeling of relocation we made multiple assumptions (Appendix A) regarding voluntary and involuntary relocation between the regions. We ranked regions based on their risk exposure, coming to the conclusion that regions 2 and 5 are more prone to catastrophic events in comparison to the rest. 

To determine the probability of which individuals relocate, we used available information (hazard rate, population density, risk exposure and housing costs coupled with our stated assumptions) to create two transition matrices for voluntary and involuntary relocations (Appendix B).

Using the transition matrices and projecting its respective transition probabilities on the  population data multiplied by the expected relocation, we can determine the population of each region on a year to year basis. To generate the 10 year projection, we ran our projection function 10 times using the previous years data to obtain the new set of population.

## Pricing/Program Cost

We priced the cost on a 10 year time horizon. Our costs include the average claims cost per year and the relocation costs, both voluntary and involuntary, that are covered under our program. 
The average claims cost is calculated using 
$$Claims Cost = Severity * Frequency$$

<p align="center">
<img src="https://user-images.githubusercontent.com/87253028/227992094-4f5e69b3-107a-4f95-83ea-159278d0dcdf.png"> 
</p>

The graph above shows the claims cost for property damage in the six different regions. It can be observed that region two has the most claims for property damage, while the rest of the regions are similar.

Relocation costs will be considered through the population movement between each region. Using the median transportation and relocation costs given in the ED data, we are able to calculate the involuntary and voluntary displacement costs to a high degree of certainty. By taking a weighted average of the displacement costs we are able to come up with the expected relocation expense that would be paid per year. 

The total price of the program will therefore be the average claims cost per year plus the relocation costs. In order to maintain the total costs to remain under 10% of the projected GDP, we adjust the percent covered in each of the relocation schemes. We also aim to monitor the pricing to ensure that this goal is achieved.

Under current models we have projected to cover 5% of involuntary displacements and a 10% coverage of the difference in geographic risk from relocation for voluntary relocation.

We then projected the population per region using a mean growth rate calculated from the years 2019-21. The next step was to find the mean value for a property within each of the regions using the property value distribution data provided, and the results are as follows:
- Regions: (1) 359827.5 (2) 313217.5 (3) 302862.5 (4) 187360.0 (5) 206862.5 (6) 247597.5

To find the total expected insured amount, we must consider the value of household goods, accommodation costs, psychological costs and relocation costs as per program criteria.

- Household goods values are approximated at 5% of expected property value.
- Accommodation is approximated at 0.1% of expected property value and is expected to last 3 weeks.
- Psychological is approximated at 0.075% of expected property value and is expected to last 5 weeks.

Summing these variables up gives us a pre-inflation, expected number for insured amount per individual which we used to cross check our claim cost model.

- Insured per individual per region: (1) 20420.21 (2) 17775.09 (3) 17187.45 (4) 10632.68 (5) 11739.45 (6) 14051.16

Refer to appendix 3.1 for post adjusted inflation values.

## Assumptions
| Variable | Assumption |
| --- | ----------- | 
|Inflation | A moving average of order 5 was used to forecast inflation.|
|Involuntary Displacement |If property damage is greater than 500000, then it is considered to be involuntary displacement.|
|Voluntary Displacement |If property damage is greater than the median house price in the respective region, then it is considered to be voluntary displacement.|
|Population|Mean growth rate from the years 2019-2021 is used to explain and project future population trends.|
|Property value|Distribution consisted of categories/brackets for property values. An average of the category’s bounds were taken to result in a singular number to be used in expected value calculation.|
|Household goods value| Predicted to be 5% of property value.|
|Accommodation value|Accommodation for individuals making claims is provided. The value is based on property value to replicate quality of life, resulting in 0.1% of property value. Provided accommodation is expected to last 3 weeks.|
|Psychological impacts|Expected to last 5 weeks, and reflected as 0.075% of expected property value.|
|Hazard event|Hazard events occur uniformly through each region, affecting the whole region, not partially.|
|Exchange rate|US$ to Ꝕ is 1.321 (1 US$ = 1.321Ꝕ).|

## Risk Mitigation Considerations

The design of this social insurance program to cover the country of Storslysia from climate-related catastrophes due to the prevalence of climate change comes along with risks. In the sections below, quantitative and qualitative risks will be listed out, along with strategies and risk mitigation tactics. 

### Quantitative Risks
|Risk Category|Risk|Mitigation|
|:----|:----|:----|
|Financial|Pricing and insured amount of each individual. This includes cost of relocation, compensation due to displacement, and ongoing support for individuals post displacement and relocation. |Solvency & Coverage of all catastrophes|
|Actuarial|Inaccurate estimation regarding likelihood of catastrophic events, in which displacement and relocation is needed afterwards. |Frequency projection model of minor, medium and major events per year is used (based on historical data). This is used to determine the probability and likelihood of these climate and hazard events. |
|Actuarial |Inaccurate estimation for severity of catastrophic events.|Risk amplification factor is used to determine the change in atmosphere CO2. Allows for increased occurrence of climate change to be included in predictions. |

### Qualitative Risks
|Risk Category	|Risk|	Mitigation|
|:----|:----|:----|
|Social	|The potential for social unrest due to tensions from displacement of communities.| Alertness and campaigns can be raised to mitigate such social risks to bring light for the importance and benefits for this social insurance program. |
|Psychological | Trauma stress and mental health issues led from displacement and relocation for the community.|	An approximation for financial needs regarding psychological impacts have been made. It is approximated at 0.075% of the expected property value for each individual and insured sum is expected to be use to treat trauma stress and mental health problems for the following 5 weeks post relocation and displacement. |
|Political|	Potential backlash criticism from political standpoint causing lack of support and underfunding for this program.|Non-financial matters including political support is managed by another task force, and financial funding is managed under the Chief Actuary of Storslysia’s insurance regulator.|

<p align="center">
<img src="https://user-images.githubusercontent.com/87253028/227772527-ecdbbd90-5eb2-4927-85f5-a3c7c0e1997b.png"> 
</p>

1: Financial - Risk of pricing and sum insured for individual being too large
<br/>
2: Actuarial - Inaccurate estimation of likelihood for climate-related catastrophic event
<br/>
3: Actuarial - Inaccurate estimation of severity for climate-related catastrophic event
<br/>
4: Social - Potential for social unrest from displacement
<br/>
5: Psychological - Trauma, stress and mental health issues from displacement and relocation
<br/>
6: Political - Backlash, criticism from political standpoint, lack of support and underfunding


## Data and Data Limitation

### Hazard data
Hazard data shows historical hazard events and reflects the region the event takes place, duration, fatalities and its property damage.
The limitations of hazard event data:
- Limited location, as the data splits the country into six regions we are not able to accurately map the hazard event to a specific place, as we have to assume the whole region would experience the disaster.
- Limited variables, the data provided does not give us the full image of the disaster as it lacks important features like economic impact, psychological impact etc to allow us to have a full understanding of the impact of these hazard events.
- The data is limited to only providing us with the hazard event, and no contextual information about the event. Hence, there are inconsistencies in the data where for the same region and same hazard event we might observe very different property damage, which can hinder the training of our machine learning model.

### Economic and demographic (ED) data
ED data comprises various features based on region. Our program considers the following features:  
- Census as of July 1 for the years 2019-21,
- GDP for the years 2019-20,
- Person per household for 2016-20,
- Temporary housing cost with disaster (per person per month), and
- Property value distribution data.

### The limitations of ED data:
- Census data only available for the years 2019-2021. This presents difficulty in projecting trends in population growth over the next few years as there are limited data points. Impossible to discover if changes in population follow a trend or are one-off occurrences.
- Property value distribution data provides categorical values. In addition, the bracket values are inconsistent for each category. This presents the issue of how accurate we can predict the expected property value per region as assumptions will be needed.


### Inflation and interest (II) data
The limitations of II data:
- There was a lack of historical data that explained the inflation variable, and thus a less accurate but more simple approach of forecasting was considered. 
- In 2003, inflation was recorded at -990%.
- The outlier in 2003 was not included in the moving average when forecasting inflation. A simple moving average of order 5 was used to simplify inflation forecasting. The government overnight bank lending rate, 1-year and 10-year risk free rates were not used in the projection of inflation as they are not good predictors of inflation. 
- Missing data entry for government overnight bank lending rate in 1987.
- Missing data entry for 1-year risk rate in 2018.





