# X_Ray_Image_Classification w/ Convolutional Neural Network

# Introduction
It has been reported that patients with COVID-19 may have pneumonia as a complication, meaning a number of cases of pneumonia may increase constantly. Therefore, I built a CNN model which can aid a doctor to dignose the pneunomia from X_ray image of patient's lungs; moreover, to identify if the cause of infection is either bacterial or viral. Hence, model will facilitate earlier treatment, resulting in improved clinical outcomes.  

# Background
Pneumonia is an infectious respiratory disease that causes inflammation of air sacs in one or both lungs. Pneumonia is usually caused by bacteria and virus and some common symptoms amongs the patients are cough with phlegm (pus), fever, and difficulty breathing. 
A chest X-ray is mainly used to diagnose pneumonia. 

Datasets used in this study are from the pediatric patients of one to five years old from Guangzhou Women and Children’s Medical Center, Guangzhou. All chest X-ray imaging was performed as part of patients’ routine clinical care.
To read more about, visit -> https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia 

# Project at a glance
1. Used **OpenCV** to access and preprocess the X_Ray images 
2. Used **ImageDataGenerator** to perform a data augmentation to reduce overfitting.
3. Used **Keras** to construct two CNN (Convolutional Neural Network) models for a binary classifications (Normal vs. Pneumonia and Bacterial vs. Viral) 
4. Used **Scikit-learn** to evaluate the model with a confusion matrix


# Model Validations
A model with one convolution layer with a max pooling and two dense layers achieved the highest accuracy. (Conv -> Pool -> Fully_Connected)

Followings are a progress of how I went about improving the model.

## 1st_model
Model achieved an accuracy of 99.6% in training while an accuracy of 72.4% in test; therefore, a model was overfitted.
Both cases achieved a recall(sensitivity) of 100% for pneumonia, proving the model is capable of identifying pneumonia.
On the other hand, precisions for train and test were 100% and 69% resepctively, meaning it may not as effective in a sense of assisting a doctor. 

## 2nd_model
I have decided to implement a data augmentation to reduce overfitting becasue X_Ray images from the datasets were pre_examined by experts, which means the quality of images is relatively hard to match.
In test, the model achieved an accuracy of 87.3 % with a sensitivity of 87%. Therefore, it was safe to say that the model was improved both overfitting and reliability by the method of data augmentation. 
