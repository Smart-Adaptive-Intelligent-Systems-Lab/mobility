# UNLV_movement
Using AI to detect if a patient has a Mild Traumatic Brain Injury based on the way they walks. It's proven that a patient with this kind of injury has a walking imperment. We then use this fact to detect with AI an undiagnosed mTBI by recolting walking data of the patient and analyse them.


# First Dataset - Movmement AAL

The project Movement AAL is an experience made in experimental condition to predict Indoor Movement in an office environment. In the repository "./MovementALL/papers/*" you can find 4 different papers related to this experience using reservoir computing (A deep learning algorithm) to predict if the subject is about to leave the office based on his walking path. This experiment use 3 different set of room. in each set of room there is 4 Radio signal sensors, linked to a sensor located on the chest of the subject. The goal is to use the strength of all 4 sensors to locate the subject and predict where he is going. 

## Data Structure

In this dataset, the folder "./MovementALL/dataset/" you can find 314 files containing between 28 and 126 rows (based on the length of the path) the time difference between each row is 1/8 second. Each row has 4 different values, the radio signal strength for the 4 sensors of the room. The file "./MovementALL/groups/MovementALL_DatasetGroup.csv" contains the id numbeer of the room where the experiment was made for each files. The file "./MovementALL/groups/MovementALL_Paths.csv" contains the id number of the path for each files.

## Treatment

We used this experience to train a Long Short Term Memory algorithm to be able to detect wich path were curved in order to then transfer this knowledge on the other dataset, using a transfer algorithm. We used this technic because the data of the Nursing college were supposed to be too light to train a full model by themself. Our statement was that being able to detect a curve in the walking path of a patient would be close to detect walking imperment.

Long short term memory algorithm is a recurrent network, we used this algorithm for his ability to treat sequence data.

Data organisation. spliting the data into 2secondes samples = 16 rows per sequences

To have more sample we used a special technic. doing a sample from row 1 - 16 then 2- 17 then 3-18. By doing that we would have way more sample more than 10 times the number of samples. 

With the 8487 samples, I did a train test validation split. 50% train 30% test 20% validation. And then used them to train an LSTM model with 200 epoch and a batch_size of 256. The accuracy of the model with those settings is 99%. But an accuracy like that can be due to an overfitting.

To remove the hypothesis of an overfitting I did a K-fold cross Validation. A K-fold cross validation is a technic to train multiple model by splitting the data differently 10 times. By doing that we make sure that every rows are used for training testing and validate. 

With the K-fold cross validation all the accuracy are between 75% and 98%.

In the file "./MovementALL_LSTM.ipynb" and "./MovementALL_LSTM.ipynb" you can found all the treatment We did on those data. The first file contains the data analyse and cleaning with the training of a single model. This model accuracy goes up to 99% with the right settings and 200 epochs. On the second file you can find the same analysis and cleaning but with a training using K-fold Cross Validation to make sure there is no overfitting on the data.

