# FluVaccinationRates

Predicting State Flu Vaccination Coverage

Insight Seattle 18c: Ori Weiner, Wik Hung Pun, Willy Voje, Regina Carns, Lauren Kendrick

*Note, this is a text-only version of our report, which is fully available as a PDF (contact us)*

Executive Summary
Problem Statement 
The goal of this report is to identify potential data sources and create a month to month model of flu vaccination coverage at the state and national levels that does not rely on phone survey data.
Approach
We assessed several data sources to see whether they correlate, or co-vary, with the flu vaccination rates estimated in the CDC’s FluVaxView tool.  We created a model using the data sources which had the highest correlation. We also incorporated a ‘time lag’ to account for the possibility that a person’s expression of interest or awareness of the flu vaccine may precede receiving the vaccine.
Data Sources Attempted 
State immunization registries
Social media
Internet searches
Key Findings
Google searches for flu shot and related terms are highly correlated to flu vaccination rates.
State level immunization registries based on medical provider reports may not be promising data sources.
Mentions of the flu vaccine on Twitter may be linked to flu vaccination rates, but this data is difficult to resolve geographically and may not be useful for predicting flu vaccinations.
Our overall model has an R2 value of approximately .89, compared to R2 of approximately .94 for the historical ‘baseline’ model. Our model slightly underperforms the historical FluVaxView baseline, but Google Trends data is more easily accessible and has a higher temporal and geographical resolution than phone survey data, making it potentially useful for real-time vaccination coverage monitoring.  Google Trends data will also have potential to track changes in future flu vaccination trends.

II. Potential Data Sources

There are several ways to discover who is getting flu shots and where, at each stage of the process from flu shots being manufactured to after they have been administered. Flu manufacturers can report how many doses were sold and where they were distributed. Those who administer the flu vaccine may be able to report how many doses they administered and to whom; these include hospitals, clinics, workplaces, schools, and commercial pharmacies. 

Each of these methods requires voluntary reporting from the organizations in question, which may be complicated by regulations or privacy concerns and has administrative overhead. In the short timeframe available to us, we opted not to pursue any sources that might require lengthy negotiations to secure. Many state health organizations, however, do make their data publicly available on the Internet, so we investigated these as additional sources of vaccination records. 

Data derived from observing the Internet activity of individual flu shot recipients may also be freely available online.  People who are planning to get a flu vaccine may research the vaccine or discuss their plans online; after they get it, they may post to social media about their experiences.  

Social media sources vary widely in how they make their data accessible and how much data they are willing to share. Some make all their data available, both current and historical; most provide access only to a limited subset of data. Two of the most popular social media platforms, Facebook and Instagram, allow almost no access to their data. Twitter data is more accessible, although historical data can still be time-consuming to acquire; previous work on using social media to monitor influenza vaccinations has used Twitter data.  Google Trends, a service provided by Google that monitors the volume of searches on a given term over time, also gives comparatively easy access to historical data.  

Our goal in this project was to examine these sources to data to determine whether any of them could be a reliable indicator for the extent of vaccination coverage at any given time and location. 

Establishing ground truth
Social media posts and Google searches are a form of proxy data--they do not directly measure the number of people who have received their flu vaccine at any given time, but we hope they might correlate well with the real data. State health data are a direct measurement of vaccinations administered, but may not include sources such as commercial pharmacies or workplaces that are not part of the formal reporting system. In order to determine whether these sources are accurate, we compare them to the best available source that directly measures vaccination coverage, the NIS and BRFSS phone surveys. This is the “ground truth”, the most direct measure of the data we actually want to measure. 

Flu vaccination rate is naturally extremely seasonal. Rates rarely vary by more than 10 percentage points from year to year, so the simplest possible “model” of vaccination rates--simply guessing that coverage in November of 2018, for example, will be the same as coverage in November of 2017--is likely to be fairly accurate. 
Baseline: Predict flu vaccination rate from previous year ground truth
We use a historical baseline model as a reference to better understand the performance of the predictive models we might construct based on other data sources. For our work, we took the baseline model to be that the reported vaccination rates of previous years can be used to predict the vaccination rate of future years for each individual state. To build this prediction the monthly vaccination rates each state for years 2014-15 and 2015-16 were averaged and compared against the years 2016-17 and 2017-18 years vaccination rates. The performance of these models were determined using “coefficient of determination” , or “R2 value”, a metric that describes how well a model performs at predicting the variation in the data. The optimal value for this metric is 1, indicating that all variance in data was predicted by the model. The results of the prediction for each state are presented below. The model performs well with an average R2 of 0.98 +/- 0.01 and 0.90 +/- 0.06 for 2016-17 and 2017-18 respectively (error shown is 95% confidence interval). The decrease in model performance from 2016-17 and 2017-18 is due to this naive model failing to account for yearly trends in vaccination coverage. For example, Tennessee has seen a consistent decrease in vaccination coverage over the past 5 years.  Purely historical models will not maintain their predictive power over time, as trends in flu vaccination may change in future years.

