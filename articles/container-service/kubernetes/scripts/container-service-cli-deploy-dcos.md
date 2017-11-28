---
title: aaaAzure exemplo de Script CLI - criar Cluster do ACS DC/sistema operacional | Microsoft Docs
description: "Exemplo de script da CLI do Azure – criar o Cluster DC/SO do ACS"
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
ms.openlocfilehash: cbc990e5e650487d6aa4572c7ff5e1c3fa150906
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="e7cd4-104">Criar um cluster de DC/SO do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="e7cd4-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="e7cd4-105">Este exemplo cria um cluster do Serviço de Contêiner do Azure executando DC/SO.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e7cd4-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e7cd4-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="e7cd4-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e7cd4-107">Clean up deployment</span></span> 

<span data-ttu-id="e7cd4-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e7cd4-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e7cd4-109">Script explanation</span></span>

<span data-ttu-id="e7cd4-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e7cd4-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e7cd4-112">Command</span><span class="sxs-lookup"><span data-stu-id="e7cd4-112">Command</span></span> | <span data-ttu-id="e7cd4-113">Observações</span><span class="sxs-lookup"><span data-stu-id="e7cd4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e7cd4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e7cd4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e7cd4-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e7cd4-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="e7cd4-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="e7cd4-117">Cria e cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="e7cd4-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e7cd4-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7cd4-118">Next steps</span></span>

<span data-ttu-id="e7cd4-119">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e7cd4-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e7cd4-120">Exemplos de script CLI de serviço de contêiner do Azure adicionais podem ser encontrados no hello [documentação do serviço de contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e7cd4-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
