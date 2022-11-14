# IceJamProjectFall2022

Research question: 
Can Sentinel-1 Interferometric Spectral Aperture Radar (InSAR) data be used to accurately detect conditions of ice jam formation in frozen channels (i.e., emergent slopes) in the Mohawk River system in New York state? 

This study will focus specifically on the years 2016-2020 in order to evaluate whether InSAR data can be used to predict the occurrences of historic ice jam formation on the Mohawk River. The level of accuracy (i.e., the correlation of fit between emergent slope prediction and ice jam formation) will additionally be assessed throughout this period.

Data source description: 
This study will utilize Interferometric Spectral Aperture Radar (InSAR) data collected by the Sentinel-1 satellite. The data will be acquired using the Copernicus Open Access Hub (Copernicus Sentinel data, 2010) and the Alaska Satellite Facility (ASF, https://storymaps.arcgis.com/stories/68a8a3253900411185ae9eb6bb5283d3), which allows for fast, cloud-based processing of InSAR products from Sentinel-1.  Sentinel-1 collects C-band radiation, which is useful for this study in that it is not limited by cloud cover and can detect the presence of wet snow. Sentinel-1 data from the winters of 2015-2020 in the vicinity of the Mohawk River will be analyzed in October and November of 2022. 

Additionally, data about historic ice jams in the years 2015-2020 will be collected from the Cold Regions Research Engineering Laboratory (CRREL)’s Ice Jam Database (https://icejam.sec.usace.army.mil/).


Data processing and model description:
Sentinel-1 SAR datafiles from the winter seasons of 2015-2020 will be processed according to data availability (the 12-day temporal resolution of Sentinel-1). InSAR interferograms indicating vertical displacement in the Mohawk River channel at each interval will be generated using the ASF’s “InSAR on Demand.” Vertical displacement, and its predicted magnitude using SAR will be measured. Periods of rapid increase in vertical displacement over time will be compared with the CRREL database of ice jam formation in order to assess whether this variable can be used to predict ice jam formation. The effectiveness of InSAR measurement of vertical displacement will be assessed by comparison of InSAR measurements with USGS stream gauge measurements of channel flow, specifically those made by stationary sensors fixed to bridges. Fit between the InSAR measurements and those of the USGS stream gages at predicted ice jam events will be compared via linear regression. All data will be processed in Python. 


File structure:
  IceJamProjectFall2022_data.ipynb
    A dataset of Sentinel-1 InSAR image folders generated from the Alaska Satellite Facility (ASF). Of interest are vertical displacement(_vert_disp) and       coherence (_corr) maps within a given folder.
  
  2019_2020_IceJamProjectFall2022.ipynb
    Python script for data download, image plotting, and masking for InSAR data from the winter of 2019-2020. Vertical displacement maps are masked with by     coherence values of greater than 0.8.

  2018_2019_IceJamProjectFall2022.ipynb
    Python script for data download, image plotting, and masking for InSAR data from the winter of 2018-2019. Vertical displacement maps are masked with by     coherence values of greater than 0.8.
  
 2017_2018_IceJamProjectFall2022.ipynb
    Python script for data download, image plotting, and masking for InSAR data from the winter of 2017-2018. Vertical displacement maps are masked with by     coherence values of greater than 0.8.
    
 2016_2017_IceJamProjectFall2022.ipynb
    Python script for data download, image plotting, and masking for InSAR data from the winter of 2016-2017. Vertical displacement maps are masked with by     coherence values of greater than 0.8.
  
  
