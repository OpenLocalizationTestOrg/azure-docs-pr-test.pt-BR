---
title: aaaAzure exemplo de Script CLI - dimensionar um Cluster ACS | Microsoft Docs
description: "Exemplo de script CLI do Azure – ajustar a escala de um cluster do ACS"
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
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="84a28-104">Ajustar a escala de um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="84a28-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="84a28-105">Este exemplo ajusta a escala do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="84a28-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="84a28-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="84a28-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="84a28-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="84a28-107">Clean up deployment</span></span> 

<span data-ttu-id="84a28-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="84a28-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="84a28-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="84a28-109">Script explanation</span></span>

<span data-ttu-id="84a28-110">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="84a28-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="84a28-111">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="84a28-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84a28-112">Command</span><span class="sxs-lookup"><span data-stu-id="84a28-112">Command</span></span> | <span data-ttu-id="84a28-113">Observações</span><span class="sxs-lookup"><span data-stu-id="84a28-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84a28-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="84a28-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="84a28-115">Dimensionar um cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="84a28-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84a28-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84a28-116">Next steps</span></span>

<span data-ttu-id="84a28-117">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84a28-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="84a28-118">Exemplos de script CLI de serviço de contêiner do Azure adicionais podem ser encontrados no hello [documentação do serviço de contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="84a28-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

