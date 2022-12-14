# Detection of Ice Jam events using Interferometric Synthetic Aperture Radar (InSAR) along the Mohawk River, Schenectady County, New York, USA
# EAR:609: Environmental Data Science
December 16, 2022


# Introduction
	
	As satellite-based detection techniques become more advanced and widely accessible, their application to societal problems increases in relevancy
(Chaouch et al., 2012; Van der Sanden et al., 2020). In upstate New York, some of the most common environmental hazards to society are flooding events; as
such, application of satellite-acquired data used to predict and understand flooding events is beneficial to the state’s population. In the case of the 
Mohawk River in Schenectady County, New York, flooding due to winter ice jamming events is a persistent problem which has been monitored to some extent 
since the 1960s (Garver, 2018). In fact, ice jam-driven flooding events in the Mohawk River system are more common than flooding events driven by storm 
runoff during warmer months (Williams, 2019). This persistence of ice jamming events and the resulting geohazard that they pose to society has led to 
development of the Mohawk River Ice Jam Monitoring project, a network of four United States Geological Survey (USGS) stream gages and monitoring sites 
across an approximately 15-mile span of the Mohawk River. While this monitoring system has been incredibly helpful in detecting and studying ice jams as 
they occur on the Mohawk River, this kind of infrastructure is not available in most river systems across the Northeast United States, where the threat of 
ice jam-related flooding also exists. This project aims to evaluate whether Sentinel-1 satellite-derived Interferometric Synthetic Aperture Radar (InSAR) 
can be used to detect and study ice jamming events that could potentially lead to flooding. 
	Ice jamming events are chronic along the Mohawk River in Schenectady County for several reasons. These include the low gradient of the river near 
