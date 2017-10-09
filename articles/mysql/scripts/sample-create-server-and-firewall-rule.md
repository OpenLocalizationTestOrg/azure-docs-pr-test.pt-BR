---
title: AAA "CLI do Azure Script - criar um banco de dados do Azure para MySQL | Microsoft Docs"
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
ms.openlocfilehash: 1d619ee0547efd8275eaf7c1347b6c3427025c3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="15a31-103">Criar um servidor MySQL e configurar uma regra de firewall usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="15a31-103">Create a MySQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="15a31-104">Este exemplo de script da CLI cria um Banco de Dados do Azure para servidor MySQL e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="15a31-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="15a31-105">Depois que o script hello é executado com êxito, Olá MySQL servidor acessível por todos os serviços do Azure e Olá configurado o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="15a31-105">Once hello script runs successfully, hello MySQL server is accessible by all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="15a31-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="15a31-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="15a31-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="15a31-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="15a31-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="15a31-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="15a31-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="15a31-109">Sample script</span></span>
<span data-ttu-id="15a31-110">Esse script de exemplo, edite Olá realçado linhas toocustomize Olá administrador username e password.</span><span class="sxs-lookup"><span data-stu-id="15a31-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="15a31-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="15a31-111">Clean up deployment</span></span>
<span data-ttu-id="15a31-112">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="15a31-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="15a31-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="15a31-113">Script explanation</span></span>
<span data-ttu-id="15a31-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="15a31-114">This script uses hello following commands.</span></span> <span data-ttu-id="15a31-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="15a31-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="15a31-116">**Comando**</span><span class="sxs-lookup"><span data-stu-id="15a31-116">**Command**</span></span> | <span data-ttu-id="15a31-117">**Observações**</span><span class="sxs-lookup"><span data-stu-id="15a31-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="15a31-118">az group create</span><span class="sxs-lookup"><span data-stu-id="15a31-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="15a31-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="15a31-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="15a31-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="15a31-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="15a31-121">Cria um servidor MySQL que hospeda os bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="15a31-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="15a31-122">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="15a31-122">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="15a31-123">Cria um servidor de toohello de acesso do firewall regra tooallow e bancos de dados sob ele do intervalo de endereços IP hello inserido.</span><span class="sxs-lookup"><span data-stu-id="15a31-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="15a31-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="15a31-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="15a31-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="15a31-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="15a31-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15a31-126">Next steps</span></span>
- <span data-ttu-id="15a31-127">Para obter mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15a31-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="15a31-128">Experimente scripts adicionais: [exemplos da CLI do Azure para o Banco de Dados do Azure para MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="15a31-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
