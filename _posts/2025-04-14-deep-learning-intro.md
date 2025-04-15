## Linear regression
Regression problems pop up whenever we want to predict a numerical value, for example predicting prices or sizes.

Linear means that the *output* is probably tied to the *input* linearly.
For example, y = 3x + 1.
y grows as x grows.
It could also be like y = -2x + 9, 
then y decreases as x increases.

## The model
Lets take the example of predicting the price of a house based on its area.
So the formula in linear regression looks something like:
$$
price = 𝑤_area · area + 𝑤_age · age + 𝑏
$$

Here, $$𝑤_area and 𝑤_age$$ are the **weights** and b is the **bias**.
All of them are calculated during the **training phase**.
In the **test phase** (where we acctually give the model the area of the house and expect it to give us its estimated price), the **weights** and the **bias** are *constants*.

### The Loss Function
Essentially, measures the error for a single training example.
$$
loss = \frac{1}{2}(y_{pred} - y_{true})^2
$$
This is a way to measure *the quality* of our model (thus, the quality of our *weights* and *bias*).

### Finding the weights and the bias
Often you will use *gradient decsent* algorithm.
Our goal is to **minimize** the cost (or loss) of the system. 

The most naive application of gradient descent consists of taking the derivative of the loss function, which is an average of the losses computed on every single example in the dataset.
This is super slow and also probably contains redundancy - but it is also quite powerful.

The other extreme is use **only one** example from the dataset, stochastically.
That's why this approach is called *SGD* - stochastic gradient descent.
This approach, although faster the the previous, still takes time to compute, because one sample means *vector X vector* operations, instead of *matrix X vector*, which are slower. 

So the most common option is work with *batches*, small groups of samples each time.

#### Gradient Descent
How do we actually minimize the cost?
The gradient represents the slope. 
We want t

-----------------------

# 📊 Linear Regression vs Logistic Regression 

| Feature               | Linear Regression                      | Logistic Regression                            |
|-----------------------|----------------------------------------|------------------------------------------------|
| **Type of Problem**   | Regression (continuous output)         | Classification (binary or multi-class)         |
| **Output**            | Real number (e.g., 12.3, -5.7)         | Probability (between 0 and 1)                  |
| **Prediction Formula**| $$y = Xw + b$$                       | $$\hat{y} = \sigma(Xw + b)$$|
| **Loss Function**     | Mean Squared Error (MSE)               | Binary Cross-Entropy (Log Loss)                |

| **Use Cases**         | Price prediction, stock values         | Spam detection, fraud detection                |
| **Solvable Analytically?** | Yes (Normal Equation)             | No – requires gradient descent                 |


### Softmax Regression

Essentialy, is the close to logistic: classifies to classes.
But unlike the logistic that classifies to 2 classes (yes/no questions), 
the softmax regression can classify to many classes.
It out put is not a single probablity but rather a **distribution* of probabilities.


## Switching to a **Deep Network**
### Motivation
Using a linear network is OK and gave us a pretty good accuracy.
If we wish to make it higher, we should consider adding more layers and make it a *deep network*.
The reason it helps is by making the output *not monotonic to the input*.
In a linear model, no matter how many layers we add without activation functions, the entire network still behaves like a single linear transformation. 

This means it can only learn decision boundaries that are straight lines. However, real-world data often requires non-linear decision boundaries. By adding non-linear activation functions between layers (like ReLU, tanh, or sigmoid), we introduce flexibility to the model.

Take clothing classification as an example. Suppose we're trying to classify images of shirts, pants, and shoes. A linear model might struggle if "shirts" and "pants" look similar in color or texture - it can only separate them with a straight decision boundary.
But a deep network with non-linear activation functions can learn higher-level patterns like sleeves or buttons, making it much better at telling the categories apart.

As a result, deep networks can capture and represent non-monotonic, non-linear, and highly expressive functions that a simple linear model cannot.

### Practical guide
Here, Pytorch *really* makes our life easy.
All we need to change is the definition of the model.
```
from torch import nn 

 = nn.Sequential( 
          nn.Linear(784,20), 
          nn.ReLU(), 
          nn.Linear(20,10), 
          nn.LogSoftmax(dim=1)   
)    
```

Here, we added a hidden layer with 20 neurons.

