## Demonstrator
{:#demonstrator}

This Web application demonstrates the prediction of the current phase duration of a live traffic light in [Antwerp](https://www.openstreetmap.org/#map=19/51.21205/4.39717). The green, red and blue line on the chart shows respectively the minimum, maximum and predicted duration in seconds of the phase. 
This client harvests the latest data from the Open Traffic Lights [API](https://lodi.ilabt.imec.be/observer/rawdata/latest) and constructs frequency distributions with the same strategy as [](#results).

This vizualization gives some insights:

* The minimum and maximum duration can differ tens of seconds, especially in the beginning. With the predicted phase, a user can have a better understanding how long the phase will probably take.
* When the minimum and maximum duration align, and thus it becomes certain how long the phase take, the blue line gets mostly corrected with a few seconds. This behavior hints to our result from the average prediction error ([](#mae-prediction)). 

The source code can be found as a Codepen at [https://codepen.io/kridhaen/pen/VJrezO/](https://codepen.io/kridhaen/pen/VJrezO/).

<figure id="codepen">
<center>
<img src="img/demo-2.png">
</center>
<figcaption markdown="block">
With the blue line, we have a better understanding how the predicted phase duration relates to its minimum and maximum phase duration and whether it was close to the real duration.
</figcaption>
</figure>

<p class="codepen" data-height="761" data-theme-id="0" data-default-tab="result" data-user="kridhaen" data-slug-hash="VJrezO" style="height: 761px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="OpenTrafficLightsPredictor">
  <span>See the Pen <a href="https://codepen.io/kridhaen/pen/VJrezO/">
  OpenTrafficLightsPredictor</a> by kridhaen (<a href="https://codepen.io/kridhaen">@kridhaen</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>