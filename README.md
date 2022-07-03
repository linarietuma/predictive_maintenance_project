# Predictive Maintenance Project 

## About 
### The Project 

The project explores the application of Long Short-Term Memory (LSTM) neural network on a  time series dataset to predict failure of a water pump to allow for timely maintenance. 

### The Background

LSTMs are a type of Recurrent Neural Network (RRN). RNNs differ from more traditional feed-forward NNs due to their ability to account for contextual information of data. This characteristic makes RRNs superior when working with time-series and sequential data (i.e., ). RRNs are trained using back propagation through time (BPTT) - an extension of backpropagation used in traditional feed-forward NNs.

RRNs are susceptible to exploding and vanishing gradients due to the recurrent flow of inputs through the network. Long Short-Term Memory (LSTM) networks were designed to address the vanishing gradient problem of RRNs and effectively handle extended sequences. LSTMs achieve this by having Gated Cells that can discard irrelevant information.


### The Data

![](img/nan_matrix.png)

The project uses a sensor dataset from Kaggle - [pump_sensor_data.](https://www.kaggle.com/datasets/nphantawee/pump-sensor-data/metadata) There are 52 sensors with a measurement made every minute for 220320 minutes (153 days). The `machine_status` column is the target feature to used as a predictor for machine breakdown. 

Feature Summary:
- Timestamps in 1-minute time steps
- 52 Sensors 
- Machine Status (Normal, Broken, Recovering) (target feature)

### The Model

![](img/model.png)

The following model will use a stacked LSTM architecture, i.e., the model is made up of  multiple LSTM layers.  The additional complexity of a deep `LSTM` model allows for higher abstraction to capture more complex input patterns. 

The model has an input layer with dimensions that fit the input, two `LSTM` layers with 20 and 42 nodes respectively and two output layers - one for the label encoded data, the other for one-hot encoded data (for results analysis the one-hot encoded layer data are used). For both hidden layers `relu` activation function is used to address the exploding/ vanishing gradient problem associated with activation function likes `sigmoid` or `tanh`. For the output layer `softmax` activation is used to - a type of `sigmoid` function used in classification problems with more then two classes.

The output layers are `Dense` layers, i.e., each node in a `Dense` layer is influenced by every node from the previous layer. The `Dense` layer has a single output node for the label encoded y values (i.e., an array of categorical y values is encoded as an array of integers) while the `Dense` layer of one-hot encoded y values has a node for each column in the encoded matrix. 

### Built With

* Python version: 3.8.12
* Pandas version: 1.3.4
* Seaborn version: 0.11.2
* Sklearn version: 1.0.2
* Numpy version: 1.19.5
* Matplotlib version: 3.4.2
* Tensorflow version: 2.6.0

## Results


![](img/acc_loss_graph.png)

The dataset is heavily unbalanced, and classifying all instances as the dominant class would already give an accuracy of 95.7%. The graph above shows the model's accuracy and loss on the training dataset. The training dataset achieves an accuracy of ~99.5% which suggests that the model is not classifying all instances as the dominant class and the classification is not random. So far so good! Next the model was tested using the test dataset. 

![](img/predctions.png)

The model achieved an accuracy of 98.5%. The graphs above display the predicted and actual values of the test dataset. The model does not identify the `BROKEN` event but that's to be expected with only seven `BROKEN` instances in the whole dataset. However, the beginning of the `RECOVERING` phase matches near identically to the target data. The data were shifted by 10 minutes thus giving an accurate indication of machine failure 10 minutes in advance.

To better evaluate the performance of the model additional performance metrics besides accuracy are considered.  The confusion matrix suggests that all `NORMAL` instances were correctly classified, however almost a third of the `RECOVERING` instances where misclassified as `NORMAL`. This coincides with the predictions from the chart above where during the `RECOVERING` phase in the test data there's a dip.

![](img/conf_matrix.png)

## Future Improvements

- Explore additional architectures (i.e., additional LSTM layers, different activation functions, increased/ decreased number of nodes).
- Explore additional time shifts (in the current model, data are shifted by 10 minutes).
- Introduce feature engineering (besides removing/ fixing features with an excessive number of NaNs, feature engineering has not been used).


## Acknowledgements

The project uses a sensor dataset from Kaggle - [pump_sensor_data.](https://www.kaggle.com/datasets/nphantawee/pump-sensor-data/metadata)

For an introduction into RRNs [MIT's 6.S191 Lecture on RRNs](https://youtu.be/qjrad0V0uJE) has been a valuable resource.

A useful resource for understanding Keras LSTM architecture - [Keras LSTM Diagram](https://github.com/MohammadFneish7/Keras_LSTM_Diagram).

The project has been heavily inspired by Jan Werth's article - [LSTM for Predictive Maintenance on Pump Sensor Data.](https://towardsdatascience.com/lstm-for-predictive-maintenance-on-pump-sensor-data-b43486eb3210)
