Tutorial: Brain View
===========================
![example](https://user-images.githubusercontent.com/90367338/222876561-46612718-3baa-427a-88d0-264c5d953a2e.png)
===========================

# Catalog


* [1 Getting started](#1-getting-started)

* [2 Contacts](#2-contacts)


****


# 1 Getting started

1. Data Prepare

   (1) Prepare a color (value) array and a size array in Python. They can be either `list` or `numpy.ndarray` instances.

   (2) Call the `build_txt()` function in `utils.py` to easily generate a .node file with `160` rows and `6` columns. Elements in one row are split by space. Each element can be an integer or float number.

   Example: file `output/example.node`.

2. Launch BrainNet Viewer in MATLAB

   (1) In MATLAB, open BrainNetViewer/BrainNet.m. Then run it.

   ```shell
   >> BrainNet
   Please cite:
   Xia M, Wang J, He Y (2013) BrainNet Viewer: A Network Visualization Tool for Human Brain Connectomics. PLoS ONE 8: e68910.
   An example:
   'The brain networks were visualized with the BrainNet Viewer (http://www.nitrc.org/projects/bnv/) (Xia et al., 2013)'.
   ```
![Screenshot 2023-03-03 at 10 39 24 PM](https://user-images.githubusercontent.com/90367338/222876172-55e4f318-3795-49a9-90dd-31af9230c395.png)

   (2) Then in BrainNet Viewer, click File > Load File. In "Surface file", browse and choose "./data/surface.nv"; in "Node file", browse and choose the node file you just generated (example: "./output/example.node"); leave the rest two fields blank. Click "OK".
![Screenshot 2023-03-03 at 11 08 14 PM](https://user-images.githubusercontent.com/90367338/222876199-b6aba102-c8a7-4bdd-b01c-169e64af3830.png)

   (3) You may modify the settings under the left-side tabs. (Typically, you can modify the color and size features under the "Node" tab. Here, for example, we set Node > Color > Colormap to "Jet"). Then click "OK".
![Screenshot 2023-03-03 at 11 22 15 PM](https://user-images.githubusercontent.com/90367338/222876218-c797fe79-4fa3-4e95-a142-4add4753e3e9.png)
![Screenshot 2023-03-03 at 11 22 35 PM](https://user-images.githubusercontent.com/90367338/222876222-7ebdaccc-dca6-4815-b8f3-c8c139dc603c.png)

   (4) Click "Save Figure" to save the generated brain view plot. (In the example case, since the size array are set the same, we have balls in the figure with the same size)
![Screenshot 2023-03-03 at 11 22 51 PM](https://user-images.githubusercontent.com/90367338/222876228-18a600bf-c03b-4ca7-87f1-d5a2a4c431a3.png)
 

3. Install MATLAB (Optional)
   
   Wake Forest students have free access to download and use MATLAB. To learn more, please visit https://software.wfu.edu/download/matlab/.

4. Paraview

   (1) Data Prepare

   Prepare a .txt file with 160 rows and m columns. Elements in one row are split by space. Each element can be an integer or float number.
Example: file data/example.txt. Here m=1 and data type is float.

   (2)Build .vtk file

   In a Windows terminal, cd to this repo's root directory, then

   ```shell
   $ .\bin\Network2DestrieuxSurfaceRendering.exe .\bin\icbm_avg_mid_sym_mc_right_hires.vtk ${YOUR_INPUT_TXT_PATH} ${YOUR_RIGHT_OUTPUT_TXT_PATH_WITHOUT_SUFFIX} -V .\bin\Atlas_Right_Destrieux.txt -R .\bin\RightROI2NodeLookupTable.txt -m ${THE_COLUMN_NUMBER_M}
   $ .\bin\Network2DestrieuxSurfaceRendering.exe .\bin\icbm_avg_mid_sym_mc_left_hires.vtk ${YOUR_INPUT_TXT_PATH} ${YOUR_LEFT_OUTPUT_TXT_PATH_WITHOUT_SUFFIX} -V .\bin\Atlas_Left_Destrieux.txt -R .\bin\LeftROI2NodeLookupTable.txt -m ${THE_COLUMN_NUMBER_M}
   ```

   Example: 
   
   ```shell
   $ .\bin\Network2DestrieuxSurfaceRendering.exe .\bin\icbm_avg_mid_sym_mc_right_hires.vtk .\data\example.txt .\output\example_right -V .\bin\Atlas_Right_Destrieux.txt -R .\bin\RightROI2NodeLookupTable.txt -m 1
   $ .\bin\Network2DestrieuxSurfaceRendering.exe .\bin\icbm_avg_mid_sym_mc_left_hires.vtk .\data\example.txt .\output\example_left -V .\bin\Atlas_Left_Destrieux.txt -R .\bin\LeftROI2NodeLookupTable.txt -m 1
   ```
   
   Then the output .vtk file will be generated in the given output path, like file output/example_right_1.vtk and output/example_left_1.vtk).

   For convenience generating the figure for this project.
   You can see the word file in the original_spatial_txt file. Just copy paste the command line
   into the windows terminal, then you get the .vtk files ready for use.

   (3)Install App ParaView

   Home page: https://www.paraview.org/

   Click "DOWNLOAD"

   Download and install "ParaView-5.11.0-Windows-Python3.9-msvc2017-AMD64.msi"

   (5)Operations in ParaView

   File -> Open ... (choose the .vtk files)

Hint: you can open multiple .vtk files at a time. Click the "eye" button near the .vtk file's name to make it visible (or invisible)

# 2 Figure Generation for Elsevier
Title: A multiscale model to explain the spatiotemporal progression of
amyloid beta and tau pathology in Alzheimer’s disease.

This Project file is intend to generate the initial graph for figure 4 and 5 in the article.
1. Figure 4.
   
   This graph generate the spatial spread of 2 key biomarkers in the Alzheimer's disease.
   We will use the resubmission.py to generate the required .txt files.

   (1)What it Does:

   For each category (APET, TPET) and for each subject file i = 0–3, the script:
Compares predicted results to ground truth labels. 
Computes the accuracy for each file.
Highlights mismatches in the prediction:
0.00 = low accumulation,
1.00 = high accumulation,
2.00 = False Positive (Predicted 1, Truth 0),
3.00 = False Negative (Predicted 0, Truth 1).
Saves a new version of each prediction file as {category}_{i}_new.txt.

   (2)output:

   resub/pred/APET/APET_0_new.txt

   resub/pred/TPET/TPET_0_new.txt

   ...

   (3)How to use:

   Use the file generated in the resubmission.py to create the .vtk files
   described above. Hint: the command line word document is inside the folder
   respectively. 
   
   The color file is stored inside the screen_shot file if you need.

2. Figure 5.

   This graph generates the spatial dynamics of neurodegeneration and correlation analysis with
   amyloid and tau.

   



# 3 Contacts


Please email chenm@wfu.edu




