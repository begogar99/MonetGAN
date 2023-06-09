# MonetGAN 
## Painting with Generative Adversarial Networks: Generating Monet-Style Images Using Novel Techniques
### UW CSE 599 G1 - Deep Learning Final Project
This project was developed by Garrett Devereux, Deekshita S. Doli, and Begoña García Malaxechebarría as part of the graduate deep learning class at University of Washington, instructed by Ranjay Krishna and Aditya Kusupati.

### Introduction
Generative Adversarial Networks (GANs) have emerged as a powerful and versatile tool for generative modeling. In recent years, they have gained significant popularity in various research domains, particularly in image generation, enabling researchers to address challenging problems by generating realistic samples from complex data distributions. In the art industry, where tasks often require significant investments of time, labor, and creativity, there is a growing need for more efficient approaches that can streamline subsequent project phases. To this end, we present MonetGAN, a pioneering framework based on the Least Squares Deep Convolutional CycleGAN, specifically tailored to generate images in the distinctive style of 19th century renowned painter Claude Monet. After achieving non-trivial results with our baseline model, we explore the integration of advanced techniques and architectures such as ResNet Generators, a Progressive Growth Mechanism, Differential Augmentation, and Dual-Objective Discriminators. Through our research, we find that we can achieve superior results with small changes to gradually build up a successful model, rather than adding too many varying complexities all at once. These outcomes underscore the intricacies involved in the training of GANs, while also opening up promising avenues for further advancements at the intersection of art and artificial intelligence.

### Baseline Model
Our baseline model is built upon the Kaggle [I'm Something of a Painter Myself](https://www.kaggle.com/competitions/gan-getting-started) dataset, and employs a Least Squares Deep Convolutional CycleGAN. This model serves as our initial reference point for comparison and evaluation. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-deep-learning-monetganv1).

### [Pre-trained model](https://github.com/begogar99/MonetGAN/blob/main/MonetGAN_Pretrained.ipynb)
Subsequently, we utilized the official pre-trained CycleGAN model, specifically designed for the monet2photo task, to apply it to our dataset. This step allowed us to explore the results and identify areas for improvement, enabling us to analyze how the model could be further enhanced.

### [Industry model](https://github.com/begogar99/MonetGAN/blob/main/MonetGAN_Industry.ipynb)
Due to our interest in improving the evaluation of image quality produced by our model, we began exploring the concept of Human eYe Perceptual Evaluation. This led us to delve deeper into NVIDIA’s StyleGAN with truncation architecture, known for its ability to achieve hyper-realistic results in HYPE. However, integrating the StyleGAN architecture into our already complex model proved to be a more challenging task than anticipated. Considering our limited time constraints, we made the decision to initially focus on implementing its Progressive Growth Mechanism. 

### [ResNet Generators model] (https://github.com/begogar99/MonetGAN/blob/main/MonetGAN_ResNetGenerators.ipynb)
To enhance our model's performance and generalization, we employed data augmentation, expanding the dataset with diverse examples through various image transformations. Additionally, we implemented ResNet generators, similar to the UNet generators used in our baseline. The key distinction is that ResNet generators use residual blocks with short skip connections, while UNet generators employ long skip connections from output concatenations. You can find our Kaggle submission [here](https://www.kaggle.com/code/deekshitadoli/notebooke0627ec9f2/notebook).

### Differential Augmentation model
Recall that the dataset had 7028 photos but only 300 Monet paintings. To tackle the challenge of Data Efficient learning, we introduced a Differential Augmentation block before the Monet Discriminator. This block applies random augmentations to the Generated Monet and Real Monet images, preventing memorization by the discriminator. The augmentations include changes in brightness, saturation, and contrast, as well as translations and cutouts. This approach enables the Discriminator to learn more valuable features and pass them to the generator. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-deep-learning-diffaug-dc-cyclegan).

### Dual-Objective Discriminator model
In our implementation, we devised a novel approach by splitting the discriminator into two heads, each with its own unique loss function. This technique serves as regularization for the discriminator, introducing two distinct objectives. By doing so, we prevent the discriminator from relying solely on memorization and encourage it to provide more informative feedback to the generator. Theoretically, this setup allows the generator to enhance its results by effectively deceiving both heads of the discriminator. You can find our Kaggle submission [here](https://www.kaggle.com/code/garrettdevereux/uw-dc-d2cyclegan).

### Research Materials
The [paper](https://github.com/begogar99/MonetGAN/blob/main/MonetGAN_Paper.pdf) and [poster](https://github.com/begogar99/MonetGAN/blob/main/MonetGAN_Poster.pdf) for the final presentation of our project are available for access.
