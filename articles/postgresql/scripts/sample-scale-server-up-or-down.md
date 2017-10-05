---
title: "Script da CLI do Azure – dimensionar o Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – dimensionar o Banco de Dados do Azure para o servidor PostgreSQL para um nível de desempenho diferente após consultar a métrica."
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
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="34ce3-103">Monitore e dimensione um único servidor PostgreSQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="34ce3-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="34ce3-104">Este exemplo de script da CLI dimensiona um único Banco de Dados do Azure para o servidor PostgreSQL para um nível de desempenho diferente após consultar a métrica.</span><span class="sxs-lookup"><span data-stu-id="34ce3-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="34ce3-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="34ce3-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="34ce3-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="34ce3-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="34ce3-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="34ce3-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="34ce3-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="34ce3-108">Sample script</span></span>
<span data-ttu-id="34ce3-109">Neste script de exemplo, altere as linhas destacadas para personalizar o nome de usuário administrador e a senha.</span><span class="sxs-lookup"><span data-stu-id="34ce3-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="34ce3-110">Substitua a ID da assinatura usada nos comandos do monitor AZ pela sua ID de assinatura. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Criar e escalar o Banco de Dados do Azure para PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="34ce3-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="34ce3-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="34ce3-111">Clean up deployment</span></span>
<span data-ttu-id="34ce3-112">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="34ce3-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="34ce3-113">[!code-azurecli-interactive[principal](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Excluir o grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="34ce3-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="34ce3-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="34ce3-114">Script explanation</span></span>
<span data-ttu-id="34ce3-115">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="34ce3-115">This script uses the following commands.</span></span> <span data-ttu-id="34ce3-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="34ce3-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="34ce3-117">**Comando**</span><span class="sxs-lookup"><span data-stu-id="34ce3-117">**Command**</span></span> | <span data-ttu-id="34ce3-118">**Observações**</span><span class="sxs-lookup"><span data-stu-id="34ce3-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="34ce3-119">az group create</span><span class="sxs-lookup"><span data-stu-id="34ce3-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="34ce3-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="34ce3-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="34ce3-121">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="34ce3-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="34ce3-122">Cria um servidor PostgreSQL que hospeda os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="34ce3-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="34ce3-123">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="34ce3-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="34ce3-124">Lista o valor de métrica para os recursos.</span><span class="sxs-lookup"><span data-stu-id="34ce3-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="34ce3-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="34ce3-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="34ce3-126">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="34ce3-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="34ce3-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="34ce3-127">Next steps</span></span>
- <span data-ttu-id="34ce3-128">Leia mais sobre a CLI do Azure: [Documentação da CLI do Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="34ce3-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="34ce3-129">Experimente scripts adicionais: [Exemplos da CLI do Azure para o Banco de Dados do Azure para PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="34ce3-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="34ce3-130">Leia mais informações sobre dimensionamento: [Camadas de serviço](../concepts-service-tiers.md) e [Unidades de computação e unidades de armazenamento](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="34ce3-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
