# UWMedMarch22
Hello and welcome to the repo for the data processing and analysis for the data collected from UWMed ICUs on March 22nd.

The intended workflow for this repo is to interact with the data files via the jupyter notebooks. There are two jupyter notebook files in this repo as of 3/27, dataCleaning.ipynb and Analysis.ipynb. Below I will describe the function of both of these notebooks, as well as the other python files, and the purpose of each directory folder.

### dataCleaing.ipynb
This jupyter notebook is intended to be used to convert the raw.txt files that are collected from the sensors and convert them into .csv files with valid datetime object timestamps. The raw data collected from the sensors is not synchronized, and is in imperfect intervals i.e. one sensor will record every 10 seconds at 10:10:04, 10:10:14, 10:10:24 etc. etc. while another will be recording at 10:10:08, 10:10:18, 10:10:28. In this file we first are synchronizing the time intervals down to the nearest 10s place, and then using linear interpolation and 0 padding to increase the resolution of the data to 1 second intervals. In this file we also have to handle irregular gaps, different timezone settings on the sensors, and any look at diagnostic lists generated and stored inside the dataInfo directory to determine the quality of the collected data.
This notebook uses three python functions I created.
- fixYearStamp.py: this python function takes in the path to the incorrectly formatted raw sensor file, an example of the incorrect string, the correct date, indeces for the array positions of the full timestamp string, and finally the amount to shift the datestamp backwards. This function will parse through a file and for instance if you had datestamps misformatted, displaying 22/3/21 instead of 2021/3/22, will find all of these instances and convert them to the correct format, while simultaneously shifting their times back to the correct time zone if they are also off. This was created to fix and error where one sensor would shift forward 7 hours and change its date formatting in the file occasionally. 
- fillDf.py: this function will fill gaps in the sensors according to a set threshold. Anything below the time threshold will be interpolated, anything above 0 padded.
- cleanUp.py: this function removes 0/0/0 and other data before the specified cutoff, helps prep the file to be imported as a dataframe and merge the time and date columns into 1.

### Analysis.ipynb
This notebook is used to plot the data after it has been organized into csv files. It primarily uses matplotlib and custom specified colors and setting in order to create appealing graphs.


