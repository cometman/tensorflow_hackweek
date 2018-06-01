# TensorFlow Hackweek Evaluation / Playing

## Setup Tensorflow in VirtualEnv
Requires Python3 to run. Install via Virtualenv

https://www.tensorflow.org/get_started/eager


The Iris classification problem


```bash
# to run example iris example. 
python2 iris.y  
```


## TensorFlow Object Detection API

Checkout locally: https://github.com/tensorflow/models

Installation: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md

```python
python3 -mpip install matplotlib
```

Activate VirtualEnv
```
cd ~/tensorflow_hackweek
source ./bin/activate
```

If issue:
"RuntimeError: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends. If you are using (Ana)Conda please install python.app and replace the use of 'python' with 'pythonw'. See 'Working with Matplotlib on OSX' in the Matplotlib FAQ for more information."

solution: https://stackoverflow.com/questions/21784641/installation-issue-with-matplotlib-python

### Miniconda
Install https://conda.io/miniconda.html

```
~/miniconda3/bin/conda env create -f environment.yml
```

### OpenCV3
brew install opencv3 --with-contirb --with-qt5

### Running 
```
python3 object_detection_app.py --source=1
```


### Training object detector data set
https://towardsdatascience.com/how-to-train-your-own-object-detector-with-tensorflows-object-detector-api-bec72ecfe1d9

#TFRecord file format


# Known issues
- Could not get camera access in VirtualEnv
- OpenCV 3.0.0 no longer exists on conda, so using 3.1.0 which may crash according to OP

