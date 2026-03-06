# PyTorch

<hr>

## Table of Contents

> label

<hr>

## Imports

```python
# Basics
import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
```

## Artificial Neural Network (ANN)
- Each neuron has $x$ weights and 1 bias term where $x$ is the size of the input. 

```python
# Parameters
image_size = 28 * 28
input_channels = 1
input_neurons = input_channels * image_size
fc1_hidden_neurons = 30

class TwoLayerANN(nn.Module):
    def __init__ (self):
        super(TwoLayerANN, self).__init__()
        self.name = "TwoLayerANN"

        # fully-connected layers => summarize input into features
        self.fc1 = nn.Linear(input_neurons, fc1_hidden_neurons)
        # each neuron has (input_neurons) weights and 1 bias term,
        # totalling ((input_neurons + 1) * fc1_hidden_neurons) parameters
        self.fc2 = nn.Linear(fc1_hidden_neurons, 1)  # output layer

        # dropout: randomly disabling neurons w/ a probability p #          to improve generalization & prevent overfitting
        self.drop = nn.Dropout(p = 0.3)

    def forward(self, x):
        x = x.view(-1, 1 * image_size)  # flatten
        x = self.fc1(x)     # fully-connected 1
        x = F.relu(x)       # activation
        x = self.drop(x)    # dropout
        x = self.fc2(x)     # fully-connected 2
        # usually, do not apply activation on output layer
        # sigmoid activation is automatically applied w/
        #       criterion = nn.BCEWithLogitsLoss()
        return x
```

### Deconstructed Simple ANN

```python
# Key Functions
def activation(x):
    return 1/(1 + math.exp(-x))     # sigmoid
    return

def loss(y, t):
    return (y-t)**2       # MSE
    return -t*math.log(y + 0.000001) - (1-t)*math.log(1-y+ 0.000001)    # CE

# this function is derived by chain rule
def gradient(x, y, t):
    return 2 * x * (y - t) * y * (1 - y)    # sigmoid + MSE
    return x*(y-t)                          # sigmoid + CE

def SimpleANN(x, w, t, iter, lr):
    """
    x - input data
    w - weights
    t - ground-truth labels
    iter - number of iterations/epochs
    lr - learning rate
    """
    total_err = 0

    # iterate over epochs
    for i in range(iter):
        err, y = [], []
        # iterate over each data point
        for n in range(len(x)):
            v = 0
            # forward pass, iterate over each feature
            for d in range(len(x[0])):
                v += x[n][d] * w[d]     # weighted sum: x . w
            y.append(activation(v))     # prediction
            err.append(loss(y[n], t[n]))

            # backward pass
            for p in range(len(w)):
                dw = gradient(x[n][p], y[n], t[n])
                w[p] -= lr * dw         # weight update
    total_err = sum(err)/len(x)
    return (y, w, err)
```

<br><br><br><br><br><br><br><br><br><br><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Tensors

Tensors are $n$-dimensional arrays that can be used with a GPU to accelerate computing.

```python
# initialize a random tensor
x = torch.rand(4, 3)    # rows, columns

# initialize a zero tensor
x = torch.zeros(4, 3)

# initalize a tensor with manually entered data
x = torch.tensor([2.1, 4.0, -5.2])

# initialize a tensor with data from numpy
data = np.array([2.1, 4.0, -5.2])
x = torch.tensor(data)

# convert a tensor into a numpy array
x_np = x.numpy()

# convert a one-element tensor into a number
x_num = x.item()

# tensor element-wise multiplication
print(x * y)

# tensor multiplication
print(x @ y.T)

# tensor size operator
print(x.size())

# resize a tensor
x = torch.zeros(4, 3)
y = x.view(12)      # one row of 12 columns
z = x.view(-1, 4)   # three rows of 4 columns
                    # a size of -1 is inferred from other dimensions
```

## Normalization

The purpose of normalizing inputs is to prevent a model from paying too much attention to features with larger ranges of magnitude.

### Batch Normalization

```python
linear = torch.nn.Linear(64, 128)  # maps 64-dim input to 128 dims
bn = torch.nn.BatchNorm1D(128)
...
output = bn(linear(input))
```

- Note: a moving average mean and variance are maintained for use at inference time
  Pros:
- higher learning rates spped up the training process
- regularizes the model
- less sensitive to initialization
  Cons:
- depends on batch size (no effect with small batch sizes)
- cannot work with SGD

### Layer Normalization

```python
linear = torch.nn.Linear(64, 128)  # maps 64-dim input to 128 dims
ln = torch.nn.LayerNorm(128)
...
output = ln(linear(input))
```

Pros:

- simpler to implement, no moving averages
- not dependent on batch size

## Regularization

### Dropout

Dropout is a method of regularization by randomly turning off some neurons.

- During training: random activations are dropped (set to zero) with probability $p$
- During inference: weights are multiplied by $(1-p)$ to maintain the probability distribution

```python
linear = torch.nn.Linear(64, 128)  # maps 64-dim input to 128 dims
drop = torch.nn.Dropout(p=0.3)
...
output = drop(linear(input))
```

### Weight Decay

Weight decay is a method of regularization by preventing weights from growing too much (lowers variance).

```python
torch.optim.Adam(model.parameters(), lr=0.001, weight_decay=1e-8)
```

## 2-Layer Artificial Neural Network (ANN)

