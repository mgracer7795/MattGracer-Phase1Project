
# Analyzing the Aviation data set

## Overview

This project involves comprehensive tasks: cleansing, analyzing, and visually interpreting insights extracted from the aviation dataset. Our end goal is to provide the company with actionable recommendations, guiding their potential entry into the aviation sector by suggesting specific specifications or brands worthy of investment.


## Business Understanding

As part of our company's strategic expansion into new sectors for portfolio diversification, we are actively exploring opportunities within the aviation industry. This endeavor involves the potential acquisition and operation of both commercial and private aircraft. However, recognizing our limited knowledge of the inherent risks associated with aircraft ventures, our objective is to systematically assess and identify aircraft options that offer the lowest potential risks. The ultimate aim is to provide the head of the newly established aviation division with insightful recommendations that will facilitate informed decisions regarding the selection and procurement of aircraft. By translating our findings into actionable insights, we intend to mitigate risks and pave the way for a successful entry into the aviation market.
 To guide our approach, below are our key business questions:
* What are the potential risks associated with aircraft ventures, and how can these risks be effectively mitigated?
* Which aircraft options present the lowest inherent risks, considering factors such as safety records?
* How can we translate our findings into tangible recommendations that the head of the new aviation division can utilize to make well-informed decisions on aircraft procurement?
 

## Data Understanding and Analysis

The [data](https://www.kaggle.com/datasets/khsamaha/aviation-accident-database-synopses?select=AviationData.csv) we worked with is the NTSB aviation accident database which contains information from 1962 and later about civil aviation accidents and selected incidents within the United States, its territories and possessions, and in international waters.


### Original data description
The original data set contains 90348 entries and 31 columns including:

Event.Id
Investigation.Type      
Accident.Number         
Event.Date               
Location                
Country                 
Latitude                
Longitude               
Airport.Code            
Airport.Name            
Injury.Severity         
Aircraft.damage         
Aircraft.Category       
Registration.Number     
Make                    
Model                   
Amateur.Built           
Number.of.Engines       
Engine.Type             
FAR.Description         
Schedule                
Purpose.of.flight       
Air.carrier             
Total.Fatal.Injuries    
Total.Serious.Injuries  
Total.Minor.Injuries    
Total.Uninjured         
Weather.Condition       
Broad.phase.of.flight   
Report.Status           
Publication.Date


### Dropped columns
Some columns were dropped since they are not related to our business questions.
The dropped columns are:
* Location, Latitude, and Longitude, since we are not interested in the specific location of the incident.
* Airport.Code and Airport.Name since we are not interested the origin and the destination of the plane, and it had a lot of NaNs.
* Injury.Severity since it is already expanded into the 3 columns Total.Fatal.Injuries, Total.Serious.Injuries, and Total.Minor.Injuries.
* Registration number, purpose of flight, Air.carrier, Broad.phase.of.flight, Publication.Date were dropped since they are not related to our business questions.


### Dropping rows and replacing missing values
* Since the business question was about the potentian investment in airplanes, we had to drop every other category in the Aircraft.Category.
* We dropped the rows that have zeroes in all the injury fields and the uninjured field, because this can mean that the airpcraft was empty which is misleading.
* NaNs in the four fields of Total.Fatal.Injuries, Total.Serious.Injuries, Total.Minor.Injuries, and Total.Uninjured were replaced with zero assuming that fields were not filled because they were zeros.
* In the fields Country, Aircraft.damage, Engine.Type, Report.Status, Weather.Condition, and 'Amateur.Built', we replaced NaNs with 'unknown'.
* In the Number.of.Engines field, we replaced the NaNs with 0 since it is a numeric field.


### Cleaned data description
The Cleaned data set contains 27519 entries and 24 columns including:

Event.Id
Investigation.Type
Accident.Number
Event.Date
Country
Aircraft.damage
Aircraft.Category
Make
Model
Amateur.Built
Number.of.Engines
Engine.Type
Total.Fatal.Injuries
Total.Serious.Injuries
Total.Minor.Injuries
Total.Uninjured
Weather.Condition
Report.Status
Year
Month
Number of passengers
Fatality rate
Uninjured rate


### New fields:
* Year and Month fields were extracted from the event date field originally in the data set
Number of passengers is the addition of the 4 fields (Total.Fatal.Injuries, Total.Serious.Injuries, Total.Minor.Injuries, and Total.Uninjured)
* Fatality rate is the result of dividing the Total.Fatal.Injuries column by the Number of passengers. It gives an indication of the percentage of dead passengers after a crash or incident.
* Uninjured rate is the result of dividing the Total.Uninjured column by the Number of passengers. It gives an indication of the percentage of unharmed passengers after a crash or incident.


### Data analysis
![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Distribution%20of%20Accidents%20Over%20the%2012%20Months.png)
This line graph shows the distribution of accidents over the months. July has the biggest portion since it is the peak of the high season.

![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Number%20of%20Incidents%20per%20Make.png)
This graph shows the frequency of accidents per Manufacturer, it shows that the numbers of accidents in Cessna Piper, and Beech are significantly higher than any other manufacturer

![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Number%20of%20Accidents%20by%20Number%20of%20Engines.png)
This graph shows the distribution of accidents by number of engines. The biggest portion of airplanes that had accidents were equipped only 1 engine, when it goes to 2 engines, the number of accidents is much lower, it almost drops to zero when a plane has 3 engines

![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Accidents%20per%20Type%20of%20Engine.png)
This graph shows the distribution of accidents over the different types of engines. The biggest portion of airplanes that had accidents were equipped with Reciprocating, Turbo Prop, and Turbo fan engines.

![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Average%20Fatality%20Rate%20per%20Manufacturer.png)
This graph shows the average percentage of deaths in the accidents of each manufacturer. Socata, Mitsubishi, Rans, and Lancair have the highest rates so passengers are more likely to die in case of an accident.

![](https://github.com/mgracer7795/MattGracer-Phase1Project/blob/master/Graphs/Average%20Uninjured%20Rate%20per%20Make.png)
This Graph shows the average percentage of uninjured passengers in the accidents of each manufacturer. Bombardier, Mcdonnell Douglas, Airbus, and Boeing have the highest average of uninjury rate so passengers are likely to be uninjured in case of an accident.


## Recommendations
* Airplanes with more than one engine have less risk of accidents. 2 engines is good, but three or more is ideal.
* The safest engine types and Geared Turbofan, then Electric, turbo shaft and turbo jet. other types like reciprocating, turbo prop, or turbo fans and jet have a much higher risk.
* Bombardier, Mcdonnell Douglas, Airbus, and Boeing have the highest average of uninjured passenger rates so passengers are likely to survive  an accident. These makes are to be considered.
* Socata, Mitsubishi, Rans, and Lancair have the highest fatality rates so passengers are more likely to die in  an accident. These makes are to be avoided.
** Based on these findings, we recommend commercial and cargo aviation, since these types require big airplanes with multiple engines, with McDonnell Douglas, Airbus and Boeing as manufacturers to be considered.**


## Links
* [Engine characteristics dashboard](https://public.tableau.com/views/EngineCharacteristics/Enginecharacteristics?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)

* [Fatality and survival rates dashboard](https://public.tableau.com/views/FatalityandSurvivalRates/FatalityandSurvivalRates?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)
