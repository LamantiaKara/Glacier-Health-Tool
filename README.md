# Glacier-Snowline-Tool
**If you use this tool please cite XXXXX**

The Glacier Snowline Tool is a Google Earth Engine Tool for assessing yearly glacier health metrics (total area, snow covered area, snowline elevation, and accumulation area ratio) from Landsat imagery. More details on the tools, its structure, and validation can be found in the associated paper (XXXXX). 

## How to use the Glacier Snowline Tool

The following provides a step by walkthrough of the Glacier Snowline Tool and demonstrates its functions. If you have never used Google Earth Engine before you will need to [create a Google Earth Engine account](https://console.cloud.google.com/earth-engine/welcome) and *register for a non-commercial cloud project* before you are able to access the tool. This will include answering a few questions to ensure you qualify (all research and education purposes are covered), and you will only need to do this the first time you use Google Earth Engine. Use of the Glacier Snowline tool is not permitted for commerical purposes, please contact the authors if you are a user who wants to proceed under commercial purposes. 

## Getting Started: Choose a Dataset

The Glacier Snowline Tool runs through Google Earth Engine using JavaScript API. To access the tool click [here](https://code.earthengine.google.com/3dc8385812f74001207dc0d3d171fb1f). Once opened, a welcome page will appear as shown below, prompting you to select either the RGI Glacier outlines or the RGI Complex Outlines. You will need to click on your preferred dataset, and it will load it into the tool.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/welcomeScreen.png?raw=true)

## Step 1: Select a Glacier ROI

Once the preferred dataset is loaded the console will print the dataset select and you will be able to toggle between the map or satellite layers as the basemap to zoom into your area of interest. The Glacier Snowline Tool is set up for a 'point and click' selection where you will use the mouse pointer to click within the glacier outline. The tool will then select the outline, reload only the selected outline, display it in red, and set it as the ROI with a 100 meter buffer. The console will print the RGI ID number.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectGlacier.png?raw=true)

## Step 2: Set Parameters for Imagery Collection

The Glacier Snowline Tool loads with a panel on the left to enable the user to adjust parameters for imagery selection. You will be prompted to enter a glacier name for file export purposes. The other parameters are purely for imagery collection including start and end year, target month of interest, cloud cover, and minimum sun angle. Once selected, the you are able to click the 'Collect Imagery' button and the Glacier Snowline Tool will display the first image collected in RGB as well as printing out how many total images fit the criteria, the final yearly images selected, and a list of cloud cover percentages for each year (see below). You can adjust the parameters and re-run 'Collect Imagery' process as many times as needed until you are confident your selection is satisfactory. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/collectImagery.png?raw=true)

## Step 3: Choose Parameters for Image Analysis - DEM

After you have completed the imagery selection, you will need to choose a DEM source under the 'Processing Options' panel. This is available via a dropdown menu with the DEM options including version 4 of ArcticDEM and the COPDEM for global coverage. In the event of ArcticDEM being selected for a glacier not within the bounds of the DEM an error message will print in the console. Conversely, confirmation will print in the console if the DEM chosen covers the selected glacier. See below for an example of a non Arctic located glacier where ArcticDEM was intially chosen and then corrected to COPDEM.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectDEM.png?raw=true)

## Step 4: Choose Parameters for Image Analysis - Masking Strength

The masking selection uses a technique to remove surrounding bedrock and water with a thermal band to blue band ratio and a threshold of the blue band [Mousssavi et al., 2020](https://www.mdpi.com/2072-4292/12/1/134). You have the option to choose a 'light', 'normal', or 'aggresive' mask, or turn it off completely. The thresholds for each of these are as follows: light (thermal/blue >0.9 & blue <0.1), normal (thermal/blue >0.9 & blue <0.2), and aggressive (thermal/blue >0.85 & blue <0.2). When chosen, the respective ratio will print on the console, of if turned off, the console will print 'Masking Disabled.'

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectMask.png?raw=true)

## Step 5: Run Analysis

After all the above parameters are selected, your next step is to click the 'Run Analysis' button to produce the yearly health metrics for your selected glacier. The map will display the first image analyzed with the snow cover (light green) and total area (blue) as filled polygons. The console will print a sample of the first year's results with all the calculated variables and their respective uncertainty errors, the total amount of images analyzed, and a note that the analysis is complete. If the user goes back to Steps 3 & 4 and changes parameters to re-run the analysis, the map will clear with each run but the console will continue to print underneath each new output. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/runAnalysis.png?raw=true)

## Step 6: Export Results

Once you have obtained the analysis results, the final step is to export all data. The Glacier Snowline Tool generates four export tasks including 1) a csv file with all the imagery information, the calculated yearly health metrics, and uncertainty error, 2) a csv file of the snow cover area binned into 50 meter elevation bins, and 3) yearly shapefiles of the snow cover and 4) total area. To initiate these exports, select the 'Tasks' tab (right of the 'Console' tab) and click the 'Run' button next to one of the tasks. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/exportTasks.png?raw=true)

You will be prompted with an export window that will preset the file name and google drive destination folder. These parameters are editable in the export window if you would like to change the file or folder names. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/exportTask.png?raw=true)

Select the 'Run' button to begin the export and the task will appear under 'Submitted Tasks' in the console. While the data is being exported, you will have to wait. Once completed, the tasks will change from a grey fill to a blue fill and the files will be available in their respective GoogleDrive folders. See below for an example of three completed tasks and one still running.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/taskCompleted.png?raw=true)

After all the tasks haved finished, this means you are done! You have completed all the steps to acquiring your yearly snowline data from the Glacier Snowline Tool. 

## Acknowledgements

This readme file was written by Kara Lamanta (Ohio State University). Any questions or queries should be directed to her.

## Disclaimer

Data in the Glacier Snowline Tool are provided as given, and the authors take no responsibility for how data extracted are used. The Glacier Snowline Tool is strictly intended for non-commercial use.
