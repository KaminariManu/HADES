# HADES: Hostile Attack Detection and Evaluation Strategy

**Team Members:**  
- Emanuele Cuono Amoruso  
- Luigi Barbato  
- Aurora Maio

---

## Project Overview

HADES is a research-based project that investigates the vulnerabilities of Convolutional Neural Networks (CNNs) when exposed to adversarial attacks. Our goal is to study how subtle, often imperceptible, perturbations can lead robust deep learning models astray and to evaluate various defenses aimed at mitigating these vulnerabilities. Using the GoogLeNet architecture and the CIFAR-10 image classification dataset, we build a comprehensive framework that generates adversarial examples, applies state-of-the-art attack mechanisms, and tests defensive strategies to improve the robustness of neural networks.

---

## Adversarial Attacks Explored

Adversarial attacks exploit the inherent weaknesses of deep learning models by making carefully crafted modifications to inputs. In HADES, we focus on several key types:

### Types of Adversarial Attacks
- **White-box Attacks:** These attacks assume full knowledge of the target model (architecture, weights, etc.) to generate effective perturbations.
- **Black-box Attacks:** Without accessing the internal structure of the model, these attacks rely solely on input-output pairs to infer the model’s vulnerabilities.

### Specific Attack Methods
1. **FGSM (Fast Gradient Sign Method):**  
   - *Overview:* Uses the sign of the gradient of the loss with respect to the input to create a perturbation scaled by a factor ε.
   - *Characteristics:* A one-shot method that is computationally efficient and provides a quick way to evaluate model sensitivity.
2. **PGD (Projected Gradient Descent):**  
   - *Overview:* An extension of FGSM, PGD iteratively applies small FGSM steps while keeping the perturbation bounded within a specified neighborhood.
   - *Characteristics:* Generally more potent than FGSM due to its iterative refinement, albeit with increased computational demands.
3. **JSMA (Jacobian-based Saliency Map Attack):**  
   - *Overview:* A targeted attack that identifies the most influential pixels based on the Jacobian (i.e., the gradient of the output with respect to the input) and perturbs them to force the model into a desired misclassification.
   - *Characteristics:* Although it offers precise targeting, JSMA is particularly CPU-bound and computationally intensive with current tools.

---

## Defense Strategies

Along with generating and understanding adversarial attacks, HADES explores two primary defense mechanisms to improve model robustness:

### 1. Adversarial Training
- **Description:** Involves augmenting the training process by including adversarial examples along with clean data.  
- **Benefits:** Provides strong, specific protection against the types of attacks seen during training.
- **Trade-offs:** Typically results in a lower accuracy on clean images and may not generalize to unseen types of adversarial attacks.

### 2. Defense Distillation
- **Description:** Implements a two-model approach where a “Teacher” model, pre-trained with clean and adversarial examples, transfers its knowledge to a “Student” model through soft labels.
- **Benefits:** Helps in slightly improving model robustness under adversarial settings.
- **Trade-offs:** Requires additional computational resources and may not perform equally well against all attack types, especially when using a pre-trained model rather than a specialized architecture.

---

## Experimental Setup & Results

The experimental part of HADES leverages the GoogLeNet architecture, renowned for its inception layers which balance depth and efficiency by running convolutions of various sizes in parallel. The CIFAR-10 dataset—a benchmark in image classification—is used to assess model performance under hostile conditions.

### Key Observations:
- **FGSM & PGD:** Quickly expose the sensitivity of the model, proving that even minimal perturbations can significantly harm performance.
- **JSMA:** Validates the ability to force specific misclassifications by perturbing crucial pixels, albeit at higher computational costs.
- **Adversarial Training:** Demonstrates strong defense capabilities against the particular type of attack it is trained on but at a slight overall accuracy cost.
- **Defense Distillation:** Contributes limited improvements in robustness while imposing a higher computational burden during the training phase.

Additionally, data augmentation emerged as an effective supplementary technique—particularly for smaller perturbation values—to balance the model's robustness against adversarial inputs and its accuracy on clean data.

---

## Conclusions & Future Work

HADES has provided a framework that not only exposes the weaknesses of modern CNNs to adversarial attacks but also rigorously evaluates current defensive strategies. Some key conclusions include:

- **Trade-offs in Defense Techniques:** Both adversarial training and defense distillation improve robustness but often reduce performance on clean inputs or require significant computational resources.
- **Efficacy of Data Augmentation:** This simple yet effective method can enhance defense, especially when perturbation strengths are relatively low.

### Future Directions:
- **Optimize JSMA:** Focus on improving efficiency for targeted pixel perturbations.
- **Broader Architectural Comparisons:** Evaluate newer network architectures to examine if improvements in robustness are linked to model structure rather than just defense methodologies.
- **Hybrid Approaches:** Explore training regimes that combine adversarial defense methods to offer comprehensive protection against a variety of attack types.
- **Multi-Attack Robustness:** Develop defenses that provide generalized protection rather than being specific to one type of adversarial attack.

---

## Repository Structure

- **/attacks:** Scripts implementing FGSM, PGD, and JSMA attacks.  
- **/defenses:** Implementation of adversarial training and defense distillation techniques.  
- **/data:** Scripts for processing and augmenting CIFAR-10 images.  
- **/results:** Jupyter notebooks, plots, and logs documenting experimental outcomes.  
- **README.md:** Comprehensive documentation of the project, including setup instructions, experimental details, and future work.

---

## References

1. Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). *Explaining and Harnessing Adversarial Examples*. [https://arxiv.org/abs/1412.6572](https://arxiv.org/abs/1412.6572)
2. Szegedy, C., Liu, W., Jia, Y., Sermanet, P., Reed, S., Anguelov, D., Erhan, D., Vanhoucke, V., & Rabinovich, A. (2014). *Going Deeper with Convolutions*. [https://arxiv.org/abs/1409.4842](https://arxiv.org/abs/1409.4842)
3. Costa, J. C., Roxo, T., Proença, H., & Inácio, P. R. M. (2024). *How Deep Learning Sees the World: A Survey on Adversarial Attacks & Defenses*. IEEE Access, 12, 61113–61136. [https://doi.org/10.1109/access.2024.3395118](https://doi.org/10.1109/access.2024.3395118)
4. Wiyatno, R., & Xu, A. (2018). *Maximal Jacobian-based Saliency Map Attack*. [https://arxiv.org/abs/1808.07945](https://arxiv.org/abs/1808.07945)
5. Papernot, N., McDaniel, P., Wu, X., Jha, S., & Swami, A. (2016). *Distillation as a Defense to Adversarial Perturbations against Deep Neural Networks*. [https://arxiv.org/abs/1511.04508](https://arxiv.org/abs/1511.04508)
