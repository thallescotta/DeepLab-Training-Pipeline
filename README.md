# Pipeline de Treinamento DeepLab 🧠

Este repositório é baseado no código Keras disponível no site da documentação oficial do DeepLabV3+: 

https://github.com/rishizek/tensorflow-deeplab-v3-plus

https://keras.io/examples/vision/deeplabv3_plus/

https://github.com/thallescotta/DeepLab-Training-Pipeline/blob/main/Multi%E2%80%90class-segmentation-of-temporomandibular-joint-using-ensemble-deep-learning.pdf


## Construção do Modelo DeepLabV3+ 🛠️

O DeepLabV3+ estende o DeepLabV3 adicionando uma estrutura de codificador-decodificador. O módulo codificador processa informações contextuais em múltiplas escalas aplicando convoluções dilatadas em várias escalas, enquanto o módulo decodificador refina os resultados da segmentação ao longo das bordas dos objetos.

## Instalação 🚀

### 1. Instalar o Docker 🐳

Encontre os arquivos de instalação no diretório `scripts`.

```bash
bash install_docker_ce.sh
```

### 2. Baixar o Dataset Pascal VOC 📦

Baixe o conjunto de dados Pascal VOC usando o comando abaixo:

```bash
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
```

### 3. Extrair o Dataset e Colocar em `dataset-dir` 🗂️

Extraia o dataset e mova para o diretório apropriado:

```bash
tar -xvf VOCtrainval_11-May-2012.tar -C /home/thalles/DeepLab-Training-Pipeline/dataset-dir/
```

### 4. Construir a Imagem Docker 🏗️

Construa a imagem Docker para o ambiente de treinamento:

```bash
docker build -t deeplab-training-pipeline /home/thalles/DeepLab-Training-Pipeline/
```
![image missing](/2.JPG "Image")

### 5. Configurar o Caminho do Dataset no Script `docker_run.sh` 📍

Edite o arquivo `docker_run.sh` para configurar o caminho do dataset:

```bash
nano /home/thalles/DeepLab-Training-Pipeline/scripts/ubuntu/docker_run.sh
```

Dentro do arquivo, encontre e edite a variável `DATASET_LOC` para refletir o caminho correto do seu dataset:

```bash
DATASET_LOC=/home/thalles/DeepLab-Training-Pipeline/dataset-dir/VOCdevkit/VOC2012
```

Salve e feche o arquivo.

### 6. Criar o Container com o Dataset Compartilhado 🏗️

Crie o container Docker que utilizará o dataset:

```bash
bash /home/thalles/DeepLab-Training-Pipeline/scripts/ubuntu/docker_run.sh
```
![image missing](/Tensor.jpg "Tensor")

### 7. Executar o Treinamento 🏋️‍♂️

Dentro do container Docker, execute o script de treinamento:

```bash
bash train.sh
```



![image missing](/3.JPG "Image")

```bash
history
bash /home/thalles/DeepLab-Training-Pipeline/scripts/ubuntu/docker_run.sh
```





# DeepLab Training Pipeline (Original Article)

This repo is based on the Keras code available in here - https://keras.io/examples/vision/deeplabv3_plus/

## Building the DeepLabV3+ model

DeepLabv3+ extends DeepLabv3 by adding an encoder-decoder structure. The encoder module processes multiscale contextual
information by applying dilated convolution at multiple scales, while the decoder module refines the segmentation
results along object boundaries.

![image missing](/deeplabv3_plus_diagram.png "DeepLabV3 Diagram")

## Installation

### Install docker

Find the installation files under scripts directory

```bash
bash install_docker_ce.sh
```

### Install nvidia-docker runtime

```bash
bash install_nvidia-runtime.sh
```

### Download the dataset

[comment]: <> (This is trained using Crowd Instance-level Human Parsing Dataset)

[comment]: <> (Link - https://drive.google.com/uc?id=1B9A9UCJYMwTL4oBEo4RZfbMZMaZhKJaz)

Pascal VOC download link

http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar

### Extract the dataset and keepunder dataset-dir

[comment]: <> (unzip instance-level-human-parsing.zip)

[comment]: <> (mv instance-level_human_parsing <dataset-dir>)

```bash
tar -xcf VOCtrainval_11-May-2012.tar
mv VOCtrainval_11-May-2012 <dataset-dir>
```

### Build the docker

```bash
bash build.sh
```

### Set the path to the dataset location in docker_run.sh script

[comment]: <> (DATASET_LOC=<dataset-dir>/instance-level_human_parsing/instance-level_human_parsing)
```bash
DATASET_LOC=<dataset-dir>/VOCtrainval_11-May-2012/VOCdevkit/VOC2012
```

### Create container with the shared dataset

```bash
bash docker_run.sh
```

### Run the training

```bash
bash train.sh
```
