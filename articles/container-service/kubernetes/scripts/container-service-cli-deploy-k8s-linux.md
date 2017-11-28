---
title: aaaAzure exemplo de Script CLI - criar o ACS Linux Kubernetes Cluster | Microsoft Docs
description: "Exemplo de script da CLI do Azure – criar o Cluster Linux Kubernetes do ACS"
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
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: cf3798ea8b08e3fc32acb35dabab4b2fbea179dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="24055-104">Criar um Cluster do Linux do Kubernetes do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="24055-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="24055-105">Este exemplo cria um cluster do Serviço de Contêiner do Azure executando Kubernetes para contêineres baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="24055-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="24055-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="24055-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="24055-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="24055-107">Clean up deployment</span></span> 

<span data-ttu-id="24055-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="24055-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="24055-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="24055-109">Script explanation</span></span>

<span data-ttu-id="24055-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="24055-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="24055-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="24055-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="24055-112">Command</span><span class="sxs-lookup"><span data-stu-id="24055-112">Command</span></span> | <span data-ttu-id="24055-113">Observações</span><span class="sxs-lookup"><span data-stu-id="24055-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24055-114">az group create</span><span class="sxs-lookup"><span data-stu-id="24055-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="24055-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="24055-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24055-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="24055-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="24055-117">Cria e cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="24055-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="24055-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24055-118">Next steps</span></span>

<span data-ttu-id="24055-119">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24055-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="24055-120">Exemplos de script CLI de serviço de contêiner do Azure adicionais podem ser encontrados no hello [documentação do serviço de contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="24055-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

