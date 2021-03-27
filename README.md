# UWMedMarch22
Hello and welcome to the repo for the data processing and analysis for the data collected from UWMed ICUs on March 22nd.

The intended workflow for this repo is to interact with the data files via the jupyter notebooks. There are two jupyter notebook files in this repo as of 3/27, dataCleaning.ipynb and Analysis.ipynb. Below I will describe the function of both of these notebooks, as well as the other python files, and the purpose of each directory folder.

### dataCleaing.ipynb
This jupyter notebook is intended to be used to convert the raw.txt files that are collected from the sensors and convert them into .csv files with valid datetime object timestamps. The raw data collected from the sensors is not synchronized, and is in imperfect intervals i.e. one sensor will record every 10 seconds at 10:10:04, 10:10:14, 10:10:24 etc. etc. while another will be recording at 10:10:08, 10:10:18, 10:10:28. In this file we first are synchronizing the time intervals down to the nearest 10s place, and then using linear interpolation and 0 padding to increase the resolution of the data to 1 second intervals. In this file we also have to handle irregular gaps, different timezone settings on the sensors, and any look at diagnostic lists generated and stored inside the dataInfo directory to determine the quality of the collected data.
This notebook uses three python functions I created.
- fixYearStamp.py 
- fillDf.py 
- cleanUp.py.

fixYearStamp.py 
