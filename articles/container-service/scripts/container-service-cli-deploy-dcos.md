---
title: "Exemplo de script da CLI do Azure – criar o Cluster DC/SO do ACS | Microsoft Docs"
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
ms.openlocfilehash: 4efd7dea04fd3486f875e57737e438c966872dd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="09bdb-104">Criar um cluster de DC/SO do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="09bdb-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="09bdb-105">Este exemplo cria um cluster do Serviço de Contêiner do Azure executando DC/SO.</span><span class="sxs-lookup"><span data-stu-id="09bdb-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="09bdb-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="09bdb-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="09bdb-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="09bdb-107">Clean up deployment</span></span> 

<span data-ttu-id="09bdb-108">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="09bdb-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="09bdb-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="09bdb-109">Script explanation</span></span>

<span data-ttu-id="09bdb-110">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="09bdb-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="09bdb-111">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="09bdb-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="09bdb-112">Command</span><span class="sxs-lookup"><span data-stu-id="09bdb-112">Command</span></span> | <span data-ttu-id="09bdb-113">Observações</span><span class="sxs-lookup"><span data-stu-id="09bdb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="09bdb-114">az group create</span><span class="sxs-lookup"><span data-stu-id="09bdb-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="09bdb-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="09bdb-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="09bdb-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="09bdb-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="09bdb-117">Cria e cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="09bdb-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09bdb-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09bdb-118">Next steps</span></span>

<span data-ttu-id="09bdb-119">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09bdb-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="09bdb-120">Exemplos adicionais de script CLI do Serviço de Contêiner do Azure podem ser encontrados na [documentação do Serviço de Contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="09bdb-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>