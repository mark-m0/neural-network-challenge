# neural-network-challenge

# Overview

This project aims to develop a neural network model that can be utilized in the selection of applicants for funding by our company, Alphabet Soup. The goal was to find a way to predict if applicants will be successful if they are funded by our company. By using a neural network model, the hope is to train a computer to be able to predict this success at an accuracy of 75% or greater.

# Results
## Preprocessing of Data
In the development of the neural network, we must first take in the data provided by the business team. The data contains information from over 34,000 organizations we have funded in the past. Each organization has the following data associated with it:

* **EIN and NAME**—Identification columns

* **APPLICATION_TYPE**—Alphabet Soup application type

* **AFFILIATION**—Affiliated sector of industry

* **CLASSIFICATION**—Government organization classification

* **USE_CASE**—Use case for funding

* **ORGANIZATION**—Organization type

* **STATUS**—Active status

* **INCOME_AMT**—Income classification

* **SPECIAL_CONSIDERATIONS**—Special consideration for application

* **ASK_AMT**—Funding amount requested

* **IS_SUCCESSFUL**—Was the money used effectively


These variables must be preprocessed in order to effectively create the dataframe which will be utilized by the model. The target variable (the variable we will try to predict) is the **IS_SUCCESSFUL** variable. From here, we remove the **EIN** and **NAME** columns, as they do not provide any useful information for the purpose of the model. The remaining variables are utilized in the model as "features". The **APPLICATION_TYPE** and **CLASSIFICATION** columns get processed into bins in order to make the data easier to process. Finally, the categorical data is converted to numeric data for the model to interpret. 

## Creation of the initial model
The data gets placed into X and y values before being put into training and testing variables. The X values are scaled down to eliminate potential bias from the size of the values. The model is now defined. The structure of the model is shown in the below screenshot.

![image](https://user-images.githubusercontent.com/106498287/204122275-dd10e71b-7c7e-4d0f-b843-5efaf959e113.png)

This initial model utilizes two hidden layers and an output layer. The first layer has 80 neurons and the second has 30. Both use the "relu" activation function. The output layer has a single neuron with a "sigmoid" activation function. The first layer was given 80 neurons as it is about double the number of input dimensions to provide a solid starting point. The second layer uses 30 neurons as it is less than 50% of the initial layer. The output layer uses a single neuron as we only want a single output. The "relu" functions that are used take in the positive data that is being fed in. The "sigmoid" function in the output layer allows for the data to be classified as a predicted value between 0 and 1 which is what we are aiming for in our predictions. 

Next, we fit the data to our model in order to train it. This is done utilizing 100 epochs, so that the model has a chance to learn from its previous iterations through the data and improve. The model, now trained, is evaluated, giving us an accuracy of 0.7250145673751831, or about 72.50% accuracy.

## Optimizing the Model
The accuracy in the initial model did not yield the accuracy that was hoped for. This is where optimization becomes a factor. Various factors can be changed in order to optimize the model. I decided to focus on changing the parameters within the model's layers and the number of epochs that the model is run through. 

The first attempt at this involved changing the number of neurons in each layer, the total number of layers, and the final activation function, as shown in the screenshot below.

![image](https://user-images.githubusercontent.com/106498287/204123128-98427e2e-fb39-470a-95f9-24f5dade0c1a.png)

As can be seen, the first layer uses 130 neurons, the second layer uses 60 neurons, the third uses 15 neurons, and the final activation function is changed to "tanh". The decision to change the activation function was made in order to see if the data would react better to the constraints provided by this function. 

This model was also fit and trained using 200 epochs, effectively doubling the learning that could be done. The outcome of this model was an accuracy score of 0.7257142663002014, or about 72.57% accuracy. This once again did not meet the standard aimed for, but showed slight improvement.

The next model attempt aimed to utilize a model tuner. This essentially creates a model and attempts to optimize the hyperparameters that make a neural network tick. The code that goes into the tuner is shown below in a screenshot.

![image](https://user-images.githubusercontent.com/106498287/204123352-4fcd5104-8b2b-483c-a092-c899c20bcfdc.png)

This model went through 508 different trials attempting to find the best possible accuracy score. This step took the most time, as each trial will run through varying epochs in an attempt to find the overall "winning" combination. This took 1 hour and 45 minutes to process. To my surprise, this method yielded an accuracy of 0.7281632423400879, or 72.82%. 

In a final attempt to optimize the model, I decided to utilize some features from the tuner model and incorporate them into a final model, in hopes of reaching the 75% accuracy score. This involved 3 hidden layers and an output layer once again using the "sigmoid" function. The first layer uses 135 neurons, the second uses 69 neurons, and the third uses 11 neurons. The number of epochs that the model will be fitted to and trained on was chosen as 12. The information is also displayed in the below screenshot.

![image](https://user-images.githubusercontent.com/106498287/204123564-5bc9be66-54f3-4dfb-9712-b61d67b114df.png)

This model resulted in an accuracy score of 0.726064145565033, or 72.61%. As such, the best working model (the tuner model) was saved for potential further use/optimization.


## Summary
The goal of the model was to achieve an accuracy score of 75% or greater. The initial model came in with an accuracy of about 72.50%. This left room for improvement. The optimization attempts did not achieve this either. The best scoring model was the model generated through the tuner, which resulted in an accuracy of about 72.82%. Although improvements were seen, they were not nearly as great as one would hope. My recommendation is to continue to optimize this model by adding in the use of PCA and t-SNE models in the pre-processing stage. This could potentially bring the overall noise of the data down to a level where the model is able to more accurately predict the success of a funded applicant.
