## Abstract
Dynamic traffic lights change their current phase duration according to the situation on the intersection, such as crowdedness. In Flanders, only the minimum and maximum duration of the current phase is published. When route planners want to reuse this data they have to predict how long the current phase will take in order to route over these traffic lights. 
We tested for a live Open Traffic Lights dataset of Antwerp how frequency distributions of phase durations (i) can be used to predict the duration of the current phase and (ii) can be generated client-side on-the-fly with a demonstrator.
An overall mean average error (MAE) of 5.1 seconds is reached by using the median for predictions. A distribution is created for every day with time slots of 20 minutes. This result is better than expected, because phase durations can range between a few seconds and over two minutes.
When taking the remaining time until phase change into account, we see a MAE around 10 seconds when the remaining time is less than a minute which we still deem valuable for route planning. 
Unfortunately, the MAE grows linear for phases longer than a minute making our prediction method useless when this occurs. 
Based on these results, we wish to present two discussion points during the workshop.

<span class="printonly firstpagefooter">
<span class="footnotecopyright">
This is a print-version of an article first written for the Web. The Web-version is available at https://brechtvdv.github.io/Article-Predicting-traffic-light-phases .                              
Copyright © 2019 for this paper by its authors. Use permitted under Creative Commons License Attribution 4.0 International (CC BY 4.0).
</span>
</span>