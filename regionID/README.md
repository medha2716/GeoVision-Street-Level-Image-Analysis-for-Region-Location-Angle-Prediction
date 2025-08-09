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

# Region Classification

I used transfer learning with a pre-trained ConvNeXt-Base CNN model. The model was fine-tuned on regional image data with 15 classes. For pre-processing, I implemented data augmentation including random crops, flips, rotations, and color adjustments to improve generalization.

To enhance performance, I added dropout (0.2) before the final classification layer to reduce overfitting. The training used Adam optimizer with a small learning rate (0.00002) and weight decay. I implemented early stopping and learning rate reduction to optimize training.

The model training included batch processing with careful monitoring of validation metrics. This transfer learning approach leverages the powerful feature extraction capabilities of ConvNeXt while adapting it specifically for region classification.

Link to model: https://iiithydstudents-my.sharepoint.com/:u:/g/personal/medha_prasad_students_iiit_ac_in/EYbXDqCIsN1HsxYYWPssFacBdRJnPx62uGtxt6uAvSZNRg?e=AiL4xW

