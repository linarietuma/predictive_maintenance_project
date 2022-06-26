# Predictive Maintenance Project 

## About the Project 

Recurrent Neural Networks (RRNs) account for the context and sequence of the data therefore suited for time series analysis.


RRNs are trained using back propagation through time (BPTT) - an extension of backpropagation used in traditional feed-forward NNs.

RRNs are limited in the number of past time steps that can be remembered and susceptible to exploding and vanishing gradient due to recurrent flow of inputs through the network. Long Short-Term Memory (LSTM) neural networks are an extension of RRNs design to address the vanishing gradient problem of RRNs. LSTMs achieve this by having Gated Cells that have the ability to discard irrelevant information.


Long Short-Term Memory (LSTM) neural network used predict failure of a water pump to allow for timely maintenance.

### Built With

* Python version: 3.9.12
* Pandas version: 1.4.2
* Numpy version: 1.22.3
* Matplotlib version: 3.5.1
* Tensorflow version: 2.4.1


## Acknowledgements

The project uses a sensor dataset from Kaggle - [pump_sensor_data.](https://www.kaggle.com/datasets/nphantawee/pump-sensor-data/metadata)

For an introduction into RRNs [MIT's 6.S191 Lecture on RRNs](https://youtu.be/qjrad0V0uJE) has been a valuable resource.

The project has been heavily inspired by Jan Werth's article - [LSTM for Predictive Maintenance on Pump Sensor Data.](https://towardsdatascience.com/lstm-for-predictive-maintenance-on-pump-sensor-data-b43486eb3210)
