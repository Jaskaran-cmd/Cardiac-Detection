# Cardiac-Detection

An enlarged heart may be the result of a short-term stress on the body, such as pregnancy, or a medical condition, such as the weakening of the heart muscle, coronary artery disease, heart valve problems or abnormal heart rhythms. But the Detection of the enlarged heart involves processing the dicom images and manually annotate the bounding boxes around the heart . So why not automate the process of putting bounding boxes around the heart .The Image Data and the CSV files can be found at kaggle and the link is provided below 
https://www.kaggle.com/c/rsna-pneumonia-detection-challenge/discussion/70427

# Preprocessing

The preprocessing step involves manually annote the training data and store the information about bounding in csv format corresponding to the label .The next step involves Extracting the image from the dicom files using few lines of code and then storing it to the training and validation directories .we use pathlib for easy path handling 
while extracting the image in the for loop we are calculating the data to find mean and standard deviation to normailise the image while data augmentation 
and we resize and rescale and the image look something like this 

![image](https://user-images.githubusercontent.com/64350022/148531016-3c6c52b4-de31-4d8b-aa57-5eea55c33f17.png)


# Custom Dataset Creation 


We make use of Pytorch Dataset class from torch.utils.Dataset to create custom dataset which when indexed ,will return image and the bounding boxex coordinate .as usual we will overide the len and getitem magic method's from the PyTorch Dataset class. Also if augmentation pipeline is given to the init method then the model will perform  the augmentation both on image and the bounding boxes coordinate 
after creating custom datasets and augmenting the image and bounding boxes coordinates the image looks like asa shown in the figure below
![image](https://user-images.githubusercontent.com/64350022/148532489-9a221e2a-5c21-4857-a451-637c8f5354db.png)


# Model Creation 
We are using resnet18 Model Architecture to create our model  and the model architecture looks something like this 


![image](https://user-images.githubusercontent.com/64350022/148529782-b24de982-6ee2-45a0-87be-5f70559939cf.png)

as you can see from above image ResNet18 has 3 input channels in conv1 layer  and 1000 output neurons , But for our Model we require Input shape to have only 1 channel and 4 output neurons since the output has 4 coordinates of the bounding boxes 

# Model Evaluation
We use Mean Squared Error to evaluate our model and use it as loos function of the model .AFter Training the model for 200 epochs with learning learning rate 1e-4
I got MSE of 64 on validation and 24 on training data 
and if i visualize the image and the predicted bounding boxes we get the iamge as shown in the figure below 



![image](https://user-images.githubusercontent.com/64350022/148532842-2f7708e4-edf5-45c7-844a-ca3529d8f4d2.png)


where white box indicates the predicted box
and magenta box indicates the actual bounding box 


