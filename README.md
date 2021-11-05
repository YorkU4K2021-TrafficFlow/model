# Setup Instruction (WIP)
## Steps Taken
1. Copy this repo and download and install docker.
2. Create instance of tensorflow 1.4.1 docker image as suited to your hardware listed [here](https://hub.docker.com/r/tensorflow/tensorflow/tags/?page=1&name=1.3.0 "here"). I used the following and will use the name tf141 from here on;
`docker run --name tf141 --gpus all -it tensorflow/tensorflow/tensorflow:1.4.1-devel-gpu-py3 bash`

3. Inside the docker container, run;
`apt-get update`
`curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py`
`python get-pip.py`
	_I also recommend getting a text editor, I use vim;_
	`apt-get install vim`

4. Outside the docker container, run;
`docker cp ./example/ tf141:/home/`

5. Back inside the docker;
`mv ../home/example ~ && cd example`
`pip install -r requirements.txt`

`python -m scripts.generate_training_data --output_dir=data/PEMS-BAY --traffic_df_filename=data/pems-bay.h5`*

`python -m scripts.gen_adj_mx  --sensor_ids_filename=data/sensor_graph/graph_sensor_ids.txt --normalized_k=0.1    --output_pkl_filename=data/sensor_graph/adj_mx.pkl`*

`python run_demo.py --config_filename=data/model/pretrained/PEMS-BAY/config.yaml`*

\* _currently this yields an error of a missing dataset due to training data generation scripts failing. Will investigate further.

## Docker Image
~~If you just want to run with my setup, I've created a docker image [here](https://hub.docker.com/layers/175787563/tynt7/trafficflow-tf-1.3.0/latest/images/sha256-4433674720e966488fa85419e4c98cc761372a706862801b5140f638b12cb036?context=repo "here"). This image uses the GPU optimizers, as far as I understand will not be friendly if you don't have a dedicated GPU.~~
Don't use this docker image it won't ever work I used the wrong tensorflow.
