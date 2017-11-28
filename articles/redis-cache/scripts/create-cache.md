---
title: aaaAzure exemplo de Script CLI - criar um Cache Redis do Azure | Microsoft Docs
description: "Exemplo de Script da CLI do Azure – Criar um Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="05ce7-103">Criar um Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="05ce7-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="05ce7-104">Nesse cenário, você aprenderá como toocreate um Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="05ce7-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="05ce7-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="05ce7-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="05ce7-106">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="05ce7-106">Script explanation</span></span>

<span data-ttu-id="05ce7-107">Esse script usa Olá toocreate comandos a seguir, um grupo de recursos e um cache redis.</span><span class="sxs-lookup"><span data-stu-id="05ce7-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="05ce7-108">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="05ce7-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="05ce7-109">Command</span><span class="sxs-lookup"><span data-stu-id="05ce7-109">Command</span></span> | <span data-ttu-id="05ce7-110">Observações</span><span class="sxs-lookup"><span data-stu-id="05ce7-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="05ce7-111">az group create</span><span class="sxs-lookup"><span data-stu-id="05ce7-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="05ce7-112">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="05ce7-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="05ce7-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="05ce7-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="05ce7-114">Crie uma instância do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="05ce7-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="05ce7-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05ce7-115">Next steps</span></span>

<span data-ttu-id="05ce7-116">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="05ce7-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="05ce7-117">Exemplos de script CLI do Azure Redis Cache adicionais podem ser encontrados no hello [documentação do Cache Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="05ce7-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
