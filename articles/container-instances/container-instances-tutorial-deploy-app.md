---
title: "tutorial de instâncias de contêiner aaaAzure - implantar aplicativo | Microsoft Docs"
description: "Tutorial de Instâncias de Contêiner do Azure – implantar aplicativo"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="47efb-103">Implantar um contêiner tooAzure instâncias de contêiner</span><span class="sxs-lookup"><span data-stu-id="47efb-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="47efb-104">Isso é hello última de um tutorial de três partes.</span><span class="sxs-lookup"><span data-stu-id="47efb-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="47efb-105">Nas seções anteriores, [uma imagem de contêiner foi criada](container-instances-tutorial-prepare-app.md) e [enviada por push tooan registro de contêiner do Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="47efb-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="47efb-106">Esta seção conclui o tutorial Olá Implantando Olá contêiner tooAzure instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="47efb-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="47efb-107">As etapas concluídas incluem:</span><span class="sxs-lookup"><span data-stu-id="47efb-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47efb-108">Definição de um grupo de contêiner usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="47efb-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="47efb-109">Implantar grupo de contêiner hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="47efb-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="47efb-110">Exibição de logs de contêiner</span><span class="sxs-lookup"><span data-stu-id="47efb-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="47efb-111">Implantar o contêiner de saudação usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="47efb-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="47efb-112">Olá CLI do Azure permite a implantação de um contêiner de tooAzure instâncias de contêiner em um único comando.</span><span class="sxs-lookup"><span data-stu-id="47efb-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="47efb-113">Desde que a imagem de contêiner hello está hospedada no hello privada registro de contêiner do Azure, você deve incluir Olá credenciais necessário tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="47efb-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="47efb-114">Se necessário, você pode consultá-las conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="47efb-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="47efb-115">Servidor de logon do registro de contêiner (atualize com seu nome de registro):</span><span class="sxs-lookup"><span data-stu-id="47efb-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="47efb-116">Senha de registro de contêiner:</span><span class="sxs-lookup"><span data-stu-id="47efb-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="47efb-117">toodeploy sua imagem de contêiner do registro de contêiner de saudação com um recurso de solicitação de 1 núcleo de CPU e 1GB de memória, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="47efb-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="47efb-118">Em alguns segundos, você receberá uma resposta inicial do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47efb-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="47efb-119">estado de saudação tooview de implantação hello, use:</span><span class="sxs-lookup"><span data-stu-id="47efb-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="47efb-120">Podemos continuar a execução desse comando até que o estado de saudação muda de *pendente* muito*executando*.</span><span class="sxs-lookup"><span data-stu-id="47efb-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="47efb-121">Então, poderemos continuar.</span><span class="sxs-lookup"><span data-stu-id="47efb-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="47efb-122">Exibir logs de aplicativo e o contêiner de saudação</span><span class="sxs-lookup"><span data-stu-id="47efb-122">View hello application and container logs</span></span>

<span data-ttu-id="47efb-123">Depois que a implantação de saudação for bem-sucedida, abra seu endereço IP do navegador toohello mostrado na saída Olá Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="47efb-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Olá mundo aplicativo no navegador Olá][aci-app-browser]

<span data-ttu-id="47efb-125">Você também pode exibir a saída do log de saudação do contêiner de saudação:</span><span class="sxs-lookup"><span data-stu-id="47efb-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="47efb-126">Saída:</span><span class="sxs-lookup"><span data-stu-id="47efb-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="47efb-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47efb-127">Next steps</span></span>

<span data-ttu-id="47efb-128">Neste tutorial, você concluiu o processo de saudação de implantação de seu tooAzure contêineres instâncias de contêiner.</span><span class="sxs-lookup"><span data-stu-id="47efb-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="47efb-129">Olá, as etapas a seguir foram concluída:</span><span class="sxs-lookup"><span data-stu-id="47efb-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47efb-130">Implantando o contêiner de saudação do registro de contêiner do Azure usando o Olá Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="47efb-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="47efb-131">Exibindo o aplicativo hello no navegador Olá</span><span class="sxs-lookup"><span data-stu-id="47efb-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="47efb-132">Exibindo registros de contêiner de saudação</span><span class="sxs-lookup"><span data-stu-id="47efb-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
