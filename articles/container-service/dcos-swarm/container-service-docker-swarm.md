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
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="63566-104">Gerenciamento de contêiner com Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="63566-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="63566-105">O Docker Swarm fornece um ambiente para implantação de cargas de trabalho em contêineres de em um conjunto de pool de hosts do Docker.</span><span class="sxs-lookup"><span data-stu-id="63566-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="63566-106">Por docker nuvem usa Olá API nativa do Docker.</span><span class="sxs-lookup"><span data-stu-id="63566-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="63566-107">fluxo de trabalho de saudação para gerenciar contêineres em um Docker Swarm é quase idêntico toowhat seria em um único host de contêiner.</span><span class="sxs-lookup"><span data-stu-id="63566-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="63566-108">Este documento fornece exemplos simples de implantação de cargas de trabalho em contêineres em uma instância do Serviço de Contêiner do Azure do Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="63566-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="63566-109">Para obter documentação mais detalhada sobre o Docker Swarm, confira [Docker Swarm em Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="63566-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="63566-110">Pré-requisitos toohello exercícios neste documento:</span><span class="sxs-lookup"><span data-stu-id="63566-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="63566-111">Criar um Cluster Swarm no Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="63566-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="63566-112">Conecte-se com o cluster de por nuvem Olá no serviço de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="63566-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="63566-113">Implantar um novo contêiner</span><span class="sxs-lookup"><span data-stu-id="63566-113">Deploy a new container</span></span>
<span data-ttu-id="63566-114">toocreate um novo contêiner no hello Docker Swarm, use Olá `docker run` comando (garantindo que você abriu um mestre de toohello de túnel SSH de acordo com os pré-requisitos de saudação acima).</span><span class="sxs-lookup"><span data-stu-id="63566-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="63566-115">Este exemplo cria um contêiner de saudação `yeasy/simple-web` imagem:</span><span class="sxs-lookup"><span data-stu-id="63566-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="63566-116">Depois que o contêiner de saudação tiver sido criado, use `docker ps` tooreturn informações sobre o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="63566-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="63566-117">Observe aqui agente Olá por nuvem que está hospedando o contêiner de saudação é listada:</span><span class="sxs-lookup"><span data-stu-id="63566-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="63566-118">Agora você pode acessar o aplicativo hello que está em execução neste contêiner por meio do nome DNS público Olá Olá por nuvem agente do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="63566-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="63566-119">Você pode encontrar essas informações no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="63566-119">You can find this information in hello Azure portal:</span></span>  

![Resultados da visita real](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="63566-121">Por padrão, Olá balanceador de carga possui portas 80, 443 e 8080 aberto.</span><span class="sxs-lookup"><span data-stu-id="63566-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="63566-122">Se você quiser tooconnect em outra porta você precisará tooopen essa porta no hello balanceador de carga do Azure para Olá Pool de agente.</span><span class="sxs-lookup"><span data-stu-id="63566-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="63566-123">Implantar vários contêineres</span><span class="sxs-lookup"><span data-stu-id="63566-123">Deploy multiple containers</span></span>
<span data-ttu-id="63566-124">Como vários contêineres são iniciados, executando 'docker run' várias vezes, você pode usar o hello `docker ps` toosee de comando que hospeda os contêineres de saudação estão em execução no.</span><span class="sxs-lookup"><span data-stu-id="63566-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="63566-125">O exemplo hello abaixo, as três contêineres são distribuídos igualmente por três agentes de por nuvem hello:</span><span class="sxs-lookup"><span data-stu-id="63566-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="63566-126">Implantar contêineres usando Docker Compose</span><span class="sxs-lookup"><span data-stu-id="63566-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="63566-127">Você pode usar a implantação de saudação tooautomate Docker compor e a configuração de vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="63566-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="63566-128">toodo, portanto, verifique se foi criado um túnel de Secure Shell (SSH) e variável Olá DOCKER_HOST foi definido (consulte Olá pré-requisitos acima).</span><span class="sxs-lookup"><span data-stu-id="63566-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="63566-129">Crie um arquivo docker-compose.yml em seu sistema local.</span><span class="sxs-lookup"><span data-stu-id="63566-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="63566-130">toodo isso, use [exemplo](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="63566-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="63566-131">Executar `docker-compose up -d` toostart implantações de contêiner de saudação:</span><span class="sxs-lookup"><span data-stu-id="63566-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

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

<span data-ttu-id="63566-132">Por fim, Olá lista de contêineres em execução será retornada.</span><span class="sxs-lookup"><span data-stu-id="63566-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="63566-133">Essa lista mostra contêineres Olá que foram implantados usando o Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="63566-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="63566-134">Naturalmente, você pode usar `docker-compose ps` tooexamine somente Olá contêineres definidos no seu `compose.yml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="63566-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63566-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63566-135">Next steps</span></span>
[<span data-ttu-id="63566-136">Saiba mais sobre o Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="63566-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

