## Deep Learning Fundamentals

- **Epoch**:
    
    - An **epoch** is one complete cycle through the entire training dataset.
    - During each epoch, the model learns by processing all the training samples in the dataset once, adjusting its weights to improve based on the error it makes.
    - Training typically involves many epochs, allowing the model to gradually improve as it cycles through the dataset multiple times
    
- **Batch**:
    
    - A **batch** is a subset of the training dataset processed at once. Instead of training on all samples at once (which would be computationally intensive), the model is trained on small batches of data, called **mini-batches**.
    - In your code, `batch_size=64` means that each batch contains 64 images.
    - The model processes each batch one at a time, and for each batch, it calculates an **output** and an **error** based on that batch alone.
    - This approach is called **mini-batch training** and helps with faster computation and smoother optimization.
    
- **Forward Pass**:
    
    - In a **forward pass**, the input data (images in this case) moves forward through the neural network layers to produce an output (prediction).
    - For example, if the input image is of a cat, the network’s prediction output might indicate probabilities that the image belongs to various classes (cat, dog, car, etc.).
    - In this code, `output = model(data)` performs a forward pass using the `model` on the current `data` (batch of images) to get the `output` (predictions).
    
- **Loss Function**:
    
    - The **loss function** (or cost function) measures the difference between the predicted output and the actual target labels.
    - Here, `criterion = nn.CrossEntropyLoss(reduction="sum")` specifies the **Cross-Entropy Loss**, which is commonly used for classification tasks.
    - This function calculates how far the model's predictions are from the true labels for the current batch.

- **Cross-Entropy Loss**: 

	- In classification tasks, **Cross-Entropy Loss** is used to measure how well the model's predictions match the true labels.
	- Cross-Entropy Loss compares the predicted probabilities for each class (output of the model) with the true label (actual class) and calculates a single value that represents the “error” for that prediction.
	    - If the model predicts a cat image with a high probability for "cat" and low probabilities for other classes, Cross-Entropy Loss will be low.
	    - If the model predicts incorrectly (e.g., high probability for “dog” when the image is a cat), Cross-Entropy Loss will be high.

**Formula**: Cross-Entropy Loss LLL for a single example with true label yyy and predicted probability p(y)p(y)p(y) for each class CCC is given by:

![[crossentropy.png]]

This loss function encourages the model to assign high probabilities to the correct class and low probabilities to incorrect classes.

- **Backward Pass (Backpropagation)**:
    
    - After computing the loss, the network performs a **backward pass** to adjust the weights in the network based on the loss.
    - The **loss.backward()** function in the code calculates the gradient of the loss with respect to each weight in the network.
    - These gradients tell us the direction and magnitude by which each weight should be adjusted to reduce the loss.

- **Optimization**:
    
    - The **optimizer** uses the gradients calculated during the backward pass to update the weights of the model.
    - ![[gradient.png]]
    - The line `optimizer.step()` updates each weight in the network based on its gradient, the learning rate, and any additional parameters like momentum.
    - The learning rate (`lr=0.003` here) controls how large a step each weight takes in the direction of minimizing the loss.

- Training through forward pass
	- start with some random weights, biases, learning weight
- computing the loss function 
- optimization through backpropagation
	- using Gradient descent for optimizing the weights
		- taking gradient of loss function w.r.t weights in each iteration
		- Update the weights by **subtracting** the gradient from the weights (go in the opposite direction of gradient to decrease the loss)
	- using using adaptive learning methods to adapt learning rates to loss landscape/ model in order to get a good loss landscape at the end
		 - Adam
		 - SGD  :  instead of taking gradient from all the weights over the entire dataset, only pick a batch of data and compute gradient of weights   -> faster and more accurate gradient
			 - we can compute batches of data in parallel (GPU)
- Regularization to overcome overfitting (overfit to training data)
	 - Dropout method : randomly drop half of the neurons (set activation to zero) in a seperate iteration that will forces the network to not rely on that neurons during training forward pass
		 - the network learn to build pathways from input and that it can not rely on single features of the training set too extensively 
	 - Early stopping : find the bias/variance tradeoff and stop training at a point that has low test loss and training loss , exactly before going to overfitting  

### Deep Sequence Modelling 
#### RNN

