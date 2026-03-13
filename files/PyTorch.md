# PyTorch

<hr>

## Table of Contents

> [Basics](#basics)
>
> > [Imports](#imports)
> > [Getting Images](#getting-images)
> > [Tensors](#tensors)
> > [GPU Acceleration](#gpu-acceleration)

> Helper Functions
>
> > [Data Loading Helpers](#data-loading-helpers)
> > [Training Helpers](#training-helpers)
> >
> > > [Tuning Hyperparameters](#tuning-hyperparameters)
> > > [Testing](#testing)

> [Artificial Neural Network (ANN)](#artificial-neural-network-ann)
>
> > [Dropout](#dropout)
> > [Batch Normalization](#batch-normalization)
> > [Layer Normalization](#layer-normalization)
> > [Deconstructed Simple ANN](#deconstructed-simple-ann)

> [Convolutional Neural Network](#convolutional-neural-network-cnn)

<hr>

## Basics

- PyTorch is a Python-based neural networks package.
- Technically, NumPy can be used to do everything PyTorch does, but PyTorch does it faster (especially with CUDA GPU).

### Imports

```python
# Basics
import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim

import matplotlib.pyplot as plt     # for showing images
import numpy as np

# for preparing train/val/test datasets
from torch.utils.data.sampler import    SubsetRandomSampler
import torchvision.transforms as transforms
```

## GPU Acceleration

- The GPU and CPU have separate memory, so data must be moved between them explicitly.
- GPU tensors cannot be used directly with PyTorch or NumPy.

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

# when instantiating the model,
net = Net().to(device)

# in evaluate() and train_net(),
inputs, labels = inputs.to(device), labels.to(device)
```

### Getting Images

- Images can be represented as a NumPy array of pixels with dimensions $\text{height}\times\text{width}\times\text{channels}$.

```python
# load an image
img = plt.imread("PATH_TO_IMAGE")

# show an image
plt.imshow(img)

# add a constant value to each pixel
img_add = np.clip(img + constant, 0, 1)
# note: pixel range must be between [0,1],
#       so clip to set values outside the range to the nearest endpoint

# crop an image (slice)
img_crop = img[0:150, 20:150, :3]
# height (y), width (x), channels
```

### Tensors

- A PyTorch tensor is an $n$-dimensional array with additional features tailored for deep learning.

```python
# initialize a tensor
tensor = torch.rand(rows, columns)   # random values
tensor = torch.zeros(rows, columns)  # all zeros
tensor = torch.tensor(array)         # from an array

# convert a NumPy array to a PyTorch tensor
tensor = torch.from_numpy(numpy_arr)
# convert a PyTorch tensor to a NumPy array
numpy_arr = tensor.numpy()
# convert a PyTorch tensor into a number
num = tensor.item()

# element-wise multiplication
z = x * y
# matrix multiplication
z = x @ y.T

# get the shape of a tensor
shape = tensor.shape

# resize a tensor
new_tensor = tensor.view(columns)   # 1 row
new_tensor = tensor.view(-1, rows)  # size -1 is inferred from tensor dimensions

# swap the order of two dimensions (transpose)
new_tensor = tensor.transpose(dim1_idx, dim2_idx)
# note: does NOT modify in place

# insert an additional dimension of size one
new_tensor = tensor.unsqueeze(idx)  # slides existing dims to the right
# note: does NOT modify in place
```

### Data Loading Helpers

```python
def get_relevant_indices(dataset, classes, target_classes):
    """ Returns the indices that belong to the desired target classes.

    Args:
        dataset: Dataset object
        classes: list of strings denoting the name of each class
        target_classes: list of strings denoting the name of the desired classes,
                        should be a subset of 'classes'
    Returns:
        indices: list of indices that have labels corresponding to the target classes
    """
    indices = []
    for i in range(len(dataset)):
        label_index = dataset[i][1]
        label_class = classes[label_index]
        if label_class in target_classes:
            indices.append(i)
    return indices

def get_data_loader(target_classes, batch_size):
    """ Loads images of each class, splits the data into train/val/test datasets.
    Returns the data loaders for the train/val/test datasets.

    Args:
        target_classes: list of strings denoting the name of the desired classes,
                        should be a subset of 'classes'
        batch_size: integer representing the number of samples per batch
    Returns:
        train_loader: iterable training dataset organized according to batch size
        val_loader: iterable validation dataset organized according to batch size
        test_loader: iterable testing dataset organized according to batch size
        classes: list of strings denoting the name of each class
    """
    classes = ('cat', 'dog')

    # tensor transformation
    transform = transforms.Compose(
        [transforms.ToTensor(),
        # normalization: scaling numeric input into a common range
        #                to prevent features with larger magnitudes from
        #                having too much influence on weights
        transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))] # normalize between [-1, 1]
    )

    # example: load CIFAR10 training data
    trainset = torchvision.datasets.CIFAR10(root='./data', train=True,
                                            download=True, transform=transform)

    # get the list of indices to sample from
    relevant_indices = get_relevant_indices(trainset, classes, target_classes)

    # split into train/val/test
    np.random.seed(1000)    # for reproducible randomness
    np.random.shuffle(relevant_indices)
    train_split = int(len(relevant_indices) * 0.8) # split at 80%
    val_split = int()

    # NEED TO LOOK AT MY LAB 3 CODE HERE

    # split into train/val/test indices
    relevant_train_indices, relevant_val_indices = relevant_indices[:split], relevant_indices[split:]
    train_sampler = SubsetRandomSampler(relevant_train_indices)
    train_loader = torch.utils.data.DataLoader(trainset, batch_size=batch_size,
                                               num_workers=1, sampler=train_sampler)
    val_sampler = SubsetRandomSampler(relevant_val_indices)
    val_loader = torch.utils.data.DataLoader(trainset, batch_size=batch_size,
                                              num_workers=1, sampler=val_sampler)

    return train_loader, val_loader, test_loader, classes
```

### Training Helpers

```python
def get_model_name(name, batch_size, learning_rate, epoch):
    """ Generate a name for the model containing all hyperparameters.
    """
    return "model_{0}_bs{1}_lr{2}_epoch{3}".format(name, batch_size, learning_rate, epoch)

def evaluate(net, loader, criterion):
    """ Evaluate a network on the validation/test set.

    Args:
        net: PyTorch neural network object
        val_loader: Pytroch data loader for the set
        criterion: loss function
    Returns:
        err: scalar for the avg classification error over the set
        loss: scalar for the avg loss over the set
    """
    total_loss = 0.0
    total_err = 0.0
    total_epoch = 0
    for i, data in enumerate(loader, 0):
        inputs, labels = data
        inputs, labels = inputs.to(device), labels.to(device)   # move to GPU
        outputs = net(inputs)
        loss = criterion(outputs, labels.float())
        correlation = ((outputs > 0.0).squeeze().long() ! = labels) # for binary classifications
        total_err += int(corr.sum())
        total_loss += loss.item()
        total_epoch += len(labels)
    err = float(total_err) / total_epoch
    loss = float(total_loss) / (i + 1)
    return err, loss

def plot_training_curve(path):
    """ Plots the training curve for a model run, given the csv files
    containing the train/validation error/loss.

    Args:
        path: path of the csv files produced during training
    """
    train_err = np.loadtxt("{}_train_err.csv".format(path))
    val_err = np.loadtxt("{}_val_err.csv".format(path))
    train_loss = np.loadtxt("{}_train_loss.csv".format(path))
    val_loss = np.loadtxt("{}_val_loss.csv".format(path))
    plt.title("Train vs Validation Error")
    n = len(train_err) # number of epochs
    plt.plot(range(1,n+1), train_err, label="Train")
    plt.plot(range(1,n+1), val_err, label="Validation")
    plt.xlabel("Epoch")
    plt.ylabel("Error")
    plt.legend(loc='best')
    plt.show()
    plt.title("Train vs Validation Loss")
    plt.plot(range(1,n+1), train_loss, label="Train")
    plt.plot(range(1,n+1), val_loss, label="Validation")
    plt.xlabel("Epoch")
    plt.ylabel("Loss")
    plt.legend(loc='best')
    plt.show()

def train_net(net, batch_size=64, learning_rate=0.01, num_epochs=30):
    # set classes the net will classify
    target_classes = ['cat', 'dog']
    torch.manual_seed(1000)     # for reproducible randomness
    train_loader, val_loader, test_loader, classes = get_data_loader(target_classes, batch_size)

    # define loss function and optimizer
    criterion = nn.BCEWithLogitsLoss()      # for binary classifications
    criterion = nn.CrossEntropyLoss()       # for multi-class classifications
    optimizer = optim.SGD(net.parameters(), lr=learning_rate, momentum=0.9)

    # set up NumPy arrays to store training/test loss/error
    train_err = np.zeros(num_epochs)
    train_loss = np.zeros(num_epochs)
    val_err = np.zeros(num_epochs)
    val_loss = np.zeros(num_epochs)

    # train the network
    start_time = time.time()
    for epoch in range(num_epochs):
        total_train_loss = 0.0
        total_train_err = 0.0
        total_epoch = 0
        # training loop, similar to evaluate()
        for i, data in enumerate(train_loader, 0):
            inputs, labels = data
            # zero the parameter gradients
            optimizer.zero_grad()
            # forward pass, backward pass, and optimize
            outputs = net(inputs)
            loss = criterion(outputs, labels.float())
            loss.backward()
            optimizer.step()
            # calculate stats
            correlation = ((outputs > 0.0).squeeze().long() != labels)
            total_train_err += int(corr.sum())
            total_train_loss += loss.item()
            total_epoch += len(labels)
        train_err[epoch] = float(total_train_err) / total_epoch
        train_loss[epoch] = float(total_train_loss) / (i+1)
        val_err[epoch], val_loss[epoch] = evaluate(net, val_loader, criterion)

        # print an update
        print(("Epoch {}: Train err: {}, Train loss: {} |"+
               "Validation err: {}, Validation loss: {}").format(
                   epoch + 1,
                   train_err[epoch],
                   train_loss[epoch],
                   val_err[epoch],
                   val_loss[epoch]))

        # save the current model (checkpoint) to a file
        model_path = get_model_name(net.name, batch_size, learning_rate, epoch)
        torch.save(net.state_dict(), model_path)
    print("Finished Training")
    end_time = time.time()
    elapsed_time = end_time - start_time
    print("Total time elapsed: {:.2f} seconds".format(elapsed_time))

    # write the train/test loss/err into CSV file for plotting later
    epochs = np.arange(1, num_epochs + 1)
    np.savetxt("{}_train_err.csv".format(model_path), train_err)
    np.savetxt("{}_train_loss.csv".format(model_path), train_loss)
    np.savetxt("{}_val_err.csv".format(model_path), val_err)
    np.savetxt("{}_val_loss.csv".format(model_path), val_loss)
```

### Tuning Hyperparameters

```python
net = Net()     # must instantiate a new Net object each time
                # or else training will continue from a previous state
train_net(net)
```

### Testing

```python
criterion = nn.BCEWithLogitsLoss()      # for binary classifications
criterion = nn.CrossEntropyLoss()       # for multi-class classifications,
                                        # performs softmax implicitly
test_err, test_loss = evaluate(net, test_loader, criterion)
```

## Artificial Neural Network (ANN)

```python
# Architecture Details
image_size = 28 * 28
num_input_channels = 1
num_input_neurons = num_input_channels * image_size
num_hidden_neurons_fc1 = 30
num_classes = 1

class TwoLayerANN(nn.Module):
    def __init__ (self):
        super(TwoLayerANN, self).__init__()
        self.name = "TwoLayerANN"

        # fully-connected layers: a collection of neurons that summarize input into features
        self.fc1 = nn.Linear(num_input_neurons, num_hidden_neurons_fc1)
        # each neuron has (num_input_neurons) weights and an additional bias term,
        # totalling ((num_input_neurons + 1) * num_hidden_neurons_fc1) parameters
        self.fc2 = nn.Linear(num_hidden_neurons_fc1, num_classes)  # output layer

    def forward(self, x):
        x = x.view(x.size(0), -1)      # flatten
        # x = x.view(-1, num_input_neurons)  # alternative
        x = self.fc1(x)     # fully-connected 1
        x = F.relu(x)       # activation
        x = self.fc2(x)     # fully-connected 2
        # usually, do not apply activation on output layer
        # sigmoid activation is implicitly applied w/
        #       criterion = nn.BCEWithLogitsLoss()
        return x
```

### Dropout

- Definition: random disabling of neurons with a probability $p$.
- Purpose: improve generalization & prevent overfitting

```python
def __init__(self):
    ...
    self.drop = nn.Dropout(p = 0.3)
    ...

def forward(self, x):
    ...
    x = self.fc1(x)
    x = F.relu(x)
    x = self.drop(x)    # after activation
    x = self.fc2(x)
    ...
```

### Batch Normalization

- Definition:
- Pros:
  - higher learning rates speed up training process
  - regularizes the model
  - makes the model less sensitive to initialization
- Cons:
  - depends on batch size (no effect with small batch sizes)
  - does not work with SGD

```python
def __init__(self):
    ...
    self.fc1 = nn.Linear(input_neurons, fc1_hidden_neurons)
    self.bn = nn.BatchNorm1D(fc1_hidden_neurons3)
    ...

def forward(self, x):
    ...
    x = self.fc1(x)
    x = F.relu(x)
    x = self.bn(x)    # after activation
    ...
```

### Layer Normalization

- Definition:
- Pros:
  - simpler to implement (no moving averages)
  - independent of batch size

```python
def __init__(self):
    ...
    self.fc1 = nn.Linear(input_neurons, fc1_hidden_neurons)
    self.ln = nn.LayerNorm(fc1_hidden_neurons)
    ...

def forward(self, x):
    ...
    x = self.fc1(x)
    x = F.relu(x)
    x = self.ln(x)    # after activation
    ...
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

## Convolutional Neural Network (CNN)

```python
class CNN(nn.Module):
    def __init__(self, num_classes = 3):
        super(CNN, self).__init__()
        self.name = "CNN"

        # convolutional layers
        self.conv1 = nn.Conv2d(in_channels=3, out_channels=16, kernel_size=5)
        # by default: stride=1, padding=0
        # pooling: ???
        self.pool = nn.MaxPool2d(kernel_size=2, stride=2)   # these params half the size
        self.conv2 = nn.Conv2d(16, 32, 5)   # previous out_channels becomes next in_channels

        # fully-connected layers
        self.fc1 = nn.Linear(32 * 5 * 5, 32)   # flatten convolutional features into hidden features
        # first param: data size after all convolutional/pooling layers
        # second param: number of hidden features
        self.fc2 = nn.Linear(32, num_classes)
        # first param: number of hidden features

    def forward(self, x):
        x = self.conv1(x)
        x = F.relu(x)
        x = self.pool(x)
        x = self.conv2(x)
        x = F.relu(x)
        x = self.pool(x)    # second pool!
        x = x.view(x.size(0), -1)    # flatten
        x = self.fc1(x)
        x = F.relu(x)
        x = self.fc2(x)
        return x
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

### Weight Decay

Weight decay is a method of regularization by preventing weights from growing too much (lowers variance).

```python
torch.optim.Adam(model.parameters(), lr=0.001, weight_decay=1e-8)
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
