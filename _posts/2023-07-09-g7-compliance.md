---
title: "Can predictive AI improve the efficacy of international organisations like the G7?"
image:
  path: /images/2023-07-10-g7-compliance/cover.png
  thumbnail: /images/2023-07-10-g7-compliance/thumbnail.png
excerpt: "For the G7 to succeed in its mission, it is critically important that member nations follow through with the commitments that they make. An interactive AI-based tool that determines the probability of each member nation meeting its commitments may improve the efficacy of the G7."
categories:
  - Development
  - Economy
  - International Cooperation
tags:
  - g7
  - canada
  - united states
  - france
  - european union
  - eu
  - united kingdom
  - uk
  - us
  - usa
  - germany
  - italy
  - japan
last_modified_at: 2023-07-09T13:12:00-05:00
---

# Key takeaways:

* Fewer than two thirds of commitments made by leaders at past G7 commitments have been met in full
* An interactive AI-based tool was built using data from commitments made at past G7 summits
* The tool determines the probability of each member nation meeting the commitments made at summits

During its almost 50-year existence, [the G7 has served as an international forum](https://en.wikipedia.org/wiki/G7) for promoting the liberal and democratic ideals championed by its members. To this effect, the organization has collectively made over six thousand commitments to tackle issues such as global development, climate change, health policy and financial regulation. Historically, however, only 62\% of these commitments have been met in full. For the G7 to succeed in its mission, it is critically important that member nations comply with the commitments that they themselves make.

For the first time, data on commitment outcomes collected by the G7 Research Group has made it possible to produce data-driven estimates of the probability that each member nation will fulfill commitments made at G7 summits.

# What is the tool?

[Past research](https://www.globalgovernanceproject.org/increasing-the-impact-of-the-g7-2/) has shown that the underlying factors behind whether G7 member nations will comply with commitments primarily relate to immutable properties such as the economic position of the country or past compliance with similar commitments. These factors cannot be leveraged to improve the probability of compliance as they cannot be changed. However, by building a model to predict compliance, it becomes possible to identify which member nations are the least likely to meet their G7 commitments – enabling resources to be leveraged to assist the member nation in fulfilling their obligations. This could improve the overall efficacy of the G7. 

![no-alignment]({{ '/images/2023-07-10-g7-compliance/tool1.png' | absolute_url }})

The [G7 Compliance Simulator](https://g7-utoronto.shinyapps.io/compliance-tool/) seeks to do exactly this. Interested parties can access the tool online and enter relevant information to identify which member nations may need assistance in meeting their G7 obligations.

![no-alignment]({{ '/images/2023-07-10-g7-compliance/tool2.png' | absolute_url }})

# How does it work?

Using each G7 members’ historic performance on 655 individual commitments (a total of 5,994 individual assessments) the impact of various summit and commitment characteristics were fitted to a binomial regression model.

This revealed that several key characteristics of summits and commitments, such as references to democracy or human rights, holding ministerial meetings before G7 summits, forming official G7 bodies in the relevant issue-area, and hosting the summit were associated with a significant increase in the probability of a given member nation complying with a specific G7 commitment.

![no-alignment]({{ '/images/2023-07-10-g7-compliance/summit.png' | absolute_url }})

Similarly, the summit host country appeared to influence levels of compliance. Compliance levels were higher when the United Kingdom hosted the G7 summit and lower when France and Canada hosted.

![no-alignment]({{ '/images/2023-07-10-g7-compliance/host.png' | absolute_url }})

There was also variation in the probability of compliance between G7 members. The European Union and United Kingdom were more likely to fulfill commitments, while France, Japan, and Italy were less likely to do so.

![no-alignment]({{ '/images/2023-07-10-g7-compliance/member.png' | absolute_url }})

Finally, compliance probability varied by the commitment’s area of focus. Compliance was more likely for commitments regarding social policy, international cooperation, information and communications technology (ICT) and digitization, labour and employment, and energy. Commitments were less likely to be achieved for commitments regarding education and gender.

![no-alignment]({{ '/images/2023-07-10-g7-compliancet/issue.png' | absolute_url }})

# What are the caveats of this approach? 

Despite the many significant variables that were found, the overall explanatory power of the model is very low. Even when all summit characteristics, member nation properties, and commitment features are considered together, only 7.3\% of the variance in G7 compliance could be explained (McFadden’s pseudo R2). This suggests that the majority of G7 compliance may be determined by unknown factors or may be simply random.

Nonetheless, there is hope for increasing G7 effectiveness. All the significant variables examined can be combined into a model to predict future compliance. The binomial logistic regression model can predict compliance in a holdout set with 67\% accuracy, while a random forest classifier model trained on the same data is able to predict compliance with 70\% accuracy. Though not perfect, this second model performs much better than chance, enabling potential compliance issues to be detected with the simulation tool as soon as commitments are made so that resources can be directed accordingly. 

Increasing G7 effectiveness by leveraging patterns associated with higher probabilities of compliance is extremely difficult, as most performance is likely determined by factors outside the control of the organization. However, by using available data to predict future compliance, it may be possible to direct resources to assist member nations at higher risk of failing to meet their obligations — thus improving the overall ability of the G7 to achieve its goals.

*All data and code for this analysis can be found [here](https://github.com/rapsoj/g7-compliance).*
*The G7 Compliance Simulator can be accessed [here](https://g7-utoronto.shinyapps.io/compliance-tool/).*










# Key takeaways:

* There is a pressing need for fare-dependent transit agencies to have access to a reliable forecast of post-pandemic ridership recovery
* This article walks through the creation of such a forecast using machine learning
* Overall, the forecast implies a "new normal" for transit ridership, with no full recovery in sight for at least the next two years

The COVID-19 pandemic has significantly affected public transit operations worldwide, with agencies experiencing up to [90% drops in ridership](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0242476) during initial lockdowns. Since then, ridership has remained substantially below pre-pandemic levels in most cities.

For transit systems that heavily depend on user fees for operational revenue, these ridership decreases [render pre-pandemic financing schemes unsustainable](https://trid.trb.org/view/1844009) and make transit dependent on external financing to maintain operations. Even as public health measures ease, the impact of the pandemic may have lingering effects on ridership that impose further financial burdens on public transit systems. Operators must plan for future dependence on external funding or alternative financing schemes until ridership returns to pre-pandemic levels.

As cities recover from the COVID-19 pandemic, there is a pressing need for fare-dependent transit agencies to have access to a reliable forecast of post-pandemic ridership recovery. Such a model would enable transit providers to understand the impact of various pandemic-related factors and predict the state of public transit use in the near future. 

This article walks through the creation of such a forecast using machine learning.

# Where does transit ridership data come from?

 **Public Transit Ridership** The number of passengers using public transportation.
{: .notice} 

In order to understand the impacts of various pandemic-related factors on transit ridership, detailed public transit ridership data is needed. Changes in transit ridership can be difficult to ascertain at a granular level as most agencies only publish ridership figures at the monthly or yearly level. Data from third party sources, such as [Google's COVID-19 Community Mobility Reports](https://www.google.com/covid19/mobility/), can be used to fill these data gaps. 

The Community Mobility Reports provide daily data at the municipal or county level on changes in the number of visitors to transit stations compared to pre-pandemic levels. When adjusting for weekday variation, these reports offer a highly reliable and comparable approximation for transit ridership during the pandemic in different regions around the world.

Fifteen major cities in five different countries are chosen for analysis, providing a case study as to how specific pandemic policies and public health circumstances affected transit ridership.

![no-alignment]({{ '/images/2022-05-10-transit-forecast/ridership.png' | absolute_url }})

Data provided by these cities on COVID-19 cases, gathering restrictions, park closures, border closures, and changes in work-related traveling can be used to model impacts on transit ridership and forecast ridership recovery for the next two years. 

By creating predictions for the selected cities, ridership recovery trends can be better understood by local transit operations and generalizations can be made about ridership trends across all cities affected by the pandemic.

# How can transit ridership be forecasted?

The following variables are included in the model:

| Variable Name               | Definition                                                            |
|-----------------------------|-----------------------------------------------------------------------|
| ``transit_demand``          | Change in visitors to transit stations compared to before the pandemic|
| ``metric_initial_drop``     | Average drop in ``transit_demand``in the first month of pandemic  |
| ``lagged_month_average``    | Average ``transit_demand`` in the previous calendar month          |
| ``past_average_month``      | Cumulative average ``transit_demand`` until the current month start|
| ``days_since_pandemic``     | Number of days since the pandemic began                               |
| ``cases_total``             | Cumulative rate of COVID-19 cases since the pandemic began            |
| ``work_from_home``          | Change in visitors to work places compared to before the pandemic     |
| ``policy_parks``            | Whether or not the city had closed off public parks                   |
| ``policy_emergency``        | Whether or not the city had a state of emergency declared             |
| ``policy_border``           | Whether or not the country had a major border closure                 |
| ``policy_gathering_low``    | Whether or not the city had prohibited indoor gatherings of 50-1,000  |
| ``policy_gathering_med``    | Whether or not the city had prohibited indoor gatherings of 5-49      |
| ``policy_gathering_hig``    | Whether or not the city had prohibited indoor gatherings more than 5  |
| ``emergency_length``        | Number of days a state of emergency was in effect                      |
| ``gathering_low_length``    | Number of days indoor gathering restrictions (50-1,000) were in effect|
| ``gathering_med_length``    | Number of days indoor gathering restrictions (5-49) were in effect    |
| ``gathering_hig_length``    | Number of days indoor gathering restrictions (<5) were in effect      |
| ``lockdown_total``          | Total number of days indoor gatherings were prohibited during pandemic|

Where ``transit_demand`` is the variable that is targeted for prediction and the other variables are the predictors.

To forecast public transit ridership using these predictors, a [Random Forest regression](https://levelup.gitconnected.com/random-forest-regression-209c0f354c84) model was trained using the available sample data. The final model explains 99.77% of the variance in public transit ridership during the pandemic.

[Variable importance](https://www.displayr.com/how-is-variable-importance-calculated-for-a-random-forest/) can be extracted from the model to better understand which pandemic-related factors have the largest impact on transit ridership.

![no-alignment]({{ '/images/2022-05-10-transit-forecast/variable_importance.png' | absolute_url }})

Unsurprisingly, average ridership in the past month has the highest predictive value in the model. This is important for forecasting, as it means that future predictions are still be highly dependent on recent ridership levels. Similarly, the change in visitors to work places compared to before the pandemic is very important to the predictions. Total bans on gathering restrictions, the initial drop in transit ridership, and the cumulative number of COVID-19 cases are also relatively important in the model, but less so than past month ridership and workplace mobility.

In order to ensure that the model is not overfit to the data, a secondary model was trained on a sample of the data that excluded the most recent one hundred days. The next one hundred days were then forecasted using this model to produce an [ex-post forecast](https://ec.europa.eu/eurostat/statistics-explained/index.php?title=Glossary:Ex-post_forecast), giving an indication of how accurate the model will be in the future when applied to data outside of the training set.

This model is indeed very accurate, with a mean absolute error of 6.1%, meaning on average the predictions were ±6.1% off from the actual change in transit ridership compared to pre-pandemic levels. This implies that forecasted values will be reasonably accurate even when they extend beyond the time frame on which the model was trained.

# When will public transit ridership return to pre-pandemic levels?

To forecast transit ridership into the future, some assumptions need to be made. To keep things simple, it can be assumed that current pandemic circumstances will remain unchanged. This assumes that public health restrictions will not revert to serve levels seen in the past, and COVID-19 case rates will remain similar to the recent rates. The difference in the number of visitors to workplaces during the pandemic is also assumed to remain similar to recent levels. Thus, the forecast is conditional on these pandemic-related variables remaining constant during the prediction period.

Likewise, it has to be assumed that no policy interventions that impact public transit use will come into effect. These include programs to incentivize ridership, such as fare reductions, or actions that subsidize personal vehicle use, such as spending on new highways. 

With these variables held constant, the factors that affect the forecasted transit ridership are time-related, based on general recovery trends that the model separates from the effects of the other variables. There are also effects caused by interactions between time and other variables. For example, gathering restrictions might be expected to have less and less effect on transit ridership over time as [pandemic fatigue](https://wdgpublichealth.ca/blog/pandemic-fatigue-what-it-and-how-do-we-move-past-it) sets in. Finally, past levels of transit ridership impact the forecast as transit ridership is evidently highly correlated with recent ridership levels.

With these assumptions, a two-year forecast can be produced for the fifteen chosen cities:

![no-alignment]({{ '/images/2022-05-10-transit-forecast/forecast.png' | absolute_url }})

To simplify the results, we can look at the average forecasted ridership levels during each quarter of the next two years:

| City          | 2022-Q2 | 2022-Q3 | 2022-Q4 | 2023-Q1 | 2023-Q2 | 2023-Q3 | 2023-Q4 | 2024-Q1 | 2024-Q2 |
|---------------|-------- |---------|---------|---------|---------|---------|---------|---------|---------|
| Brisbane      | -35.8%  | -35.9%  | -36.6%  | -37.8%  | -37.7%  | -37.0%  | -37.0%  | -36.8%  | -36.5%  |
| Calgary       | -29.5%  | -29.6%  | -29.9%  | -29.9%  | -30.1%  | -31.3%  | -30.9%  | -31.0%  | -30.7%  |
| Chicago       | -31.3%  | -30.9%  | -31.0%  | -31.0%  | -30.9%  | -30.9%  | -30.8%  | -30.9%  | -31.1%  |
| Dallas        | -27.5%  | -29.6%  | -30.2%  | -29.3%  | -27.7%  | -27.4%  | -27.4%  | -27.4%  | -27.4%  |
| Houston       | -19.8%  | -19.8%  | -19.8%  | -19.8%  | -19.8%  | -20.0%  | -19.8%  | -19.9%  | -19.8%  |
| London        | -31.5%  | -29.5%  | -29.6%  | -29.8%  | -29.8%  | -27.8%  | -24.2%  | -23.9%  | -23.9%  |
| Montréal      | -29.4%  | -23.4%  | -20.8%  | -20.3%  | -20.4%  | -18.0%  | -17.2%  | -17.1%  | -17.1%  |
| New York      | -30.1%  | -30.4%  | -30.0%  | -29.6%  | -30.0%  | -29.8%  | -29.7%  | -29.8%  | -29.7%  |
| Paris         | -11.2%  | -16.2%  | -16.0%  | -13.5%  | -12.9%  | -12.8%  | -12.7%  | -12.6%  | -12.6%  |
| Philadelphia  | -40.9%  | -34.5%  | -29.8%  | -27.5%  | -20.7%  | -20.6%  | -20.5%  | -20.4%  | -20.4%  |
| Phoenix       | -24.4%  | -25.3%  | -23.7%  | -23.2%  | -23.1%  | -23.1%  | -22.9%  | -22.9%  | -23.0%  |
| San Antonio   | -28.2%  | -28.1%  | -26.8%  | -25.9%  | -25.8%  | -25.7%  | -25.8%  | -25.8%  | -25.9%  |
| San Diego     | -31.4%  | -31.2%  | -30.5%  | -30.5%  | -30.5%  | -30.4%  | -30.1%  | -30.0%  | -30.0%  |
| San Francisco | -44.7%  | -36.0%  | -36.3%  | -31.6%  | -29.7%  | -29.7%  | -29.6%  | -29.4%  | -29.4%  |
| Toronto       | -35.7%  | -27.7%  | -21.3%  | -20.3%  | -18.9%  | -18.9%  | -18.7%  | -18.7%  | -18.6%  |

Where the values in the table are the forecasted change in transit station visitors compared to the pre-pandemic baseline.

All the cities examined are forecasted to have ridership remain below pre-pandemic levels by May 2024, though some recovery is predicted during that time interval. Paris is predicted to have the best overall recovery by the end of the two years, while Brisbane is predicted to have the worst. Relative to current levels, Philadelphia is predicted to have the greatest absolute gains in ridership while Brisbane is predicted to have the smallest.

In general, the model shows that cities that still have pandemic measures in place or have only recently lifted restrictions are likely to see some recovery as public health measures continue to ease. Conversely, cities that have had measures lifted for a longer period of time have likely already realized most of the ridership gains from lifting restrictions.

Overall, the forecast implies a "new normal" for transit ridership, with no full recovery in sight for at least the next two years. It is important that fare-dependent transit providers have access to such forecasts so that they can seek the appropriate funding structures to preserve operations until ridership fully recovers.


*All data and code for this analysis can be found [here](https://github.com/rapsoj/forecasting-transit-recovery).*
