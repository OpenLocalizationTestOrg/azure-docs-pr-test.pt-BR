---
title: aaaPush Docker imagem tooprivate do registro do Azure | Microsoft Docs
description: "Enviar por push e pull Docker registro de contêiner privado tooa imagens no Azure usando Olá CLI do Docker"
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
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="1d6a3-103">Enviar por push o seu primeiro imagem tooa privada Docker registro de contêiner usando Olá CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="1d6a3-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="1d6a3-104">Um registro de contêiner do Azure armazena e gerencia privado [Docker](http://hub.docker.com) imagens de contêiner, semelhante toohello maneira [Docker Hub](https://hub.docker.com/) armazena imagens públicas do Docker.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="1d6a3-105">Use Olá [Interface de linha de comando do Docker](https://docs.docker.com/engine/reference/commandline/cli/) (CLI do Docker) para [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/)e outras operações em seu contêiner Registro.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="1d6a3-106">Para obter mais informações e conceitos, consulte [Olá visão geral](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1d6a3-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="1d6a3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d6a3-107">Prerequisites</span></span>
* <span data-ttu-id="1d6a3-108">**Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="1d6a3-109">Por exemplo, usar Olá [portal do Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1d6a3-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="1d6a3-110">**CLI do docker** -tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instalar [mecanismo do Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="1d6a3-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="1d6a3-111">Faça logon no registro tooa</span><span class="sxs-lookup"><span data-stu-id="1d6a3-111">Log in tooa registry</span></span>
<span data-ttu-id="1d6a3-112">Executar `docker login` toolog tooyour registro de contêiner com o [credenciais de registro](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1d6a3-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="1d6a3-113">Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="1d6a3-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="1d6a3-114">Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="1d6a3-115">Verifique o nome de registro totalmente qualificado de Olá de toospecify se (todas as minúsculas).</span><span class="sxs-lookup"><span data-stu-id="1d6a3-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="1d6a3-116">Neste exemplo, é `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="1d6a3-117">Etapas toopull e enviar por push uma imagem</span><span class="sxs-lookup"><span data-stu-id="1d6a3-117">Steps toopull and push an image</span></span>
<span data-ttu-id="1d6a3-118">Olá seguir exemplo downloads Olá imagem Nginx de registro de Hub do Docker público hello, marcas de registro do contêiner do Azure privado, push tooyour registro, em seguida, extrair novamente.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="1d6a3-119">**1. Pull imagem oficial do Docker Olá para Nginx**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="1d6a3-120">Primeiro pull Olá pública Nginx imagem tooyour computador local.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="1d6a3-121">**2. Inicie o contêiner de Nginx Olá**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="1d6a3-122">Olá comando a seguir inicia Olá local Nginx contêiner interativamente na porta 8080, permitindo que você saída toosee Nginx.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="1d6a3-123">Ele remove Olá executando contêiner uma vez interrompida.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="1d6a3-124">Procurar muito[http://localhost:8080](http://localhost:8080) tooview Olá executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="1d6a3-125">Você verá um toohello semelhante de tela a seguir um.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-125">You see a screen similar toohello following one.</span></span>

![Nginx no computador local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="1d6a3-127">toostop Olá contêiner em execução, pressione [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="1d6a3-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="1d6a3-128">**3. Criar um alias de imagem Olá no registro**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="1d6a3-129">Olá comando a seguir cria um alias de imagem hello, com um registro de tooyour caminho totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="1d6a3-130">Este exemplo especifica Olá `samples` namespace tooavoid desordem na raiz de saudação do registro hello.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="1d6a3-131">**4. Push Olá imagem tooyour registro**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="1d6a3-132">**5. Baixe a imagem de saudação do registro**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="1d6a3-133">**6. Inicie o contêiner de Nginx de saudação do registro**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="1d6a3-134">Procurar muito[http://localhost:8080](http://localhost:8080) tooview Olá executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="1d6a3-135">toostop Olá contêiner em execução, pressione [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="1d6a3-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="1d6a3-136">**7. (Opcional) Remover imagem Olá**</span><span class="sxs-lookup"><span data-stu-id="1d6a3-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="1d6a3-137">Limites simultâneos</span><span class="sxs-lookup"><span data-stu-id="1d6a3-137">Concurrent Limits</span></span>
<span data-ttu-id="1d6a3-138">Em alguns cenários, a execução simultânea de chamadas pode resultar em erros.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="1d6a3-139">Olá, a tabela a seguir contém os limites de saudação de chamadas simultâneas com operações de "Push" e "Pull" no registro de contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="1d6a3-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="1d6a3-140">Operação</span><span class="sxs-lookup"><span data-stu-id="1d6a3-140">Operation</span></span>  | <span data-ttu-id="1d6a3-141">Limite</span><span class="sxs-lookup"><span data-stu-id="1d6a3-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="1d6a3-142">PULL</span><span class="sxs-lookup"><span data-stu-id="1d6a3-142">PULL</span></span>       | <span data-ttu-id="1d6a3-143">Backup too10 simultâneos recebe por registro</span><span class="sxs-lookup"><span data-stu-id="1d6a3-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="1d6a3-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="1d6a3-144">PUSH</span></span>       | <span data-ttu-id="1d6a3-145">Backup too5 simultâneos envia por registro</span><span class="sxs-lookup"><span data-stu-id="1d6a3-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d6a3-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d6a3-146">Next steps</span></span>
<span data-ttu-id="1d6a3-147">Agora que você sabe os fundamentos de saudação, você está pronto toostart usando seu registro!</span><span class="sxs-lookup"><span data-stu-id="1d6a3-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="1d6a3-148">Por exemplo, iniciar a implantação de contêiner imagens tooan [serviço de contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="1d6a3-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
