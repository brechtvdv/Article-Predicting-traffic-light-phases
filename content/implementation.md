## Predicting the phase duration
{:#predicting-the-phase-duration}
 
Instead of grouping signal phases for every fixed cycle time in related work [](cite:cites 8500307), we group in different time slots, because the traffic lights controller in [Antwerp](https://docs.wegenenverkeer.be/Vademecum
s/Vademecum%5C%20Veilige%5C%20wegen%5C%20en%5C%20kruispunten/3.2.%5C%
20Modeloplossingen%5C%20Verkeerslichten.pdf) dynamically changes the cycle time to the live situation on the intersection. As a baseline, we used no grouping in time. This means that only one distribution is created for every signal phase of a  signal group containing all historical phase durations. Next, we grouped per type of day (weekday or weekend) and for every hour. The reasoning behind this is that the traffic lights controller interacts differently during the weekends and peak hours. The last strategy is more fine-grained and groups per day (monday, tuesday...) and in time slots of 20 minutes.
To select a predicted duration $$d_p$$, we tested the median, mean and mode. We calculate the prediction error with the mean absolute error (MEA) as follows: 
$$MAE = \dfrac{1}{n}\sum_{i=1}^n|d_p(i)-d(i)|$$ .
The test cases are ran using 10-fold cross validation. First, we extracted the phase and timing of signal groups and randomly divided these in 10 groups. Then we replayed every SPAT message $$i$$, who belongs in one group, and predicted its duration $$d_p$$ and compared it with its real duration $$d$$ using the frequency distributions made from the other 9 groups.

## Results
{:#results}

To run reproducable tests, a [dataset](https://github.com/kridhaen/OpenTrafficLightsData) from 8th till 25th March 2019 is harvested from the OTL endpoint containing 50951 historical fragments.
[](#mae-prediction) shows the MAE for every grouping strategy and method we applied. We see that fine-grained grouping of phases improves the MAE which acknowledges related work [](cite:cites 7325247). Using the median also returns lower prediction errors than the mean and mode. Regardless of the signal group and signal phase, an overall MAE of 5.1 seconds is achieved.  

<figure id="mae-prediction" class="table" markdown="1">

| Method                   | No grouping (s) | Per type of day and every hour (s)  | Per day and every 20 minutes (s) |
| ------------------------ |------------|------------------------------------|------------------------------|
| Median                   | <code>6.8</code>        | <code>5.5</code>     							 | <code>5.1</code>      					| 
| Mean               	   | <code>7.0</code>        | <code>5.9</code>       						 | <code>5.6</code>					        |           
| Mode 					   | <code>7.6</code>        | <code>6.2</code>    							 | <code>6.0</code>				        | 

<figcaption markdown="block">
A prediction error of 5.1 seconds is achieved by using the median and grouping phases per day and time buckets of 20 minutes.
</figcaption>
</figure>

We go one step further by also considering how the MAE of a specific signal group evolves over time. We hypothesize that the prediction error will be higher in the beginning of a phase than on the end of the phase.
Signal phases are grouped per day and every 20 minutes and the median is used for the prediction.
 [](#time-till-transition) shows for the [signal phase](https://w3id.org/opentrafficlights/thesauri/signalphase/3) with label "Stop and remain", which corresponds with a red light, how the prediction error decreases when the time until the end of the phase also decreases. We see can three findings: first, the prediction error grows linear for phase durations above 62 seconds. This is because very long phases occur less, thus using the median for predicting these outliers is not a good fit. Secondly, we see a flatten line for phase durations between 9 and 65 seconds with a MAE around 10 seconds. This can be explained that the bulk of phases are between this interval which makes the median a good choice. Finally, between 0 and 9 seconds predicting was not necessary, because the minimum duration equals the maximum duration.

<figure id="time-till-transition">
<center>
<img style="height: auto; width: 70%" src="img/time-till-transition-2.svg">
</center>
<figcaption markdown="block">
The prediction error lowers when the phase reaches its end. This is done for the [signal phase](https://w3id.org/opentrafficlights/thesauri/signalphase/3) with label "Stop and remain".
</figcaption>
</figure>