Schenectady, both natural and man-made channel constriction, and the emplacement of the Vischer Ferry Dam, which creates a backup of water for 
approximately 10 miles along the channel (Garver and Cockburn, 2018). Four stream gages have been put in place in this area in order to monitor stream 
stage conditions: the Lock 8 gage (ID# 01354500), the Freeman’s Bridge gage (ID# 01354500), the Rexford gage (ID# 01355475), and the Vischer Ferry gage 
(ID# 01356000). This study specifically focuses on the ice jamming event that resulted from a mid-winter thaw and heavy rain event on January 23, 2019. 
This caused three ice jams to develop between the channel area northwest of Lock 8 up until the Vischer Ferry Dam (Figure 1). A subsequent thaw event on 
February 6 caused two of the smaller ice jams to collide into one approximately 8-mile-long ice jam northwest of Freeman’s Bridge. This event caused 
flooding in low-lying areas due to backup of water within the channel (Garver, 2019). This ice jamming and flooding event was identified using the Cold 
Regions Research Engineering Laboratory (CRREL) Ice Jam Database (https://icejam.sec.usace.army.mil/). The following study aims to determine whether these 
2019 ice jam and breakup events can be detected within SAR Sentinel-1 satellite data.


# Data and Methods

	This study used C-band radiation data collected by the Sentinel-1 satellite with both VV and VH polarization. These data were acquired via the 
Copernicus Open Access Hub (Copernicus Sentinel data, 2010). Sentinel-1 data products were generated using the Alaska Satellite Facility (ASF) data 
processing hub, which allows for fast, cloud-based processing of InSAR products. The Sentinel-1 satellite has a temporal resolution of 12 days; this means 
that for this study, three time-stamped SAR images were available from late January to mid-February 2019. Using the baseline tool from the ASF, two time-
referenced InSAR interferograms and vertical displacement maps were generated: January 26 to February 7, 2019, and February 7 to February 19, 2019. A 
shapefile of the Mohawk River channel geometry was obtained from the New York State Geographical Information Systems Data Repository 
(https://gis.ny.gov/gisdata/inventories/details.cfm?DSID=928). Polygons were drawn in QGIS within the Mohawk River channel around each of the four USGS 
stream gages. These polygons were then imported into python, and vertical displacement data were retrieved using the zonal statistics function. This 
produced average values of the change in vertical displacement at the given point over the image time period.  A pandas dataframe with these vertical 
displacement values, the start date and end date of the time period, and the location of each average value was prepared for analysis.
	In order to test the reliability of Sentinel-1 derived vertical displacement values, USGS stream gage data for the same time period from January
26 to February 19, 2019 were retrieved from the USGS National Water Information System web interface (NWIS; Sauer and Turnipseed, 2010). Stream stage 
height for each of the four gages was imported into python using the climata.usgs package. Imported daily average stream stage heights are plotted in 
Figure 2 using matplotlib (Hunter, 2007). These daily averages were converted from feet to meters to match the Sentinel-1 images. The change in vertical 
displacement recorded by the stream gages was calculated at the same interval as the Sentinel-1 images: from January 26 to February 7, 2019, and from 
February 7 to February 19, 2019. A pandas dataframe with vertical displacement calculated from stream stage in meters, the start date and end date of 
acquisition, and the stream gage name was assembled for analysis.
	An ordinary least squares regression was calculated for the stream gage-derived vertical displacement value versus the Sentinel-1 calculated 
vertical displacement in the Mohawk River channel for both of the measured timestamps (Figure 3). This statistical model was generated in matplotlib and 
seaborn. Other statistical aspects of the data, including skew, kurtosis, and residuals were explored using matplotlib (Hunter, 2007).

# Results
 
	USGS gage monitoring of stream stage height demonstrates a fall in stream stage from January 26 to February 1, 2019. Stream stage was high just 
before the studied time period, corresponding to the thaw event described by Garver (2019) on January 23, which caused ice breakup. Stream stage climbs 
again from February 1 to February 8, 2019, where Garver (2019) identified a second thaw and breakup event, which resulted in an 8-mile-long jam and 
flooding in low lying areas. From February 8, stream stage falls again and flattens out until the end of the studied period on February 19. Stream stage 
height measured via USGS gages corresponds to location within the channel; Lock 8, the furthest gage upstream, measures the highest stream stage. Stream 
stage during this time period decreases moving downstream within the Mohawk River. This is typical of river systems which are blocked with ice jams; 
upstream areas backfill due to the resistance to flow downstream, resulting in a positive gradient in stream stage from the downstream area to the upstream 
area (Garver, 2018; Van der Sanden et al., 2020).
	During the first timestamp, from January 26 to February 7, 2019, vertical displacement values calculated by the InSAR images showed a positive 
increase in vertical displacement. This is contrary to the data collected by USGS stream gages. Within this data, there does not appear to be a pattern 
reflective of the position within the channel. Measured vertical displacement within the channel actually increases downstream until the Vischer Ferry 
area, where displacement decreases. During the second timestamp from February 7 to 19, 2019, vertical displacement values calculated from InSAR images   
were negative, with an average value of -0.015 meters between the four stream gage locations. Similar to the previous timestamp, there does not appear to 
be a predictable relationship between position within the channel and the magnitude of vertical displacement calculated via the InSAR imagery. The lowest 
magnitude displacement value was obtained at the Freeman’s Bridge area, which in the previous timestamp contained the highest magnitude vertical 
displacement value.
	An ordinary least squares regression of vertical displacement from stream gages versus that from InSAR yields an R2 value of 0.441, a slope of 
0.200, and p-value of 0.073 (Figure 3). The R2 value and slope indicate that there is a positive correlation between stream gage and InSAR-derived 
vertical displacements. However, the p-value of greater than 0.05 indicates that this relationship is not statistically significant.

# Discussion
	 
	These results suggest difficulty in using InSAR images from Sentinel-1 to measure vertical displacement in stream channels, and as such difficulty 
to predict or study ice jamming events. Figure 3 shows the regression line plotted on top of a 1:1 line. In the ideal situation, regression between 
vertical displacement measured by stream gages versus that measured by InSAR should have a positive slope of 1, indicating that the measured values by 
both methods are the same. This is clearly not the case for these images generated by InSAR, where at times the vertical displacement value calculated is 
positive rather than negative. Additionally, the vertical displacement values calculated from the InSAR images are sometimes an order of magnitude lower 
than those measured by the USGS stream gages. Figure 4 is a histogram of the difference (stream gage vertical displacement – InSAR vertical displacement) 
between the measured values of the two methodologies. This makes the difference in measured value between stream gages and InSAR images apparent, 
especially in the case of Lock 8, which experiences a large magnitude change in vertical displacement from February 7 to 19, 2019 according to the stream 
gage data. This signal is not reflected in the InSAR generated vertical displacement maps.
	Another feature that complicates the applicability of InSAR data for studying ice jamming events is the long temporal resolution of the Sentinel-1 
satellite. For example, the Sentinel-1 satellite passed the study area on February 7. Over the next two days, stream stage on the Mohawk River peaked 
corresponding with the second thaw and breakup event described by Garver (2019). As a result, the Sentinel-1 calculated vertical displacement does not 
capture the maximum magnitude of vertical displacement. This may be an indication that ice jam and breakup events occur on an incompatible time-scale to 
the 12-day resolution of the Sentinel-1 satellite, and that key identifying features of ice jamming events may be obscured in InSAR datasets.
	Previous work has demonstrated that there may in fact be a relationship between stream gage-derived vertical displacement and that from Sentinel-1 
imagery (Van der Sanden et al., 2020). It should be noted that this study of the ice jam events in mid-winter 2019 consists of two baseline images 
composed of a total of three Sentinel-1 passes, both of which have relatively low coherence overall (max coherence ~0.10). The positive slope generated 
between stream gage and Sentinel-1 data may demonstrate that there is some relationship between the two measurements. In terms of fit, the residuals from 
the calculated regression do not appear to have a spatial pattern and are normally distributed. In terms of applicability to other systems, acquiring 
vertical displacement maps from Sentinel-1 InSAR images may be useful when used in conjunction with stream gage data. Because of the order of magnitude 
difference, without ground truth stream gage data it seems unlikely that this method can be developed to accurately predict the magnitude of vertical 
displacement change, and therefore the risk of flooding.

# Conclusions
 	
	The aim of this study was to compare the vertical displacement values calculated from Sentinel-1 InSAR images and primary measurements of stream 
stage height from USGS stream gages in order to assess whether a change in vertical displacement along a river channel indicative of flooding risk can be 
identified using satellite imagery. If successful, this would allow for freely available data on flooding risks due to ice jamming events without the 
expensive and time-consuming infrastructure of stream gage networks. However, study of the mid-winter ice jam event of 2019 on the Mohawk River calls into 
question the applicability of this technique; vertical displacement calculated via Sentinel-1 images did not have a statistically significant relationship 
with in-situ measured stream stage from USGS stream gages. In this study, InSAR was not able to detect a pattern in vertical displacement change relative 
to position within the Mohawk River channel, which is one of the main predictive features used to identify flooding risk. This study is somewhat 
inconsistent with previous results; future studies should evaluate factors such as image coherence, increased temporal resolution, and pairing with a 
small network of stream gages in order to further assess the viability of this method.

# References

Chaouch, Naira, et al., 2012, An Automated Algorithm for River ICE Monitoring over the Susquehanna River Using the MODIS Data, Hydrological Processes, vol. 28, no. 1, pp. 62–73., doi:10.1002/hyp.9548.

Garver, J.I., and Cockburn, J.M.H., “A Historical Perspective of Ice Jams on the Lower Mohawk River.” Proceedings of the 2009 Mohawk Watershed Symposium, Union College, Schenectady, NY

Garver, J.I., 2018, Ice Jam flooding on the lower Mohawk River and the 2018 mid-winter ice jam event. In: Cockburn, J.M.H. and Garver, J.I., Proceedings from the 2018 Mohawk Watershed Symposium, Union College, Schenectady NY, 23 March 2018, v. 10, p. 13-18.

Garver, J.I., 2019, The 2019 mid-winter ice jam event on the lower Mohawk River, New York, Proceedings of the 2019 Mohawk Watershed Symposium, Union College, Schenectady, NY, March 22, 2019, v. 11, p. 12-17. 

Hunter, J.D., "Matplotlib: A 2D Graphics Environment," in Computing in Science & Engineering, vol. 9, no. 3, pp. 90-95, May-June 2007, doi: 10.1109/MCSE.2007.55.

Sauer, V.B., and Turnipseed, D.P., 2010, Stage measurement at gaging stations: U.S. Geological Survey Techniques and Methods book 3, chap. A7, 45 p. (Also available at https://pubs.usgs.gov/tm/tm3-a7/.)

Van der Sanden, J.J., et al. “An Automated Procedure to Map Breaking River Ice With C-BAND Hh Sar Data.” Remote Sensing of Environment, vol. 252, 7 Oct. 2020, p. 112119., doi:10.1016/j.rse.2020.112119.

Williams, Stephen, “New study sought of flooding impact of Vischer Ferry Dam near Schenectady: FERC can require studies for Vischer Ferry dam relicensing; NYPA doesn’t think it’s necessary,” The Daily Gazette, Schenectady, NY, December 14, 2019.

  
