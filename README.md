# Kaggle_training_template
This is templates which prepare a environment for EDA, training, debug, and inferences and provide scripts for baseline models.
This template uses [gcr.io/kaggle-gpu-images/python](https://hub.docker.com/r/kaggle/python).

## Setup
1. Clone repository

```bash
git clone https://github.com/Calm-Ryan/Kaggle_training_template.git
```

2. Build docker container
```
cd 

## Directory

| <br>
|- input  - data or something that are downloaded <br>
|- models - models or outputs are exported from trainings and inferences <br>
|- notebooks - Jupyter notebooks (*.ipynb files) <br>
|- repo - some reports of our experiments and papers <br>
|   |- exp <br>
|   |- papers <br>
| <br>
|- src - All of python scripts is contained. We should save scripts which is named "*.py" files. <br>
|- tools - Docker environment with GPU.<br>
|- LICENSE - MIT LICENSE <br>
