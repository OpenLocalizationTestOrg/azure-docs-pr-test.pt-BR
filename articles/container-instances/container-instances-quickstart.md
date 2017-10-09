---
title: "aaaCreate o primeiro contêiner de instâncias de contêiner do Azure | Documentos do Azure"
description: "Implantar e começar a trabalhar com as Instâncias de Contêiner do Azure"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="ba647-103">Criar o primeiro contêiner nas Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ba647-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="ba647-104">Instâncias de contêiner do Azure torna fácil toocreate e gerenciar contêineres no Azure.</span><span class="sxs-lookup"><span data-stu-id="ba647-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="ba647-105">Esse início rápido, você criar um contêiner no Azure e expô-lo toohello internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ba647-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="ba647-106">Essa operação é concluída com um único comando.</span><span class="sxs-lookup"><span data-stu-id="ba647-106">This operation is completed in a single command.</span></span> <span data-ttu-id="ba647-107">Em poucos segundos, você verá o seguinte em seu navegador:</span><span class="sxs-lookup"><span data-stu-id="ba647-107">Within just a few seconds, you will see this in your browser:</span></span>

![Os aplicativos implantados usando Instâncias de Contêiner do Azure são exibidos no navegador][aci-app-browser]

<span data-ttu-id="ba647-109">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ba647-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ba647-110">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.12 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ba647-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="ba647-111">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba647-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ba647-112">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ba647-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="ba647-113">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ba647-113">Create a resource group</span></span>

<span data-ttu-id="ba647-114">As Instâncias de Contêiner do Azure são recursos do Azure e devem ser colocadas em um grupo de recursos do Azure, um conjunto lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ba647-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="ba647-115">Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="ba647-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="ba647-116">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="ba647-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="ba647-117">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="ba647-117">Create a container</span></span>

<span data-ttu-id="ba647-118">Você pode criar um contêiner fornecendo um nome, uma imagem do Docker e um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba647-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="ba647-119">Opcionalmente, você pode expor Olá contêiner toohello internet com um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ba647-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="ba647-120">Nesse caso, vamos usar um contêiner que hospeda um aplicativo Web muito simples escrito em [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ba647-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="ba647-121">Em alguns segundos, você deve obter uma solicitação de tooyour de resposta.</span><span class="sxs-lookup"><span data-stu-id="ba647-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="ba647-122">Inicialmente, o contêiner Olá estará em um **criando** estado, mas ele deve começar em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="ba647-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="ba647-123">Você pode verificar o status de saudação usando Olá `show` comando:</span><span class="sxs-lookup"><span data-stu-id="ba647-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="ba647-124">Na parte inferior de saudação da saída de hello, você verá o estado de provisionamento do contêiner hello e seu endereço IP:</span><span class="sxs-lookup"><span data-stu-id="ba647-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="ba647-125">Depois que o contêiner de saudação move toohello **êxito** estado, você puder alcançá-lo no navegador hello usando o endereço IP hello fornecido.</span><span class="sxs-lookup"><span data-stu-id="ba647-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Os aplicativos implantados usando Instâncias de Contêiner do Azure são exibidos no navegador][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="ba647-127">Pull Olá contêiner logs</span><span class="sxs-lookup"><span data-stu-id="ba647-127">Pull hello container logs</span></span>

<span data-ttu-id="ba647-128">Você pode extrair os logs de saudação do contêiner de saudação criadas usando Olá `logs` comando:</span><span class="sxs-lookup"><span data-stu-id="ba647-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="ba647-129">Saída:</span><span class="sxs-lookup"><span data-stu-id="ba647-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="ba647-130">Excluir contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="ba647-130">Delete hello container</span></span>

<span data-ttu-id="ba647-131">Quando tiver terminado com contêiner hello, você poderá removê-lo usando Olá `delete` comando:</span><span class="sxs-lookup"><span data-stu-id="ba647-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ba647-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba647-132">Next steps</span></span>

<span data-ttu-id="ba647-133">Todos os de saudação de código para o contêiner de saudação usado nesse início rápido está disponível [no GitHub][app-github-repo], juntamente com seu Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="ba647-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="ba647-134">Se você desejar tootry compilá-lo e implantá-la tooAzure instâncias de contêiner usando Olá registro de contêiner do Azure, continue toohello tutorial de instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba647-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba647-135">Tutoriais sobre Instâncias de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="ba647-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png