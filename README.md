# A Notebook on Quickly getting a deep learning base AMI running

## First of all, getting miniconda installed

~~~python
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
~~~

~~~python
chmod u+x Miniconda3-latest-Linux-x86_64.sh && ./Miniconda3-latest-Linux-x86_64.sh
~~~

~~~
source .bashrc
~~~

~~~python
conda install -y pytorch torchvision torchaudio cudatoolkit -c pytorch
~~~

~~~python
conda install -y pandas scikit-learn matplotlib tqdm seaborn tensorboard
~~~

~~~python
pip install wandb
~~~

~~~python
conda clean -a
~~~

## We then get going with setting up jupyterlab
installing jupyter lab

~~~python
conda install -c conda-forge jupyterlab
~~~
server-configurations:

~~~python
touch .jupyter/jupyter_server_config.py
~~~

~~~python
vi .jupyter/jupyter_server_config.py
~~~
then inside you can add this
~~~python
c.ServerApp.ip = '*' # bind to any network interface
c.ServerApp.password = u'sha256:bcd259ccf...<your hashed password here>'
c.ServerApp.open_browser = False
c.ServerApp.port = 8888 # or any other ports you'd like
~~~
then to get the password we 

~~~python
jupyter server password
~~~

then 
~~~python
cat .jupyter/jupyter_server_config.json
~~~
copy the hashed password into the .py file you created above

## Getting the lab launched

~~~
screen -S Jupyter
~~~

then 

~~~
jupyter lab
~~~

~~~
ctrl+A
~~~

~~~
ctrl+D
~~~

go here 
~~~
:8888/lab
~~~

# Mounting EBS

First let us see the name of the storage:

~~~
lsblk
~~~

We then make our file system

~~~
sudo mkfs -t xfs /dev/[drive name]
~~~

We create a dir to mount the drive in

~~~
mkdir ~/data
~~~

We mount the drive

~~~
sudo mount /dev/[drive name] ~/data
~~~

We change the permission to be able to access the drive

~~~
cd ~/data
~~~
~~~
sudo chmod go+rw .
~~~
~~~
cd ..
~~~
