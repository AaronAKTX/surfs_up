# Surfs Up

## Overview
Analysis was done on the temperature in Oahu during the months of June and December. The weather stats for these months were collected from stations in Oahu then summarized and presented. The study was performed to provide information that would help determine whether or not opening an ice cream and surf shop is an advisable business plan.

## Results:

### June Temperatures                    
 <img src = "https://github.com/AaronAKTX/surfs_up/blob/main/Resources/JuneTemps.PNG">

### Decemeber Temperatures
<img src = "https://github.com/AaronAKTX/surfs_up/blob/main/Resources/DecTemps.PNG">

### Temperature observations
- The average temperature in June is 75 degrees Fahrenheit.
  - 75 percent of the temperatures taken in the month of June are 73 degrees Fahrenheit or higher - That is both great surfing and great ice cream weather.
- The average temperature in December is 71 degrees Fahrenheit.
  - 75 percent of the temperatures taken in the month of December are 69 degrees Fahrenheit or higher - That is both great surfing and great ice cream weather.
- The temperature in two opposite times of the year both average a nice temperature for ice cream and surfing and aren't that different from each other which seems to indicate that a year-round ice cream/surf shop would be a great business.


## Summary

### Ice Cream and Surfing = the PERFECT combination
Based on the temperature data, the ice cream/surf shop is a great idea. People who surf, can pretty much surf year round looking at the temperature. People who enjoy ice cream can eat year-round without getting too cold. People who eat ice cream and surf will be in paradise with this combination.

By filtering the data a little more, I was able to find that only 5% (89 out of 1700) of the temperatures collected in June were below 70 degrees.
* query used: session.query(Measurement.date, Measurement.tobs).filter(Measurement.tobs<70).filter(extract('month', Measurement.date)==6).all()

Only about 32% (481 of 1517) of the temperatures collected in December were below 70 degrees.
* query used: session.query(Measurement.date, Measurement.tobs).filter(Measurement.tobs<70).filter(extract('month', Measurement.date)==12).all()

It was also interesting to me to note that the average temperature for all temps collected year-round was just over 73 degrees.
* query used: session.query(Measurement.date, Measurement.tobs).all()

All year summarized below.

<img src = "https://github.com/AaronAKTX/surfs_up/blob/main/Resources/AllTemps.PNG">

All signs point to opening this Surf and Scoop IMMEDIATELY!
