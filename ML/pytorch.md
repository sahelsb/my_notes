
```
import torch  
import torch.nn as nn
```

- `torch`: The main PyTorch library.
- `torch.nn`: Provides neural network components.
- `math`: Provides mathematical functions.

```
class FeedForward(nn.Module):
	def __init__(dim, dropout= 0.):
		super().__init__()
		self.norm = nn.LayerNorm(dim)
		self.dropout = nn.Dropout(dropout)
```

- `nn.Module`: The base class for all PyTorch models. This class allows you to define a network that can easily be trained and evaluated.
- `nn.LayerNorm(dim)` normalizes the inputs by subtracting the mean and dividing by the standard deviation, based on the input dimension `dim`. It stabilizes training and speeds up convergence.
- `nn.Dropout(dropout)` Dropout is a regularization technique that randomly sets a fraction of the input units to zero during training to prevent overfitting.

```
self.linear = nn.Linear(in_features, out_features, bias=True)

# apply linear layer
out = self.linear(x)
```

- **`in_features`**: The number of input features (i.e., the dimensionality of the input data).
- **`out_features`**: The number of output features (i.e., the dimensionality of the output data).
- This is the last dimention `dim` in the data, if it is a tensor, like ``[batch_size, seq_len, dim]`` to `[batch_size, seq_len, dim_head * heads]`

	In PyTorch, `nn.Linear` is a class that defines a **fully connected (linear) layer**, also known as a **dense layer**. It performs a linear transformation on the input data, essentially applying a matrix multiplication followed by an optional bias addition.
	
	A linear layer performs the following mathematical operation:
	
	Output=X⋅W+b
	
	- **`X`** is the input tensor.
	- **`W`** is the weight matrix (learned during training). The shape of **`W`** is `(out_features, in_features)`.
	- **`b`** is the bias vector (learned during training). The shape of **`b`** is `(out_features)`.
	
		The `nn.Linear` layers are, in essence, linear transformations of the kind _Ax_ + _b_.  `nn.Linear` operates on tensors in the following way: if our input tensor dimensions are (64, 512) and we perform `nn.Linear(512,1536)`, then the resulting output tensor dimensions are (64, 1536).
		
		The purpose of a linear layer is to map input features (which     
		might represent data like words, pixel values, etc.) to an output 
		with a different dimension.

```
nn.softmax(dim = -1)
nn.softmax
```

- **`dim=-1`**: The `dim` parameter specifies which dimension to apply the softmax function along. Setting `dim=-1` tells PyTorch to apply softmax to the **last dimension** of the input tensor.
	For example, if the input tensor has a shape of `(B, N, D)`, where `B` is the batch size, `N` is the sequence length, and `D` is the feature dimension, applying `nn.Softmax(dim=-1)` would normalize values along the `D` dimension.
- `nn.Softmax(dim=-1)` initializes a **softmax layer** with a specified dimension for normalization

	The `nn.Softmax` function takes an input tensor of arbitrary shape and normalizes its elements along a specified dimension (or axis) so that they sum up to 1. This operation is often applied to attention scores, or to the output layer of classification models to represent class probabilities.

```
b, n, _, h = *x.shape, self.heads
```

- **`x.shape`**: Retrieves the shape of the tensor `x`. Suppose `x` has a shape `(B, N, D)`, then `x.shape` would return `(B, N, D)`
- **`*x.shape`**: This syntax ***unpacks the shape tuple*** so that each dimension of `x`'s shape can be assigned to variables on the left side
- `b`: Will be assigned the first element of `x.shape`, typically the **batch size**.
- `n`: Will be assigned the second element of `x.shape`, usually the **sequence length**.
- `_`: Is assigned the third element of `x.shape`, often the **feature dimension**, but here it is ignored by convention  ***since `_` is a throwaway variable.***
- `h`: Is set to `self.heads`, which is a property of the class or layer and typically represents the **number of attention heads**.


```
from einops import rearrange
out = rearrange(out, 'b h n d -> b n (h d)', h= self.heads)

```

- this `rearrange` is used for tensor manipulation.
- **Input shape**: `(b, h, n, d)`
- **Output shape**: `(b, n, h * d)`


#### lambada function

