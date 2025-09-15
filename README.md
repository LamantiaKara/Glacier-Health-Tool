# Glacier-Snowline-Tool
**If you use this tool please cite XXXXX**

The Glacier Snowline Tool is a Google Earth Engine Tool for assessing yearly glacier health metrics (total area, snow covered area, snowline elevation, and accumulation area ratio) from Landsat imagery. More details on the tools, its structure, and validation can be found in the associated paper (XXXXX). 

## How to use the Glacier Snowline Tool

The following provides a step by walkthrough of the Glacier Snowline Tool and demonstrates its functions. If you have never used Google Earth Engine before you will need to [create a Google Earth Engine account](https://console.cloud.google.com/earth-engine/welcome) and *register for a non-commercial cloud project* before you are able to access the tool. This will include answering a few questions to ensure you qualify (all research and education purposes are covered), and you will only need to this the first time you use Google Earth Engine. Use of the Glacier Snowline tool is not permitted for commerical purposes, please contact the authors if you are a user who wants to proceed under commercial purposes. 

## Getting Started

The Glacier Snowline Tool runs through Google Earth Engine using JavaScript API. To access the tool click [here](https://code.earthengine.google.com/693c4d3f153208fbe5ea13255247e190). Once opened, a welcome page will appear as shown below, prompting the user to select either the RGI Glacier outlines or the RGI Complex Outlines. The user will need to click on their preferred dataset to load it into the tool.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/welcomeScreen.png?raw=true)

## Step 1: Select a Glacier ROI

Once the preferred dataset is loaded the console will print the dataset select and the user will be able to toggle between the map or satellite layers as the basemap to zoom into their general area of interest. The Glacier Snowline Tool is set up for a 'point and click' selection where the use needs to use the mouse pointer to click within the glacier outline. The tool will then select the outline, reload only the selected outline, display it in red, set it as the ROI with a 100 meter buffer, and the console will print the RGI ID number.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectGlacier.png?raw=true)

## Step 2: Set Parameters for Imagery Collection

The Glacier Snowline Tool loads with a panel on the left to enable the user to adjust parameters for imagery selection. You will be prompted to enter a glacier name for file export purposes. The other parameters are purely for imagery collection including start and end year, target month of interest, cloud cover, and minimum sun angle. Once selected, the user can click the 'Collect Imagery' button and the Glacier Snowline Tool will display the first image collected in RGB as well as printing out how many total images fit the criteria, the final yearly images selected, and a list of cloud cover percentages for each year (see below). the user is able to adjust and re-run the 'Collect Imagery' process as many times as needed until they are pleased with their selection. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/collectImagery.png?raw=true)

## Step3: Choose Parameters for Image Analysis - DEM

After the user has completed the imagery selection, they will be asked to choose a DEM source under the 'Processing Options' panel. This is available via a dropdown menu with the DEM options including version 4 of ArcticDEM and the COPDEM for global coverage. In the event of ArcticDEM being selected for a glacier not within the bounds of the DEM an error message will print in the console. Conversely, confirmation will print in the console if the DEM chosen covers the selected glacier. See below for an example of a non Arctic located glacier where ArcticDEM was intially chosen.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectDEM.png?raw=true)

## Step 4: Choose Parameters for Image Analysis - Masking Strength

The masking selection uses a technique to remove surrounding bedrock and water with a thermal band to blue band ratio and a threshold of the blue band [Mousssavi et al., 2020](https://www.mdpi.com/2072-4292/12/1/134). The user has the option to choose a 'light', 'normal', or 'aggresive' mask, or turn it off completely. The threshold ratios for each of these thresholds are as follows: light (thermal/blue >0.9 & blue <0.1), normal (thermal/blue >0.9 & blue <0.2), and aggressive (thermal/blue >0.85 & blue <0.2). When chosen, the respective ratio will print on the console, of if turned off, the console will print 'Masking Disabled.'

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/selectMask.png?raw=true)

## Step 5: Run Analysis

After all the above parameters are selected, the user is able to select the 'Run Analysis' button to complete the snowline assessment and gather yearly health metrics for the selected glacier. The map will display the first image analyzed with the snow cover (light green) and total area (blue) as filled polygons. The console will print a sample of one year's results with all the calculated variables and their respective uncertainty errors, the total amount of images analyzed, and a note that the analysis is complete. If the user goes back to Steps 3&4 and changes parameters to re-run the analysis, the map will clear with each run but the console will continue to print underneath each new selection/output. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/runAnalysis.png?raw=true)

## Step 6: Export Results

Once the use is statisfied with the analysis results, the final step is to export the results. The Glacier Snowline Tool generates four exports including a csv file with all the imagery information, the calculated yearly health metrics and uncertainty error, a csv file of the snow cover area binned into 50 meter elevation bins, and yearly shapefiles of the snow cover and total area. To initiate these exports, select the 'Tasks' tab (right of the 'Console' tab) and click the 'Run' button next to one of the tasks. The user will be prompted with an export window that will preset the file name and google drive destination folder. These parameters are editable if the user so chooses. 

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/exportTask.png?raw=true)

Select the 'Run' button to begin the export and the task will appear under 'Submitted Tasks' in the console. While the data is being exported, the user will have to wait. Once completed, the tasks will change from a grey fill to a blue fill and the files will be available in their respective GoogleDrive folders. See below for three completed tasks and one still running.

![image](https://github.com/LamantiaKara/Glacier-Snowline-Tool/blob/main/images/taskCompleted.png?raw=true)

After all the tasks haved finished, this means you are done! You have completed all the steps to acquiring your yearly snowline data from the Glacier Snowline Tool. 

## Acknowledgements

This readme file was written by Kara Lamanta (Ohio State University) and is responsible for the accuracy of the Glacier Snowline Tool description above. Any questions or queries should be directed to her.

## Disclaimer

Data in the Glacier Snowline Tool are provided as given, and the authors take no responsibility for how data extracted are used. The Glacier Snowline Tool is strictly intended for non-commercial use.
