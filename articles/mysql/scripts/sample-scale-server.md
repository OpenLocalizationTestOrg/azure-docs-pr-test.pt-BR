---
title: Exemplos da CLI do Azure para dimensionar um Banco de Dados do Azure para o servidor MySQL | Microsoft Docs
description: "Este exemplo de script da CLI dimensiona um Banco de Dados do Azure para o servidor MySQL para um nível de desempenho diferente após consultar a métrica."
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="0d14c-103">Monitorar e dimensionar um Banco de Dados do Azure para servidor MySQL usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0d14c-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="0d14c-104">Este exemplo de script da CLI dimensiona um único Banco de Dados do Azure para o servidor MySQL para um nível de desempenho diferente após consultar a métrica.</span><span class="sxs-lookup"><span data-stu-id="0d14c-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0d14c-105">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0d14c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0d14c-106">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="0d14c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="0d14c-107">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0d14c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0d14c-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0d14c-108">Sample script</span></span>
<span data-ttu-id="0d14c-109">Neste script de exemplo, altere as linhas destacadas para personalizar o nome de usuário administrador e a senha.</span><span class="sxs-lookup"><span data-stu-id="0d14c-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="0d14c-110">Substitua a ID de assinatura usada nos comandos do monitor AZ pela sua ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="0d14c-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="0d14c-111">[!code-azurecli-interactive[principal](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Criar e escalar o banco de dados do Azure para MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="0d14c-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0d14c-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="0d14c-112">Clean up deployment</span></span>
<span data-ttu-id="0d14c-113">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="0d14c-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="0d14c-114">[!code-azurecli-interactive[principal](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Excluir o grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="0d14c-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="0d14c-115">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="0d14c-115">Script explanation</span></span>
<span data-ttu-id="0d14c-116">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="0d14c-116">This script uses the following commands.</span></span> <span data-ttu-id="0d14c-117">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="0d14c-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0d14c-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="0d14c-118">**Command**</span></span> | <span data-ttu-id="0d14c-119">**Observações**</span><span class="sxs-lookup"><span data-stu-id="0d14c-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="0d14c-120">az group create</span><span class="sxs-lookup"><span data-stu-id="0d14c-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="0d14c-121">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0d14c-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0d14c-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="0d14c-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="0d14c-123">Cria um servidor MySQL que hospeda os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="0d14c-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="0d14c-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="0d14c-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="0d14c-125">Lista o valor de métrica para os recursos.</span><span class="sxs-lookup"><span data-stu-id="0d14c-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="0d14c-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="0d14c-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="0d14c-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="0d14c-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0d14c-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d14c-128">Next steps</span></span>
- <span data-ttu-id="0d14c-129">Para ler mais sobre a CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d14c-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="0d14c-130">Experimente scripts adicionais: [exemplos da CLI do Azure para o Banco de Dados do Azure para MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0d14c-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="0d14c-131">Para obter mais informações sobre dimensionamento, consulte [Camadas de serviço](../concepts-service-tiers.md) e [Unidades de computação e unidades de armazenamento](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0d14c-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
