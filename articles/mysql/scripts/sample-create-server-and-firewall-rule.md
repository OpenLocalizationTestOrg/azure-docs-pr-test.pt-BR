---
title: "Script da CLI do Azure – criar um Banco de Dados do Azure para MySQL | Microsoft Docs"
description: "Este exemplo de script da CLI cria um Banco de Dados do Azure para servidor MySQL e configura uma regra de firewall no nível do servidor."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 201db294ce362ef3e09cbe62f48bd51c8ea94dbb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="5534a-103">Criar um servidor MySQL e configurar uma regra de firewall usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5534a-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="5534a-104">Este exemplo de script da CLI cria um Banco de Dados do Azure para servidor MySQL e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="5534a-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="5534a-105">Após o script ser executado com êxito, o servidor MySQL será acessível por todos os serviços do Azure e pelo endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="5534a-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5534a-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5534a-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5534a-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="5534a-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5534a-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5534a-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5534a-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5534a-109">Sample script</span></span>
<span data-ttu-id="5534a-110">Neste script de exemplo, edite as linhas destacadas para personalizar o nome de usuário administrador e a senha.</span><span class="sxs-lookup"><span data-stu-id="5534a-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="5534a-111">[!code-azurecli-interactive[principal](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Criar um banco de dados do Azure para MySQL e a regra de firewall de nível de servidor.")]</span><span class="sxs-lookup"><span data-stu-id="5534a-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5534a-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5534a-112">Clean up deployment</span></span>
<span data-ttu-id="5534a-113">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="5534a-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="5534a-114">[!code-azurecli-interactive[principal](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Excluir o grupo de recursos.")]</span><span class="sxs-lookup"><span data-stu-id="5534a-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="5534a-115">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5534a-115">Script explanation</span></span>
<span data-ttu-id="5534a-116">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="5534a-116">This script uses the following commands.</span></span> <span data-ttu-id="5534a-117">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5534a-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5534a-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="5534a-118">**Command**</span></span> | <span data-ttu-id="5534a-119">**Observações**</span><span class="sxs-lookup"><span data-stu-id="5534a-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="5534a-120">az group create</span><span class="sxs-lookup"><span data-stu-id="5534a-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="5534a-121">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5534a-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5534a-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="5534a-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="5534a-123">Cria um servidor MySQL que hospeda os bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="5534a-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="5534a-124">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="5534a-124">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="5534a-125">Cria uma regra de firewall para permitir o acesso ao servidor e aos bancos de dados contidos nele no intervalo de endereços IP inserido.</span><span class="sxs-lookup"><span data-stu-id="5534a-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="5534a-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="5534a-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="5534a-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="5534a-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5534a-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5534a-128">Next steps</span></span>
- <span data-ttu-id="5534a-129">Para ler mais sobre a CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5534a-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="5534a-130">Experimente scripts adicionais: [exemplos da CLI do Azure para o Banco de Dados do Azure para MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5534a-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
