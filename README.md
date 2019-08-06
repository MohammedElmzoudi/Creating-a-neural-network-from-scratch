# Create-a-simple-neural-network-from-scratch
Learn how to create a fully functioning neural network with fully vectorized and simple implementations of forward and back propagation in python without the use of external machine learning libraries.

<p align="center">
  <img src="/Images/neural_network-diagram.png">
</p>  

This project aims to help you create a simple 3 layer neural network (1 output layer, 1 input layer, 1 hidden layer) with 2 activation neurons each by walking through how to implement forward and backpropagation in a vectorized format.   
  
- The sample neural network we will be building is based off of the following step-by-step backpropagation guide, which I highly recommend you begin with as it provides an excellent in-depth intuition for how each part of backpropagation is computed and will help you understand the vectorization a bit better.

> https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/.  

## Getting Started

### Weights  
The weights for each layer are stored in a 2x2 matrix, where each row indicates the neuron as a whole, and each column within the row is an individual weight attatched to that neuron.   
  
<p align="center">
  <img src="/Images/layer1_weights.png">
  <img src="/Images/layer2_weights.png">
</p>
  
> Weights for layers 2 and 3 respectively
   
### Layers  
Each computed layer will be stored in a 2x1 column vector 
  
<p align="center">
  <img src="/Images/Layer1.png">
  <img src="/Images/layer2.png">
  <img src="/Images/layer3.png">
</p>

> Layers 1, 2, and 3 respectively
  
  
## Forward Propagation

To get started we need to first calculate the values for each layer to be later used for back propagation.  

1. To find the value of a node first multiply each weight 'attatched' to the node, by a node in the previous layer, and taking the sum of all these values,(The weighted sum) this value will be refered to as the 'Z' value. Note that each node has a weight for all the nodes in the previous layer.

 <p align="center">
  <img src="/Images/z_calculation.png">
</p>

