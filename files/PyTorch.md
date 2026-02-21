# PyTorch

<hr>

## Table of Contents

> label

<hr>

## Simple Artificial Neural Network

```python
def simple_ANN(x, w, t, iter, lr):
    """
    x - input data
    w - weights
    t - ground-truth labels
    iter - number of epochs
    lr - learning rate
    """
    total_e = 0
    for i in range(iter):   # loop over epochs
        e, y = [], []
        for n in range(len(x)): # loop over each data point
            v = 0

            # forward pass
            for d in range(len(x[0])):      # loop over each feature of a data point
                v += x[n][d] * w[d]         # weighted sum
            y.append(1/(1 + math.e**(-v)))  # sigmoid activation function
            e.append((y[n]-t[n])**2)        # MSE loss function

            # backward pass (gradient descent)
            for p in range(len(w)):
                d = 2*x[n][p]*(y[n]-t[n])*(1-y[n])*y[n]  # gradient
                                                         # formula from chain rule
                w[p] -= lr * d
    total_e = sum(e)/len(x)
    return  (y, w, e)
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
# set up
import torch
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim

torch.manual_seed(1)  # set random seed for reproducibility

class ANN(nn.Module):
    def __init__ (self):
        super(ANN, self).__init__()
        self.layer1 = nn.Linear(28 * 28, 30)    # fully-connected layer
        self.drop = nn.Dropout(p=0.3)
        self.layer2 = nn.Linear(30, 1)

    def forward(self, img):
        flattened = img.view(-1, 28 * 28)
        activation1 = self.drop(self.layer1(flattened))
        activation1 = F.relu(activation1)
        activation2 = self.drop(self.layer2(activation1))
        # activation2 = F.sigmoid(activation2)
        # ^ sigmoid activation to output is applied internally
        # ^ when criterion = nn.BCEWithLogitsLoss() is used
        # ^ note: need to do it manually if criterion = nn.BCELoss() is used
        return activation2

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
        self.bn = nn.BatchNorm1D(50)
        self.layer2 = nn.Linear(50, 20)
        self.ln = nn.LayerNorm(20)
        self.layer3 = nn.Linear(20, 10)
        # one output neuron for each possible digit = 10 total
    
    def forward(self, img):
        flattened = img.view(-1, 28 * 28)
        activation1 = self.bn(F.relu(self.layer1(flattened)))
        activation2 = self.ln(F.relu(self.layer2(activation1)))
        output = self.layer3(activation2)
        # output = F.softmax(output, dim=-1)
        # ^ softmax activation is applied internally 
        # ^ when criterion = nn.CrossEntropyLoss() is used
        # ^ note: need to do it manually if criterion = nn.NLLLoss() is used
        return output

model = MNISTClassifier()

# output probabilities
prob = F.softmax(out, dim=1)
print(prob)
```