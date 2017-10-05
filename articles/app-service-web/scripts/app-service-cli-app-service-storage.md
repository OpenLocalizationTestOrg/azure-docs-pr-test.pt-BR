---
title: Exemplo de script da CLI do Azure - conectar um aplicativo Web para uma conta de armazenamento | Microsoft Docs
description: Exemplo de script da CLI do Azure - conectar um aplicativo Web para uma conta de armazenamento
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
ms.openlocfilehash: 2520eecf54b77b88d6aa1ba2e538d05e3407f3d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="c7c99-103">Conectar um aplicativo Web a uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c7c99-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="c7c99-104">Nesse cenário, você aprenderá como criar uma conta de armazenamento do Azure e um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c7c99-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="c7c99-105">Em seguida, você vinculará a conta de armazenamento ao aplicativo Web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7c99-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c7c99-106">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c7c99-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c7c99-107">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="c7c99-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="c7c99-108">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7c99-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="c7c99-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c7c99-109">Sample script</span></span>

<span data-ttu-id="c7c99-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Armazenamento do Azure")]</span><span class="sxs-lookup"><span data-stu-id="c7c99-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c7c99-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c7c99-111">Script explanation</span></span>

<span data-ttu-id="c7c99-112">Esse script usa os seguintes comandos para criar um grupo de recursos, aplicativo Web, conta de armazenamento e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="c7c99-112">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="c7c99-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="c7c99-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c7c99-114">Command</span><span class="sxs-lookup"><span data-stu-id="c7c99-114">Command</span></span> | <span data-ttu-id="c7c99-115">Observações</span><span class="sxs-lookup"><span data-stu-id="c7c99-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c7c99-116">az group create</span><span class="sxs-lookup"><span data-stu-id="c7c99-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c7c99-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c7c99-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c7c99-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c7c99-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c7c99-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7c99-119">Creates an App Service plan.</span></span> <span data-ttu-id="c7c99-120">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c99-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="c7c99-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c7c99-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c7c99-122">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c99-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c7c99-123">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c7c99-123">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="c7c99-124">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c7c99-124">Creates a storage account.</span></span> <span data-ttu-id="c7c99-125">Isso é onde os recursos estáticos serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="c7c99-125">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="c7c99-126">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="c7c99-126">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="c7c99-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="c7c99-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="c7c99-128">Cria ou atualiza uma configuração de aplicativo para um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7c99-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="c7c99-129">As configurações do aplicativo são expostas como variáveis do ambiente para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7c99-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c7c99-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7c99-130">Next steps</span></span>

<span data-ttu-id="c7c99-131">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7c99-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c7c99-132">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c7c99-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
