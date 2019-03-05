
"""
CSTUe-Team-3
05-03-2019

Segmenting retinal fundus images
Investigating the differences of a network trained on ground truth containing all vessels and the concatenation of network
outputs trained on ground truth of thin vessels and a ground truth for thick vessels (vessel width > 3 pixels).

Preprocessing:
	  Split_Vessels.py:
  		  The model will be trained on thick and thin vessels seperately. For this the ground truth of the data set should be split up
	    	Thickness threshold: the minimum amound of pixels for which a vessel will be classified as thick
		    First the skeleton of the segmented vessels will be made. Also the smallest distance from the skelet to the background
		    will be determined. This distance and the thickness threshold will be used to determine wheter the vessel should be classified
		    as thick or thin.
		    Draw Circles ???
		    Output:
		        The images with thin and images with thick vessels segmented.
		

Data augmentation:
	  Mutate_data.py:
	    	In this code, data is augmentated by mutating the original training set.
		    There are 4 operations, which are randomly applied to the training images using random.randint(0,3).
		    1) Rotation: The image, mask and segmentations of the trainingset are fliped over the x-axis, 
		       the y-axis or both. The flip direction is randomly chosen again using random.randint(0,2);
		    2) Noise: A normal distributed noise is only applied to the actual image;
		    3) Contrast change: The pixel values of the image is multiplied with a random chosen integer between 0.5 and 1.5;
		    4) Blur Kernel: Gaussian blur with sigma 2 is applied to the image.
		    Input parameters:
		    images, masks, segmentations: the original of the training set
		    noise_strength: integer, is used as standard deviation in the noise operation
		    new_records: amount of generated training samples which will be added to the original
		    seed: ????
		    Output:
		        The original and generated images, masks and segmentations.

Training:
  	Unet_transfer.py:
	    	The used netwotk is the U-net, but it is adopted with transfer learning.
		    Parameters from VGG11 trained on Imagenet data set are used to replace corresponding random initial values in U-Net. 
		    With its parameters fixed and fully-connected layers removed, VGG11 serves as an encoder in the U-Net network
		    Please always restart python console before running this file, otherwise the name of each layer would change.
		    After transfering, the Unet cannot be fed for training immediatly.
		    The transfered parameters should first be freezed and other layers should be trained first.
		    Then transfered parameters could be freed and the whole network could be trained together.
		    Learning rate for 'freezed-training' should be 1e-5

Submissions:
  	In the submission14 folder you can find a clean version of the jupyter notebook that is used for submissions.
	  In the folders, you can find the vlidation images with the predicted vessel segmentations
	  submission_log.txt:
	    	An overview of the several submitted models and their corresponding dice scores.
"""
