# Pipeline de Treinamento DeepLab 🧠

Este repositório é baseado no código Keras disponível no site da documentação oficial do DeepLabV3+.

## Construção do Modelo DeepLabV3+ 🛠️

O DeepLabV3+ estende o DeepLabV3 adicionando uma estrutura de codificador-decodificador. O módulo codificador processa informações contextuais em múltiplas escalas aplicando convoluções dilatadas em várias escalas, enquanto o módulo decodificador refina os resultados da segmentação ao longo das bordas dos objetos.

## Instalação 🚀

### 1. Instalar o Docker 🐳

Encontre os arquivos de instalação no diretório `scripts`.

```bash
bash install_docker_ce.sh
```

### 2. Instalar o runtime do Nvidia-Docker 🎮

```bash
bash install_nvidia-runtime.sh
```

### 3. Baixar o Dataset Pascal VOC 📦

Baixe o conjunto de dados Pascal VOC usando o comando abaixo:

```bash
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
```

### 4. Extrair o Dataset e Colocar em `dataset-dir` 🗂️

Extraia o dataset e mova para o diretório apropriado:

```bash
tar -xvf VOCtrainval_11-May-2012.tar -C /home/thalles/DeepLab-Training-Pipeline/dataset-dir/
```

### 5. Construir a Imagem Docker 🏗️

Construa a imagem Docker para o ambiente de treinamento:

```bash
docker build -t deeplab-training-pipeline /home/thalles/DeepLab-Training-Pipeline/
```

### 6. Configurar o Caminho do Dataset no Script `docker_run.sh` 📍

Edite o arquivo `docker_run.sh` para configurar o caminho do dataset:

```bash
nano /home/thalles/DeepLab-Training-Pipeline/scripts/ubuntu/docker_run.sh
```

Dentro do arquivo, encontre e edite a variável `DATASET_LOC` para refletir o caminho correto do seu dataset:

```bash
DATASET_LOC=/home/thalles/DeepLab-Training-Pipeline/dataset-dir/VOCdevkit/VOC2012
```

Salve e feche o arquivo.

### 7. Criar o Container com o Dataset Compartilhado 🏗️

Crie o container Docker que utilizará o dataset:

```bash
bash /home/thalles/DeepLab-Training-Pipeline/scripts/ubuntu/docker_run.sh
```

### 8. Executar o Treinamento 🏋️‍♂️

Dentro do container Docker, execute o script de treinamento:

```bash
bash train.sh
```

### 9. Verificando a Execução do Container e Iniciando o Treinamento 🧑‍💻

Após iniciar o container, você deve ver uma mensagem de inicialização do TensorFlow como mostrado na captura de tela. Essa mensagem indica que o ambiente está configurado corretamente e o treinamento está prestes a iniciar.

⚠️ **Atenção:** Para evitar problemas com permissões de usuário, considere executar o container com seu próprio usuário. Isso evita que arquivos sejam criados com permissões que possam complicar o acesso posterior.

```bash
docker run -u $(id -u):$(id -g) deeplab-training-pipeline
```

Depois de iniciar o container corretamente, use o comando:

```bash
bash train.sh
```

Isso irá começar o processo de treinamento do modelo DeepLabV3+ com base no dataset configurado.





# DeepLab Training Pipeline

This repo is based on the Keras code available in here - https://keras.io/examples/vision/deeplabv3_plus/

## Building the DeepLabV3+ model

DeepLabv3+ extends DeepLabv3 by adding an encoder-decoder structure. The encoder module processes multiscale contextual
information by applying dilated convolution at multiple scales, while the decoder module refines the segmentation
results along object boundaries.

![image missing](assets/deeplabv3_plus_diagram.png "DeepLabV3 Diagram")

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