A **lambda function** in Python is a concise way to create an **anonymous function**, meaning a function that is defined without a name

```
lambda arguments: expression
```

- **`lambda`**: Keyword used to define a lambda function.
- **`arguments`**: A comma-separated list of parameters that the function takes (like a regular function).
- **`expression`**: A single expression that is evaluated and returned when the lambda function is called.

Lambda functions are commonly used with **functional programming constructs** like `map()`, `filter()`, and `reduce()`.

```
# Regular function 
def add(x, y): 
return x + y 

# Lambda function 
add_lambda = lambda x, y: x + y
```

#### map

```
map(function, iterable)

```

The `map` function applies a given function to each element of an iterable (like a list, tuple, etc.) and returns a new iterable with the results.

- `function`: The function to apply.
- `iterable`: The data structure to which the function will be applied.

```
numbers = [1, 2, 3, 4]
# Square each number using a lambda function 
squared = map(lambda x: x ** 2, numbers)
```

- The lambda function `lambda x: x ** 2` squares each element in the `numbers` list.


#### Matrix Multiplication

**`matmul`** (Matrix Multiplication) Or @

- **`matmul`** is a function in **NumPy** and **PyTorch** for performing matrix multiplication.
- Performs standard **matrix multiplication**
- **Equivalent to using the `@` operator.**

```
A = np.array([[1, 2], [3, 4]]) 
B = np.array([[5, 6], [7, 8]]) 

result = np.matmul(A, B)

result = torch.matmul(Q,K)

```

 **`.` (Dot Notation)**:

- **`dot()` function** in NumPy (or **`.` notation in object-oriented libraries**) serves multiple purposes:

    - Performs **dot product** for 1D arrays.
    - Performs **matrix multiplication** for 2D arrays.
    - Generalized for tensors but with different behavior from `matmul`.

### kwargs

```
def forward(self, x, **kwargs):
	return self.fn(self.norm(x), **kwargs)

```

-  kwargs : any additional argument that you want to pass to the function

## Building a Neural Network

