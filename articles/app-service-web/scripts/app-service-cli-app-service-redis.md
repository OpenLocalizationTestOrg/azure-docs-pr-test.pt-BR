---
title: Exemplo de script da CLI do Azure - Conectar um aplicativo Web a um cache redis | Microsoft Docs
description: Exemplo de script da CLI do Azure - Conectar um aplicativo Web a um cache redis
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="32da3-103">Conectar um aplicativo Web a um cache redis</span><span class="sxs-lookup"><span data-stu-id="32da3-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="32da3-104">Nesse cenário, você aprenderá a criar um Cache Redis do Azure e um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da3-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="32da3-105">Em seguida, você vinculará o cache redis ao aplicativo Web usando as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32da3-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="32da3-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="32da3-106">Sample script</span></span>

<span data-ttu-id="32da3-107">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Cache Redis do Azure")]</span><span class="sxs-lookup"><span data-stu-id="32da3-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="32da3-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="32da3-108">Script explanation</span></span>

<span data-ttu-id="32da3-109">Esse script usa os seguintes comandos para criar um grupo de recursos, o aplicativo Web, o cache redis e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="32da3-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="32da3-110">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="32da3-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="32da3-111">Command</span><span class="sxs-lookup"><span data-stu-id="32da3-111">Command</span></span> | <span data-ttu-id="32da3-112">Observações</span><span class="sxs-lookup"><span data-stu-id="32da3-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="32da3-113">az group create</span><span class="sxs-lookup"><span data-stu-id="32da3-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="32da3-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="32da3-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="32da3-115">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="32da3-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="32da3-116">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32da3-116">Creates an App Service plan.</span></span> <span data-ttu-id="32da3-117">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da3-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="32da3-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="32da3-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="32da3-119">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da3-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="32da3-120">az redis create</span><span class="sxs-lookup"><span data-stu-id="32da3-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="32da3-121">Crie uma nova instância do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="32da3-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="32da3-122">É aqui que os dados serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="32da3-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="32da3-123">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="32da3-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="32da3-124">Lista as teclas de acesso para a instância do cache redis.</span><span class="sxs-lookup"><span data-stu-id="32da3-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="32da3-125">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="32da3-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="32da3-126">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da3-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="32da3-127">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32da3-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32da3-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32da3-128">Next steps</span></span>

<span data-ttu-id="32da3-129">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32da3-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="32da3-130">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="32da3-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
