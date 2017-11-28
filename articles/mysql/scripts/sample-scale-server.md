---
title: exemplos de aaaAzure CLI tooscale um banco de dados do Azure para o MySQL server | Microsoft Docs
description: "Esse exemplo de script CLI dimensiona o banco de dados do Azure para o nível de desempenho diferente do MySQL server tooa depois de consultar as métricas de saudação."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="08fc5-103">Monitorar e dimensionar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="08fc5-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="08fc5-104">Esse exemplo de script CLI dimensiona um único banco de dados do Azure para o nível de desempenho diferente do MySQL server tooa depois de consultar as métricas de saudação.</span><span class="sxs-lookup"><span data-stu-id="08fc5-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="08fc5-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="08fc5-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="08fc5-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="08fc5-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="08fc5-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="08fc5-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="08fc5-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="08fc5-108">Sample script</span></span>
<span data-ttu-id="08fc5-109">No script de exemplo, altere Olá realçado linhas toocustomize Olá administrador username e password.</span><span class="sxs-lookup"><span data-stu-id="08fc5-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="08fc5-110">Substitua a id de assinatura de saudação em Olá az monitor comandos com sua id de assinatura.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="08fc5-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="08fc5-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="08fc5-111">Clean up deployment</span></span>
<span data-ttu-id="08fc5-112">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="08fc5-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="08fc5-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="08fc5-113">Script explanation</span></span>
<span data-ttu-id="08fc5-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="08fc5-114">This script uses hello following commands.</span></span> <span data-ttu-id="08fc5-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="08fc5-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="08fc5-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="08fc5-116">**Command**</span></span> | <span data-ttu-id="08fc5-117">**Observações**</span><span class="sxs-lookup"><span data-stu-id="08fc5-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="08fc5-118">az group create</span><span class="sxs-lookup"><span data-stu-id="08fc5-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="08fc5-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="08fc5-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08fc5-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="08fc5-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="08fc5-121">Cria um servidor MySQL que hospeda os bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="08fc5-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="08fc5-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="08fc5-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="08fc5-123">Lista o valor de métrica Olá para recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="08fc5-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="08fc5-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="08fc5-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="08fc5-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="08fc5-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08fc5-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08fc5-126">Next steps</span></span>
- <span data-ttu-id="08fc5-127">Para obter mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08fc5-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="08fc5-128">Experimente scripts adicionais: [exemplos da CLI do Azure para o Banco de Dados do Azure para MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="08fc5-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="08fc5-129">Para obter mais informações sobre dimensionamento, consulte [Camadas de serviço](../concepts-service-tiers.md) e [Unidades de computação e unidades de armazenamento](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="08fc5-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
