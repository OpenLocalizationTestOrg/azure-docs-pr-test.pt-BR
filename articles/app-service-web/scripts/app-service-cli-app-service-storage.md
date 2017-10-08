---
title: aaaAzure exemplo de Script CLI - se conectar a uma conta de armazenamento do tooa de aplicativo web | Microsoft Docs
description: Script CLI do Azure de exemplo - conectar a uma conta de armazenamento do tooa de aplicativo web
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
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="303fd-103">Conecte-se a uma conta de armazenamento do tooa de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="303fd-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="303fd-104">Nesse cenário, você aprenderá como toocreate uma conta de armazenamento do Azure e um Azure aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="303fd-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="303fd-105">Em seguida, você vinculará aplicativo hello armazenamento conta toohello web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="303fd-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="303fd-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="303fd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="303fd-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="303fd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="303fd-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="303fd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="303fd-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="303fd-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="303fd-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="303fd-110">Script explanation</span></span>

<span data-ttu-id="303fd-111">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web, conta de armazenamento e recursos todos relacionados a seguir.</span><span class="sxs-lookup"><span data-stu-id="303fd-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="303fd-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="303fd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="303fd-113">Command</span><span class="sxs-lookup"><span data-stu-id="303fd-113">Command</span></span> | <span data-ttu-id="303fd-114">Observações</span><span class="sxs-lookup"><span data-stu-id="303fd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="303fd-115">az group create</span><span class="sxs-lookup"><span data-stu-id="303fd-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="303fd-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="303fd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="303fd-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="303fd-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="303fd-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="303fd-118">Creates an App Service plan.</span></span> <span data-ttu-id="303fd-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="303fd-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="303fd-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="303fd-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="303fd-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="303fd-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="303fd-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="303fd-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="303fd-123">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="303fd-123">Creates a storage account.</span></span> <span data-ttu-id="303fd-124">Isso é onde serão armazenados os ativos de saudação estático.</span><span class="sxs-lookup"><span data-stu-id="303fd-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="303fd-125">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="303fd-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="303fd-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="303fd-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="303fd-127">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="303fd-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="303fd-128">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="303fd-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="303fd-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="303fd-129">Next steps</span></span>

<span data-ttu-id="303fd-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="303fd-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="303fd-131">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="303fd-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
