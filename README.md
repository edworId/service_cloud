<h1 align="center"> Serviço YOLO na Google Cloud Platform (GCP) </h1>

## Índice

1. INTRODUÇÃO
2. VANTAGENS
3. YOLO
4. GCP Setup
5. Configuração do Sistema
6. Comandos Systemctl
7. Integração com GCP

## INTRODUÇÃO

Este repositório contém um projeto que utiliza o algoritmo YOLO (You Only Look Once) para detecção de objetos com integração ao serviço configurado na GCP. Este README fornece informações essenciais para configurar, executar e gerenciar o serviço usando o `systemctl`, proporcionando facilidade de gerenciamento e automação.

O systemctl é uma ferramenta de controle e gerenciamento central para o sistema e o gerenciador de serviços systemd. Ele desempenha um papel crucial em sistemas operacionais baseados em systemd, como muitas distribuições Linux modernas, tais como o Ubuntu 16.04 e posteriores.

## VANTAGENS:
	
  - O `systemctl` fornece uma interface de linha de comando simples e consistente para gerenciar serviços, tornando as operações de inicialização, parada e reinicialização intuitivas.
  - Automatiza a resolução de dependências entre unidades (serviços), garantindo que serviços dependentes sejam iniciados ou parados na ordem apropriada.
  - Facilita o monitoramento do status de unidades com o comando `status`, fornecendo informações detalhadas, mensagens de log associadas e indicadores visuais do estado da unidade.
  - Integra-se ao `journalctl`, consolidando logs de sistema e permitindo que os usuários obtenham informações detalhadas sobre o histórico de eventos do sistema.
  - Utiliza arquivos de configuração padronizados para definir propriedades de unidades, simplificando a leitura, escrita e manutenção das configurações do sistema.
  - Permite facilmente habilitar ou desabilitar serviços para serem iniciados automaticamente durante a inicialização do sistema, proporcionando flexibilidade na configuração do ambiente.
  - Além de serviços, `systemctl` gerencia timers (tarefas agendadas), sockets (comunicação entre serviços) e outras unidades, proporcionando uma gestão completa do sistema.

O `systemctl` se destaca como uma ferramenta poderosa e versátil para administradores de sistemas, oferecendo controle robusto sobre o ambiente do sistema operacional.


## YOLO

YOLO é uma técnica de detecção de objetos em imagens e vídeos que se destaca pela sua eficiência, processando a imagem inteira de uma vez, em vez de dividir a imagem em grades. Ele fornece resultados rápidos e precisos, sendo amplamente utilizado em diversas aplicações.




### DESVANTAGENS:
	
	- Há uma tonelada de solicitações de recursos para upgrade que ainda estão em andamento (como capacidade de autorregistro e autoinspeção de contêineres, cópia de arquivos do host para o contêiner e muito mais).
	- Há momentos em que um container fica inativo, então depois disso, ele precisa de uma estratégia de backup e recuperação, embora existam várias soluções, mas que não são automatizadas ou nem muito escaláveis ainda.
	- Em comparação com as máquinas virtuais, os contêineres Docker oferecem menos sobrecarga, mas não sobrecarga zero.
	- O principal problema é que se um aplicativo projetado para ser executado em um contêiner do Docker no Windows, ele não pode ser executado no Linux ou vice-versa. No entanto, as máquinas virtuais não estão sujeitas a essa limitação.
	- Podemos dizer que, para aplicativos que requerem interfaces ricas, o Docker não é uma boa solução.

<h1 align="center">  </h1>
<p align="center">
<img width="900", img src="https://github.com/edworId/yolo_docker/blob/main/Estrutura%20Docker.jpeg"/>
</p>

<h6 align="center"> Estrutura Docker </h6>

Este projeto fornece uma implementação fácil e rápida para executar o YOLO (You Only Look Once) em um ambiente Docker usando Python. O YOLO é um algoritmo de detecção de objetos em imagens e vídeos em tempo real.

## Pré-requisitos

Certifique-se de ter o Docker instalado em sua máquina antes de prosseguir. Você pode encontrar instruções de instalação [aqui](https://docs.docker.com/get-docker/).

```
sudo apt update && sudo apt upgrade
```
```
curl -fsSL https://get.docker.com | bash
```

## DOCKER IMAGE: 
Nesta etapa, você escreve um Dockerfile que cria uma imagem do Docker. A imagem contém todas as dependências que o aplicativo Python precisa, incluindo o próprio Python.

### Exemplo de Imagem:

```
# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

Agora você deve rodar o código abaixo para poder construir a sua imagem

```
docker build -t nome_da_imagem .
```

## Instruções de Uso da Docker

```
$ docker ps (LISTAR CONTAINERS)
$ docker ps -a (LISTAR CONTAINERS ATIVOS E INATIVOS)
$ docker start container_id  (Starta o container que está parado) 
$ docker exec - it container_id bash  (Entramos dentro da docker em root)
$ docker inspect container_id  (Inspeção)
$ docker run -p 2300:5000 -d docker_image  (conectar entre ips)
$ docker rm 'container' (Remove containers indesejados)
$ docker rmi 'imagem' (Remove imagens indesejados)
```



## Arquivos disponíveis

app_teste - Usado para teste do funcionamento do YOLO com ultralytics sem docker
app_custom - Usado para um modelo custom do YOLO já para ser integrado com a imagem Docker que será criada (faça as alterações no código sobre o modelo e a imagem)
dockerfile - Utilizado para criação da imagem com as instalações devidas para seu funcionamento e instrunções de cópia de todos arquivos presentes na pasta
predict.csv - resultado do teste realizado
dog.jpeg - imagem do teste
yolov5s.pt - modelo baixado para o teste com a ultralytics 

    
<h1 align="center">  </h1>

CLONE: 
```
git clone git@github.com:edworId/service_cloud.git
```
<h1 align="center"> Autores </h1>

| [<img src="https://avatars.githubusercontent.com/u/110691832?s=400&u=e671447386d38975c165bff78b715ea80549c069&v=4" width=115><br><sub>Edmundo Lopes Silva</sub>](https://github.com/edworId) |  
| :---: |      
| [<img src="https://avatars.githubusercontent.com/u/70495992?s=400&u=08519f58327d4fe11229ea8fc47b9d2d1be689a5&v=4" width=115><br><sub>Michael Botelho</sub>](https://github.com/michaelbs09) |  

<p align="center">
<img src="https://img.shields.io/badge/Python-14354C?style=for-the-badge&logo=python&logoColor=white"/>
</p>