FluVaxView Aggregated Data
Each year the CDC aggregates data from the Behavioral Risk Factor Surveillance System (BRFSS), the National Health Interview Survey (NHIS), and the National Immunization Survey-Flu. (NIS-Flu) to generate influenza vaccination coverage in the United States. The aggregate data details the monthly vaccination rates per-state across both age and racial demographics. Consequently, this data was the most complete and easiest to interface with of the potential ground-truth data. Though convenient, the process of data aggregation causes a loss of granularity that we would otherwise have access to. For this stage of analysis we reasoned that this loss of information was insignificant relative to the convenience. Consequently FluVaxView data was used used as the ground-truth data set.  FluVaxView data for two representative states for the 2014-2017 flu seasons are presented below.

B. Health data - Counting vaccinations
The best possible predictor of flu vaccination coverage would be an actual count of flu shots administered; however, data sources that record this type of information are not unified across all types of flu shot providers and may involve incomplete or voluntary reporting, leading to large, systematic errors.  The CDC has access to the numbers of flu vaccines produced and distributed, but these numbers reflect only an upper bound on the number of flu shots that could be administered.  Organizations that deliver large numbers of flu shots such as CVS and Walgreens collect data on people receiving the immunizations.  This data could be useful to describe this subpopulation of flu shot recipients, but would exclude flu shots delivered through other venues such as workplaces or doctors’ offices.  During this brief modeling effort, we did not obtain flu shot record data from CVS, Walgreens, or insurance companies, but future modeling efforts could request it to complement data related to flu vaccinations from other sources.

State immunization registries represent another potential source of records of flu shots administered.  States may keep records of reports of immunizations administered to children, adults, or Medicare recipients as part of an online registry or information system.  However, these reports come from participating clinics and medical providers, and in some states reporting occurs on a voluntary basis.  This leads to data with systematic errors as some providers may not report flu immunizations at all and others may report intermittently.  Additionally, flu vaccines may be administered through workplaces or providers outside the scope of immunization registry participation.
State immunization registry data on flu vaccinations may be available for most or all states if requested from state health boards.  Most states do not publish this data online, and it may be hard to access for the number of years in the past that would be helpful for building a model.  Publishing online may be more common for flu vaccination among Medicare, Medicaid recipients or children.  To test whether state immunization registry data could be useful for the current modeling effort, we examined flu vaccination data for 2015-2017 for children in the state of Washington, and compared to the data available for the same age group between 6 months and 17 years of age in FluVaxView data for the state of Washington.  


The graph above shows that the fraction of flu vaccination coverage reported occurring between October and December in the State of Washington for children in this age range is much lower than the corresponding fraction in FluVaxView.  Also, the value increases instead of decreasing for the year 2016.  This suggests a low correlation and suggests that state immunization registry data may not be a promising source for predicting the population coverage levels represented in the FluVaxView data.  Additional years of data and additional states might provide a more complete gauge of the usefulness of this resource, but we were not able to access much more data from these sources at this point.
C. Internet Search
Google Trends 
There are many search terms that could indicate public interest in receiving a flu shot, including “flu shot”, “flu shot near me”, “flu shot cvs”. Google Trends allows us to see how many times a given search was performed during a given time period. We theorize that people planning to get a flu shot are more likely to Google for terms like these shortly before getting the shot. 

We brainstormed several search terms that might be related to intent to vaccinate, as shown in the plot below. In this plot, red colors indicate terms that are correlated with each other--search traffic for one term is high at the same time as its correlated term. Blue colors indicate search terms that are not well correlated. The plot shows two sets of terms that all correlate with each other (the two larger red squares.) The large red square shows search terms correlated with ‘flu shot’; these searches peak early in flu season, when people are getting vaccinated.  Terms in the smaller red square peak later in the season, when the actual incidence of flu begins to rise. ‘Vaccines’ is not well correlated with any other search terms, because most vaccines other than the flu vaccine do not have a seasonal pattern. 
Flu search trend correlations



We found that searches for the term ‘flu shot’ correlated well with FluVaxView data, except for an anomaly during the 2017-2018 flu season. During this season, searches spiked as usual in October, but then spiked again in January when media coverage of an especially bad flu season and a relatively ineffective flu vaccine led to an increase in searches without a corresponding increase in vaccinations. This ‘double spike’ is clearly visible in the orange line in the graph below. 


Fortunately we were able to correct for this spurious data by adding the search term ‘flu news’ to our model; since this term spiked in January, but not in October, it allowed our model to ‘cancel out’ the false spike. This worked well for this particular case and could potentially work to correct for other false spikes based on media coverage, but with only one case of anomalous data it is difficult to be sure.  
D. Social media
Twitter 
Although social media, such as Twitter, may represent a good data source for examining the perception and coverage of flu vaccine across the nation, the utility value of Twitter data at the state level is very limited due to the scarcity of the data and potential bias associated with it. For instance, searching the hashtag, “#flushot”, only returned about 1400 tweets from 2015-2018 across all 50 states due to only a very small subset of the twitter users elected to geotag their tweets (to “geotag” is to mark a tweet with a latitude and longitude indicating the Twitter user’s location at the time the tweet was published.) A broader search term such as “flu”  returned more results (90,000 geotagged tweets) but likely still under-represents the total number of tweets during the same period. 


