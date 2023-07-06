docker をセットアップした際のメモ

# 1 NVIDIA Dockerのインストール

## 1 Dockerをインストール
~~~ bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker your-user
~~~

your-user はあなたのユーザー名に置き換えてください。

## 2 NVIDIA Dockerのリポジトリをシステムに追加
~~~ bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
~~~

## 3 NVIDIA Dockerをインストール
~~~ bash
sudo apt-get update
sudo apt-get install -y nvidia-docker2
~~~


## 4 Dockerデーモンを再起動
~~~ bash
sudo systemctl restart docker
~~~

<br>

# NVIDIA Dockerを使用
~~~ bash
sudo docker run -it --gpus all nvidia/cuda:12.1.0-base-ubuntu20.04
~~~
この--gpus allフラグは、すべての利用可能なGPUをコンテナに公開することを意味します。
特定のGPUだけを公開したい場合は、フラグを--gpus '"device=1,2"'のように設定できます。
ここでは、デバイス1とデバイス2のみがコンテナに公開されます。