## Demonstrator
{:#demonstrator}

This application demonstrates a Web client that predicts the phase duration of a live traffic light in [Antwerp](https://www.openstreetmap.org/#map=19/51.21205/4.39717). The green line on the chart shows minimum duration in seconds of the phase, like wise the red line shows the maximum duration. A blue line will show the predicted duration, but the client first needs to construct frequency distributions by continuously fetching the latest data from the [OTL API](https://lodi.ilabt.imec.be/observer/rawdata/latest). Frequency distributions are made with the third grouping strategy, for every signal group, signal phase, day and time slots of 20 minutes. The median is calculated at the start of a new phase for the predicted phase.

This vizualization gives some insights:

* The predicted phase duration increases the insight how long the phase will actual take, especially when the minimum and maximum duration differ tens of seconds.
* When the minimum duration aligns with the maximum duration, the blue line gets corrected with a few seconds. This behavior corresponds with the average results from [](#mae-prediction).

The source code can be found as a Codepen at [https://codepen.io/kridhaen/pen/VJrezO/](https://codepen.io/kridhaen/pen/VJrezO/).

<figure id="codepen">
<center>
<img src="img/demo-2.png">
</center>
<figcaption markdown="block">
Webapplication that shows the minimum (green), maximum (red) and predicted (blue) phase duration (seconds) of a live traffic light in Antwerp. The predicted phase duration is calculated by creating a frequency distribution on-the-fly from the live data.
</figcaption>
</figure>

<p class="codepen" data-height="761" data-theme-id="0" data-default-tab="result" data-user="kridhaen" data-slug-hash="VJrezO" style="height: 761px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="OpenTrafficLightsPredictor">
  <span>See the Pen <a href="https://codepen.io/kridhaen/pen/VJrezO/">
  OpenTrafficLightsPredictor</a> by kridhaen (<a href="https://codepen.io/kridhaen">@kridhaen</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>