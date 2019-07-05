## Related work
{:#related work}

The [Open Traffic Lights](https://opentrafficlights.org) (OTL) [](cite:cites vandevyvere_mepdaw_2019) project proposes a strategy for publishing traffic lights data in a semantical and technical interoperable way. First, with the OTL ontology, global identifiers (URIs) are defined for a subset of the terms of the currently used datastandards SPAT and MAP. SPAT defines the signal phase and timing of a signal group to which a traffic light belongs. MAP defines the geometry of the departure and arrival lanes and how these connections relate to a signal group. By agreeing on the semantics of these terms and applying RDF for describing facts, data publishers are not limited to the currently defined datastructure in JSON format. OTL also defines how the data can be published as time sorted [Linked Data Fragments](https://brechtvdv.github.io/Article-Open-Traffic-Lights/#specification). This allows HTTP clients to not only retrieve the latest value of a signal group, but also its historic values through pagination links which can be used for predicting the signal phase duration of signal group.

Predicting the phase duration has been done in related work [](cite:cites 8500307, 7325247). In their experiments, tests have been run on traffic lights with a fixed cycle time. This means that a group of signal phases occur repeatedly between fixed time intervals. The traffic lights in Antwerp, from which we will use the data, have a [variable cycle time](http://docs.wegenenverkeer.be/Publicaties/Brochure%20Verkeerslichtengeregelde%20kruispunten.pdf). Depending on the situation of the intersection, signal phases can be extended or shortened which influences its cycle time. However the algorithms described in related work for predicting future phases cannot be reused, some ideas can still be applied. [Ibrahim et al.](cite:cites 8500307) proposes a frequency distribution for the phase duration for every signal phase and fixed cycle time, because an intersection can have a different fixed cycle time for example during working days, than in the weekend. Bodenheimer et al. [](cite:cites 7325247) proposes to do this for time slots of 15 minutes and for the type of day (working or vacation day).
With a frequency distribution, a fixed predicted phase duration $$d_p$$ can be selected by using a method like the mean, mode and modus. Using the cumulative frequency distribution also allows predicting with a fixed probability [](cite:cites 6965983). For example: when 10% of the historic phase durations happened before the predicted phase duration $$d_p$$, so $$F(d_p) = 0.1$$, then we can say with a probability of 90% ($$1-F(d_p)$$) that the real phase duration $$d$$ will take longer than $$d_p$$.

<!-- The idea is that historical values are a good reflection of future phases, so future phases will have a similar frequency distribution. The chance that a real phase duration will happen before the predicted duration corresponds with $$P(d≤d_p) = F(d_p)$$. 

For example: it is 90% sure that a phase will take longer when choosing a phase duration as prediction that corresponds with the first 10% of the cumulative frequency distribution.

the probability $$a$$ that the real phase duration $$d$$ takes longer than the predicted duration $$d_p$$ ($$a = P(d>d_p))$$). By taking the cumulative frequency distribution of phase durations $$F$$, then the chance that the . We can calculate $$a$$ by taking the reverse with the formula: $$a = 1-F(d_p)$$. This allows predicting with a fixed  -->