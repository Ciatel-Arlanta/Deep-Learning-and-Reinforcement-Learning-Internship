## **CNN_Cifar.ipynb: CNN from Scratch**

This notebook details the process of building a **Convolutional Neural Network (CNN)** from the ground up to classify images from the CIFAR-10 dataset.

### **Performance Analysis**

|Metric|Value|
|:--|:--|
|**Train Accuracy**|94.00%|
|**Validation Accuracy**|80.97%|
|**Test Accuracy**|80.24%|


### **Model Architecture Summary**

| Component                   | Description                                                 |
| :-------------------------- | :---------------------------------------------------------- |
| **Input shape**             | (32, 32, 3)                                                 |
| **Total Conv Layers**       | 3 convolutional layers.                                     |
| **Downsampling**            | MaxPooling2D with a (2, 2) pool size.                       |
| **Normalization**           | Batch Normalization is used after each convolutional layer. |
| **Regularization**          | Dropout with rates of 0.25, 0.4, and 0.5.                   |
| **Final feature reduction** | `Flatten()`                                                 |
| **Output**                  | Dense layer with softmax activation and 10 units.           |

### **Training Details**

|Component|Value|
|:--|:--|
|**Optimizer**|Adam with a learning rate of 0.001.|
|**Loss**|`categorical_crossentropy`|
|**Batch Size**|64|
|**Epochs**|30, with EarlyStopping.|
|**Learning Rate Schedule**|`ReduceLROnPlateau`, monitoring validation accuracy with a patience of 3 and factor of 0.5.|
|**Regularization**|Dropout (0.25, 0.4, 0.5) and BatchNormalization.|
|**Final Downsampling**|Not applicable, uses `Flatten`.|

![image](https://github.com/user-attachments/assets/adee1b85-e6ff-4d78-a679-f4a5deb52986)

### **Learnings**

- Builds a custom CNN architecture tailored for the CIFAR-10 dataset.
- Employs data normalization using the mean and standard deviation of the dataset to improve model training.
- Effectively uses `MaxPooling` for downsampling and feature extraction.
- Combines `Dropout` and `BatchNormalization` to prevent overfitting and improve generalization.
- Utilizes the `Adam` optimizer and a `ReduceLROnPlateau` learning rate schedule for efficient training.

---

##  **CIFAR10_MobileNetV2.ipynb: Transfer Learning**

This notebook uses **transfer learning** with the pre-trained **MobileNetV2** model to classify images from the CIFAR-10 dataset.

### **Performance Analysis**

|Metric|Value|
|:--|:--|
|**Train Accuracy**|88.85%|
|**Validation Accuracy**|88.76%|
|**Test Accuracy**|88.76%|


### **Model Architecture Summary**

|Component|Description|
|:--|:--|
|**Input shape**|Images are resized to (224, 224, 3).|
|**Base Model**|MobileNetV2 with 'imagenet' weights and `include_top=False`.|
|**Fine-tuning**|The last 20 layers of the MobileNetV2 base model are unfrozen for fine-tuning.|
|**Top Layers**|`GlobalAveragePooling2D`, followed by a Dense layer with ReLU activation, BatchNormalization, Dropout, and a final Dense output layer with softmax.|
|**Downsampling**|Handled by the strided convolutions within the MobileNetV2 architecture.|
|**Normalization**|BatchNormalization is used in the custom top layers.|
|**Regularization**|Dropout with a rate of 0.5 and L2 regularization with a factor of 0.001.|
|**Final feature reduction**|`GlobalAveragePooling2D()`|
|**Output**|Dense layer with softmax activation and 10 units.|

### **Training Details**

|Component|Value|
|:--|:--|
|**Optimizer**|Adam with a learning rate of 0.0001 and gradient clipping.|
|**Loss**|`categorical_crossentropy`|
|**Batch Size**|64|
|**Epochs**|10|
|**Learning Rate Schedule**|`ReduceLROnPlateau`, monitoring validation loss with a patience of 3 and factor of 0.5.|
|**Regularization**|Dropout (0.5), L2(0.001), and BatchNormalization.|
|**Data Augmentation**|`ImageDataGenerator` with rotation, width and height shifts, horizontal flip, and zoom.|

![image](https://github.com/user-attachments/assets/874409df-0707-41a0-95f5-3030170b6e88)


### **Learnings**

- Demonstrates the power of transfer learning by using a pre-trained model on a new dataset.
- Uses extensive data augmentation to increase the diversity of the training data and prevent overfitting.
- Shows how to fine-tune a pre-trained model by unfreezing and training the top layers.
- Employs a `Lambda` layer to resize input images to match the requirements of the base model.
- Uses a low learning rate and gradient clipping to ensure stable training during fine-tuning.