```python

model = ANN()

criterion = nn.BCEWithLogitsLoss()
optimizer = optim.SGD(model.parameters(), lr=0.005, momentum=0.9)

# training example for a binary classification problem
for (image, label) in mnist_train:
    # ground truth: is the digit less than 3?
    actual = torch.tensor(label < 3).reshape([1,1]).type(torch.FloatTensor)
    out = model(img_to_tensor(image))   # make prediction
    loss = criterion(out, actual)       # calculate loss
    loss.backward()         # obtain gradients
    optimizer.step()        # update parameters
    optimizer.zero_grad()   # important clean up step

# tracking error rate and accuracy for above example
error = 0
for (image, label) in mnist_train:
    prob = torch.sigmoid(model(img_to_tensor(image)))
    if (prob < 0.5 and label < 3) or (prob >= 0.5 and label >= 0.3):
        # threshold set to 0.5
        error += 1
    print("Training Error Rate:", error/len(mnist_train))
    print("Training Accuracy:", 1 - error/len(mnist_train))
```

### Multi-Class ANN Architecture

```python
# MNIST Classifier example
class MNISTClassifier(nn.Module):
    def __init__(self):
        super(MNISTClassifier, self).__init__()
        self.layer1 = nn.Linear(28 * 28, 50)
        # 28 * 28 = 784 pixels to 50 features
        # of params = 784 * 50 + 50 bias
        self.bn = nn.BatchNorm1D(50)
        self.layer2 = nn.Linear(50, 20)
        # 50 features to 20 more specific structures
        self.ln = nn.LayerNorm(20)
        self.layer3 = nn.Linear(20, 10)
        # 20 specific structures to 10 output classes
        # one output neuron for each possible digit = 10 total

    def forward(self, img):
        flattened = img.view(-1, 28 * 28)
        activation1 = self.bn(F.relu(self.layer1(flattened)))
        activation2 = self.ln(F.relu(self.layer2(activation1)))
        output = self.layer3(activation2)
        # output = F.softmax(output, dim=-1)
        # ^ softmax activation is applied internally
        # ^ when criterion = nn.CrossEntropyLoss() is used
        # ^ numerically stable when done this way
        # ^ note: need to do it manually if criterion = nn.NLLLoss() is used
        return output

model = MNISTClassifier()

# output probabilities
prob = F.softmax(out, dim=1)
print(prob)
```

## Convolutional Neural Network (CNN)

```python
class CNN(nn.Module):
    def __init__(self, num_classes=3):
        super(CNN, self).__init__()
        self.name = "CNN"

        # convolutional layers
        self.conv1 = nn.Conv2d(in_channels=3, out_channels=16, kernel_size=5)
        # stride = 1, padding = 0 by default
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)   # halves size
        # out_channels before becomes in_channels now
        self.conv2 = nn.Conv2d(16, 32, 5)
        # pools again

        # fully-connected layers
        self.fc1 = nn.Linear(32 * 5 * 5, 32)    # flatten conv features into hidden features
        # first param = out_channels * length * height
        self.fc2 = nn.Linear(32, num_classes)   # output layer into logits
        # first param = number of out before
        # second param = number of classes

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        # note: pool applied twice
        x = x.view(-1, 10 * 5 * 5)  # flatten
        x = F.relu(self.fc1(x))
        x = self.fc2(x)
        return x
```

### LeNet-5

```python
class LeNet5(nn.Module):
    def __init__(self):
        super(LeNet5, self).__init__()
        self.conv1 = nn.Conv2d(1, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(5 * 5 * 16, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)
    def forward(self, x):
        x = self.pool(F.reul(self.conv1(x)))
        x = self.pool(F.reul(self.conv2(x)))
        x = x.view(-1, 5 * 5 * 16)
        x = F.tanh(self.fc1(x))
        x = F.tanh(self.fc2(x))
        x = self.fc3(x)
        return x
```

## Transfer Learning

```python
import torchvision.models

# pretrained models
alexnet = torchvision.models.alexnet(pretrained=True)
Inception = torchvision.models.inception.inception_v3(pretrained=True)
vgg16 = torchvision.models.vgg.vgg16(pretrained=True)
vgg19 = torchvision.models.vgg.vgg19(pretrained=True)
resnet18 = torchvision.models.resnet.resnet18(pretrained=True)
resnet152 = torchvision.models.resnet.resnet152(pretrained=True)

# example use
# Load pretrained model
alexnet = torchvision.models.alexnet(pretrained=True)

# Freeze feature extractor
for param in alexnet.features.parameters():
    param.requires_grad = False

# Replace classifier for new task
alexnet.classifier = nn.Sequential(
    nn.Dropout(0.5),
    nn.Linear(256 * 6 * 6, 256),
    nn.ReLU(),
    nn.Linear(256, num_classes)
)

# Train only the new classifier!
```

![image](https://i.ibb.co/prKc2DvC/Gemini-Generated-Image-e8hls0e8hls0e8hl.png)

## GPU Acceleration

- GPU and CPu have sepearate memories, so data must be moved between them explicitly

```python
if torch.cuda.is_available():
    model.cuda()       # moves the model to the GPU
    imgs = imgs.cuda()
    labels = labels.cuda()

# convert a GPU tensor back intoa CPU tensor
cpu_array = gpu_tensor.cpu().numpy()
# note: u cannot use a GPU tensor directly with numpy or matplotlib
```

note remember to instatiate new models when training LOL
