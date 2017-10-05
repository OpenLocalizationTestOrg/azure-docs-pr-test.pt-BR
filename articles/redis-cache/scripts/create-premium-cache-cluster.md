---
title: "Amostra de Script de Azure CLI – Criar um Cache Redis Premium do Azure com o cluster | Microsoft Docs"
description: "Amostra de Script de Azure CLI – Criar um Cache Redis de camada Premium do Azure com o cluster"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="9a56c-103">Criar um Cache Redis Premium do Azure com cluster</span><span class="sxs-lookup"><span data-stu-id="9a56c-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="9a56c-104">Nesse cenário, você aprenderá como criar um Cache Redis Premium do Azure de camada de 6 GB com o cluster habilitado e dois fragmentos.</span><span class="sxs-lookup"><span data-stu-id="9a56c-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="9a56c-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9a56c-105">Sample script</span></span>

<span data-ttu-id="9a56c-106">[!code-azurecli[principal](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Cache Redis do Azure")]</span><span class="sxs-lookup"><span data-stu-id="9a56c-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9a56c-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="9a56c-107">Script explanation</span></span>

<span data-ttu-id="9a56c-108">Esse script usa os seguintes comandos para criar um grupo de recursos e um Cache Redis de camada Premium com cluster habilitado.</span><span class="sxs-lookup"><span data-stu-id="9a56c-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="9a56c-109">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="9a56c-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9a56c-110">Command</span><span class="sxs-lookup"><span data-stu-id="9a56c-110">Command</span></span> | <span data-ttu-id="9a56c-111">Observações</span><span class="sxs-lookup"><span data-stu-id="9a56c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9a56c-112">az group create</span><span class="sxs-lookup"><span data-stu-id="9a56c-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9a56c-113">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9a56c-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9a56c-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="9a56c-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="9a56c-115">Crie uma instância do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="9a56c-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9a56c-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a56c-116">Next steps</span></span>

<span data-ttu-id="9a56c-117">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a56c-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9a56c-118">Exemplos adicionais de scripts da CLI do Cache Redis do Azure podem ser encontrados na [Documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9a56c-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>