---
title: AAA "banco de dados no Azure de escala de Script CLI do Azure para PostgreSQL | Microsoft Docs"
description: "Exemplo de Script do Azure CLI - escala banco de dados para o nível de desempenho diferentes de tooa PostgreSQL servidor depois de consultar as métricas de saudação."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="26015-103">Monitore e dimensione um único servidor PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="26015-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="26015-104">Esse exemplo de script CLI dimensiona um único banco de dados do Azure para o nível de desempenho diferentes PostgreSQL servidor tooa depois de consultar as métricas de saudação.</span><span class="sxs-lookup"><span data-stu-id="26015-104">This sample CLI script scales a single Azure Database for PostgreSQL server tooa different performance level after querying hello metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="26015-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="26015-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="26015-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="26015-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="26015-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="26015-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="26015-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="26015-108">Sample script</span></span>
<span data-ttu-id="26015-109">No script de exemplo, altere Olá realçado linhas toocustomize Olá administrador username e password.</span><span class="sxs-lookup"><span data-stu-id="26015-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="26015-110">Substitua a id de assinatura de saudação em Olá az monitor comandos com sua id de assinatura.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="26015-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="26015-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="26015-111">Clean up deployment</span></span>
<span data-ttu-id="26015-112">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="26015-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="26015-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="26015-113">Script explanation</span></span>
<span data-ttu-id="26015-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="26015-114">This script uses hello following commands.</span></span> <span data-ttu-id="26015-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="26015-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26015-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="26015-116">**Command**</span></span> | <span data-ttu-id="26015-117">**Observações**</span><span class="sxs-lookup"><span data-stu-id="26015-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="26015-118">az group create</span><span class="sxs-lookup"><span data-stu-id="26015-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="26015-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="26015-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26015-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="26015-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="26015-121">Cria um servidor PostgreSQL que hospeda os bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="26015-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="26015-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="26015-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="26015-123">Lista o valor de métrica Olá para recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="26015-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="26015-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="26015-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="26015-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="26015-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26015-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26015-126">Next steps</span></span>
- <span data-ttu-id="26015-127">Para obter mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="26015-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="26015-128">Experimente scripts adicionais: [Exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="26015-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="26015-129">Leia mais informações sobre dimensionamento: [Camadas de serviço](../concepts-service-tiers.md) e [Unidades de computação e unidades de armazenamento](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="26015-129">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
