# 📘 Overview
# ⚙️ Flow
## 1.Flowchart 1: Open cpu.tab, randomly sample 30 records as test data, with the remainder used as training data, and imitate the Bagging approach by training 5 Tree models, then take their average as the output value. 

 Step 1: Use Select Columns and reset the class as the target. 
 
 <img width="576" height="611" alt="image" src="https://github.com/user-attachments/assets/ec77e3f2-a198-47e9-834d-6dbcd4009149" />
 
Step 2: Split the data, reserving 30 records as test data, with the remainder used as training data for the model.

<img width="571" height="397" alt="image" src="https://github.com/user-attachments/assets/ab385198-f01d-4d55-8fea-7c279ab72205" />

Step 3: Perform Bagging, where the sampling method is with replacement. Therefore, we use the Data Sampler, select Bootstrap, and remove the replicable option to achieve the with-replacement effect, ensuring that the samples drawn for the five models are not identical but different.

<img width="570" height="378" alt="image" src="https://github.com/user-attachments/assets/4c2670c1-5a88-46da-863f-4806fb9ada74" />

Step 4: Build a tree model and feed the sampled data from the previous step into the tree model for training, using the default parameters for the tree model.

<img width="524" height="306" alt="image" src="https://github.com/user-attachments/assets/cdfad570-6ccc-423a-b15a-e996c127fc50" />

Step 5: Use Prediction to perform testing; the accuracy of the tested models is shown in the figure on the right.

<img width="572" height="282" alt="image" src="https://github.com/user-attachments/assets/c2cd9289-7118-402d-a9f6-5be62f5f1bec" />

Step 6: Use Formula to average the class predictions from models 1-5; the formula is shown in the figure on the right.

<img width="557" height="467" alt="image" src="https://github.com/user-attachments/assets/eac0eaf2-6861-49d6-a324-829144bf8b4d" />

Step 7: Use Data Table to print and confirm the average values calculated in the previous step.

<img width="570" height="289" alt="image" src="https://github.com/user-attachments/assets/d2143cd1-01ef-408a-902d-5cd95cc7e1df" />

<img width="308" height="420" alt="image" src="https://github.com/user-attachments/assets/017812e1-b054-4760-9403-31253a54fd22" />

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

## Flowchart 1: Using the same training and test data, build two additional models, namely Tree and AdaBoost, find the better parameter combinations, and compare them with the Bagging done in the previously mentioned sections. 

Step 1: Open the tree model and prediction simultaneously, and adjust the parameters to the optimal situation by observing changes in MAPE and MSE.

<img width="552" height="201" alt="image" src="https://github.com/user-attachments/assets/f906b739-5cfb-4e27-b1f0-5d3e83b0dad0" />


Step 2: Open the AdaBoost model and prediction simultaneously, and do the same as the previous step.

<img width="559" height="216" alt="image" src="https://github.com/user-attachments/assets/edbb4364-b1b9-48b0-8853-7bbf79e637cd" />


Step 3: Compare; solely in terms of MSE and MAPE, it is found that although AdaBoost is significantly lower than Tree, the performance in the model comparison section is not ideal. It is suspected 
that this is due to overfitting in the above fine-tuning, where AdaBoost was tuned too closely to the training set.

<img width="567" height="97" alt="image" src="https://github.com/user-attachments/assets/82ad07b6-33f3-4a23-81c3-5911720b0337" />

<img width="560" height="182" alt="image" src="https://github.com/user-attachments/assets/1c9db591-6c8d-4e9e-86cd-7fb6f43164b3" />

Step 4: Fine-tune AdaBoost once more by opening the AdaBoost model, prediction, and Test and Score for adjustment, with the goal of improving the model comparison slightly. Finally, it is found that when AdaBoost's estimator = 50, the model's win rate is relatively high, but still only 0.338.

<img width="553" height="438" alt="image" src="https://github.com/user-attachments/assets/754c0c7c-dfe9-4e1d-9b27-efb76ab79aa4" />

<img width="560" height="163" alt="image" src="https://github.com/user-attachments/assets/2e22e1ba-1ffe-4d8c-aba5-4b6c5167c04c" />


Step 5: Compare with the Bagging model created in the previous two questions; it is found that the Tree after parameter adjustment has the highest win rate, while AdaBoost has the lowest win rate.

<img width="549" height="238" alt="image" src="https://github.com/user-attachments/assets/933c7cc6-977c-4330-90de-3161f3f37bb6" />

## 4.Flowchart 2: Use 10-fold cross-validation to find the better parameter combinations for three models (Tree, kNN, AdaBoost).

Since the models include AdaBoost, we uniformly adopt bootstrap for sampling in these three models. Below, the test data will be visualized and output using a scatter plot, where the bluer and smaller the points, the lower the MAPE of their parameter combinations.

| Description |Fogure|
| :--- | :--- |
|The figure on the right is the scatter plot for AdaBoost testing; MAPE is minimized when the number of estimators = 7.|<img width="574" height="387" alt="image" src="https://github.com/user-attachments/assets/626312f1-604d-4028-8ee9-ed61cf5280bb" />|
|The figure on the right is the scatter plot for KNN testing; MAPE is minimized when the number of neighbors = 2.|<img width="588" height="396" alt="image" src="https://github.com/user-attachments/assets/8512dc35-4005-4fa8-8935-a49bf1e35fff" />|
|The figure on the right is the scatter plot for Tree testing; MAPE is minimized when the minimum number of instances = 2, and do not split smaller than = 2 or 3.|<img width="583" height="393" alt="image" src="https://github.com/user-attachments/assets/1ac58898-2805-4617-aeb5-44a7999ac3a8" />|

## 5.Flowchart 2: Using the above three models as level-0 models for Stacking, does the combined model outperform a single model? (20%)

Step 1: Connect the above three models to Stacking using the Learner -> Learners method, as shown in the figure below.

<img width="728" height="419" alt="image" src="https://github.com/user-attachments/assets/03740fdf-838e-4a32-90b5-c15c67cfd3f7" />

<img width="737" height="416" alt="image" src="https://github.com/user-attachments/assets/0093d805-b7f8-40e6-ae4a-7c9bcf92517d" />

<img width="737" height="409" alt="image" src="https://github.com/user-attachments/assets/d7f033a3-52c1-44e5-aa56-9b20ee1f45e3" />

Step 2: At the Test and Score section, check whether Stacking's accuracy is superior to the other three models. The accuracy is shown in the figure below. We can see that Stacking only outperforms AdaBoost; it is speculated that this may be a result caused by overfitting or bias due to the sampling method.

<img width="777" height="200" alt="image" src="https://github.com/user-attachments/assets/717937b0-e760-427c-a600-efd3bc1e0a79" />





