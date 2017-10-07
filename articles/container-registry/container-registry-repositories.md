---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="67cf2-103">Repositórios de Registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="67cf2-103">Azure container registry repositories</span></span>

<span data-ttu-id="67cf2-104">Registro de contêiner do Azure permite que você toostore imagens de contêiner em repositórios.</span><span class="sxs-lookup"><span data-stu-id="67cf2-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="67cf2-105">Armazenando imagens em repositórios, você poderá ter grupos de imagens (ou versão de imagens) em ambientes isolados.</span><span class="sxs-lookup"><span data-stu-id="67cf2-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="67cf2-106">Você pode especificar esses repositórios quando você enviar por push do registro tooyour de imagens.</span><span class="sxs-lookup"><span data-stu-id="67cf2-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="67cf2-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67cf2-107">Prerequisites</span></span>
* <span data-ttu-id="67cf2-108">**Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="67cf2-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="67cf2-109">Por exemplo, usar Olá [portal do Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67cf2-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="67cf2-110">**CLI do docker** -tooset do computador local como um host e acesso Olá CLI do Docker comandos do Docker, instalar [mecanismo do Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="67cf2-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="67cf2-111">**Baixe uma imagem** - efetuar o Pull de uma imagem de registro de Hub do Docker público Olá rotulá-lo e por push tooyour registro.</span><span class="sxs-lookup"><span data-stu-id="67cf2-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="67cf2-112">Para obter orientação sobre como enviar por push e pull imagens, consulte [registro particular do Docker Push imagem tooAzure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67cf2-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="67cf2-113">Exibir os repositórios em Olá Portal</span><span class="sxs-lookup"><span data-stu-id="67cf2-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="67cf2-114">Depois de ter enviado do registro de contêiner de tooyour de imagens, você pode ver uma lista de repositórios de saudação hospedagem imagens Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67cf2-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="67cf2-115">Se você seguiu as etapas de Olá Olá [registro particular do Docker Push imagem tooAzure](container-registry-get-started-docker-cli.md) artigo, agora você deve ter uma imagem Nginx no registro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="67cf2-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="67cf2-116">Como parte das instruções Olá, você deve ter especificado um namespace para a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="67cf2-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="67cf2-117">O exemplo hello abaixo, o comando de saudação envia repositório de "exemplos" hello NGinx imagens toohello:</span><span class="sxs-lookup"><span data-stu-id="67cf2-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="67cf2-118">O Registro de Contêiner do Azure dá suporte a namespaces do repositório de vários níveis.</span><span class="sxs-lookup"><span data-stu-id="67cf2-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="67cf2-119">Esse recurso permite que você toogroup coleções de aplicativo específico de tooa relacionados de imagens, ou uma coleção de desenvolvimento de toospecific aplicativos ou equipes operacionais.</span><span class="sxs-lookup"><span data-stu-id="67cf2-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="67cf2-120">tooread mais sobre repositórios nos registros de contêiner, consulte [registros de contêiner do Docker privada no Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="67cf2-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="67cf2-121">repositórios de registro de contêiner de saudação tooview:</span><span class="sxs-lookup"><span data-stu-id="67cf2-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="67cf2-122">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67cf2-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="67cf2-123">Em Olá **registro de contêiner do Azure** folha, registro de saudação selecione desejar tooinspect</span><span class="sxs-lookup"><span data-stu-id="67cf2-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="67cf2-124">Na folha de registro de saudação, clique em **repositórios** toosee uma lista de todos os repositórios de saudação e suas imagens</span><span class="sxs-lookup"><span data-stu-id="67cf2-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="67cf2-125">(Opcional) Selecione marcas toosee a imagem específica</span><span class="sxs-lookup"><span data-stu-id="67cf2-125">(Optional) Select a specific image toosee tags</span></span>

![Repositórios no portal de saudação](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="67cf2-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67cf2-127">Next steps</span></span>
<span data-ttu-id="67cf2-128">Agora que você sabe os fundamentos de saudação, você está pronto toostart usando seu registro!</span><span class="sxs-lookup"><span data-stu-id="67cf2-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="67cf2-129">Por exemplo, iniciar a implantação de contêiner imagens tooan [serviço de contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="67cf2-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
