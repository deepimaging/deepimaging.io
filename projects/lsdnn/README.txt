Data location
Data collection, annotation and resizing (when necessary) is described in section 2.3 of the paper. 
For thin smear, there were 328 cropped cells containing malaria infection and have dimension 28x28x96, where 28x28 are the height and width of the images collected from 96 LEDs. The raw 28x28x96x328 image cube is located at:
/data/thin_smear/raw_data/examples_with_malaria/all_with_malaria_combo_328.mat   
The 96 LEDs used were lit individually, starting with Red, green and finally blue. The images from each of these LEDs were then concatenated in an RGB format: images 1-32 were collected using Red LEDs, images 33-64 from Green LEDs and finally 65-96 from Blue LEDs. Of these 96 images saved, the following image positions in the 28x28x96 cube were noise and are ignored going forward: 1, 11, 20, 33, 43, 52, 65, 75, 84. 
By ignoring the above noise images, we essentially have 328 individual cells containing malaria with dimension 28x28x87. As described in the paper, we also ignored the central LED positions: images 2, 34 and 53 were not used. This bring our final data that we used in our analysis to have the dimensions 28x28x84x328.
We had 795 cells not containing the infection, and are located at: 
/data/thin_smear/raw_data/examples_without_malaria/all_without_malaria_combo_328.mat 
The data in this folder is of dimension 28x28x96x795. We ignored the same images numbers in the 3rd dimension as described above for the infected cells, and we finally used a cube of dimension 28x28x84x795.
Similar data collection was performed on thick smear, and the final datasets created are located at:
/data/thick_smear/raw_data/images_infected_thicksmear_colorcombo.mat
/data/thick_smear/raw_data/images_noinfection_thicksmear_colorcombo_1400.mat 

Data augmentation
We applied 4 different augmentation techniques: 
-	Each data is rotated in steps of 90 degrees, 
-	The rotated data are then blurred using a pre-defined Gaussian (not sure, need to confirm if its gaussian or sinc function) blur kernel
-	The data from the 2 augmentation techniques above are then deformed. We use elastic deformation based on ideas of the paper: “best practices for convolutional neural networks applied to visual document analysis”, Patrice Y.S, Dave S and John Pratt. Proceeding of severing International conference on document analysis and recognition (ICDAR 2003). We write our own function describing the ideas in the paper.
-	Finally, Gaussian noise is added to the above data.
After the augmentation, the data is reshaped, normalized and randomly permitted before being saved as text files on disk. The files are saved as training and test datasets.
The data augmentation code is located here:
/data/thin_smear/data_augmentation_RGB.m
In the code above, we used our implementation of the Patrice et. al paper using a function located at: 
/data/thin_smear/elastic_deformation_RGB.m
Similar data augmentation on thick smear dataset was performed using the codes above by replacing the thin smear with thick smear dataset.
Loading the data into tensorflow. 
Data is read into memory using the script:
example_CNN_code/read_in_data.py
In this file, the saved text files are read into memory, reshaped, concatenated and then finally used to create a DataSet type. A custom made function read_data_sets_RGB inside the script is used to do all this.
The neural network used to train on the data is defined in the file 
/example_CNN_code/malaria_realdata_RGB_2.py
In this file, 6 different LED illumination patterns are tested:
-	single central LED from each channel illuminating the sample
-	One off axis LED from each channel illuminating the sample
-	Positive and negative LED light where we set one most LEDs to zero and 2 from each channel are non-zero. One of these 2 LEDs has a +1 value while the other one,  in opposing off-axis location has a -1 value.
-	All LEDs turned on at the same time. Simulating Kohler’s illumination pattern. 
-	Random LEDs chosen to illuminate the sample, and can have either +1 or -1 value.
-	Optimized LED case where the brightness and which LED turns on is determined by the neural network. The weights in this case are considered variables and are hence changed as the network is trained, unlike the other 5 cases where the weights are constants.
After training each of the above cases for 15 different times, each for 30,000 iterations, the following are saved as text files on disk as they are used later for analysis:
-	classification predictions with prefix final_predictions_repnum
-	Correctly classified with prefix successful_classifications_repnum
-	The final weights into the network with prefix final_weights_outloop
-	The LEDs pattern with a prefix added_intensity_weights_outloop
Similar loading and training on thick smear dataset was performed using the codes above by replacing the thin smear with thick smear dataset.
Data analysis
The final results reported in our paper are located in the following locations:
For thin smear, the folders containing the results is 
/thin_malaria_final_results/Final_15x_nocenter_results/
In this folder, the final individual and also the combined RGB final results are separately located in separate folders with appropriate names. 
The average scores, standard deviation and majority votes from the 15 iterations are calculated using the script:
/thin_malaria_final_results/process_results.m
The LED plots are created using the script:
/thin_malaria_final_results/malaria_LED_plotting.m
The variance of each LED was calculated using the script: 
/thin_malaria_final_results/LED_variance_calc.m
The 2 above scripts use positions_refocn1_180res.mat file located in the same folder that creates the positions of the LEDs used in collecting the data found.
The thick smear final results are located in the folder:
/Thick_malaria_final_results/Final_results/
Similar analysis code on the thick smear datasets in the above folder as well.
Transfer learning.
To test our results’ usefulness in under slightly different physical parameters, additional data was collected at Duke university in Durham using a slightly different physical microscope. Data annotation was then performed on the this dataset to determine the ground truth, and then this dataset was passed to our trained and saved model to get classification heat map.
Additional data was collected at Duke university in Durham, and is located here:
/data/classification_heatmap