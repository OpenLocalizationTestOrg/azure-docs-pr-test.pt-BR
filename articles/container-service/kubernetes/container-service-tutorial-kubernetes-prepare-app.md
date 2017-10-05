---
title: "Tutorial do Serviço de Contêiner do Azure – preparar o aplicativo | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – preparar o aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="4b6fe-104">Criar imagens de contêiner a serem usadas com o Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="4b6fe-104">Create container images to be used with Azure Container Service</span></span>

<span data-ttu-id="4b6fe-105">Neste tutorial, parte um de sete, um aplicativo de vários contêineres é preparado para uso em Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="4b6fe-106">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="4b6fe-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="4b6fe-107">Clonando a fonte do aplicativo do GitHub</span><span class="sxs-lookup"><span data-stu-id="4b6fe-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="4b6fe-108">Criando uma imagem de contêiner a partir da origem de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4b6fe-108">Creating a container image from the application source</span></span>
> * <span data-ttu-id="4b6fe-109">Testando o aplicativo em um ambiente Docker local</span><span class="sxs-lookup"><span data-stu-id="4b6fe-109">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="4b6fe-110">Uma vez concluído, o seguinte aplicativo estará acessível em seu ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-110">Once completed, the following application is accessible in your local development environment.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="4b6fe-112">Nos tutoriais subsequentes, a imagem de contêiner é carregada em um Registro de Contêiner do Azure e, em seguida, é executada em um cluster Kubernetes hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4b6fe-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4b6fe-113">Before you begin</span></span>

<span data-ttu-id="4b6fe-114">Este tutorial assume uma compreensão básica dos conceitos fundamentais do Docker como contêineres, imagens de contêiner e comandos básicos do docker.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="4b6fe-115">Se necessário, consulte [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para conhecer os conceitos básicos de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="4b6fe-116">Para concluir este tutorial, você precisa de um ambiente de desenvolvimento do Docker.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-116">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="4b6fe-117">O Docker fornece pacotes que configuram facilmente o Docker em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="4b6fe-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="4b6fe-118">Obter o código de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4b6fe-118">Get application code</span></span>

<span data-ttu-id="4b6fe-119">O aplicativo de exemplo usado neste tutorial é um aplicativo de votação básico.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-119">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="4b6fe-120">O aplicativo consiste de um componente Web de front-end e uma instância Redis de back-end.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-120">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="4b6fe-121">O componente Web é empacotado em uma imagem de contêiner personalizada.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-121">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="4b6fe-122">A instância Redis utiliza uma imagem não modificada do Hub Docker.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-122">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="4b6fe-123">Use o git para baixar uma cópia do aplicativo em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-123">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="4b6fe-124">Dentro do diretório clonado está o código-fonte do aplicativo, um arquivo Docker Compose pré-criado e um arquivo de manifesto Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-124">Inside the cloned directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="4b6fe-125">Esses arquivos são usados para criar ativos em todo o conjunto de tutoriais.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-125">These files are used to create assets throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="4b6fe-126">Criar imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="4b6fe-126">Create container images</span></span>

<span data-ttu-id="4b6fe-127">O [Docker Compose](https://docs.docker.com/compose/) pode ser utilizado para automatizar a compilação de imagens de contêiner e a implantação de aplicativos de vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-127">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="4b6fe-128">Execute o arquivo docker-compose.yml para criar a imagem de contêiner, baixe a imagem Redis e inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-128">Run the docker-compose.yml file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="4b6fe-129">Quando completado, use o comando [docker images](https://docs.docker.com/engine/reference/commandline/images/) para ver as imagens criadas.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-129">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="4b6fe-130">Observe que três imagens foram baixadas ou criadas.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="4b6fe-131">A imagem *azure-vote-front* contém o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-131">The *azure-vote-front* image contains the application.</span></span> <span data-ttu-id="4b6fe-132">Foi derivado da imagem *nginx-flask*.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-132">It was derived from the *nginx-flask* image.</span></span> <span data-ttu-id="4b6fe-133">A imagem Redis foi baixada do Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-133">The Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="4b6fe-134">Execute o comando [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) para ver os contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-134">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="4b6fe-135">Saída:</span><span class="sxs-lookup"><span data-stu-id="4b6fe-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="4b6fe-136">Testar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="4b6fe-136">Test application locally</span></span>

<span data-ttu-id="4b6fe-137">Navegue até http://localhost:8080 para ver o aplicativo em execução.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-137">Browse to http://localhost:8080 to see the running application.</span></span>

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4b6fe-139">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="4b6fe-139">Clean up resources</span></span>

<span data-ttu-id="4b6fe-140">Agora que a funcionalidade do aplicativo foi validada, os contêineres em execução podem ser interrompidos e removidos.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-140">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="4b6fe-141">Não exclua as imagens de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-141">Do not delete the container images.</span></span> <span data-ttu-id="4b6fe-142">A imagem *azure-vote-front* serão carregada em uma instância do Registro de Contêiner do Azure no próximo tutorial.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-142">The *azure-vote-front* image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="4b6fe-143">Execute o seguinte para interromper os contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-143">Run the following to stop the running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="4b6fe-144">Exclua os contêineres com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-144">Delete the stopped containers with the following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="4b6fe-145">Ao concluir, você terá uma imagem de contêiner que contém o aplicativo Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-145">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b6fe-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b6fe-146">Next steps</span></span>

<span data-ttu-id="4b6fe-147">Neste tutorial, um aplicativo foi testado e imagens de contêiner foram criadas para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="4b6fe-148">As etapas a seguir foram concluídas:</span><span class="sxs-lookup"><span data-stu-id="4b6fe-148">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b6fe-149">Clonando a fonte do aplicativo do GitHub</span><span class="sxs-lookup"><span data-stu-id="4b6fe-149">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="4b6fe-150">Criando uma imagem de contêiner a partir da origem do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4b6fe-150">Created a container image from application source</span></span>
> * <span data-ttu-id="4b6fe-151">Testando o aplicativo em um ambiente Docker local</span><span class="sxs-lookup"><span data-stu-id="4b6fe-151">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="4b6fe-152">Avance para o próximo tutorial para saber mais sobre como armazenar imagens de contêiner em um Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b6fe-152">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b6fe-153">Enviar imagens por push ao Registro de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="4b6fe-153">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)