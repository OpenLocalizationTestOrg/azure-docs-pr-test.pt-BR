---
title: "Exemplo de script da CLI do Azure – ajustar a escala de um cluster do ACS | Microsoft Docs"
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
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="65fe7-104">Ajustar a escala de um cluster do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="65fe7-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="65fe7-105">Este exemplo ajusta a escala do Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="65fe7-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="65fe7-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="65fe7-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="65fe7-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="65fe7-107">Clean up deployment</span></span> 

<span data-ttu-id="65fe7-108">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="65fe7-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="65fe7-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="65fe7-109">Script explanation</span></span>

<span data-ttu-id="65fe7-110">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="65fe7-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="65fe7-111">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="65fe7-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="65fe7-112">Command</span><span class="sxs-lookup"><span data-stu-id="65fe7-112">Command</span></span> | <span data-ttu-id="65fe7-113">Observações</span><span class="sxs-lookup"><span data-stu-id="65fe7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="65fe7-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="65fe7-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="65fe7-115">Dimensionar um cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="65fe7-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="65fe7-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65fe7-116">Next steps</span></span>

<span data-ttu-id="65fe7-117">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65fe7-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="65fe7-118">Exemplos adicionais de script CLI do Serviço de Contêiner do Azure podem ser encontrados na [documentação do Serviço de Contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="65fe7-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

