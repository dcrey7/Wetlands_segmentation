# Wetlands Segmentation App

This Hugging Face Space provides an interactive web interface for segmenting wetland areas in satellite imagery using a DeepLabv3+ model.

## Features

- Upload satellite imagery in common formats (JPG, PNG) or GeoTIFF format
- Optionally upload ground truth masks for evaluation
- Visualize wetland segmentation predictions
- Calculate metrics (IoU, Precision, Recall, F1) when ground truth is provided
- View wetland coverage percentage statistics

## Usage Instructions

1. **Upload Input Image**:
   - Use the "Upload Image" tab for common image formats (JPG, PNG, etc.)
   - Use the "Upload TIFF" tab for GeoTIFF files with multiple bands

2. **Upload Ground Truth (Optional)**:
   - If you have a ground truth mask, upload it to see evaluation metrics
   - The ground truth should be a binary mask where white (255) represents wetlands

3. **Analyze**:
   - Click the "Analyze Image" button to process the image
   - View the segmentation results and statistics

## Model Information

This app uses a model from the [dcrey7/wetlands_segmentation_deeplabsv3plus](https://huggingface.co/dcrey7/wetlands_segmentation_deeplabsv3plus) repository.

**Model Architecture:**
- DeepLabv3+ with ResNet-50 backbone
- Input: RGB satellite imagery (optimal size: 128×128 pixels)
- Output: Binary segmentation mask (Wetland vs Background)

The model was trained on a dataset of satellite imagery containing wetland regions, focusing on environmental monitoring and conservation planning applications.

## Example Output

When you upload an image, the app will display:
- The original input image
- The predicted wetland segmentation mask
- Ground truth mask (if provided)
- Statistics including wetland coverage percentage
- Evaluation metrics (if ground truth is provided)

## Limitations

- The model works best on imagery similar to its training data
- Performance may vary depending on image quality and characteristics
- The model is designed for 128×128 pixel inputs (images will be resized)
- While the model can process images with any number of bands, it was trained on RGB data

## License

This application and the underlying model are available under the Apache 2.0 license.

Check out the configuration reference at https://huggingface.co/docs/hub/spaces-config-reference
