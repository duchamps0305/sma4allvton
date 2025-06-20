# sm4llVTONs: A Family of Specialized Virtual Try-On Models

**Authors:** Andrea Baioni, Alex Puliatti  
**Contact:** [andrea@andreabaioni.com](mailto:andrea@andreabaioni.com), [a@puliatti.com](mailto:a@puliatti.com)

---

sm4llVTONs (same methodology 4 all VTON) is a new family of highly efficient and specialized diffusion models for virtual try-on (VTON) applications, and more. This page provides an overview of our current models, methodology, and performance benchmarks. The full details of our training methodology and architecture will be published in our upcoming research paper.

---

### Our Current Models

The sm4llVTONs family consists of several lightweight models, each an expert in a specific VTON domain. This specialization allows them to achieve state-of-the-art results on relatively small, targeted datasets.

| Model Name       | Task                     | Status  |
| ---------------- | ------------------------ | ------- |
| sm4ll-eye        | Sunglasses & Eyewear     | Pre-release |
| sm4ll-shoes      | Shoes & Footwear         | Pre-release |
| sm4ll-face       | Face Swapping            | Beta    |
| sm4ll-top        | Upper Body Garments      | Alpha   |
| sm4ll-bottom     | Lower Body Garments      | Alpha   |
| sm4ll-dress      | Dresses                  | Alpha   |
| sm4ll-bg         | Background Replacement   | Alpha   |

### Key Philosophy & Features

Our work is guided by a core philosophy that distinguishes it from general-purpose VTON and image editing models. Instead of a single, large model that handles many tasks, sm4llVTONs are experts fine-tuned for a single purpose. This results in higher fidelity, better detail preservation, and more intuitive control. Our methodology is built around a "train-like-you-infer" principle, ensuring that our models perform reliably on in-the-wild images, not just curated datasets.

---

## Methodology

While the complete methodology will be detailed in our paper, we can share a high-level overview of our three-stage process.

### Data Curation & Preparation

The model is trained on a dataset constructed from paired image sources and various augmentation techniques, such as cropping to mask size, automasking, etc. To improve robustness to real-world use cases, we employ an inference-aware masking strategy during the training phase. Instead of applying the best possible masking pipeline specific to the dataset, we employ the best possible masking pipeline that would be applied during inference. This way, we generate masks that simulate user behavior in production pipelines, enhancing the model's robustness against variance and artifacts common in user-uploaded content.

### The Training Process

All models in the sm4llVTONs family are trained using a unified methodology derived from foundational instruction-based models. We have introduced significant modifications to the training loop, including an optimized loss calculation. This technique focuses the model’s learning exclusively on the relevant image regions, which dramatically improves sample efficiency and the quality of the final result.

### Inference & Validation

Inference is handled via ComfyUI, in an environment that mirrors the training conditions. Our most critical component is a custom, and tailored to the model’s objective, automasking process that is consistent between training and real-world use. This end-to-end consistency is fundamental to our models' success and addresses a common pitfall in VTON systems, where models fail to generalize because their training data does not reflect real-world input.

---

## Results

### Glasses
| Example 1 | Example 2 | Example 3 | Example 4 |
| :---: | :---: | :---: | :---: |
| <img src="Assets/glass_1.jpg" alt="Glasses Example 1" width="200"/> | <img src="Assets/glass_2.jpg" alt="Glasses Example 2" width="200"/> | <img src="Assets/glass_3.jpg" alt="Glasses Example 3" width="200"/> | <img src="Assets/glass_4.jpg" alt="Glasses Example 4" width="200"/> |

### Top
| Example 1 | Example 2 | Example 3 | Example 4 |
| :---: | :---: | :---: | :---: |
| <img src="Assets/top_1.jpg" alt="Top Garment Example 1" width="200"/> | <img src="Assets/top_2.jpg" alt="Top Garment Example 2" width="200"/> | <img src="Assets/top_3.jpg" alt="Top Garment Example 3" width="200"/> | <img src="Assets/top_4.jpg" alt="Top Garment Example 4" width="200"/> |

### Bottom
| Example 1 | Example 2 | Example 3 | Example 4 |
| :---: | :---: | :---: | :---: |
| <img src="Assets/bottom_1.jpg" alt="Bottom Garment Example 1" width="200"/> | <img src="Assets/bottom_2.jpg" alt="Bottom Garment Example 2" width="200"/> | <img src="Assets/bottom_3.jpg" alt="Bottom Garment Example 3" width="200"/> | <img src="Assets/bottom_4.jpg" alt="Bottom Garment Example 4" width="200"/> |

### Dresses
| Example 1 | Example 2 | Example 3 | Example 4 |
| :---: | :---: | :---: | :---: |
| <img src="Assets/dress_1.jpg" alt="Dress Example 1" width="200"/> | <img src="Assets/dress_2.jpg" alt="Dress Example 2" width="200"/> | <img src="Assets/dress_3.jpg" alt="Dress Example 3" width="200"/> | <img src="Assets/dress_4.jpg" alt="Dress Example 4" width="200"/> |

### Shoes
| Example 1 | Example 2 | Example 3 | Example 4 |
| :---: | :---: | :---: | :---: |
| <img src="Assets/shoes_1.jpg" alt="Shoes Example 1" width="200"/> | <img src="Assets/shoes_2.jpg" alt="Shoes Example 2" width="200"/> | <img src="Assets/shoes_3.jpg" alt="Shoes Example 3" width="200"/> | <img src="Assets/shoes_4.jpg" alt="Shoes Example 4" width="200"/> |

### Qualitative Evaluations

- **Flux Kontext**: We struggled to find a consistent prompt structure for desired image modifications. Results shown are the best achievable but may not represent the model's full potential.
- **GPT-4o**: Produces aesthetically pleasing images but often generates a new image rather than modifying the original, which is unsuitable for production environments.
- **FASHN.ai**: Unique in its predictive approach to autosegmentation. Some poor results are likely due to limitations in the segmentation system, not the underlying model.
- **CatVTON Flux**: Performs well in generalization, even with out-of-scope items like eyewear and shoes, despite being trained on a dataset optimized for garments.
- **sm4llVTONs**: Our models consistently demonstrated stronger performance in:
    - Delivering accurate results through specialized, expert models.
    - Minimally affecting the input image while maintaining product precision, a key concern in production pipelines.

---

## Outside of Traditional VTON Use-Cases

### Face-swap

Currently in its initial stages, **sm4ll-face** has undergone preliminary testing against best-in-class, publicly available face swapping models: **ACE++** and **ReActor**. In these evaluations, **sm4ll-face** has demonstrated superior performance by achieving the best *Fréchet Inception Distance (FID)* and *CLIP* scores.

---

The sm4llVTONs family of models represents a significant step forward in specialized virtual try-on applications. By focusing on lightweight, expert models and a "train-like-you-infer" methodology, we achieve high-fidelity results that are robust to real-world conditions. Future work will involve releasing the full research paper with detailed benchmarks and continuing the development of our alpha and beta models.

---

## BibTeX

```bibtex
@inproceedings{sm4llVTONs2025,
  title={sm4llVTONs: A Family of Specialized Virtual Try-On Models},
  author={Andrea Baioni and Alex Puliatti},
  year={2025}
}
