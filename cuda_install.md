# ubuntu 22.04 に CUDA Toolkit 12.2をインストールした際のメモ


## CUDA Toolkit 12.2 Downloads
[公式サイト](https://developer.nvidia.com/cuda-toolkit-archive) でインストールコマンドが得られる

~~~ bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.2.0/local_installers/cuda-repo-ubuntu2204-12-2-local_12.2.0-535.54.03-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-2-local_12.2.0-535.54.03-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-2-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
~~~


## CUDA Toolkitが正しくインストールされていることを確認
~~~ bash
/usr/local/cuda/bin/nvcc --version
~~~


- `nvcc` で次のようなエラーになる場合はPATHを追加する
~~~ bash
Command 'nvcc' not found, but can be installed with:
sudo apt install nvidia-cuda-toolkit
~~~

- PATHを追加 
~~~ bash
echo 'export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}' >> ~/.bashrc
source ~/.bashrc
~~~