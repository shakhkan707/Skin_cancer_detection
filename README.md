# Skin Cancer Detection Project

## Group: IT-2208
**Students:** Aniyar Baibossyn, Almas Murat, Shakhnazar Kapar  

## I. Introduction

### Problem
Skin cancer presents a significant global health risk, underscoring the need for early detection to facilitate effective treatment. Traditional diagnostic methods based on visual inspection can be subjective and inconsistent. This project aims to revolutionize skin cancer detection by developing a TensorFlow model utilizing transfer learning to improve diagnostic accuracy and efficiency.

### Literature Review with Links
In the pursuit of improved diagnostic tools, machine learning has emerged as a transformative force. Studies by Kim et al. and Nancy et al. highlight the significance of deep learning and transfer learning in enhancing image classification tasks in medical diagnostics. This project builds upon these findings to create a more reliable and accessible solution.

### Current Work
Our approach harnesses the power of pre-trained models, adapting them through transfer learning to recognize patterns indicative of malignant or benign skin lesions. This method not only accelerates the training process but also promises to deliver superior diagnostic capabilities.

## II. Data and Methods

### Information about the Data
The dataset comprises a diverse collection of skin lesion images, meticulously labeled as malignant or benign. Through exploratory data analysis, we've uncovered valuable insights into the dataset’s characteristics, ensuring our model is trained on a well-rounded and representative sample.

![Our Dataset](https://github.com/Aniyear/FINAL/blob/main/images/1.jpg)
![Our Dataset2](https://github.com/Aniyear/FINAL/blob/main/images/2.jpg)
```
Train Dataset:
malignant    900
benign       900

Validation Dataset:
benign       298
malignant    297

Test Dataset:
benign       150
malignant    148

```


### Description of the ML/DL Models
At the heart of our solution is TensorFlow, which we’ve employed to construct and fine-tune our machine learning models. The integration of transfer learning techniques allows us to utilize the robust feature extraction capabilities of established models, tailoring them to our specific use case.
```
import tensorflow_hub as hub

module_url = "https://tfhub.dev/google/tf2-preview/inception_v3/feature_vector/4"
m = tf.keras.Sequential([
    hub.KerasLayer(module_url, output_shape=[2048], trainable=False),
    tf.keras.layers.Dense(1, activation="sigmoid")
])

m.build([None, IMG_HEIGHT, IMG_WIDTH, 3])

m.compile(loss="binary_crossentropy", optimizer="adam", metrics=["accuracy"])

m.summary()
```
We adjusted the dimensions of all images to (224, 224, 3) to align with the input requirements of the InceptionV3 architecture. To leverage transfer learning, we utilized the TensorFlow Hub library to import and incorporate the InceptionV3 architecture, along with its pre-trained weights from ImageNet. By setting the 'trainable' parameter to False, we ensured that the pre-trained weights remain fixed during our training process. Additionally, we appended a final output layer comprising a single unit. This layer is designed to produce an output value ranging between 0 and 1. A value closer to 0 signifies a prediction of "benign," while a value closer to 1 indicates a prediction of "malignant."

KerasLayer (Transfer Learning from InceptionV3):
Description: This layer uses transfer learning from the InceptionV3 architecture via TensorFlow Hub. It takes the preprocessed input images of size (224, 224, 3) and extracts features from them. The output shape is (None, 2048), meaning that each input image is represented by a feature vector of length 2048.

Dense (Final Output Layer):
Description: This layer is the final output layer of the model. It has 1 unit, which outputs a single scalar value representing the predicted probability of the input image belonging to the "malignant" class. The output is a value between 0 and 1, where values close to 0 indicate a prediction of "benign" and values close to 1 indicate a prediction of "malignant".

## III. Results

### Results with Tables, Pictures, and Interesting Numbers
![Changes](https://github.com/Aniyear/FINAL/blob/main/images/3.jpg)

![Changes](https://github.com/Aniyear/FINAL/blob/main/images/4.jpg)

![Changes](https://github.com/Aniyear/FINAL/blob/main/images/5.jpg)

![Changes](https://github.com/Aniyear/FINAL/blob/main/images/6.jpg)

## IV. Discussion

### Critical Review of Results
While our results are promising, we maintain a critical perspective, acknowledging the model’s limitations and the need for further testing on broader datasets to ensure its robustness and reliability.

### Next Steps
Looking ahead, we aim to refine our model through advanced hyperparameter tuning, exploration of novel pre-trained models, and the incorporation of data augmentation strategies. The ultimate goal is to deploy a scalable and user-friendly application, making skin cancer screening more accessible than ever before.

## Conclusion

This project stands as a beacon of innovation in the field of medical image analysis, showcasing the transformative potential of TensorFlow and transfer learning in the fight against skin cancer. With continued development and refinement, we are poised to make a significant impact on global health.

## References

1. Kim, H. E., Cosa‐Linan, A., Santhanam, N., Jannesari, M., Maros, M. E., & Ganslandt, T. (2022). Transfer learning for medical image classification: a literature review. *BMC Medical Imaging, 22*(1). [https://doi.org/10.1186/s12880-022-00793-7](https://doi.org/10.1186/s12880-022-00793-7)
2. Nancy, V. a. O., Prabhavathy, P., Arya, M. S., & Ahamed, B. S. (2023). Comparative study and analysis on skin cancer detection using machine learning and deep learning algorithms. *Multimedia Tools and Applications, 82*(29), 45913–45957. [https://doi.org/10.1007/s11042-023-16422-6](https://doi.org/10.1007/s11042-023-16422-6)
3. Preprocessing and augmentations Classification Dataset (v11, Noise - 0 to 0.6) by RedRonin. (n.d.). Roboflow. [https://universe.roboflow.com/redronin/preprocessing-and-augmentations-zl5il/dataset/11](https://universe.roboflow.com/redronin/preprocessing-and-augmentations-zl5il/dataset/11).
