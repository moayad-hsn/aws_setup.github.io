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
jupyter lab
~~~

go here 
~~~
:8888/lab
~~~

# Running Tensorboard on aws and access through localhost

You would have installed tensorboardX and tensorboard

~~~
pip install tensorboard
~~~

~~~
pip install tensorboardX
~~~

Then in a local terminal run 

~~~
ssh -i '.\Documents\Other docs\Key\Moayad.pem' -NL 6006:localhost:6006 ubuntu@
~~~
replace the key file if needed and add the public IP address. Then on a browser navigate to 

~~~
http://localhost:6006/
~~~
