# 2019-automated factsheets for sediment (& phosphorus input) into waterbodies
## (based on a 20 year long soil erosion database in the region of Frienisberg, Switzerland)

Author: David Remund 13-104-591, University of Berne, Seminar Geodata analysis and modelling (Springsemester 2019)

## aim of the scripts:

The aim of the scripts is to make PDF overview sheets that show for so called region-period objects (e.g. Frienisberg 1997-2007) important information about sediment & phosphorus input.

## methodical realization:

The aim is reached with 4 scripts. The first script makes a treelike output folder structure for the input data (which was already calculated beforehand in this case). The second script copies initial the sediment (phosphorus) input rasters to the right destination folder in the created treelike output folder structure. Some rasters are had to be summed up prior to the copying process. The third script checks if some "strange rasters" have been created during the copying process (probably these strange rasters are temporary storage files). If a strange raster should be detected, then this script deletes them. The fourth and last script calculates afterwards the total sum [t] and the mean annual input [t/ha*a] and makes boxplots as well as timeseries. All the calculated elements are drawn together on a PDF sheet.

## used software:

The programming was done with Python 3.6 in the IDE PyCharm 2018.2.5 Community Edition.

## workflow

The workflow of this project consists of four scripts and is the same for sediment & phosphorus input. Therefore the workflow is only explained for the sediment input. 
(remark for the lecturer: Only the sediment input scripts are commented comprehensibly. Therefore, please only grade the scripts for the sediment input (for phosphorus input, the script that sould check strange rasters wasn't implemented, because the check was done manually))

The first script is called make_db_structure_SE.py, the second copy_management_SE.py, the third check_strange_rasters.py and the fourth and last one create_pdf_spreadsheet_SE.py. (for phosphorus input check the corresponding _PE.py scripts). 

*script 1: make_db_structure_SE.py*

This script creates for each region-period object like Frienisberg 1997-2007 a treelike folder structure, where the sediment input can be copied to afterwards (the treelike folder structure is shown at the begining of script 1). It needs several input paths (line 51-66): path where the treelike folder structure starts, path where the vector files are stored, path were the raster files are stored, path of a helping script (that aids to extract information out of attribute tables).

Once the input paths are specified, you can run the script without further editing anything if you have the same vector and raster data as I used. If you want to adjust this script to other data, it's important to note that the naming convention of the input vectors and rasters is crucial. E.g. the FEKRE01_M1_037_SE.shp vector file has a corresponding sediment input raster called FEKRE01_M1_037_SE.tif. Also the naming of the vector attribute table, in my case e.g. "Datum" or "Parzelle", is crucial as well as it's format. E.g. the date in the attribute table column "Datum" was sometimes recorded as string and sometimes as timestamp. 

Special attention sould be paid to the following: At the end of the script, one additional "strange folder" was created (probably a temporary storage file...) which is deleted at the very end of the script. In line 59 poped up an exclamation make (import of the aiding script) - igonre this exclamation mark!


*script 2: copy_management_SE.py*

This script copies each sediment input raster to the right branch in the threelike folder structure. Sometimes rasters also had to be summed up prior to copying. The script needs several input paths (line 47-67): path where the treelike folder structure starts, path where the vector files are stored, path were the raster files are stored, path of the helping script, path where the mean annual sediment input is stored (because this was calculated in advance…).

Once the input paths are specified, you can run the script without further editing anything if you have the same vector and raster data as I used. If you want to adjust the script, also note that the naming convention of the vector and raster data is important as well as the naming of the attribute table columns as well as their formats. The summing up of the rasters in my case was relatively easy, since all rasters e.g. in Frienisberg 1997-2007 had the same X-Y-extent! The X-Y extent of all summed up rasters has to be the same, otherwise the programmed approach in this script won't works.

Special attention sould be paid to the following: Convert the rasters to numpy arrays and then sum up the rasters! In this way, the execution of the script is much quicker. At the end, don't forget to convert the numpy array back to a raster and set the output coordinate system. In the developing stage of this script, it did not always work properly. To note such errors during the copying process, cotrol is very crucial. After I copied some files to a new branch in the treelike folder structure, I always checked if the sum of all rasters in e.g. Frienisberg 1997-2007 is still the same as before (see table 1). The scripts were not uploaded on Github but can be easily deduced out of script 2.

Table 1: control table to be sure that the copying worked

region-period object:	Sum [t]:
Frienisberg_97_07	    200.90
Frienisberg_07_17	    42.16
Lobsigen_97_07	      43.66
Lobsigen_07_17	      4.01
Schwanden_97_07	      61.97
Schwanden_07_17	      7.05
Seedorf_97_07	        4.66
Seedorf_07_17	        2.67
Suberg_97_07	        122.00
Suberg_07_17	        29.93
















