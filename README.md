# Setup Instruction (WIP)
## Steps Taken
1. Copy this repo and download and install docker.
2. Create instance of tensorflow 1.3.0 docker image as suited to your hardware listed [here](https://hub.docker.com/r/tensorflow/tensorflow/tags/?page=1&name=1.3.0 "here"). I used the following and will use the name tf130 from here on;
`docker run --name tf130 --gpus all -it tensorflow/tensorflow/tensorflow:1.3.0-devel-gpu-py3 bash`

3. Inside the docker container, run;
`apt-get update`
`curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py`
`python get-pip.py`
	_I also recommend getting a text editor, I use vim;_
	`apt-get install vim`

4. Outside the docker container, run;
`docker cp ./example/ tf130:/home/`

5. Back inside the docker;
`mv ../home/example ~ && cd example`
`pip install -r requirements.txt`
`python run_demo.py`*

\* _currently this yields the error;_
`Traceback (most recent call last):`
	`File "run_demo.py", line 9, in <module>`
		`from model.dcrnn_supervisor import DCRNNSupervisor`
	`File "/root/example/model/dcrnn_supervisor.py", line 13, in <module>`
		`from lib.AMSGrad import AMSGrad`
	`File "/root/example/lib/AMSGrad.py", line 5, in <module>`
		`from tensorflow.python.eager import context`
`ImportError: No module named eager`

## Docker Image
If you just want to run with my setup, I've created a docker image [here](https://hub.docker.com/layers/175787563/tynt7/trafficflow-tf-1.3.0/latest/images/sha256-4433674720e966488fa85419e4c98cc761372a706862801b5140f638b12cb036?context=repo "here"). This image uses the GPU optimizers, as far as I understand will not be friendly if you don't have a dedicated GPU.
