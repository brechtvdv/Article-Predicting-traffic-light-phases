## Abstract
<!-- -->
Nowadays, dynamic traffic lights with a variable phase duration
are widely used. This means that the end time of the phase is unknown,
thus smart mobility applications such as route planners have to predict the
phase duration. In this paper, a short-term prediction for variable phase
durations is made from frequency distributions created using SPaT messages
published with Linked Data Fragments. We grouped the observed
historical phase durations in frequency distributions depending on the time
slot of the observations and made predictions by calculating the median of
the distribution. Using the described methods on an intersection in the city
of Antwerp, an average prediction error of 5,1 seconds is achieved. By using
frequency distributions, a prediction with a fixed confidence can be made.
For example, on average a prediction can be made for 60% of the phase
duration with a fixed confidence of 90%. Although a frequency distribution
gives smart mobility applications a better understanding how long a
phase duration will take, historical data needs to be client-side processed in
advance. In future work, frequency distributions could be published with
Linked Data Fragments.