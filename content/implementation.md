## Predicting the phase duration
{:#predicting-the-phase-duration}

<span class="comment" data-author="RV">You don't say which algo you are using and why. Not enough to reproduce.</span>

To be able to predict the phase duration of a dynamically changing traffic light phase, there are two steps we take: first, we create frequency distributions like in related work [](cite:cites 8500307) from a dataset with occured phases and then we pick a predicted duration from the distribution that is active at the moment that is tested using a certain method. 
Since traffic patterns can change depending on the time of the day or day of the week, we tested multiple strategies [](cite:cites 7325247) to group signal phases for the creation of a distribution.
As a baseline, frequency distributions are created for every signal group and signal phase. 
Then, we grouped phases according to its type of day (weekday or weekend) and in time slots of every hour. The reasoning behind this is that a traffic light interacts differently during the weekends and peak hours. The last strategy works per day (Monday, Tuesday...) and in time slots of 20 minutes.
To predict the duration of a phase from a received SPAT message, we tested a few basic selectors: mean, mode and average. These selectors are ran on the frequency distribution that is relevant for the moment the SPAT message is generated and only consider phase durations from the distribution that take longer than its current phase duration, because these can still historically happen.
We choose these selectors instead of graph transformations [](cite:cites 7013336), because we discovered that certain phase durations of our tested dataset occur more frequently than others ([https://kridhaen.github.io/OpenTrafficLightsDistributionsVisualizer/](https://kridhaen.github.io/OpenTrafficLightsDistributionsVisualizer/)) creating peaks in its frequency distribution. This made us hypothesise that this behavior will benefit using a method like the mean.
Finally, to express the prediction error we calculate the mean absolute error (MEA) for every SPAT message $$i$$ as follows [](cite:cites 8500307) where $$d_p(i)$$ is the predicted duration and $$d(i)$$ the real duration of $$i$$: 
$$MAE = \dfrac{1}{n}\sum_{i=1}^n|d_p(i)-d(i)|$$ . 

<!-- 
2 experiments: overall MAE and with time until phase change: how are they calculated
 -->

## Results
{:#results}

We use the traffic lights data from the intersection in Antwerp which has a [variable cycle time](http://docs.wegenenverkeer.be/Publicaties/Brochure%20Verkeerslichtengeregelde%20kruispunten.pdf).
To run reproducible tests, we harvested a [dataset](https://github.com/kridhaen/OpenTrafficLightsData) from 8th till 25th March 2019 from the OTL endpoint containing 50951 historical fragments.
The test cases are ran using 10-fold cross validation. First, we extracted the phase and timing of signal groups and randomly divided these in 10 groups. Then we replayed every SPAT message $$i$$, who belongs in one group, and predicted its duration $$d_p$$ using the frequency distributions made from the other 9 groups and compared it with its real duration $$d$$. Only SPAT messages where the duration is unknown (minimum and maximum duration differ) are considered.

[](#mae-prediction) shows the MAE for every grouping strategy and method we applied. We see that fine-grained grouping of phases improves the MAE which acknowledges related work [](cite:cites 7325247). Also, using the median returns lower prediction errors than the mean and mode.
A very good result is considered around 2 seconds according to Bodeheimer et al. [](cite:cites 7325247), but for a basic algorithm and without using external detector information an overall MAE of 5.1 seconds is still lower than expected. Especially because this test considers SPAT messages whose time till phase change is still very high (>30s), thus we expect it to have a very high prediction error.

<figure id="mae-prediction" class="table" markdown="1">

| Method                   | No grouping (s) | Per type of day and every hour (s)  | Per day and every 20 minutes (s) |
| ------------------------ |------------|------------------------------------|------------------------------|
| Median                   | <code>6.8</code>        | <code>5.5</code>     							 | <code>5.1</code>      					| 
| Mean               	   | <code>7.0</code>        | <code>5.9</code>       						 | <code>5.6</code>					        |           
| Mode 					   | <code>7.6</code>        | <code>6.2</code>    							 | <code>6.0</code>				        | 

<figcaption markdown="block">
An overall prediction error of 5.1 seconds is good, because a prediction is made for every SPAT message without using external datasets. This hints that some dynamic traffic lights of Antwerp probably follow a predictable pattern which is good for route planning.

<!-- <span class="comment" data-author="RV">Don't tell what we see—interpret. What are we supposed to see? Good, bad?</span>
 --></figcaption>
</figure>

To test this causality between the MAE of a signal group and its time until phase change, we plotted this in [](#time-till-transition) for one [signal group](https://opentrafficlights.org/id/signalgroup/K648/3) showing signal phase "[Stop and remain](https://w3id.org/opentrafficlights/thesauri/signalphase/3)" (red line) and "[Protected Movement Allowed](https://w3id.org/opentrafficlights/thesauri/signalphase/6)" (green line). The other signal groups can be found here: [https://kridhaen.github.io/OpenTrafficLightsDistributionsVisualizer/](https://kridhaen.github.io/OpenTrafficLightsDistributionsVisualizer/) by pressing the arrow button to "Visualization of the prediction error for each time to phase change for large dataset".
The latter shows a prediction error of almost 0 seconds which can be confirmed with its [frequency distribution](https://kridhaen.github.io/OpenTrafficLightsDistributionsVisualizer/): its phase duration generally takes 15s and exceptionally 18s. With this knowledge, route planners can safely assume that this signal group will have a green time of at least 15s.
For the former signal phase, we see three findings. 
First, between 0 and 9 seconds there is no prediction error, because the minimum duration equaled the maximum duration. Next, we see a flat line for phase durations between 9 and 65 seconds with a MAE around 10s. Planning a route with such error rate can still be valuable, for example when the phase is 60s before change: one the one hand a prediction of 50s can lead to 10s of waiting before a red light, on the other hand a prediction of 70s means that it is already 10s green with 5s remaining. This raises a new challenge whether the driver will be able to pass the green light in those 5 seconds depending on the crowdedness.
Lastly, above 65 seconds the prediction error grows linear. Although these long phase durations occur exceptionally, otherwise the overall MAE would be much higher, route planning during such a phase would return completely unreliable results. 

<figure id="time-till-transition">
<center>
<img style="height: auto; width: 70%" src="img/time-till-transition-3.svg">
</center>
<figcaption markdown="block">
Predicting the duration of signal phase "Protected Movement Allowed" (green line) for this signal group is perfectly possible as its prediction error is almost 0 seconds. 
For signal phase "Stop and remain" (red line), we deem a prediction error around 10s still valuable, but would require additional information to anticipate on worst case predictions.
</figcaption>
</figure>

<!-- <span class="comment" data-author="RV">Good, bad, success, failure??</span>
 -->
