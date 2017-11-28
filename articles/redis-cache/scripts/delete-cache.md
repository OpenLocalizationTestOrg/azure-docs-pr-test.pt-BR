---
title: "Exemplo de Script da CLI do Azure – Excluir um Cache Redis do Azure | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure – excluir um Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="b447c-103">Excluir um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="b447c-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="b447c-104">Nesse cenário, você aprenderá como excluir um Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b447c-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b447c-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b447c-105">Sample script</span></span>

<span data-ttu-id="b447c-106">[!code-azurecli[principal](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Cache Redis do Azure")]</span><span class="sxs-lookup"><span data-stu-id="b447c-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b447c-107">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b447c-107">Script explanation</span></span>

<span data-ttu-id="b447c-108">Esse script usa os comandos a seguir para excluir uma instância de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b447c-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="b447c-109">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="b447c-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b447c-110">Command</span><span class="sxs-lookup"><span data-stu-id="b447c-110">Command</span></span> | <span data-ttu-id="b447c-111">Observações</span><span class="sxs-lookup"><span data-stu-id="b447c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b447c-112">exclusão de redis az</span><span class="sxs-lookup"><span data-stu-id="b447c-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="b447c-113">Excluir uma instância do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="b447c-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b447c-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b447c-114">Next steps</span></span>

<span data-ttu-id="b447c-115">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b447c-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b447c-116">Exemplos adicionais de scripts da CLI do Cache Redis do Azure podem ser encontrados na [Documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b447c-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>