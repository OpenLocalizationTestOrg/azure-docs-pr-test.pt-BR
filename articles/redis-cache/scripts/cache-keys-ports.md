---
title: "Exemplo de script de CLI do Azure – Obtenha o nome de host, portas e chaves de Cache Redis do Azure | Microsoft Docs"
description: "Exemplo de script de CLI do Azure – Obtenha o nome de host, portas e chaves da instância Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: cd9adc784bceb0fff5e7c2bbee2be0950c51c8f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="ec52a-103">Obtenha o nome de host, portas e chaves de Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="ec52a-103">Get the hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="ec52a-104">Neste cenário, você aprende como recuperar nome de host, portas e as chaves usadas para conexão com uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec52a-104">In this scenario, you learn how to retrieve the hostname, ports, and keys used to connect to an Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ec52a-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ec52a-105">Sample script</span></span>

<span data-ttu-id="ec52a-106">[!code-azurecli[principal](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Cache Redis do Azure")]</span><span class="sxs-lookup"><span data-stu-id="ec52a-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="ec52a-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ec52a-107">Script explanation</span></span>

<span data-ttu-id="ec52a-108">Esse script usa os seguintes comandos para recuperar nome de host, chaves e portas de uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec52a-108">This script uses the following commands to retrieve the hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="ec52a-109">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="ec52a-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ec52a-110">Command</span><span class="sxs-lookup"><span data-stu-id="ec52a-110">Command</span></span> | <span data-ttu-id="ec52a-111">Observações</span><span class="sxs-lookup"><span data-stu-id="ec52a-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ec52a-112">apresentação de redis az</span><span class="sxs-lookup"><span data-stu-id="ec52a-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="ec52a-113">Recupere os detalhes de uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec52a-113">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="ec52a-114">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="ec52a-114">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="ec52a-115">Recupere chaves de acesso para uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec52a-115">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ec52a-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec52a-116">Next steps</span></span>

<span data-ttu-id="ec52a-117">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec52a-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ec52a-118">Exemplos adicionais de scripts da CLI do Cache Redis do Azure podem ser encontrados na [Documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ec52a-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>