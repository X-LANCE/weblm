# Hierarchical Multimodal Pre-training for Visually Rich Webpage Understanding

> This is the official implementation of our WSDM 2024 paper [WebLM](https://arxiv.org/abs/2402.18262). The pre-training data as well as pre-trained weights will be publicly available soon.


## Introduction

WebLM is a multimodal pre-training neural network designed to address the limitations of solely modeling text and structure modalities of HTML in understanding webpages. WebLM employs the hierarchical structure of webpages to extract structure-based visual feature and achieves significant improvement on several webpage understanding tasks.

The overall architecture is shown as follows:

<p align="center">
  <img src="https://raw.githubusercontent.com/X-LANCE/weblm/main/assets/model_architecture.png" alt="Model Architecture" width="80%"/>
</p>

### Data Preparation
- Data Collection: Collect 6 million webpages from over 60,000 domains (including HTML code, screenshots, and metadata)
- Data Preprocessing: Extract code segment (128 < token number < 512 ) and corresponding image area as input features

### Input Embeddings
- Separate structure tokens from content tokens to get text embeddings: $$t_i = TokEmb(w_i) + TagEmb({tag}_i) + PosEmb1D(i) + SegEmb({seg}_i)$$
- Align visual features with HTML inputs to get image embeddings: $${v}^{img}_{i} = {RoSPool}({VisualEncoder(I)})_{n_i}$$ 


$${v}^{box}_{i} = {Concat}({PosEmb2D_x}(x_0, x_1, w), {PosEmb2D_y}(y_0, y_1, h))$$


$${v}_i = {v}^{img}_{i} + {v}^{box}_{i},$$



### Pre-training Tasks
- **Masked Language Modeling (MLM)**: predict the masked content tokens
- **Tree Structure Prediction (TSP)**:         predict the tree relationship between structure and content inputs (parent-child, ancestor-descendent, other-relations)
- **Visual Misalignment Detection (VMD)**: identify the visual misalignment (enlarging or reducing image region by 50%) to enhance the visual robustness






## Citation

If you find WebLM useful in your research, please cite the following paper:

<pre>
@article{xu2024hierarchical,
  title={Hierarchical Multimodal Pre-training for Visually Rich Webpage Understanding},
  author={Xu, Hongshen and Chen, Lu and Zhao, Zihan and Ma, Da and Cao, Ruisheng and Zhu, Zichen and Yu, Kai},
  journal={arXiv preprint arXiv:2402.18262},
  year={2024}
}
</pre>
