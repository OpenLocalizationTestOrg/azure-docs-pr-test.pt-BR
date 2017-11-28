---
title: "banco de dados do SQL Azure aaaCLI exemplo-monitor escala único | Microsoft Docs"
description: "Toomonitor de script de exemplo CLI do Azure e a escala de um único banco de dados do SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="b3382-103">Use toomonitor CLI e dimensionar um único banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="b3382-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="b3382-104">Este exemplo de script CLI do Azure é dimensionado um único nível de desempenho diferentes de tooa de banco de dados SQL do Azure depois de consultar informações sobre o tamanho do banco de dados de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="b3382-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b3382-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b3382-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b3382-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3382-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b3382-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b3382-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b3382-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3382-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b3382-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b3382-109">Clean up deployment</span></span>

<span data-ttu-id="b3382-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="b3382-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b3382-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b3382-111">Script explanation</span></span>

<span data-ttu-id="b3382-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3382-112">This script uses hello following commands.</span></span> <span data-ttu-id="b3382-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="b3382-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b3382-114">Command</span><span class="sxs-lookup"><span data-stu-id="b3382-114">Command</span></span> | <span data-ttu-id="b3382-115">Observações</span><span class="sxs-lookup"><span data-stu-id="b3382-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3382-116">az group create</span><span class="sxs-lookup"><span data-stu-id="b3382-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b3382-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b3382-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3382-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="b3382-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="b3382-119">Cria um servidor lógico que hospeda um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b3382-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="b3382-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="b3382-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="b3382-121">Mostra informações de uso de tamanho de saudação para um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b3382-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="b3382-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="b3382-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="b3382-123">Atualiza as propriedades do banco de dados (como Olá camadas ou desempenho do nível de serviço) ou move um banco de dados em, em ou entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="b3382-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b3382-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="b3382-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b3382-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="b3382-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b3382-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3382-126">Next steps</span></span>

<span data-ttu-id="b3382-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3382-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b3382-128">Exemplos de script CLI do banco de dados SQL adicionais podem ser encontrados no hello [documentação de banco de dados do Azure SQL](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3382-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
