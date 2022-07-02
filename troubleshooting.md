# Troubleshooting 

## Tensorflow errors

### Error 1
**Context:** the error occurs upon instantiating the keras Sequential() model in the following code:

`model = keras.Sequential()`

The error occurs with the following Python and library versions:

- Python version: 3.8.12
- Pandas version: 1.3.4
- Seaborn version: 0.11.2
- Sklearn version: 1.0.2
- Numpy version: 1.19.5
- Matplotlib version: 3.4.2
- Tensorflow version: 2.6.0 & 2.5.0

**Error Message:** `TypeError: Parameter to MergeFrom() must be instance of same class: expected tensorflow.TensorShapeProto got tensorflow.TensorShapeProto.`

**The Fix:**  This fix works in M1 Macbook Air with Miniforge Conda installer.

1. Open the file `../miniforge3/envs/bio/lib/python3.8/site-packages/tensorflow/python/__init__.py `.
2. Swap the order of these lines:

`from tensorflow.python.eager import context`

`from tensorflow.python import pywrap_tensorflow as _pywrap_tensorflow`

to 

`from tensorflow.python import pywrap_tensorflow as _pywrap_tensorflow`

`from tensorflow.python.eager import context`

3. Save the file and rerun the code.