we will use the [FashionMNIST](https://www.kaggle.com/datasets/zalando-research/fashionmnist) dataset, which is readily available in PyTorch’s torchvision library. This dataset contains 70,000 grayscale images of 10 different classes of clothing items.

```
import torch  
from torch import nn  
from torch.utils.data import DataLoader  
from torchvision import datasets  
# from torchvision.transforms import ToTensor
from torchvision import transforms

```

- `torch`: The core PyTorch library for building and training neural networks.
-  `nn`: A submodule of `torch` containing building blocks for neural networks like layers and activation functions.
- `DataLoader`: A class from `torch.utils.data` that helps us load and iterate over datasets in batches.
- `datasets`: A submodule of `torchvision` providing access to pre-downloaded datasets like Fashion MNIST.
-  `ToTensor`: A data transform that converts images to PyTorch tensors.

After we are done importing libraries, its time we download the training dataset and test data set too from the FashionMNIST

### Download data

```
# download training data from the FashionMNISTdataset.
training_data = datasets.FashionMINST(train = True, transform = ToTensor(), download = True, root= "./data")

# download test data from the FashionMNIST dataset.
test_data = datasets.FashionMINST(train = False, transform = ToTensor(), download = True, root = "./data")

```


 - We also apply the `ToTensor` transform, which converts the raw image data (pixel intensities between 0 and 255) into PyTorch tensors.
- The `download=True` argument specifies that the dataset should be downloaded if it is not already available in the `root` directory.
 
**Alternative Transfromation** :

```
transform = transforms.compose(
[transforms.ToTensor(),
transforms.Normalize((0.5,), (0.5,))]
)
```

- `transforms.ToTensor()` - Converts the input **PIL Image** or **numpy.ndarray** into a PyTorch tensor. This is necessary because the **neural network models in PyTorch expect tensors as inputs**.

- The `transforms.Normalize()` transformation is normalizing the tensor with mean `0.5` and standard deviation `0.5`. This will transform the pixel values of the input image from the original range of [0, 1] to the range of [-1, 1]. This is because neural networks generally work better when the input data is centered around zero and has a relatively small range of values. By normalizing the pixel values to be between -1 and 1, we center the data around 0, which can help with the optimization process.
### Data Loaders

Next step is to define or dataset loaders, Data loaders will help us load the dataset in batches, making it easier to manage memory and speed up training of our model. To define our data loaders for our model, we first declare the loading batch size.

```
batch_size = 64

# create data loaders
training_loader = DataLoader(training_data, batch_size = batch_size)
test_loader = DataLoader(test_data, batch_size = batch_size)

for X, y in test_loader:  
print(f"Shape of X [N C H W]: {X.shape}")  
print(f"Shape of y: {y.shape} {y.dtype}")  
break
 
```

We just define the batch size, which will help control how many images are processed at once during training.

- `DataLoader` is a utility class that provides an easy way to load data in batches from a dataset. It helps to handle the complexities of dealing with large datasets, such as shuffling, batching, and parallel data loading. `DataLoader` takes as input a PyTorch dataset and various other parameters, such as batch size, shuffle, and num_workers (number of processes to use for loading the data). It then returns an iterator that generates batches of data as tensors, which can be easily used for training or evaluation.
- The `DataLoader` class is particularly useful when working with large datasets that cannot be loaded entirely into memory at once. It allows us to efficiently load and process only a subset of the data at a time, which saves memory and speeds up the training process.
- Our configuration is that the data loaders will feed the data into the neural network in batches during training and evaluation.

Also we use the `for` loop to iterate through the batches of data and prints the shapes of the input images (`X`) and their corresponding labels (`y`). We see that `X` has a shape of `[batch_size, channel, height, width]`, where `batch_size` is 64 in this case, `channel` is 1 (grayscale images), and `height` and `width` are both 28 (representing the 28x28 pixel images). The labels `y` are a one-dimensional tensor of integers representing the clothing categories.

 lets then define how we mount our model unto our devices, in our case we will mount it into our CPU device.
 
### Mount model on device

device = (  "cuda"  if torch.cuda.is_available()  else 
"mps"  if torch.backends.mps.is_available()  else 
"cpu" )  
print(f"Using {device} device")


### Defining the Neural Network Model

We define a simple fully connected neural network. Our model will have three layers with [ReLU](https://builtin.com/machine-learning/relu-activation-function#:~:text=ReLU%2C%20short%20for%20rectified%20linear,as%20the%20rectifier%20activation%20function) activations in between.

To define a neural network in PyTorch, we create a class that inherits from nn.Module.
We define the layers of the network in the **init** function and specify how data will pass through the network in the forward function.

```
class NeuralNetwork(nn.Module):

	def __init__(self):
		super.__init__()
		self.Flatten = nn.Flatten()
		self.linear_relu_stack = nn.Sequential(
		nn.Linear(28*28 , 512), 
		nn.ReLU(),  
		nn.Linear(512, 512),  
		nn.ReLU(),  
		nn.Linear(512, 10))
		
	def forward(self, x):
		x = self.Flatten(x)
		logits = self.linear_relu_stack(x)
		return logits

model = NeuralNetwork().to(device)
print(model)
	
```

```
OUTPUT

NeuralNetwork(  
(Flatten): Flatten(start_dim=1, end_dim=-1)  
(linear_relu_stack): Sequential(  
(0): Linear(in_features=784, out_features=512, bias=True)  
(1): ReLU()  
(2): Linear(in_features=512, out_features=512, bias=True)  
(3): ReLU()  
(4): Linear(in_features=512, out_features=10, bias=True)  
)  
)
```

- **nn.Module**: Base class for all neural network modules in PyTorch.
- **Flatten**: Flattens the input tensor.
-  **nn.Sequential**: A sequential container to define the layers of the model.
- **nn.Linear**: Fully connected layer.
- **nn.ReLU**: ReLU activation function.

**Alternative** :  you can also define each layer seperately without  a sequential container.

```
from torch import nnclass Network(nn.Module):  
    def __init__(self):  
        super().__init__()  
          
        # Inputs to hidden layer linear transformation  
        self.hidden = nn.Linear(784, 256)  
        # Output layer, 10 units - one for each digit  
        self.output = nn.Linear(256, 10)  
          
        # Define sigmoid activation and softmax output   
        self.sigmoid = nn.Sigmoid()  
        self.softmax = nn.Softmax(dim=1)  
          
    def forward(self, x):  
        # Pass the input tensor through each of our operations  
        x = self.hidden(x)  
        x = self.sigmoid(x)  
        x = self.output(x)  
        x = self.softmax(x)  
          
        return x
```

Note: The `**softmax**` **function,** also known as `**softargmax**` or `**normalized**` `**exponential function**`is a function that takes as input a vector of _K_ real numbers, and normalizes it into a probability distribution of _K_ probabilities.

### Defining the Loss Function and Optimizer

The loss function measures how well the model’s predictions match the actual labels. while the optimizer updates the model parameters to minimize the loss.

```
loss_fn = nn.CrossEntropyLoss()
optimizer = torch.optim.SGD(model.parameters(), lr=1e-3, momentum=0.9)

```


- **nn.CrossEntropyLoss**: is a loss function used primarily for classification tasks where the model predicts probabilities for each class. It combines `nn.LogSoftmax()` and `nn.NLLLoss()` in one single class. The CrossEntropyLoss expects raw logits (the output of the model before applying soft max) as input. It computes the soft max internally to normalize logits and then computes the negative log likelihood loss between the predicted class probabilities and the actual target labels.

- **torch.optim.SGD**: also is the optimizer that implements Stochastic Gradient Descent (SGD), a fundamental optimization algorithm used for training neural networks. SGD updates the model parameters in the direction of the negative gradient of the loss function with respect to the parameters. The `model.parameters()` argument specifies which parameters of the model should be optimized. Here, `torch.optim.SGD()` is used to create a stochastic gradient descent (SGD) optimizer, which updates the model parameters using gradients computed on randomly selected subsets of the training data, rather than the full training set.

- **lr (Learning rate)**: which is a scalar factor that controls the step size taken during optimization. It determines how much to change the model parameters with respect to the gradient of the loss function. A higher learning rate can speed up convergence, but if it’s too high, it may cause the model to overshoot optimal values. Conversely, a lower learning rate can improve stability and precision but may require more iterations to converge.

- **momentum**: Momentum simply is a parameter that accelerates SGD in the relevant direction and dampens oscillations. It improves the convergence rate and helps SGD to escape shallow local minima more effectively. A common value for momentum is 0.9, but it can be tuned depending on the specific problem and dataset characteristics.

After initializing the optimizer, the model parameters can be updated using the `optimizer.step()` method, **and the gradients can be zeroed out using the `optimizer.zero_grad()` method, in each iteration of the training loop**.

### Defining our Training Function

```
def train(dataloader, model, loss_fn, optimizer)
size = len(dataloader.dataset)

for batch, (X,y) in enumerate(dataloader):
	X = X.to(device)
	y = y.to(device)

	# compute predicted y by passing X to the model
	prediction = model(X)
	
	# compute the loss
	loss = loss_fn(prediction, y)

	# apply zero gradients, perform a backward pass, and update the weights
	optimizer.zero_grad()
	loss.backward()
	optimizer.step()
	
	# print training progress  
	if batch % 100 == 0:  
		loss_value = loss.item()  
		current = batch * len(X)  
		print(f"loss: {loss_value:>7f}
		[{current:>5d}/{size:>5d}]")

	
```

### Define test function

```
def test(model, dataloader, loss_fn):
	size = len(dataloader.dataset)
	num_batches = len(dataloader)
	model.eval()
	test_loss, correct = 0

	with torch.no_grad():
		for X, y in dataloader:
			X = X.to(device)
			y = y.to(device)
			prediction = model(X)
			predicted = prediction.argmax(1)

			test_loss += loss_fn(prediction, y).item()
			total += y.size(0)
			correct += (predicted == y).type(torch.float).sum().item()
		
		correct /= size
		
	accuracy = 100 * correct / total
	test_loss /= num_batches
	
	print('Test Accuracy: {:.2f}%, Test Loss: {:.4f}'.format(accuracy, test_loss))
```

- The `with torch.no_grad()` statement is used to temporarily disable gradient calculation during inference or evaluation of a neural network model. In PyTorch, when a tensor is involved in a computation that requires gradients to be computed, a computational graph is constructed to keep track of the operations performed on the tensor. This graph is then used to compute the gradients of the output with respect to the input using backpropagation. However, during inference or evaluation of the model, we don’t need to compute gradients, and keeping track of the computational graph would only consume memory and computational resources. By wrapping the inference or evaluation code in a `with torch.no_grad()` statement, we can temporarily disable gradient computation and avoid building the computational graph, which can significantly speed up the computation and reduce the memory consumption.
### Define training loop

The training process is conducted over several iterations (epochs). During each epoch, the model learns parameters to make better predictions.
We print the model’s accuracy and loss at each epoch; we’d like to see the accuracy increase and the loss decrease with every epoch.

```
epochs= 5
for t in range(epochs):
print(f"Epoch {t+1} /n----------------------")
train(trainig_loader, model, loss_fn, optimizer)
test(test_loader, model, loss_fn)
```

**epochs**: Number of times to iterate over the entire training dataset in our case 5 times.

At this point, we already have a trained model that can perfectly predict and classify images and provide output value or expected value as the case may be.


### Save Model

Moving forward, next thing to consider is ways to save our trained model, so that when we want to use or deploy them for application usage, we can easily call them and provide the required classes and values.


To save our defined model, we follow the following ways;

```
if args.save-model:

	save_path = Path(f"./models/{args.model}")

	save_path.mkdir(parents=True, exist_ok=True)

	file_name = "best_model.pth"

	file_path = save_path / file_name

	torch.save(best_model , file_path)

	print(f"Best model saved with validation accuracy: {best_accuracy:.2f}% and test accuracy: {test_accuracy:.2f}%")

```

This approach will save the model and and serialize the internal state dictionary (containing the model parameters).


After saving the model, if next time we want to use our model for predictions, we will first load them into our compute space. And to do that we;

```
model = NeuralNetwork().to(device)
model.load_state_dict(torch.load("model.pth"))
```

The above process involves loading our model which also includes re-creating the model structure and loading the state dictionary into it.

### Model Usage for prediction

```
classes = [
	"T-shirt/top",  
	"Trouser",  
	"Pullover",  
	"Dress",  
	"Coat",  
	"Sandal",  
	"Shirt",  
	"Sneaker",  
	"Bag",  
	"Ankle boot",
]

# set the model to evaluation mode
model.eval()

sample_index = 1  # sample Index (Change this index to select a different sample)
x, y = test_data[sample_index][0], test_data[sample_index][1]

# make prediction without gradient calculation
with torch.no_grad():
	x = x.to(device)
	prediction = model(x.unsqueeze(0))

	predicted, y = classes[preciction.argmax(dim=1).item()], classes[y]

```

```
OUTPUT

# OUTPUT: Predicted: "Pullover", Actual: "Pullover"
```

`**classes**`: This is a list of class labels that correspond to the categories the model is trained to recognize. Each index in this list represents a specific class.

`**model.eval()**`: Sets the model to evaluation mode. This is important because some layers (e.g., dropout, batch normalization) behave differently during training and evaluation. In evaluation mode, these layers operate in inference mode, ensuring consistent results during testing.

```
x, y = test_data[0][0], test_data[0][1]
```
`**x, y = test_data[0][0], test_data[0][1]**`: Selects the first sample from the `test_data` dataset. `x` is the input data (e.g., an image), and `y` is the corresponding label (e.g., the class index).


`**with torch.no_grad():**`: Disables gradient calculation, which is not needed for evaluation and reduces memory usage and computation time.

`**x = x.to(device)**`: Moves the input data to the specified device (CPU or GPU) where the model is located.

`**pred = model(x)**`: Passes the input data through the model to obtain the predictions. `pred` is typically a tensor containing the output logits or probabilities for each class.

`**pred[0].argmax(0)**`: Finds the index of the class with the highest score in the model's output for the first (and only) sample in the batch. This index corresponds to the predicted class.

`**classes[pred[0].argmax(0)]**`: Uses the index to look up the predicted class label from the `classes` list.

`**classes[y]**`: Uses the true label index `y` to look up the actual class label from the `classes` list.


#### `torch.rand`

`torch.rand` generates random values between 0 and 1
`torch.randn`