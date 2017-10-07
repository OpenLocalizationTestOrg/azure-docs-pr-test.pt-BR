---
title: aaaAzure exemplo de Script CLI - Get hello nome de host, portas e chaves para Cache Redis do Azure | Microsoft Docs
description: "Exemplo de Script CLI do Azure - Get hello nome do host, portas e chaves para uma instância de Cache Redis do Azure"
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
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="2346b-103">Obter Olá nome de host, portas e chaves de Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="2346b-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="2346b-104">Nesse cenário, você aprenderá como chaves, portas e tooretrieve Olá hostname usado instância de Cache Redis do Azure tooan tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2346b-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="2346b-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2346b-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="2346b-106">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2346b-106">Script explanation</span></span>

<span data-ttu-id="2346b-107">Esse script usa Olá comandos tooretrieve Olá hostname, chaves e portas de uma instância de Cache Redis do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="2346b-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="2346b-108">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="2346b-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2346b-109">Command</span><span class="sxs-lookup"><span data-stu-id="2346b-109">Command</span></span> | <span data-ttu-id="2346b-110">Observações</span><span class="sxs-lookup"><span data-stu-id="2346b-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2346b-111">apresentação de redis az</span><span class="sxs-lookup"><span data-stu-id="2346b-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="2346b-112">Recupere os detalhes de uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="2346b-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="2346b-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="2346b-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="2346b-114">Recupere chaves de acesso para uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="2346b-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="2346b-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2346b-115">Next steps</span></span>

<span data-ttu-id="2346b-116">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2346b-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2346b-117">Exemplos de script CLI do Azure Redis Cache adicionais podem ser encontrados no hello [documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2346b-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
