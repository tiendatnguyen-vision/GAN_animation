# GAN_animation
# Abstract
In this project, i implement DCGAN for animation images. During the implementation, i got a lot of problems such as "mode collapse", "low quality generated image", "vanishing gradient", "checkerboard effect". I have step-by-step overcome these problems by applying some tricks and techniques recommended for GAN. 
For more detail, i overcome the "mode collapse" problem by applying "unrolled GAN" technique, that mentioned in https://jonathan-hui.medium.com/gan-unrolled-gan-how-to-reduce-mode-collapse-af5f2f7b51cd , for implementation of "unrolled GAN", i reference to the code from https://github.com/andrewliao11/unrolled-gans/blob/master/unrolled_gan.ipynb

To overcome the "vanishing gradient" problem, i make the discriminator less strong by flipping labels by 5% when training both generator and discriminator. This trick is mentioned in https://github.com/jaingaurav3/GAN-Hacks (trick 2 and trick 6). Furthermore, i also apply "label smoothing" technique and "dropout layer for discriminator" to limit strength of the discriminator. By using thse tricks, the accuracy of the discriminator rarely get higher than 0.95 ( actually it usually ranges from 0.6 to 0.9) and its loss never reach 0 ( it usually ranges from 0.5 to 1.0). So, the tricks effectively helps my model to escape from the "vanishing gradient" problem. Furthermore,

To improve the quality of generated image, my recommendation is to add batch normalization to the generator. I have tried to remove batch normalization layers from generator and then, the model started to generate garbage images without any reasonable pattern. Actually, i also add batch normalization to the discrimator because it helps model converge faster and also helps the training process more stable. 

My model get "checkerboard effect" in generated image because i use deconvolutional layers in the generator. To overcome it, i follow the guide from this link : https://distill.pub/2016/deconv-checkerboard/ . The tip is to use kernel size as a multiple of stride in each deconvolutional layer. 

I also implement some other tricks such as : 
- Label smoothing
- Remove fully connected layers in both generator and discriminator
- Leaky ReLU
- Sampling vectors from Gaussian distribution as input for the generator
- A deeper architecture for discriminator than generator 
The tricks are mentioned in https://github.com/jaingaurav3/GAN-Hacks 

# Data preparation
The data folder contains images used for training GAN model. For demo, i only upload 20 images in the "data" folder. You can download the full dataset from 
https://www.kaggle.com/soumikrakshit/anime-faces

# Installation 
- tensorflow==1.15.0
- keras==2.3.1
- opencv-python==3.4.3.18
- opencv-contrib-python==3.4.3.18

# Training
To train, simply run the file "train.py", during training process, a folder named "save" would be created, then weight and generated image during training will be saved into this folder. 
To load a trained model, please use the function "load_model" inside the class GAN. 

# Demo result 
In folder "image", i upload some generated images of my model after training about 1700 epochs. 







