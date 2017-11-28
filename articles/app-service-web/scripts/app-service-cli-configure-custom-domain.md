---
title: "aaaAzure exemplo de Script CLI - mapear um aplicativo web do domínio personalizado tooa | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - mapa de um aplicativo web do domínio personalizado tooa"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="b6682-103">Mapa de um aplicativo web do domínio personalizado tooa</span><span class="sxs-lookup"><span data-stu-id="b6682-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="b6682-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com seus recursos relacionados e, em seguida, mapeia `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="b6682-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b6682-105">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b6682-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b6682-106">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6682-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b6682-107">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6682-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b6682-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b6682-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b6682-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b6682-109">Script explanation</span></span>

<span data-ttu-id="b6682-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b6682-110">This script uses hello following commands.</span></span> <span data-ttu-id="b6682-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="b6682-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b6682-112">Command</span><span class="sxs-lookup"><span data-stu-id="b6682-112">Command</span></span> | <span data-ttu-id="b6682-113">Observações</span><span class="sxs-lookup"><span data-stu-id="b6682-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6682-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b6682-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b6682-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b6682-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b6682-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="b6682-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b6682-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6682-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b6682-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="b6682-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b6682-119">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6682-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b6682-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="b6682-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="b6682-121">Mapeia um aplicativo de web tooa domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="b6682-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6682-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6682-122">Next steps</span></span>

<span data-ttu-id="b6682-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6682-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b6682-124">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b6682-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
