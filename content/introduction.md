## Introduction
{:#introduction}

During 2018, the city of Antwerp has invested in connecting the traffic lights controller of one intersection to the Internet. With the Open Traffic Lights project[](cite:cites vandevyvere_mepdaw_2019), these data have been published on the Web as Linked Open Data setting the foundation for reuse. Typically, the phase and timing of a traffic light is used for [Green Light Optimal Speed Advisory (GLOSA)](cite:cites 6799846) systems to save fuel through speed advice or count-down timer [](cite:cites dynamiceco). While GLOSA systems focus on the event of approaching an intersection, routeplanners have a more global view of the journey where fuel savings is only one parameter. 
Implementing live features like these on the server-side requires a much more complex technology stack than traditional origin-destination route planning queries requiring permanent tracking of the user.
Recently, work has been done on generic routeplanning clients for [public transport](cite:cites colpaert_icwe_2017) and [road networks](colpaert_eswc_demo_2019) performing the route planning algorithm on the client-side. Extending such a client with the consumption of traffic lights data introduces challenges, such as forecasting the phase duration[](cite:cites spat_amsterdam). 

serverless route planning

<!-- In this paper, we describe how routeplanners can discover, integrate and predict traffic lights data. First, we describe in related work how traffic lights data are structured and how its phase duration can be predicted. Next, we describe how routeplanners can discover and integrate traffic lights data and how predictions can be made from the Open Traffic Lights data. Then we demonstrate with a  proof-of-concept. -->
