---
title: "Exemplo de script da CLI do Azure – Obter detalhes de um Cache Redis do Azure | Documentos o Microsoft"
description: "Exemplo de script da CLI do Azure – Obter detalhes de um Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="df87c-103">Obter detalhes de um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="df87c-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="df87c-104">Nesse cenário, você aprende como recuperar os detalhes de uma instância de Cache Redis do Azure, incluindo seu status de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="df87c-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="df87c-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="df87c-105">Sample script</span></span>

<span data-ttu-id="df87c-106">[!code-azurecli[principal](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Cache Redis do Azure")]</span><span class="sxs-lookup"><span data-stu-id="df87c-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="df87c-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="df87c-107">Script explanation</span></span>

<span data-ttu-id="df87c-108">Esse script usa os seguintes comandos para recuperar detalhes de uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="df87c-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="df87c-109">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="df87c-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="df87c-110">Command</span><span class="sxs-lookup"><span data-stu-id="df87c-110">Command</span></span> | <span data-ttu-id="df87c-111">Observações</span><span class="sxs-lookup"><span data-stu-id="df87c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df87c-112">apresentação de redis az</span><span class="sxs-lookup"><span data-stu-id="df87c-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="df87c-113">Recupere os detalhes de uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="df87c-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="df87c-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df87c-114">Next steps</span></span>

<span data-ttu-id="df87c-115">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df87c-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="df87c-116">Exemplos adicionais de scripts da CLI do Cache Redis do Azure podem ser encontrados na [Documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df87c-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>