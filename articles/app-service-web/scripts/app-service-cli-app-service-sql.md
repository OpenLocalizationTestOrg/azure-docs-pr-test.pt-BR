---
title: aaaAzure exemplo de Script CLI - se conectar a um banco de dados SQL de tooa do aplicativo de web | Microsoft Docs
description: Script CLI do Azure de exemplo - conectar a um banco de dados SQL de tooa do aplicativo de web
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="976b3-103">Conectar a um banco de dados SQL de tooa do aplicativo de web</span><span class="sxs-lookup"><span data-stu-id="976b3-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="976b3-104">Nesse cenário, você aprenderá como toocreate um banco de dados do SQL Azure e um Azure aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="976b3-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="976b3-105">Em seguida, você vinculará aplicativo hello SQL banco de dados toohello web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="976b3-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="976b3-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="976b3-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="976b3-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="976b3-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="976b3-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="976b3-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="976b3-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="976b3-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="976b3-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="976b3-110">Script explanation</span></span>

<span data-ttu-id="976b3-111">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web, banco de dados SQL e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="976b3-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="976b3-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="976b3-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="976b3-113">Command</span><span class="sxs-lookup"><span data-stu-id="976b3-113">Command</span></span> | <span data-ttu-id="976b3-114">Observações</span><span class="sxs-lookup"><span data-stu-id="976b3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="976b3-115">az group create</span><span class="sxs-lookup"><span data-stu-id="976b3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="976b3-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="976b3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="976b3-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="976b3-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="976b3-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="976b3-118">Creates an App Service plan.</span></span> <span data-ttu-id="976b3-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="976b3-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="976b3-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="976b3-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="976b3-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="976b3-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="976b3-122">az sql server create</span><span class="sxs-lookup"><span data-stu-id="976b3-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="976b3-123">Cria um servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="976b3-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="976b3-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="976b3-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="976b3-125">Cria um novo banco de dados com hello servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="976b3-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="976b3-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="976b3-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="976b3-127">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="976b3-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="976b3-128">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="976b3-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="976b3-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="976b3-129">Next steps</span></span>

<span data-ttu-id="976b3-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="976b3-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="976b3-131">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="976b3-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
