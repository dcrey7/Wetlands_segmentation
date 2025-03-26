# Wetland Localization Using Satellite Imagery and Deep Learning  

## 🌍 Project Overview  
This project aims to **automate wetland detection** using **Sentinel-2 satellite imagery** and **deep learning segmentation models**. Wetlands are critical for biodiversity, carbon storage, and water filtration, but mapping them manually is resource-intensive. Our solution leverages AI to provide scalable, efficient monitoring tools for environmental conservation.  

- Check out Wetands segementation app at [Hugging face space](https://huggingface.co/spaces/dcrey7/wetland_segmentation_deeplabsv3plus)
- Check out the Model card at [Hugging face model card](https://huggingface.co/dcrey7/wetlands_segmentation_deeplabsv3plus)

**Key Features**:  
- **Semantic segmentation** of wetlands using U-Net and DeepLabV3+ models.  
- **Cloud detection** pipeline to filter unusable satellite images (LightGBM classifier).  
- **Interactive web app** for visualizing predictions and wetland coverage.  
- Open-source implementation with Hugging Face Spaces deployment.  

---

## 📂 Repository Structure  
```  
├── data/                    # Raw Sentinel-2 images, masks, and shapefiles  
├── notebooks/               # Jupyter notebooks for EDA, preprocessing, and modeling  
├── docs/                    # Project report, literature review, and presentations  
└── README.md  
```  

---

## 🛠️ Technical Approach  

### **1. Data Pipeline**  
- **Data Source**: 36 Sentinel-2 images (2021–2023) of a French wetland area (62×357 pixels, 10 spectral bands).  
- **Preprocessing**:  
  - Patched images into 62×62 tiles (180 total patches).  
  - Applied padding (128×128) to preserve mask quality.  
  - Augmented data with flips, rotations, and random crops.  
- **Class Imbalance**: Wetlands covered only **8.93%** of the area → Used **Dice Loss** to handle imbalance.  

### **2. Models**  
| Model               | Architecture          | Input Bands | Test mIoU | Key Insight |  
|---------------------|-----------------------|-------------|-----------|-------------|  
| DeepLabV3+ (FT)     | ResNet-34 encoder     | RGB         | **52.71** | Best generalization |  
| U-Net (FT)          | ResNet-34 encoder     | RGB         | 50.80     | Overfitted on training data |  
| Small U-Net         | Custom lightweight    | 12 bands*   | 46.85     | Struggled with limited data |  

*Included NDVI, NDWI, and 10 Sentinel-2 bands.  

### **3. Cloud Detection**  
- **Model**: LightGBM (F1-score: **0.77**) using Coefficient of Variation (CV) features from 10 bands.  
- **Impact**: Filtered 19.4% cloudy patches to improve segmentation accuracy.  

---

## 🚀 Results  
- **Best Model**: Fine-tuned DeepLabV3+ achieved **10.02% wetland IoU** (vs. 5.34% for U-Net).  
- **Limitations**: Low resolution (54.85m/pixel) and small dataset hindered performance.  
- **Future Work**:  
  - Integrate Sentinel-1 radar data for cloud-free analysis.  
  - Scale to 1000+ high-res patches and test Swin U-Net architectures.  

---

## 🖥️ Demo App  
Try the [Hugging Face Spaces demo](https://huggingface.co/spaces/dcrey7/wetland_segmentation_deeplabsv3plus)to upload Sentinel-2 images and get wetland predictions!  

**Features**:  
- Wetland coverage % and cloud interference alerts.  
- Side-by-side comparison of ground truth vs. predictions.  

---

## 🔧 Dependencies  
```  
Python 3.8+  
torch >= 1.10  
rasterio, geopandas  
transformers.js (for web deployment)  
```  
Install: `pip install -r requirements.txt`  

---

## 📜 Citation  
```  
@misc{wetlandseg2025,  
  author = {Abhishek Thomas et al.},  
  title = {Wetland Localization via Satellite Imagery and Deep Learning},  
  year = {2025},  
  publisher = {GitHub},  
  journal = {GitHub repository},  
  howpublished = {\url{https://github.com/your-repo}}  
}  
```  

---

## 🤝 Contributors  
- **Abhishek Thomas** (Data Science, MLOps)  
- **Dilara Toygar, Erwin Byll, Henry Turnbull, Siwen Lu**  

*Part of MSc Data Science & AI at emlyon business school, in collaboration with Datacraft.*  

**Let’s democratize AI for environmental conservation!** 🌱💻  

--- 
**License**: MIT  
**Questions?** Open an issue or contact [abhishek01789@gmail.com](mailto:abhishek01789@gmail.com).  

*For detailed methodology, see [DSM_Group3_WetlandSegmentation.pdf](./docs/DSM_Group3_WetlandSegmentation.pdf).*  

--- 

### ✨ Why This Matters  
This project bridges **AI** and **ecology**—proving that scalable, open-source tools can accelerate wetland preservation. By optimizing models for the web (e.g., transformers.js), we aim to make environmental monitoring accessible to everyone.  

**Join us in building the future of WebML for sustainability!**  

---  

*(For a lightweight summary of my ML/web-dev projects, check out my [portfolio](https://github.com/dcrey7) or [LinkedIn](https://linkedin.com/in/dcrey7).)*