2. Plug the calculated Z value into an activation function. The activation function we will be using for each node is the [Sigmoid Activation Function](https://en.wikipedia.org/wiki/Sigmoid_function). 
  
<p align="center">
  <img src="/Images/activation_calculation.png">
</p>
   - If you are not yet familiar with how activation functions work I highly recommend watching this video on the topic.
<p align="center">
  <a href="http://www.youtube.com/watch?feature=player_embedded&v=m0pIlLfpXWE
  " target="_blank"><img src="http://img.youtube.com/vi/m0pIlLfpXWE/0.jpg"
  alt="Activation Function Video" width="220" height="160" border="10" /></a>

### Vectorized Implementation
Using vectorization we can caluculate the activation values for each layer in just one step, starting with the first hidden layer and continuing until you reach the output layer.

<p align="center">
  <img src="/Images/FFVectorized.png">
</p>

<p align="center">
  <img src="/Images/FFVectorized2.png">
</p>

And in python:   
```
 z_hidden_layer1 = np.matmul(weights1,input_values) + bias1
 hidden_layer1 = sigmoid(z_hidden_layer1)
 
 z_output_layer = np.matmul(weights2,hidden_layer1) + bias2
 output_layer = sigmoid(z_output_layer)
```
## Backpropagation

### Brief Explanation
- Each machine learning algorithm has what is called a loss function. This function determines how well a model is performing on a certain dataset based on how close the values that the model outputs when given a set of inputs is to the actual desired value of those inputs. The goal of any machine learning model is to minimize this cost function by finding the optimal value for each weight.
- By taking the derivative of the cost function with respect to each weight, we can find the slope of the line on the cost function when that weight is a certain value. A positive slope indicates that if the value of the weight is decreased then the cost function will also decrease, and vise-versa. By continuously subtracting the derivative w.r.t thetea from theta itself, we can eventually hope to reach a global minimum of the cost function. You can learn more about the topic [here](https://en.wikipedia.org/wiki/Gradient_descent). 
 <p align="center">
  <img src="https://thumbs.gfycat.com/KindAmpleImperialeagle-size_restricted.gif">
</p>

### Notation

<p align="center">
  <b><a>Cost Function:</a></b>
  <br><br>
  <img src="/Images/CostN.png">
</p>




<p align="center">
  <b><a>Weights:</a></b>
  <br><br>
  <img src="/Images/ThetaN.png"><br/>  
  <i><a>l = the layer of the neurons that the weights effects.</a><br/>
  <i><a>i = The specific neuron that the weight is attatched to.</a><br/>
  <i><a>j = the neuron of the previous layer that is multiplied by the weight. </a><br/>
</p>

<p align="center">
  <b><a>Weight l,i,j gradient:</a></b>
  <br><br>
  <img src="/Images/NablaN.png"><br/>  
</p>

<p align="center">
  <b><a>Delta (Will go over this later on):</a></b>
  <br><br>
  <img src="/Images/deltaN.png"><br/>  
</p>





### Derivation / Proof

__Goal__ : Find Derivative of the cost function with respect to a specific weight l,i,j. (Note that this derivation works so that any cost function can be used).  
- Also note that knowledge of the [Chain Rule](https://www.youtube.com/watch?v=6kScLENCXLg&vl=en) is required as it is used heavily throughout this proof.   
  
<p align="center">
  <br/>
  <img src="/Images/deriv0.png">
  <br/>
</p>
  
1. Using the chain rule we know that this equation can simplify.  
<p align="center">
  <br/>
  <img src="/Images/deriv1.png">
  <br/>
</p>
  
2. Remember that the Z value is just the weighted sum of the neurons in the previous layer.  
<p align="center">
  <br/>
  <img src="/Images/deriv2.png"><br/>  
  <br/>
  <sub><i><a>When taking the derivative with respect to a variable, every term that does not contain the variable will equate to zero</a><br/>
  <i><a>Because of this, we can ignore all summations that do not contain theta. </a><br/>
  <i><a> 2.1 </a><br/>
  <br/>
  <img src="/Images/deriv2.1.png"><br/>
  <br/>
  <i><a>And we can treat z as a single, simple term and take its derivative. </a><br/>
  <br/>
  <i><a> 2.2 </a><br/>
  <br/>
  <img src="/Images/deriv2.2.png"><br/>
  <br/>
  <i><a> 2.3 </a><br/>
  <br/>
  <img src="/Images/deriv2.3.png"><br/>
  <br/>
  <i><a> 2.4 </a><br/>
  <br/>
  <img src="/Images/deriv2.4.png"><br/>
  <br/>
  <i><a>Now the derivative of z^l is just the neuron in the previous layer that multiplies the theta we are solving for. </a><br/></sub>
</p>
    
3. The derivative of the cost function with respect to any z value is called delta, or the error value for that node. Because 'z' is the weighted sum of all the nodes in the previous layer, if the derivative of the cost w.r.t 'z' (or the slope of the tangent line on the cost function when z is a certain value ) is extremely low, this means that your current z value is already in it's best position to provide the lowest possible value of the cost function and vise versa. This essentially tells you how 'wrong' your combination of weights and biases are, hence the name delta.
<p align="center">
  <sub><i><a><b> Goal: Find- </a><br/></b>
  <br/>
  <img src="/Images/deriv3.0.png"><br/>  
  <br/>
  <i><a> 3.1 </a><br/>
  <i><a> Using the chain rule we can break this down further </a><br/>
  <br/>
  <img src="/Images/deriv3.1.png"><br/>  
  <br/>
  <i><a>  </a> Intuitively this makes sense. Given a node, all the nodes in the layer after it take said node into their calculation, so it only makes sense that when trying to get to the z value of a node through the chain rule, you must go through the outermost layers first to find it's derivative, like peeling an oninon to get to it's center. <br/>
  <br/>
  <i><a> 3.2 </a><br/>
  <i><a> As pointed out earlier, the derivative of the cost function with respect to any Z value is called delta, so we can re-write this as: </a><br/>
  <br/>
  <img src="/Images/deriv3.2.png"><br/>  
  </sub>
</p>
    
 4. Now we just need to find the derivative of each z value in the next layer with respect to the z value of the current layer.
 <p align="center">
  <sub> <i><a> 4.1 </a><br/>
  <i><a> The Z values of any layer are just the weighted sum of the values in the previous layer, so the z values in layer l+1 should be the weighted sum of the output values of layer l </a><br/>
  </br>
  <img src="/Images/deriv4.1.png"><br/>  
  </br>
  <i><a> 4.2 </a><br/>
  <i><a> Similar to our earlier situation, any term that does not contain the z value we are finding the derivative with respect to, will equate to zero, so we can re-write the term as follows:</a><br/>
  </br>
  <img src="/Images/deriv4.2.png"><br/> 
  </br>
  <i><a> 4.3 </a><br/>
  <i><a> Which then becomes:</a><br/>
  </br>
  <img src="/Images/deriv4.3.png"><br/> 
  </br>
  <img src="/Images/deriv 4.35.png"><br/>   
  </sub>
</p>

5. We've done it! After this derivation we end up with:
    
<p align="center">
  <sub><br/><i><a> 5.1 </a><br/>
  <img src="/Images/deriv5.png"><br/>  
  <br/>
  <i><a> 5.2 </a><br/>
  <i><a> This entire term is the delta value of the node theta is attatched to: </a><br/>
  <br/>
  <img src="/Images/deriv5.22.png"><br/>  
  <br/>
  <i><a> 5.3 </a><br/>
  <i><a> So we can re-write this as: </a><br/>
  <br/>
  <img src="/Images/deriv5.3.png"><br/>  
  <br/>
  </sub>
</p>
    
- In total, what this really means is that we multiply the delta value of every node in the next layer, with the theta that multiplies the node connected with the theta value that we are finding the gradient for in the current layer (the 'current node'). After this we multiply by the derivative of our sigmoid function with respect to the current node's z value and finally multiply by the output value of the node in the previous layer that multiplies with the theta we are finding the gradient for to form the current node's z value. Wow, that was a mouthful. I really suggest taking a moment (or a few weeks) to sit down and really digest what is happening here to fully grasp this crucial concept in neural networks.
 