- Training 
	- RNN has a state ht that is updated at each time step as a sequence is processed
	- Internal state at each time t itself, is calculated based on the input at time t and previous hidden state  -> recurrence formula
	- output vector at time t is calculated based on the internal state at time t
	- Reuse the same weights and same recurrence function at every time step
	- summarizing all the input in the last hidden state

- Backpropagation
	- Total value of the loss is the sum of the loss from each time step
	
- Embedding of input data(language) into a numerical vector
	- fixed-size one-hot embedding vector of numbers for each letter in our vocabulary
	
- handle variable length of input and output data


		 
### What is latent space

When we see animals like cats, dogs, or horses, we don’t memorize every detail of each species but instead create a mental template based on general features.
in latent space, deep learning models map animals with shared features closer together, so the model can classify a new animal based on these learned patterns.

In essence, latent space serves as a blueprint of input data, retaining only the most defining characteristics and reducing the computational complexity of high-dimensional data.
The primary objective of deep learning is to transform raw data—like the pixel values of an image—into suitable internal representations or feature vectors from which the learning subsystem, often a classifier, can detect or classify patterns.

A deep learning model takes raw data as input and outputs discriminative features that lie in a lower-dimensional space called latent space. These features allow the model to tackle various tasks such as classification, regression, and reconstruction. Encoding data in a low-dimensional latent space before tasks like classification or regression addresses the need for data compression, especially with high-dimensional input. Encoding this data into latent space enables the system to capture useful patterns without processing each pixel individually.

#### Early Dimensionality Reduction Techniques: PCA and LDA

Latent space has its roots in dimensionality reduction and feature extraction techniques. Principal Component Analysis (PCA), developed in the early 20th century, was one of the first approaches to reduce the dimensions of high-dimensional data by identifying and retaining only the principal components, or directions of maximum variance. By transforming the data along these key directions, PCA created simplified, lower-dimensional representations that allowed for easier analysis. The success of PCA illustrated the potential of compressed, meaningful data representations, paving the way for modern latent spaces.
Similarly, Linear Discriminant Analysis (LDA), another early technique, sought to reduce data dimensions for classification tasks. Unlike PCA, LDA is supervised and maximizes the separability between different classes by finding a linear combination of features that differentiates them. By mapping data to a new, lower-dimensional space with clearly defined clusters, LDA enabled easier classification and analysis.

#### The Shift to Neural Network-Based Representations

With advancements in machine learning, researchers began developing neural network-based methods to capture non-linear relationships in data—an area where traditional methods like PCA and LDA were limited. This shift led to the emergence of autoencoders, a type of neural network that learns efficient, compressed representations of data by mapping it into latent space using an encoder-decoder structure.

Autoencoders consist of two main components:

Encoder: Compresses input data into a latent representation, reducing its dimensionality.
Decoder: Reconstructs the original data from the latent representation, ensuring the compressed data retains critical features.

Autoencoders introduced the concept of an adaptable, data-specific latent space that could learn complex, non-linear patterns, making them ideal for tasks such as noise reduction, anomaly detection, and dimensionality reduction.

Variational Autoencoders (VAEs) expanded on this idea by introducing probabilistic elements into latent space. Unlike traditional autoencoders, VAEs encode data as a probability distribution over the latent space, typically a Gaussian, from which new samples can be drawn.

#### Latent Space in Generative Adversarial Networks

The advent of Generative Adversarial Networks (GANs) transformed latent space into a foundation for data generation. GANs employ a generator-discriminator structure, where the generator takes random vectors from latent space and maps them to realistic data points, while the discriminator learns to distinguish between real and generated samples. This adversarial setup allows GANs to generate highly realistic outputs, with latent space acting as a “creative” space from which new data can be sampled and generated.

#### Applications of latent space

###### 1. Data Compression
One of the most practical uses of latent space is in data compression. By mapping high-dimensional input data into a lower-dimensional latent representation, models can capture the essential features of the data while significantly reducing its size.
###### 2. Anomaly Detection
Latent space representations make it possible to detect anomalies by highlighting data points that deviate significantly from learned patterns
##### 3. Data Generation
Latent space is crucial in generative modeling, where new data samples are created by sampling from the latent space. Models like Generative Adversarial Networks (GANs) and Variational Autoencoders (VAEs) leverage this capability to generate realistic images, videos, and sounds.
##### 4. Transfer Learning
Latent space representations allow for transfer learning, where a model trained on one task can transfer its learned representations to a different but related task.


