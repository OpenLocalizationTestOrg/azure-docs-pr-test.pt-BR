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
ms.openlocfilehash: ff90aee308a993ae0d36288191d1496affacce2a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="45a5f-104">Criar um cluster de DC/SO do Serviço de Contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="45a5f-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="45a5f-105">Este exemplo cria um cluster do Serviço de Contêiner do Azure executando DC/SO.</span><span class="sxs-lookup"><span data-stu-id="45a5f-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="45a5f-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="45a5f-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="45a5f-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="45a5f-107">Clean up deployment</span></span> 

<span data-ttu-id="45a5f-108">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="45a5f-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="45a5f-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="45a5f-109">Script explanation</span></span>

<span data-ttu-id="45a5f-110">Esse script usa os seguintes comandos para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="45a5f-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="45a5f-111">Cada item em que a tabela contém links para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="45a5f-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="45a5f-112">Command</span><span class="sxs-lookup"><span data-stu-id="45a5f-112">Command</span></span> | <span data-ttu-id="45a5f-113">Observações</span><span class="sxs-lookup"><span data-stu-id="45a5f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45a5f-114">az group create</span><span class="sxs-lookup"><span data-stu-id="45a5f-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="45a5f-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="45a5f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="45a5f-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="45a5f-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="45a5f-117">Cria e cluster do ACS.</span><span class="sxs-lookup"><span data-stu-id="45a5f-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="45a5f-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45a5f-118">Next steps</span></span>

<span data-ttu-id="45a5f-119">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45a5f-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="45a5f-120">Exemplos adicionais de script CLI do Serviço de Contêiner do Azure podem ser encontrados na [documentação do Serviço de Contêiner do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="45a5f-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>