## Abstract
Traffic lights with a variable phase duration are widely used for optimizing traffic flows. Although the minimum and maximum duration of a phase is published,
<span class="comment" data-author="RV">globally, or just in Antwerp?</span>
a predicted duration with a certain confidence would increase the reusability of traffic lights data for route planners.
We tested for a live Open traffic lights dataset of Antwerp (i) how frequency distributions of phase durations can be used to predict the duration of the current phase and (ii) how frequency distributions can be created client-side and on-the-fly with a demonstrator.
An overall mean average error (MAE) of 5.1 seconds is reached by grouping the phase durations <span class="rephrase">per day and in timeslots of 20 minutes and using the median</span> to select a predicted phase duration. When taking the <span class="rephrase">time until end of phase</span> into account, we see for the bulk of phases that the MAE is flattening around 10 seconds,
<span class="comment" data-author="RV">And is that good or bad? This is an example of an observation, but without a conclusion attached to it. As such, readers will need to draw their own, and <em>if</em> they do so, it might be wrong.</span>
but grows linearly for outliers. 
<span class="comment" data-author="RV">same—good or bad?</span>
With our approach, route planners can calculate how long the current phase will take by using frequency distributions.
<span class="comment" data-author="RV">So what? Go a step further: you already said they could do that. Because of it, are their suggestions more accurate?</span>
In future work, we will investigate how traffic lights data can be integrated into road network graphs and how other Open Datasets (crowdedness counters, public transport...) can be reused to detect the outlying phase durations.


<span class="comment" data-author="RV">I don't want to undermine the work here, but I find it slightly strange. Why are we trying to predict this? Isn't it easier to get access to the control data that determines this duration? Or can you argue why it is hard/impossible to get access to that data?</span>