The Twitter trend plot above shows the number of tweets mentioning flu from January, 2015 to November, 2018. As above graph shown, the number of tweets at any given month varies greatly by the location and is not necessarily associated with the change of vaccine coverage over time. 
Instagram 
Instagram is an appealing data source because of its high volume of users. However, due to privacy concerns, Instagram makes it very difficult to access its data, and forbids “web scraping” (that is, accessing data by reading web pages rather than by using a developer interface.) Manual inspection of Instagram searches for keywords such as “flu shot” suggests that a significant percentage (over a third) of posts referencing flu shots are discussing them from an anti-vaccination perspective or suggesting naturopathic alternatives. This data might be of interest in future projects as a measure of anti-vaccination sentiment. Currently, Instagram “business accounts” can access data for a chosen keyword for the past 24 hours, so if later investigators are interested in using Instagram data this would be a possible option. 
III. Predicting State-level Coverage
We chose to use Google Trends because it is available at the state level and has high temporal resolution.  There is much more Google Trends data available than geotagged Twitter data.  Google Trends data is also highly correlated with FluVaxView monthly vaccination rates.

We created a model using data on “Flu shot” and “Flu news” searches in the first and second weeks of each month to predict the month’s flu vaccination rate.  We decided to train the model on the final two years of FluVaxView monthly data (2016-2017 and 2017-2018 flu seasons), on new vaccinations per month rather than cumulative vaccinations at each month for each season.  We then tested the model performance on the flu seasons 2014-2015 and 2015-2016.  This training and testing strategy allowed the model to learn from the sensational news trend behavior in the last year of data.  The following plot shows the model performance predicting new vaccinations each month in Texas between 2014 and 2018.

Example: Model performance on Texas vaccination rate



We compared the model performance to the baseline historical prediction performance by calculating R2 for the prediction for each state in each of the test years and comparing the average R2 and confidence interval across the model and baseline over the model years.  The R2 for each state in each test year is shown in the figure below.  The model underperformed the baseline by 0.05 on average in terms of R2, which is not a significant difference.


IV. Conclusions + Future Directions
Of the data sources we investigated, Google Trends did the best job of predicting vaccination rates. While Google Trends slightly underperforms the historical baseline model, it represents a data source that is updated in real time and is much cheaper and easier to access than phone survey data.  The data is easily available and has geographical information resolved at the state level. For high-volume search terms, including ‘flu shot’, the data is often resolvable down to metro areas or even individual cities. Google searches may be able to correct for some of the demographic bias introduced by using landline phone surveys, since use of Google for Internet search is likely to be more consistent across demographics. 
Twitter searches proved to have poor geographic resolution, but might still be useful in augmenting Google Trends data to help understand nationwide vaccination rates. 

Future work may be able to take advantage of additional data sources if more time and resources become available. Some potential data sources:

Walgreens currently maintains a “flu index” based on sales of antiviral medications, and might be willing to provide information about sales of flu vaccines to augment existing data sources. 
Instagram and Facebook historical data are difficult to access, but businesses willing to go through a process of application review can access some information from searches on hashtags such as “#flushot”. Given the wide reach of these services, it might be worth overcoming these obstacles to see whether their data are also predictive of flu vaccination coverage. 
Social media posts and Google searches can indicate intent to vaccinate; sometimes, however, they indicate anti-vaccination sentiments. Future work might incorporate anti-vaccination keywords and hashtags as another input to a model predicting vaccination coverage. 
Even more google trends searches may be useful. For example, while most correlations we found were extremely high relative to ‘flu shot’, the search term ‘flu shot near me’ had only 0.77 correlation and may be a useful addition or even replacement to ‘flu shot’ (although it has a lower volume of searches).  The most relevant searches may change over time, for example, as Google updates their search term autocomplete algorithm.
Premium membership in the twitter API can be used to acquire much more data and make a stronger attempt to include this important source in the final model.

One of the biggest hurdles to using more data sources is the number of data points in the ground truth. While we fitted every state to an individual model, one could consider aggregating states by regions to increase data for further analysis. With even more data, it may be possible to begin using more complex models than the one we have used here, and to allow for interactions between different data sources.

Our overall model has an R2 value of approximately .89, compared to R2 of approximately .94 for the ‘baseline’ model. Our model slightly underperforms the historical FluVaxView baseline, but Google Trends data is more easily accessible and has a higher temporal and geographical resolution than phone survey data, making it potentially useful for real-time vaccination coverage monitoring.  Google Trends data will also have potential to track changes in future flu vaccination trends and provide an alert for low vaccine coverage on a regional basis (which could then be verified using phone surveys), whereas the baseline cannot predict year-to-year changes by definition.
