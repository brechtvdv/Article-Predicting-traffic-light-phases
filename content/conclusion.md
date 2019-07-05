## Discussion
{:#discussion}

Different approaches are possible to create these distributions over the Web: on the one hand, a client can do all the work, which we showed in our demo, by downloading fragments from the [OTL API](https://lodi.ilabt.imec.be/observer/rawdata/latest) and building the distributions client-side.
<span class="comment" data-author="RV">Why is that relevant though? This is about the goodness of the prediction, not about who does it?</span>
This requires high bandwidth consumption and processing power, but allows new ways of grouping signal phases. For example by querying other Open Datasets (weather data, crowdedness detectors at the intersection...). On the other hand, the server can internally maintain frequency distributions and only publish the likely time and confidence in SPAT messages. Although this answers the current SPAT standard, this gives no flexibility for the client to e.g. predict an interval instead of one phase duration. A third option is to publish frequency distributions as metadata of a signal group. This introduces a new trade-off between server and client effort: frequency distributions can be exposed as cacheable fragments supporting serverless route planning interfaces, while clients can still mix these with other datasets and setting custom prediction preferences.  

Future work should be done how frequency distributions or in general summaries of sensor data can be published with RDF.
<span class="comment" data-author="RV">Why? That seems unrelated.</span>
Also, we need to investigate how a client-side route planner (cfr. [Planner.js](https://planner.js.org/)) can integrate this data into its internal road network and how this can influence the user perceived journey experience.

