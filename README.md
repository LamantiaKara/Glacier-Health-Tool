# Glacier-Health-Tool v1 (2026)
**If you use this tool please cite [our preprint here](https://eartharxiv.org/repository/view/12615/)**

## To use this tool click [here](https://code.earthengine.google.com/a06a61e63c9dc0615ec8e823628e24e0).

The Glacier Health Tool is a Google Earth Engine tool for assessing yearly glacier health metrics (total area, snow-covered area, snowline elevation, and accumulation area ratio) derived from Landsat imagery. More details about the tool, its structure, and its validation can be found in the [associated preprint](https://eartharxiv.org/repository/view/12615/). 

## How to use the Glacier Health Tool

The following provides a step by step walkthrough of the Glacier Health Tool and demonstrates its functions. If you have never used Google Earth Engine before you will need to [create a Google Earth Engine account](https://code.earthengine.google.com/a06a61e63c9dc0615ec8e823628e24e0) and *register for a non-commercial cloud project* before you are able to access the tool. This will include answering a few questions to ensure you qualify (all research and education purposes are covered), and you will only need to do this the first time you use Google Earth Engine. Detailed instructions for signing up are available [here](https://courses.spatialthoughts.com/gee-sign-up.html). The Glacier Health Tool is provided under a Creative Commons Attribution-NonCommercial license. Commercial use is not permitted without prior permission from the authors. Users seeking to use the tool for commercial purposes must contact the authors to obtain permission.

## Getting Started - Step 1: Choose a Dataset

The Glacier Health Tool runs through Google Earth Engine using JavaScript API. To access the tool click [here](https://code.earthengine.google.com/a06a61e63c9dc0615ec8e823628e24e0). Once opened, a welcome page will appear as shown below, prompting you to select either the RGI glacier product or the RGI glacier complex product (RGI v7.0). You will need to click on your preferred dataset, and it will load it into the tool's map view.

If the user prefers to load the RGI glacier dataset (complex is not yet available) themselves, the GEE Community Catalog provides instructions [here](https://gee-community-catalog.org/projects/rgi/?h=rgi). 

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/welcomeScreen.png?raw=true)

## Step 2: Select a Glacier ROI and Set a Buffer

Once the preferred dataset is loaded the console will print the dataset selected and you will be able to toggle between the map or satellite layers as the basemap to zoom into your area of interest. The Glacier Health Tool is set up for a 'point and click' selection where you will use the mouse pointer to click within the glacier outline. The tool will then select the chosen glacier RGI outline, print the RGI ID number in the console, and display a default 50 m buffer in red. At the bottom right of the screen, the allows for the user to toggle the buffer, in 50 m increments from 0 to 200 m. If changed, the map will reload and display the buffer with the original RGI outline. The buffer will not include any nearby RGI outlines to avoid overlap in highly glaciated areas.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/selectGlacier.png?raw=true)

## Step 3: Set Parameters for Imagery Collection

The Glacier Health Tool loads with a panel on the left to enable the user to adjust parameters for imagery selection. You will be prompted to enter a glacier name for file export purposes. The other parameters are to set preferences for imagery collection including start and end year, target month of interest, cloud cover, and minimum sun angle. Once selected, you will be able to click the 'Collect Imagery' button and the Glacier Health Tool will display the first image collected in RGB and print the total number of images that meet the criteria, the final yearly images selected, and a list of cloud cover percentages for each year (see below). You can adjust the parameters and re-run 'Collect Imagery' process as many times as needed until you are confident your selection is satisfactory. 

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/collectImagery.png?raw=true)

## Step 4: Choose Parameters for Image Analysis - DEM

After you have completed the imagery selection, you will need to choose a Digital Elevation Model (DEM) source under the 'Processing Options' panel. This is available via a dropdown menu with the DEM options including ArcticDEM version 4 and the 30m COPDEM for global coverage. In the event ArcticDEM is selected for a glacier not within the bounds of the DEM, an error message will print in the console alerting the user that this DEM does not cover the selected glacier. Conversely, confirmation will print in the console if the DEM chosen covers the selected glacier. See below for an example of a non Arctic located glacier where ArcticDEM was intially chosen and then corrected to COPDEM.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/selectDEM.png?raw=true)

## Step 5: Choose Parameters for Image Analysis - Masking Strength

The next step involves the masking selection, which removes surrounding bedrock and water so the analysis is focused only on snow and ice. This is accomplished with ratios and thresholds of the thermal and blue band, following the approach documented in [Mousssavi et al., 2020](https://www.mdpi.com/2072-4292/12/1/134). You can choose a 'light', 'moderate', or 'high' mask, or turn it off entirely. This option will control how aggressively non-ice areas are removed. The thresholds used are:
      - Light (thermal/blue >0.9 & blue <0.1)
      - Moderate (thermal/blue >0.9 & blue <0.2)
      - High (thermal/blue >0.85 & blue <0.2)
When a mask is chosen, the respective thresholds will print on the console. If turned off, the console will print 'Masking Disabled.' See below for an example where 'Moderate' was initially chosen, and then the masking was turned off.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/selectMask.png?raw=true)

## Step 6: Run Analysis

After all the above parameters are selected, click the 'Run Analysis' button to produce the yearly health metrics for your selected glacier. The map will display the first image analyzed with the snow cover (light green) and total area (blue) as filled polygons. The console will print the results for the first analyzed year, including all calculated variables, uncertainties (reported in the relevant units but derived from fixed percentages), the total number of images analyzed, and a note indicating the analysis is complete. If the user goes back to Steps 3-5 and changes parameters to re-run the analysis, the map will clear with each run but the console will continue to print underneath each new output. If the user wants to change DEM or masking options, Run Analysis can be run as many times as the user prefers, similar to Collect Imagery.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/runAnalysis.png?raw=true)

## Step 7: Export Results

Once you have obtained the analysis results, the final step is to export all data. The Glacier Health Tool generates five export tasks including 1) a csv file with all the imagery information, the calculated yearly health metrics, and uncertainties, csv files of the 2) snow cover area and 3) total area binned into 50 meter elevation bins, and 4) shapefiles of the yearly snow cover and 5) total area. To initiate these exports, select the 'Tasks' tab (right of the 'Console' tab) and click the 'Run' button next to one of the tasks. See below for a sample of these export tasks.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/exportTasks.png?raw=true)

You will be prompted with an export window that will preset the file name and google drive destination folder. These parameters are editable in the export window if you would like to change the file or folder names. The folder will be generated in your Google Drive if it does not already exist.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/sampleExportTask.png?raw=true)

Select the 'Run' button to begin the export and the task will appear under 'Submitted Tasks' in the console. While the data is being exported, you will have to wait (only a few minutes!). Once completed, the tasks will change from a grey fill to a blue fill and the files will be available in their respective GoogleDrive folders. See below for an example of two completed tasks and three submitted but still running.

![image](https://github.com/LamantiaKara/Glacier-Health-Tool/blob/main/images/taskCompleted.png?raw=true)

Once all taks have finished, the process is complete. You have successfully acquired the yearly glacier health metrics generated by the Glacier Health Tool. 

## Acknowledgements

This readme file was written by Kara Lamantia (University of Bristol). Any questions or queries should be directed to her.

## Disclaimer

Data in the Glacier Health Tool are provided as given, and the authors take no responsibility for how data extracted are used. 

## License

This project is licensed under the Creative Commons
Attribution–NonCommercial–ShareAlike 4.0 International License.

See the [LICENSE](LICENSE) file for details.

© 2026 Kara Lamantia
