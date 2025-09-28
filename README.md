# DenseNet and Attention-based DenseNet for Surface Defect Classification

## 1. Introduction
Surface defect detection is an important task in industrial quality control. Manual inspection of steel surfaces is time-consuming and prone to errors. Automated methods using deep learning can improve both accuracy and efficiency.  

In this project, we implement and compare two models:  
1. A standard DenseNet-121 model.  
2. A custom DenseNet-121 model with attention layers added after dense blocks.  

The goal is to classify six types of steel surface defects from the **NEU Surface Defect Database**.

---

## 2. Dataset
We use the **NEU Surface Defect Database**, available on Kaggle:  
[NEU Surface Defect Database](https://www.kaggle.com/datasets/kaustubhdikshit/neu-surface-defect-database)

- Total images: 1,800  
- Image size: 200 × 200 pixels  
- Number of classes: 6  
- Each class has 300 images  

Classes included:  
- Crazing (Cr)
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/d2896b74-c05c-4e08-9e8a-75cffecb90f0" />

- Inclusion (In)
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/03e753aa-8beb-4fe0-9293-af23bb0a99d5" />

- Patches (Pa)
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/2d474e6c-05d3-42ff-b8b0-24877d16dbab" />

- Pitted Surface (PS)
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/a684b527-8914-4ad7-bef7-4af9878858b0" />

- Rolled-in Scale (RS)
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/ace2b060-cb42-490f-bd23-d9e2f650186b" />
 
- Scratches (Sc)  
<img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/9ab691ce-40b1-40b2-b47f-cca63822306d" />


We split the dataset into training, validation, and test sets. Images were resized, normalized, and augmented where needed.

---

## 3. Methodology
### 3.1 Baseline DenseNet
- We use DenseNet-121 and modify the final layer for 6-class classification.  
- DenseNet is well-suited for this problem because its dense connections improve feature reuse and gradient flow.  

### 3.2 Attention-based DenseNet
- We introduce attention blocks after dense blocks.  
- The purpose of attention is to help the model focus more on important regions of the image (such as defect areas).  

### 3.3 Training Details
- Optimizer: Adam  
- Loss Function: CrossEntropyLoss  
- Epochs: 25  
- Learning Rate Scheduler: ReduceLROnPlateau  
- Metrics: Accuracy, F1-score, Confusion Matrix  

---

## 4. Results
### DenseNet (Baseline)
- Validation Accuracy: up to 100%  
- Validation Loss: very low, showing good convergence  

### DenseNet with Attention
- Validation Accuracy: up to 99.22%  
- Slightly weaker accuracy compared to baseline  
- Attention maps provide better interpretability of the model’s decisions  

---

## 5. Conclusion
<img width="853" height="470" alt="image" src="https://github.com/user-attachments/assets/1dd42c81-7f7a-4fb7-ab88-a44bdea9a378" />
<img width="853" height="470" alt="image" src="https://github.com/user-attachments/assets/2cff70ad-d649-40a6-a48f-e189e5a59c6e" />
<img width="857" height="470" alt="image" src="https://github.com/user-attachments/assets/39ea3080-b76a-48f0-9869-a487eb1e0d6b" />
<img width="849" height="470" alt="image" src="https://github.com/user-attachments/assets/c160a38b-430c-45ba-ab16-28ddaee781b0" />


- DenseNet is a very strong model for steel surface defect classification.  
- Adding attention layers did not improve accuracy but made the model more interpretable.  
- This shows that attention is useful when we need transparency in model predictions, even if accuracy does not increase.  

<img width="548" height="698" alt="image" src="https://github.com/user-attachments/assets/2714d3be-c134-4f26-8e57-96d3cb43acb4" />


### Key Takeaways
- Baseline DenseNet achieved the best accuracy.  
- Attention-based DenseNet showed good interpretability.  
- Both models are suitable for real-world defect detection tasks.  

### Future Work
- Experiment with larger datasets.  
- Try hybrid CNN-Transformer models (such as Swin Transformer).  
- Deploy models into real-time inspection systems.  

---

## 6. Usage
### Training
Run the notebook to train both models. The training loop and validation loop are already included.  

### Saved Models
After training, models are saved as:  
- `densenet.pth`  
- `densenet_attention.pth`  

### Inference
You can reload the saved models and test them on new images. Upload an image and the model will predict one of the six defect classes.

---
