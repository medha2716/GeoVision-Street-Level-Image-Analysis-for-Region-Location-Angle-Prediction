<style>
body {
  background: linear-gradient(135deg, #d1c4e9, #b2ebf2, #ffccbc, #c8e6c9);
  font-family: "Segoe UI", "Roboto", "Helvetica Neue", sans-serif;
  padding: 2rem;
  line-height: 1.6;
  color: #333;
}
h1 {
  background: none;
  -webkit-background-clip: initial;
  -webkit-text-fill-color: black;
  color: black;
}
h2, h3 {
  background: linear-gradient(90deg, #7e57c2, #26c6da, #ffa726, #66bb6a);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
code {
  background: rgba(0,0,0,0.05);
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
}
pre {
  background: #f5f5f5;
  padding: 1rem;
  border-radius: 8px;
  overflow: auto;
}
</style>


# Geolocation

This model predicts the location (latitude/longitude) where a photo was taken using:

- **EfficientNet B1**: Pre-trained image recognition model that I fine-tuned for this task (transfer learning)
- **Data augmentation**: Random flips, rotations, and color changes to make training more robust
- **CLAHE**: Added selectively (30% chance) to enhance contrast in images from densely sampled regions
- **Attention mechanism**: Helps the model focus on important parts of the image based on region
- **Region embedding**: Converts region IDs into number patterns the model can understand (Used region predictions instead of ground truth region labels)
- **Dual prediction heads**: Separate parts of the model predicted latitude and longitude
- **Weighted loss function**: Values latitude accuracy slightly more than longitude (1.2:0.8)
- **Early stopping**: Stops training when the model stops improving to prevent overfitting
- **Mixed precision training**: Uses automatic mixed precision where supported for faster training

This combines computer vision with location awareness to make better predictions.

Link to model: https://iiithydstudents-my.sharepoint.com/:u:/g/personal/medha_prasad_students_iiit_ac_in/ERixmSqg_Z5Hi0XPB2zfiR8Baoo6TpJgrnlLevYP5Xi4QA?e=8mgmQw