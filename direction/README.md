
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

# Angle Prediction

The model uses a fine-tuned EfficientNet-B0 CNN backbone for angle prediction in images.

Here's a summary of the key technical aspects:

- **Model Architecture**: Pre-trained EfficientNet-B0 backbone with custom layers for angle prediction (trasnfer learning)

- **Region-Aware Design**: Incorporates region embeddings through an attention mechanism to contextualize predictions (Used region predictions instead of ground truth region labels)

- **Angular Output**: Predicts angles as unit vectors $(\sin \theta, \cos \theta) \in \mathbb{R}^2$ where $\|v\| = 1$, enabling seamless handling of circular data where $0^\circ$ and $360^\circ$ are identical

- **Loss Function**: Uses a weighted combination
  $$
  L = \alpha \cdot L_{\text{vector}} + (1-\alpha) \cdot L_{\text{angle}}
  $$
  where:

  - $L_{\text{vector}} = 1 - (\hat{v} \cdot v)$ measures vector alignment (dot product between predicted and true unit vectors)

  - $L_{\text{angle}} = \frac{\min(|\hat{\theta} - \theta|, 360 - |\hat{\theta} - \theta|)}{180}$ directly minimizes angular distance while respecting circularity

- **Data Processing**: Uses region information from a separate model's predictions to enhance angle estimation

- **Augmentation Strategy**: Carefully implements color jittering, random crops, and Gaussian blur while avoiding rotations that would alter the angle ground truth

- **Training Approach**: Employs weighted sampling to balance angle distribution across 36 bins (10° each)

- **Optimization**: Uses AdamW with OneCycleLR scheduler and gradient clipping to stabilize training

The sine-cosine representation effectively handles the circular nature of angles and improves training stability by mapping the periodic domain to a continuous representation in $\mathbb{R}^2$.

Link to model weight: https://iiithydstudents-my.sharepoint.com/:u:/g/personal/medha_prasad_students_iiit_ac_in/EXT00YH6FC1Gt5twU1U84gQBnyfHacY_MwtmL5IDX4Trog?e=70hvaX




