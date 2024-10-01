Identify similarity between House Images


Datasets Available:
1.	Image Dataset:
•	HouseID
•	imageURL
•	longitude
•	latitude
•	reg_no
•	direction
2.	Manual_comparison matrix: labelled dataset to train the model
a.	HouseID1
b.	HouseID2
c.	distance
d.	isSameHouse (aka label, 1: same, 0: different)

The second dataset is initially needed for model building and evaluation. Eventually, for rest of the data, only the distance needs to be measured and stored.

Image Pre-processing

For each image, perform quality checks and standardize the images along with extracting the metadata information (hash values etc.).

Feature set Building: Comparison Matrix

For each image, fetch the images that are within the threshold distance and compare each one of them against the image under consideration to capture the Similarity Metrics e.g.

-	Peak Signal-to-Noise Ratio (PSNR)
-	Structural Similarity Index (SSIM)
-	Multi-Scale Structural Similarity Index (MS-SSIM)
-	Mean Squared Error (MSE)
-	Root Mean Squared Error (RMSE)
-	Visual Information Fidelity (VIF)
-	Spectral Angle Mapper (SAM)
-	Relative Average Spectral Error (RASE)
-	Universal Quality Image Index (UQI)
-	ERGAS
-	Spatial Correlation Coefficient (SCC)
-	Hamming distance of Average Hash (aHash)
-	distance of Perceptual Hash (pHash)
-	distance of Difference Hash (dHash)
-	distance of Median Hash (mHash)
-	distance of Wavelet Hash (wHash)

Store these metrics values against HouseID1_HouseID2 key combination. (a simple unique key can be created using the lexicographical order combination of two IDs)

*We need to note down the calculation duration of each metric for inclusion in final feature set.


Model Building, Training & Evaluation

Build a classifier using the manual comparison matrix along with the feature set built above. Divide the data amongst training/test sets to evaluate the model.

We need to identify the features which are significant to capturing the differences between the images. Use the feature significance along with the calculation cost to find the optimal combination of features.


Model Deployment

Batch Inference: For all the images in the dataset, identify the houses within the threshold distance, create the feature set and predict the similarity score. This can be all part of a single data pipeline.

Runtime Inference

 

Consumption

The dataset thus built can be easily used for varied purposes.
-	Reports: create report of similar houses for each state/district/tehsil.
-	Analytics: showing cluster of similar houses on a map region.
-	Alerts: Runtime inference to detect existence of similar images and either notify (asynchronous) or prevent submission continuation (synchronous prediction). 



Model Enhancement Iterations

Extract additional image metadata to enrich the feature set.
-	Detect Objects within an image
-	Comparison of objects – number, type and similarity.
-	Tag background information e.g., has_tree, has_street etc.
