# TensorFlow Hackweek Evaluation / Playing

## Setup Tensorflow in VirtualEnv
Requires Python3 to run. Install via Virtualenv

https://www.tensorflow.org/get_started/eager


The Iris classification problem


```bash
# to run example iris example. 
python3= iris.y  
```


## TensorFlow Object Detection API

https://towardsdatascience.com/building-a-real-time-object-recognition-app-with-tensorflow-and-opencv-b7a2b4ebdc32

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
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/using_your_own_dataset.md

###TFRecord file format

##LabelImg
https://github.com/tzutalin/labelImg#macos

Go through Virtualenv install to avoid issues

- Rectangle box around object, label it

```
python3 xml_to_csv.py '/Users/clayselby/Developer/tensorflow_hackweek/images'
```

### GoogleCloud ML Train model

Google Cloud account creation, enable ML APIs

Cloud bucket name - tedtestmodels
```
gcloud init
```

```
gcloud ml-engine models list
```

Upload label map and models to Googlecloud
```
gsutil cp -r data gs://tedtestmodels/data
gsutil cp label-map-full.pbtxt gs://tedtestmodels/data
```
Start tensorboard logger
```
tensorboard --logdir=gs://tedtestmodels
```

Make object detection models distribution
```
# From tensorflow/models/research/
python setup.py sdist
(cd slim && python setup.py sdist)
```

Submit job to gcloud
```
# From tensorflow/models/research/
gcloud ml-engine jobs submit training object_detection_`date +%s` \
    --runtime-version 1.2 \
    --job-dir=gs://tedtestmodels/data/jobs \
    --packages dist/object_detection-0.1.tar.gz,slim/dist/slim-0.1.tar.gz \
    --module-name object_detection.train \
    --region us-central1 \
    --config /Users/clayselby/Developer/tensorflow_hackweek/cloud.yml \
    -- \
    --train_dir=gs://tedtestmodels/data \
    --pipeline_config_path=gs://tedtestmodels/ssd_mobilenet_v1_pets.config
```

View stats
```
gcloud ml-engine jobs stream-logs object_detection_1527870848
```

## Train model steps...
- Take photos
- Label with LabelImg
- Convert to CSV
- Convert to TFRecord
- Upload model to Google Cloud Platform


# Known issues
- Could not get camera access in VirtualEnv
- OpenCV 3.0.0 no longer exists on conda, so using 3.1.0 which may crash according to OP

