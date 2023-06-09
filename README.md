# MonetGAN 
## Painting with Generative Adversarial Networks: Generating Monet-Style Images Using Novel Techniques
### UW CSE 599 G1 - Deep Learning Final Project
This project was developed by Garrett Devereux, Deekshita S. Doli, and Begoña García Malaxechebarría as part of the graduate deep learning class at University of Washington, instructed by Ranjay Krishna and Aditya Kusupati.

### Introduction
Generative Adversarial Networks (GANs) have emerged as a powerful and versatile tool for generative modeling. In recent years, they have gained significant popularity in various research domains, particularly in image generation, enabling researchers to address challenging problems by generating realistic samples from complex data distributions. In the art industry, where tasks often require significant investments of time, labor, and creativity, there is a growing need for more efficient approaches that can streamline subsequent project phases. To this end, we present MonetGAN, a pioneering framework based on the Least Squares Deep Convolutional CycleGAN, specifically tailored to generate images in the distinctive style of 19th century renowned painter Claude Monet. After achieving non-trivial results with our baseline model, we explore the integration of advanced techniques and architectures such as ResNet Generators, a Progressive Growth Mechanism, Differential Augmentation, and Dual-Objective Discriminators. Through our research, we find that we can achieve superior results with small changes to gradually build up a successful model, rather than adding too many varying complexities all at once. These outcomes underscore the intricacies involved in the training of GANs, while also opening up promising avenues for further advancements at the intersection of art and artificial intelligence.

### [Baseline Model](https://www.github.com/begogar99/MonetGAN/MonetGAN_Baseline.ipynb)
Our baseline model is built upon the Kaggle [I'm Something of a Painter Myself](https://www.kaggle.com/competitions/gan-getting-started) dataset, and employs a Least Squares Deep Convolutional CycleGAN. This model serves as our initial reference point for comparison and evaluation. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-deep-learning-monetganv1).

### [Pre-trained model]()
Subsequently, we utilized the official pre-trained CycleGAN model, specifically designed for the monet2photo task, to apply it to our dataset. This step allowed us to explore the results and identify areas for improvement, enabling us to analyze how the model could be further enhanced.

### [Industry model]()
Due to our interest in improving the evaluation of image quality produced by our model, we began exploring the concept of Human eYe Perceptual Evaluation. This led us to delve deeper into NVIDIA’s StyleGAN with truncation architecture, known for its ability to achieve hyper-realistic results in HYPE. However, integrating the StyleGAN architecture into our already complex model proved to be a more challenging task than anticipated. Considering our limited time constraints, we made the decision to initially focus on implementing its Progressive Growth Mechanism. 

### [Differential Augmentation model]()
Recall that while the dataset contained 7028 Photos, it only had 300 Monet Paintings. With such a low number of images from one of our domains, we focused on aiming to solve the problem of Data Efficient learning. The issue which such little data in one of the domains is that the discriminator is able to memorize the dataset. We introduced a Differential Augmentation block right before the Monet Discriminator. This takes in the Generated Monet and the Real Monet and performs random augmentations such as random changes in brightness, saturation, and contrast, as well as random translations and cutouts. By introducing these augmentations, memorization is prevented and the Discriminator is able to learn more valuable features that are then passed to the generator. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-deep-learning-diffaug-dc-cyclegan).

### [Dual-Objective Discriminator]()
In our implementation, we introduced a novel approach by splitting the discriminator into two heads, each with its own distinct loss function. This technique serves as a form of regularization for the discriminator, as it is now faced with two different objectives. This prevents the discriminator from simply memorizing the dataset and encourages it to provide more informative feedback to the generator. Theoretically, this setup enables the generator to improve its results by effectively fooling both heads of the discriminator. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-dc-d2cyclegan).
