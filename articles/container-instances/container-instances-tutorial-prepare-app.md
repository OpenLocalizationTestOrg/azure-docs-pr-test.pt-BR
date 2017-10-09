---
title: "aaaAzure tutorial de instâncias de contêiner - preparar seu aplicativo | Documentos do Azure"
description: "Preparar um aplicativo para implantação tooAzure instâncias de contêiner"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="ddbf7-103">Criar contêiner para implantação tooAzure instâncias de contêiner</span><span class="sxs-lookup"><span data-stu-id="ddbf7-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="ddbf7-104">As Instâncias de Contêiner do Azure permitem a implantação de contêineres do Docker na infraestrutura do Azure sem o provisionamento de máquinas virtuais ou a adoção de serviço de nível superior.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="ddbf7-105">Neste tutorial, você criará um aplicativo Web simples no Node.js e o empacotará em um contêiner que pode ser executado usando as Instâncias de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="ddbf7-106">Abordaremos:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddbf7-107">Clonando a fonte do aplicativo do GitHub</span><span class="sxs-lookup"><span data-stu-id="ddbf7-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="ddbf7-108">Criando imagens de contêiner da fonte do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ddbf7-108">Creating container images from application source</span></span>
> * <span data-ttu-id="ddbf7-109">Imagens de saudação de teste em um ambiente de Docker local</span><span class="sxs-lookup"><span data-stu-id="ddbf7-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="ddbf7-110">Tutoriais subsequentes, você carregar sua imagem tooan registro de contêiner do Azure e, em seguida, implantá-los tooAzure instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ddbf7-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ddbf7-111">Before you begin</span></span>

<span data-ttu-id="ddbf7-112">Este tutorial assume uma compreensão básica dos conceitos fundamentais do Docker como contêineres, imagens de contêiner e comandos básicos do docker.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="ddbf7-113">Se necessário, consulte [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para conhecer os conceitos básicos de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="ddbf7-114">toocomplete neste tutorial, você precisa de um ambiente de desenvolvimento do Docker.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="ddbf7-115">O Docker fornece pacotes que configuram facilmente o Docker em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="ddbf7-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="ddbf7-116">Obter o código de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ddbf7-116">Get application code</span></span>

<span data-ttu-id="ddbf7-117">exemplo Hello neste tutorial inclui um aplicativo da web simples criado no [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ddbf7-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="ddbf7-118">aplicativo Hello serve a uma página HTML estática e tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-118">hello app serves a static HTML page and looks like this:</span></span>

![Aplicativo de tutorial mostrado no navegador][aci-tutorial-app]

<span data-ttu-id="ddbf7-120">Use git toodownload Olá exemplo:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="ddbf7-121">Criar imagem de contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="ddbf7-121">Build hello container image</span></span>

<span data-ttu-id="ddbf7-122">Olá Dockerfile fornecida no repositório de exemplo hello mostra como o contêiner de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="ddbf7-123">Ele começa em um [imagem oficial do Node. js] [ dockerhub-nodeimage] com base em [Linux Alpine](https://alpinelinux.org/), uma distribuição pequena que é adequado toouse com contêineres.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="ddbf7-124">Em seguida, copia os arquivos de aplicativo hello contêiner hello, dependências usando Olá Node Package Manager é instalado e finalmente inicia o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="ddbf7-125">Saudação de uso `docker build` imagem de contêiner do comando toocreate hello, marcando-o como *aci de tutorial de aplicativo*:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="ddbf7-126">Saudação de uso `docker images` toosee imagem de saudação criada:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="ddbf7-127">Saída:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="ddbf7-128">Executar o contêiner de saudação localmente</span><span class="sxs-lookup"><span data-stu-id="ddbf7-128">Run hello container locally</span></span>

<span data-ttu-id="ddbf7-129">Antes de tentar implantar Olá contêiner tooAzure instâncias de contêiner, executá-lo localmente tooconfirm funciona.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="ddbf7-130">Olá `-d` switch permite que o contêiner Olá executadas em segundo plano hello, enquanto `-p` permite que você toomap uma porta arbitrária no seu tooport computação 80 no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="ddbf7-131">Olá abrir navegador toohttp://localhost:8080 tooconfirm que Olá contêiner está em execução.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Aplicativo hello em execução localmente no navegador Olá][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="ddbf7-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ddbf7-133">Next steps</span></span>

<span data-ttu-id="ddbf7-134">Neste tutorial, você criou uma imagem de contêiner pode ser implantado tooAzure instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="ddbf7-135">Olá, as etapas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="ddbf7-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ddbf7-136">Fonte do aplicativo hello clonagem do GitHub</span><span class="sxs-lookup"><span data-stu-id="ddbf7-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="ddbf7-137">Criando imagens de contêiner da fonte do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ddbf7-137">Creating container images from application source</span></span>
> * <span data-ttu-id="ddbf7-138">Teste o contêiner de saudação localmente</span><span class="sxs-lookup"><span data-stu-id="ddbf7-138">Testing hello container locally</span></span>

<span data-ttu-id="ddbf7-139">Avançar toohello toolearn próximo de tutorial sobre como armazenar imagens de contêiner em um registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddbf7-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ddbf7-140">Imagens de push tooAzure registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="ddbf7-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png