---
title: "Exemplo de script da CLI do Azure – conectar um aplicativo Web ao BD Cosmos | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – conectar um aplicativo Web ao BD Cosmos"
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="03de1-103">Conectar um aplicativo Web ao BD Cosmos</span><span class="sxs-lookup"><span data-stu-id="03de1-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="03de1-104">Neste cenário, você aprenderá a criar uma conta do BD Cosmos do Azure e um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="03de1-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="03de1-105">Em seguida, você vinculará o BD Cosmos ao aplicativo Web usando as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03de1-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="03de1-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="03de1-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="03de1-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="03de1-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="03de1-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="03de1-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="03de1-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="03de1-109">Sample script</span></span>

<span data-ttu-id="03de1-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "BD Cosmos do Azure")]</span><span class="sxs-lookup"><span data-stu-id="03de1-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="03de1-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="03de1-111">Script explanation</span></span>

<span data-ttu-id="03de1-112">Este script usa os seguintes comandos para criar um grupo de recursos, um aplicativo Web, o BD Cosmos e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="03de1-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="03de1-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="03de1-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="03de1-114">Command</span><span class="sxs-lookup"><span data-stu-id="03de1-114">Command</span></span> | <span data-ttu-id="03de1-115">Observações</span><span class="sxs-lookup"><span data-stu-id="03de1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="03de1-116">az group create</span><span class="sxs-lookup"><span data-stu-id="03de1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="03de1-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="03de1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="03de1-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="03de1-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="03de1-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03de1-119">Creates an App Service plan.</span></span> <span data-ttu-id="03de1-120">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="03de1-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="03de1-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="03de1-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="03de1-122">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="03de1-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="03de1-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="03de1-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="03de1-124">Cria uma conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="03de1-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="03de1-125">É aqui que os dados serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="03de1-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="03de1-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="03de1-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="03de1-127">Lista as chaves de acesso da conta especificada do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="03de1-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="03de1-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="03de1-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="03de1-129">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="03de1-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="03de1-130">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03de1-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03de1-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03de1-131">Next steps</span></span>

<span data-ttu-id="03de1-132">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="03de1-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="03de1-133">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="03de1-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
