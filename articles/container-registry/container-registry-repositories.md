---
title: "Repositórios de Registro de contêiner do Azure | Microsoft Docs"
description: "Como usar os repositórios de Registro de contêiner do Azure para imagens do Docker"
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
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="8ed52-103">Repositórios de Registro de contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed52-103">Azure container registry repositories</span></span>

<span data-ttu-id="8ed52-104">O Registro de contêiner do Azure permite armazenar imagens de contêiner em repositórios.</span><span class="sxs-lookup"><span data-stu-id="8ed52-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="8ed52-105">Armazenando imagens em repositórios, você poderá ter grupos de imagens (ou versão de imagens) em ambientes isolados.</span><span class="sxs-lookup"><span data-stu-id="8ed52-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="8ed52-106">Você pode especificar esses repositórios quando você envia imagens por push para o Registro.</span><span class="sxs-lookup"><span data-stu-id="8ed52-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8ed52-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ed52-107">Prerequisites</span></span>
* <span data-ttu-id="8ed52-108">**Registro de Contêiner do Azure** - crie um registro de contêiner em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed52-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="8ed52-109">Por exemplo, use o [Portal do Azure](container-registry-get-started-portal.md) ou a [CLI do Azure 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ed52-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="8ed52-110">**CLI do Docker** - para configurar o computador local como um host Docker e acessar os comandos da CLI do Docker, instale o [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="8ed52-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="8ed52-111">**Efetuar pull de uma imagem** – efetuar pull de uma imagem do Registro do Hub do Docker público, marcá-lo e enviá-lo por push ao seu Registro.</span><span class="sxs-lookup"><span data-stu-id="8ed52-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="8ed52-112">Para diretrizes sobre como enviar imagens por push e efetuar pull dessas imagens, consulte [Enviar imagem do Docker por push para Registro privado do Azure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ed52-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="8ed52-113">Exibindo repositórios no Portal</span><span class="sxs-lookup"><span data-stu-id="8ed52-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="8ed52-114">Depois que você tiver enviado imagens por push para o Registro de contêiner, você poderá ver uma lista dos repositórios hospedando as imagens no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed52-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="8ed52-115">Se você seguiu as etapas do artigo [Enviar imagem do Docker por push para Registro privado do Azure](container-registry-get-started-docker-cli.md), agora você deve ter uma imagem de Nginx no Registro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ed52-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="8ed52-116">Como parte das instruções, você deve ter especificado um namespace para a imagem.</span><span class="sxs-lookup"><span data-stu-id="8ed52-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="8ed52-117">No exemplo abaixo, o comando envia a imagem NGinx para o repositório "samples":</span><span class="sxs-lookup"><span data-stu-id="8ed52-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="8ed52-118">O Registro de Contêiner do Azure dá suporte a namespaces do repositório de vários níveis.</span><span class="sxs-lookup"><span data-stu-id="8ed52-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="8ed52-119">Esse recurso permite que você agrupe coleções de imagens relacionadas a um aplicativo específico ou uma coleção de aplicativos para equipes de desenvolvimento ou operacionais específicas.</span><span class="sxs-lookup"><span data-stu-id="8ed52-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="8ed52-120">Para saber mais sobre repositórios em registros de contêiner, consulte [Registros de contêiner do Docker privado no Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8ed52-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="8ed52-121">Para exibir os repositórios de Registro de contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ed52-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="8ed52-122">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8ed52-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="8ed52-123">Na folha **Registro de Contêiner do Azure**, selecione o Registro que deseja inspecionar</span><span class="sxs-lookup"><span data-stu-id="8ed52-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="8ed52-124">Na folha do Registro, clique em **Repositórios** para ver uma lista de todos os repositórios e suas imagens</span><span class="sxs-lookup"><span data-stu-id="8ed52-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="8ed52-125">(Opcional) Selecione uma imagem específica para ver as marcas</span><span class="sxs-lookup"><span data-stu-id="8ed52-125">(Optional) Select a specific image to see tags</span></span>

![Repositórios no portal](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="8ed52-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ed52-127">Next steps</span></span>
<span data-ttu-id="8ed52-128">Agora que conhece os fundamentos, você está pronto para começar a usar o registro!</span><span class="sxs-lookup"><span data-stu-id="8ed52-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="8ed52-129">Por exemplo, inicie a implantação de imagens de contêiner para um cluster de [Serviço de Contêiner do Azure](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="8ed52-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