### U-Net architecture

U-Net is a convolutional neural network (CNN) architecture that was specifically designed for biomedical image segmentation tasks.
The U-Net architecture is characterized by its U-shaped structure, which gives it its name. It consists of an encoding path and a decoding path.
- Encoding Path: This part of the network captures the context of the input image by using a series of convolutional and max-pooling layers to downsample the spatial dimensions. It “contracs” the original images.
- Decoding Path: The decoding path uses upsampling and convolutional layers to produce a segmentation map that has the same spatial dimensions as the input image. It “expands” the contracted images.
- ![[Pasted image 20241227183335.png]]

U-Net’s strength in segmentation comes from its use of skip connections, (grey arrows in the Figure 1) which connect the encoding and decoding paths by merging features, which allow for the fusion of low-level and high-level features. This helps retain spatial details lost during downsampling, preserving the image’s local and global context

```
class DoubleConv(nn.Module):  
def __init__(self, in_channels, out_channels):  
super().__init__()  
self.conv_op = nn.Sequential(  
nn.Conv2d(in_channels, out_channels, kernel_size=3, padding=1),  
nn.ReLU(inplace=True),  
nn.Conv2d(out_channels, out_channels, kernel_size=3, padding=1),  
nn.ReLU(inplace=True)  
)  
  
def forward(self, x):  
return self.conv_op(x)
```

```
class DownSample(nn.Module):  
def __init__(self, in_channels, out_channels):  
super().__init__()  
self.conv = DoubleConv(in_channels, out_channels)  
self.pool = nn.MaxPool2d(kernel_size=2, stride=2)  
  
def forward(self, x):  
down = self.conv(x)  
p = self.pool(down)  
  
return down, p
```

```
class UpSample(nn.Module):  
def __init__(self, in_channels, out_channels):  
super().__init__()  
self.up = nn.ConvTranspose2d(in_channels, in_channels//2, kernel_size=2, stride=2)  
self.conv = DoubleConv(in_channels, out_channels)  
  
def forward(self, x1, x2):  
x1 = self.up(x1)  
x = torch.cat([x1, x2], 1)  
return self.conv(x)
```



## Learning Curves

#### Accuracy Curve

On the one hand, the accuracy curve records how accurate the model’s predictions are on the given data, while the loss curve records the actual difference between the model’s prediction and the actual true output.

![[Pasted image 20250210144827.png]]

The accuracy curve (also known as the training accuracy curve) shows us how good the model is at making correct predictions on the training data as it goes through the training process. Accuracy is measured in percentages and tells us the proportion of instances the model correctly classified out of the total number of instances. So, the accuracy curve gives us a sense of how well the model fits the training data and improves its ability to make accurate predictions.

#### Loss curve

The loss curve, or training loss curve, gives us insights into how the model's performance improves over time by measuring the error (or dissimilarity) between its predicted output and the true output. The loss represents how far off the model's predictions are from the actual values.

![[Pasted image 20250210145024.png]]

By minimizing the loss, the model aims to make its predictions as close as possible to the true values.

Put simply: the loss curve shows us how the model's error decreases as it learns, which indicates an improvement in its performance.

#### Attributes of a learning curve

When we talk about a reasonable learning curve, we're looking at certain features that tell us how well a model is learning. These features include the smoothness of the curve, its convergence, and how generlizable the learning rate is.

A **smooth** learning curve means that the model's performance changes gradually and consistently as it goes through training. We like to see a smooth curve because it indicates that the model is steadily improving over time. Of course, there might be small ups and downs along the way, but if the curve has big and sudden jumps, it could be a sign that something is not quite right.

**Convergence** is a term of art for when the learning curve reaches a stable or optimal state. Ideally, we want the learning curve to converge to a point where further training doesn't lead to significant improvements. This means the model has learned as much as it can from the training data and has reached its best performance.
Convergence tells us that the model has understood the underlying patterns and relationships in the data and is making accurate predictions. We usually see convergence when the learning curve levels off or plateaus.

A good learning curve should also show that the model can **generalize** This means it doesn't just perform well on the training data but also on new, unseen data. If the learning curve shows a big difference between the model's performance on training data and test data, it's a sign of a problem. It could mean that the model is overfitting, which happens when it memorizes the training data too well and struggles to handle new examples.