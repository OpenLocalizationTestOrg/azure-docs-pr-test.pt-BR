---
title: Enviar a imagem do Docker por push para o registro privado do Azure | Microsoft Docs
description: "Envie e obtenha imagens do Docker para um registro de contêiner privado no Azure usando a CLI do Docker"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="84eea-103">Envie sua primeira imagem para um registro de contêiner privado do Docker usando a CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="84eea-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="84eea-104">Um registro de contêiner do Azure armazena e gerencia imagens de contêiner privadas do [Docker](http://hub.docker.com), de forma semelhante a como o [Docker Hub](https://hub.docker.com/) armazena imagens públicas do Docker.</span><span class="sxs-lookup"><span data-stu-id="84eea-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="84eea-105">Você usa a [Interface de Linha de Comando do Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) para [logon](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/) e outras operações no registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="84eea-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="84eea-106">Para obter mais informações e conceitos, consulte [visão geral](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="84eea-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="84eea-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="84eea-107">Prerequisites</span></span>
* <span data-ttu-id="84eea-108">**Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="84eea-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="84eea-109">Por exemplo, use o [Portal do Azure](container-registry-get-started-portal.md) ou a [CLI do Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="84eea-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="84eea-110">**CLI do Docker** - para configurar o computador local como um host Docker e acessar os comandos da CLI do Docker, instale o [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="84eea-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="84eea-111">Fazer logon em um registro</span><span class="sxs-lookup"><span data-stu-id="84eea-111">Log in to a registry</span></span>
<span data-ttu-id="84eea-112">Execute `docker login` para fazer logon em seu registro de contêiner as [credenciais de registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="84eea-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="84eea-113">O seguinte exemplo passa a ID e senha de uma [entidade de serviço](../active-directory/active-directory-application-objects.md) do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="84eea-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="84eea-114">Por exemplo, você pode atribuir uma entidade de serviço ao registro para um cenário de automação.</span><span class="sxs-lookup"><span data-stu-id="84eea-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="84eea-115">Especifique o nome totalmente qualificado do registro (todo em minúsculas).</span><span class="sxs-lookup"><span data-stu-id="84eea-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="84eea-116">Neste exemplo, é `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="84eea-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="84eea-117">Etapas para enviar e receber uma imagem</span><span class="sxs-lookup"><span data-stu-id="84eea-117">Steps to pull and push an image</span></span>
<span data-ttu-id="84eea-118">O exemplo a seguir baixa a imagem de Nginx do registro do Hub do Docker público, marca-a para o registro de contêiner do Azure privado, envia-a por push ao registro e a extrai novamente.</span><span class="sxs-lookup"><span data-stu-id="84eea-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="84eea-119">**1. Obtenha a imagem oficial do Docker para Nginx**</span><span class="sxs-lookup"><span data-stu-id="84eea-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="84eea-120">Primeiro, extraia a imagem Nginx pública para seu computador local.</span><span class="sxs-lookup"><span data-stu-id="84eea-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="84eea-121">**2. Iniciar o contêiner Nginx**</span><span class="sxs-lookup"><span data-stu-id="84eea-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="84eea-122">O comando a seguir inicia o contêiner Nginx local de forma interativa na porta 8080, permitindo que você veja a saída de Nginx.</span><span class="sxs-lookup"><span data-stu-id="84eea-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="84eea-123">Remove o contêiner em execução, uma vez interrompido.</span><span class="sxs-lookup"><span data-stu-id="84eea-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="84eea-124">Navegue até [http://localhost:8080/](http://localhost:8080) para exibir o contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="84eea-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="84eea-125">Você verá uma tela semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="84eea-125">You see a screen similar to the following one.</span></span>

![Nginx no computador local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="84eea-127">Para interromper o contêiner em execução, pressione [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="84eea-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="84eea-128">**3. Criar um alias da imagem no registro**</span><span class="sxs-lookup"><span data-stu-id="84eea-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="84eea-129">O comando a seguir cria um alias da imagem, com um caminho totalmente qualificado para o registro.</span><span class="sxs-lookup"><span data-stu-id="84eea-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="84eea-130">Este exemplo especifica o namespace `samples` para evitar confusão na raiz do registro.</span><span class="sxs-lookup"><span data-stu-id="84eea-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="84eea-131">**4. Envie a imagem para o registro**</span><span class="sxs-lookup"><span data-stu-id="84eea-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="84eea-132">**5. Obtenha a imagem do registro**</span><span class="sxs-lookup"><span data-stu-id="84eea-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="84eea-133">**6. Iniciar o contêiner Nginx no registro**</span><span class="sxs-lookup"><span data-stu-id="84eea-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="84eea-134">Navegue até [http://localhost:8080/](http://localhost:8080) para exibir o contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="84eea-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="84eea-135">Para interromper o contêiner em execução, pressione [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="84eea-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="84eea-136">**7. (Opcional) Remover a imagem**</span><span class="sxs-lookup"><span data-stu-id="84eea-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="84eea-137">Limites simultâneos</span><span class="sxs-lookup"><span data-stu-id="84eea-137">Concurrent Limits</span></span>
<span data-ttu-id="84eea-138">Em alguns cenários, a execução simultânea de chamadas pode resultar em erros.</span><span class="sxs-lookup"><span data-stu-id="84eea-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="84eea-139">A tabela abaixo contém os limites de chamadas simultâneas com operações "Push" e "Pull" no registro do contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="84eea-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="84eea-140">Operação</span><span class="sxs-lookup"><span data-stu-id="84eea-140">Operation</span></span>  | <span data-ttu-id="84eea-141">Limite</span><span class="sxs-lookup"><span data-stu-id="84eea-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="84eea-142">PULL</span><span class="sxs-lookup"><span data-stu-id="84eea-142">PULL</span></span>       | <span data-ttu-id="84eea-143">Até 10 pulls simultâneos por registro</span><span class="sxs-lookup"><span data-stu-id="84eea-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="84eea-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="84eea-144">PUSH</span></span>       | <span data-ttu-id="84eea-145">Até 5 pushes simultâneos por registro</span><span class="sxs-lookup"><span data-stu-id="84eea-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84eea-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84eea-146">Next steps</span></span>
<span data-ttu-id="84eea-147">Agora que conhece os fundamentos, você está pronto para começar a usar o registro!</span><span class="sxs-lookup"><span data-stu-id="84eea-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="84eea-148">Por exemplo, inicie a implantação de imagens de contêiner para um cluster de [Serviço de Contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="84eea-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
