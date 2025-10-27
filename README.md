# Overview
# Flow
## 1.Flowchart 1: Open cpu.tab, randomly sample 30 records as test data, with the remainder used as training data, and imitate the Bagging approach by training 5 Tree models, then take their average as the output value. 


| Step Description | Graph |
| :--- | :--- |
| Step 1: Use Select Columns and reset the class as the target. |<img width="576" height="611" alt="image" src="https://github.com/user-attachments/assets/ec77e3f2-a198-47e9-834d-6dbcd4009149" />|
|Step 2: Split the data, reserving 30 records as test data, with the remainder used as training data for the model.|<img width="571" height="397" alt="image" src="https://github.com/user-attachments/assets/ab385198-f01d-4d55-8fea-7c279ab72205" />|
|Step 3: Perform Bagging, where the sampling method is with replacement. Therefore, we use the Data Sampler, select Bootstrap, and remove the replicable option to achieve the with-replacement effect, ensuring that the samples drawn for the five models are not identical but different.|<img width="570" height="378" alt="image" src="https://github.com/user-attachments/assets/4c2670c1-5a88-46da-863f-4806fb9ada74" />|
|Step 4: Build a tree model and feed the sampled data from the previous step into the tree model for training, using the default parameters for the tree model.|<img width="524" height="306" alt="image" src="https://github.com/user-attachments/assets/cdfad570-6ccc-423a-b15a-e996c127fc50" />|
|Step 5: Use Prediction to perform testing; the accuracy of the tested models is shown in the figure on the right.|<img width="572" height="282" alt="image" src="https://github.com/user-attachments/assets/c2cd9289-7118-402d-a9f6-5be62f5f1bec" />|
|Step 6: Use Formula to average the class predictions from models 1-5; the formula is shown in the figure on the right.|<img width="557" height="467" alt="image" src="https://github.com/user-attachments/assets/eac0eaf2-6861-49d6-a324-829144bf8b4d" />|
|Step 7: Use Data Table to print and confirm the average values calculated in the previous step.|<img width="570" height="289" alt="image" src="https://github.com/user-attachments/assets/d2143cd1-01ef-408a-902d-5cd95cc7e1df" /><img width="308" height="420" alt="image" src="https://github.com/user-attachments/assets/017812e1-b054-4760-9403-31253a54fd22" />|

## 2.Flowchart 1: Calculate MAPE using the results of Bagging. 

Step 1: In the MAPE calculation formula, the 'class' is needed, but due to the issue of 'class' not being readable in the formula, it is first renamed using Edit Domain.

<img width="500" height="281" alt="image" src="https://github.com/user-attachments/assets/da35d5bf-1929-4b7d-a263-2e74ca238c5b" />

<img width="513" height="346" alt="image" src="https://github.com/user-attachments/assets/54dc9b9e-bc2b-40b7-a037-f5cf7c17238e" />

Step 2: In the MAPE calculation formula, 'error' is needed, but upon opening the data table after prediction, we found that some tree models have empty error values, so imputation was used in the middle to fill the missing values.

<img width="532" height="224" alt="image" src="https://github.com/user-attachments/assets/3caf55e9-bd60-420c-a964-1532a2464379" />

<img width="493" height="311" alt="image" src="https://github.com/user-attachments/assets/b6ce2d15-6b59-4651-87f8-baf5d8f5633f" />

<img width="532" height="437" alt="image" src="https://github.com/user-attachments/assets/b2fe9dce-cf52-463b-a7a3-3c4ab51b40ac" />


Step 3: Start listing the MAPE formula, the MAPE formula is as shown below. (abs(Tree1-new_class)+abs(Tree2-new_class)+abs(Tree3-new_class)+abs(Tree_4-new_class)+abs(Tree5-new_class))/5/new_class We first take the absolute value of each model's prediction error (originally wanted to directly use the error calculated by prediction in the formula, but due to some fields being empty and unable to perform imputation, this approach was adopted), add them up, divide by 5 to get the average error, and then divide by the actual value of class to get the average MAPE for each model on each instance.
<img width="342" height="876" alt="image" src="https://github.com/user-attachments/assets/19a747c7-42f3-45fa-a207-9b63ecfb0c25" />



