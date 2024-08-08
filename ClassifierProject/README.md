# Requirements

Must be run in a python 3.11 Environment

# Runtime

Training and building the models usualy take > 5 minutes, even when using 10 genres.
The k-fold analysis can take slightly over 30 minutes using 10 fold, over 5 repititions creating 50 folds.

# data

The midi data from magenta is in the folder "data", while movement data is in the folder "MovementData" and premade models are in "models".

# drumclassifier.ipynb

The drumclassifier file is only CNN model without any extra prebuilt layers. It takes n amount of midi segments, with 22x32 velocity data trains to classify the genres based on the velocity in the temporal dimension.

# drumcallsifier_PCA_CNN.ipynb

This is the model which is used to compare with accelerometer data (which is done in ExtractMovementData).

Much of the code in this file is the same as in drumclassifier, but it has a PCA filter which goes through every timestep and creates a list of pca objects which takes a statistical value for each time step compared to the rest of the dataset. This reduces the dimensions of midi data from 22x32 to 1x32, which the model is then trained on to match the movement data.

# drimclassifier_PCA_LDA_CNN.ipynb

The PCA_LDA_CNN uses a PCA layer, to reduce to the first 5 components, which then gets reduced further to 1 dimensions by the LDA filter. In constrast to drumclassifier_PCA_CNN, here the PCA filter is used on the whole 32 segment, instead of using a unique object on each timestep. Further the LDA is also used on the whole array, finding global patterns. To me, this means I loose the temporal pattern which I am/was interessted in exploring, but this model show much higher classification accuracy for a 1 dimensional analysis.

# ExtractMovementData.ipynb

This is where you can test classifying movement data.

I have prebuilt models which is trained on 10 genres or 2 genres, but if you want to create new models trained on other genres, it is described how to in the drumclassifier_PCA_CNN.ipynb file.
The models for the pca cnn mehtod is in "models/pca_cnn", while the models for the pca lda cnn method is in "model/pca_lda_cnn"

I have some premade movement data in MovementData which is available to test.

You only need to create a new csv file and download it into the project to test your own rythms. (I used phyphox, but any accelerometer app that can create csv file will work). Remember to match the movement to a stored bpm value.
