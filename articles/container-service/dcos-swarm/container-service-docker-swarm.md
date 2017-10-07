---
title: aaaManage Azure Swarm cluster com a API de Docker | Microsoft Docs
description: "Implantar um cluster de Docker Swarm tooa contêineres no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Gerenciamento de contêiner com Docker Swarm
O Docker Swarm fornece um ambiente para implantação de cargas de trabalho em contêineres de em um conjunto de pool de hosts do Docker. Por docker nuvem usa Olá API nativa do Docker. fluxo de trabalho de saudação para gerenciar contêineres em um Docker Swarm é quase idêntico toowhat seria em um único host de contêiner. Este documento fornece exemplos simples de implantação de cargas de trabalho em contêineres em uma instância do Serviço de Contêiner do Azure do Docker Swarm. Para obter documentação mais detalhada sobre o Docker Swarm, confira [Docker Swarm em Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Pré-requisitos toohello exercícios neste documento:

[Criar um Cluster Swarm no Serviço de Contêiner do Azure](container-service-deployment.md)

[Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Implantar um novo contêiner
toocreate um novo contêiner no hello Docker Swarm, use Olá `docker run` comando (garantindo que você abriu um mestre de toohello de túnel SSH de acordo com os pré-requisitos de saudação acima). Este exemplo cria um contêiner de saudação `yeasy/simple-web` imagem:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Depois que o contêiner de saudação tiver sido criado, use `docker ps` tooreturn informações sobre o contêiner de saudação. Observe aqui agente Olá por nuvem que está hospedando o contêiner de saudação é listada:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Agora você pode acessar o aplicativo hello que está em execução neste contêiner por meio do nome DNS público Olá Olá por nuvem agente do balanceador de carga. Você pode encontrar essas informações no hello portal do Azure:  

![Resultados da visita real](./media/container-service-docker-swarm/real-visit.jpg)  

Por padrão, Olá balanceador de carga possui portas 80, 443 e 8080 aberto. Se você quiser tooconnect em outra porta você precisará tooopen essa porta no hello balanceador de carga do Azure para Olá Pool de agente.

## <a name="deploy-multiple-containers"></a>Implantar vários contêineres
Como vários contêineres são iniciados, executando 'docker run' várias vezes, você pode usar o hello `docker ps` toosee de comando que hospeda os contêineres de saudação estão em execução no. O exemplo hello abaixo, as três contêineres são distribuídos igualmente por três agentes de por nuvem hello:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Implantar contêineres usando Docker Compose
Você pode usar a implantação de saudação tooautomate Docker compor e a configuração de vários contêineres. toodo, portanto, verifique se foi criado um túnel de Secure Shell (SSH) e variável Olá DOCKER_HOST foi definido (consulte Olá pré-requisitos acima).

Crie um arquivo docker-compose.yml em seu sistema local. toodo isso, use [exemplo](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

Executar `docker-compose up -d` toostart implantações de contêiner de saudação:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

Por fim, Olá lista de contêineres em execução será retornada. Essa lista mostra contêineres Olá que foram implantados usando o Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Naturalmente, você pode usar `docker-compose ps` tooexamine somente Olá contêineres definidos no seu `compose.yml` arquivo.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre o Docker Swarm.](https://docs.docker.com/swarm/)

