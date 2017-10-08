---
title: aaaAzure exemplo de Script CLI - conectar-se um aplicativo de web tooCosmos DB | Microsoft Docs
description: Script CLI do Azure de exemplo - conectar um aplicativo de web tooCosmos DB
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="91d95-103">Conecte-se um aplicativo de web tooCosmos DB</span><span class="sxs-lookup"><span data-stu-id="91d95-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="91d95-104">Nesse cenário, você aprenderá como toocreate uma conta de banco de dados do Azure Cosmos e um Azure aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="91d95-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="91d95-105">Em seguida, você vinculará aplicativo hello DB Cosmos toohello web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91d95-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91d95-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="91d95-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91d95-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="91d95-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="91d95-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="91d95-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="91d95-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="91d95-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="91d95-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="91d95-110">Script explanation</span></span>

<span data-ttu-id="91d95-111">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web, banco de dados do Cosmos e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="91d95-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="91d95-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="91d95-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="91d95-113">Command</span><span class="sxs-lookup"><span data-stu-id="91d95-113">Command</span></span> | <span data-ttu-id="91d95-114">Observações</span><span class="sxs-lookup"><span data-stu-id="91d95-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="91d95-115">az group create</span><span class="sxs-lookup"><span data-stu-id="91d95-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="91d95-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="91d95-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="91d95-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="91d95-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="91d95-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91d95-118">Creates an App Service plan.</span></span> <span data-ttu-id="91d95-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="91d95-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="91d95-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="91d95-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="91d95-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="91d95-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="91d95-122">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="91d95-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="91d95-123">Cria uma conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="91d95-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="91d95-124">Isso é onde os dados de saudação serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="91d95-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="91d95-125">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="91d95-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="91d95-126">Listas Olá chaves de acesso para hello especificou a conta de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="91d95-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="91d95-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="91d95-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="91d95-128">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="91d95-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="91d95-129">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91d95-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91d95-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91d95-130">Next steps</span></span>

<span data-ttu-id="91d95-131">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91d95-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="91d95-132">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91d95-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
