# ERP Classification with SVM  

## 🧠 Introduction  
This project is part of a Bachelor's thesis developed by Diego Quattrone, Francesco Santambrogio, and Andrea Scarpellini, under the supervision of Letizia Clementi and Francesco Sgherzi for Professor Marco Santambrogio at Politecnico di Milano.  

The work was presented at the **45th Annual International Conference of the IEEE Engineering in Medicine & Biology Society (EMBC)**. For more details, please refer to the published article available in this repository.

---

## 📄 Project Overview  
The project focuses on classifying EEG Event-Related Potentials (ERPs) associated with the presentation of visual stimuli using a Support Vector Machine (SVM) classifier. The dataset consists of EEG recordings captured during stimulus observation, preprocessed and analyzed for pattern extraction and classification tasks.

---

## 📂 Repository Structure  
```
├── 01 - dataset preprocessing  
│   ├── 01-Modifying_annotation_from_tsv.ipynb  
│   └── 02-Create_and_saving_epochs.ipynb  
├── 02 - epochs analysis    
│   ├── 01-Get_ERPandFeatures_from_fif.ipynb  
│   ├── 02-Check_variance.ipynb  
│   ├── 03-Read_ERP_SVM.ipynb  
│   ├── ERP_SUB  
│   └── ERP_SUB_VARIANCE  
├── Plots  
│   ├── All_categories.png  
│   ├── Animals.png  
│   ├── Body_parts.png  
│   ├── Food.png  
│   ├── Tools.png  
│   └── Vehicles.png  
└── README.md
```

---

## 🔧 How to Run the Project  

### 1️⃣ Preprocessing  
First, execute the scripts in the **`01 - dataset preprocessing`** folder in order:  
1. **01-Modifying_annotation_from_tsv.ipynb**: Modify the annotations from the original `.tsv` files.  
2. **02-Create_and_saving_epochs.ipynb**: Perform the preprocessing steps and save the data in `.fif` format for further analysis.  

### 2️⃣ Feature Extraction and Classification  
Next, run the scripts in the **`02 - epochs analysis`** folder:  
1. **01-Get_ERPandFeatures_from_fif.ipynb**: Extract ERP features from the `.fif` files.  
2. **02-Check_variance.ipynb**: Analyze variance in the extracted features.  
3. **03-Read_ERP_SVM.ipynb**: Train the SVM classifier using the extracted ERP features.  

---

## ⚙️ Preprocessing Details  
- **Filtering:** Butterworth bandpass filter (0.1–12 Hz)  
- **Re-referencing:** Common average referencing  
- **Artifact Removal:** FastICA with notch filter for ocular artifacts  
- **Downsampling:** Reduced to 250 Hz  
- **Epoching:** From -100 ms to 1000 ms relative to stimulus onset  

---

## 🔍 Feature Extraction  
The feature extraction process was conducted using the following methodology:  
1. **Segmenting the Signal:**  
   - The segmentation was performed through **visual analysis on the super grand average**, which represents the averaged ERP signals across all subjects and conditions.  
   - Time intervals were visually identified based on relevant ERP components (e.g., P1, N1, and P2).  

2. **Feature Calculation:**  
   - For each identified time interval, the **mean value of the signal was computed** and used as the input feature for classification.  
   - This approach allowed us to capture stable and meaningful features for the classification task.  

3. **Selected Channels:**  
   - Occipital area (PO7, PO3, POz, PO4, PO8, O1, O2, Oz)  

---

## 🧑‍💻 Classification details
The classification task in this project was performed using a Support Vector Machine (SVM), a supervised machine learning algorithm known for its effectiveness in binary classification tasks. SVM works by learning to classify labeled training data to make accurate predictions on unseen, unlabeled data.
- **One-vs-Rest (OvR) Classification:** Since SVM is inherently a binary classifier, and our task involves multiple visual categories (animals, body parts, food, vehicles, and tools), we employed a One-vs-Rest (OvR) approach. This involves training multiple SVM classifiers, each one distinguishing one category against the rest of the categories. In total, five SVM classifiers were trained, one for each category.
- **Training and Testing Procedure:** The data for training and testing were standardized, and the dataset was split randomly into training (70%) and testing (30%) subsets. This split was repeated ten times to ensure the robustness of the results. We also performed a tenfold cross-validation to prevent overfitting and to ensure the classifier's generalization ability.
- **Evaluation Metrics:** The classification performance was evaluated using standard metrics, including accuracy, mean, and standard deviation of predictions across the ten iterations. For comparison, we also evaluated baseline performance using EEG features from the pre-stimulus period (100 to 0 ms), where we expect the classification to be near chance (20% accuracy for five categories). This helps to ensure that the classifier is capturing meaningful patterns rather than noise.
- **Feature Importance:** To identify which features contributed most to the classification accuracy, we performed a permutation importance analysis. This method involves randomly shuffling a feature's values and measuring the drop in model performance. A significant drop in performance indicates that the feature is important for the model's prediction.
 
---

## 📊 Results  
- **Inter-Trial Analysis:** Achieved up to 97% accuracy for visual category classification  
- **Single-Trial Analysis:** Achieved up to 34% accuracy for "Body parts" category  

---

## 📈 Plots  
Plots visualizing the ERPs waveform for different categories are available in the **`Plots`** folder.  

---

## 📚 References  
1. Grootswager, T. et al. *The representational dynamics of visual objects in rapid serial visual processing streams.*  
2. Hebart, M. N. et al. *THINGS: A database of 1,854 object concepts and more than 26,000 naturalistic object images.*  

---

## 📜 License  
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

