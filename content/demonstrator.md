## Demonstrator
{:#demonstrator}

This application demonstrates a Web client that predicts the phase duration of a live traffic light in [Antwerp](https://www.openstreetmap.org/#map=19/51.21205/4.39717). This client continuously fetches the latest data fragment from the OTL API and constructs frequency distributions for every signal group, signal phase, day and time slots of 20 minutes. The median is calculated for the predicted phase duration at the start of every signal phase.

The source code can be found as a Codepen at [https://codepen.io/kridhaen/pen/VJrezO/](https://codepen.io/kridhaen/pen/VJrezO/).

<figure id="codepen">
<center>
<img src="img/demo.PNG">
</center>
<figcaption markdown="block">
TODO
</figcaption>
</figure>

<p class="codepen" data-height="761" data-theme-id="0" data-default-tab="result" data-user="kridhaen" data-slug-hash="VJrezO" style="height: 761px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="OpenTrafficLightsPredictor">
  <span>See the Pen <a href="https://codepen.io/kridhaen/pen/VJrezO/">
  OpenTrafficLightsPredictor</a> by kridhaen (<a href="https://codepen.io/kridhaen">@kridhaen</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>