---
title: aaaAzure exemplo de Script CLI - monitorar um aplicativo web com logs do servidor web | Microsoft Docs
description: Exemplo de Script CLI do Azure - monitorar um aplicativo Web com logs do servidor web
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="a063d-103">Monitorar um aplicativo web com logs do servidor Web</span><span class="sxs-lookup"><span data-stu-id="a063d-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="a063d-104">Neste cenário você criará um grupo de recursos, o plano de serviço de aplicativo, o aplicativo web e configurar web hello tooenable aplicativo logs do servidor web.</span><span class="sxs-lookup"><span data-stu-id="a063d-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="a063d-105">Em seguida, você baixará os arquivos de log Olá para revisão.</span><span class="sxs-lookup"><span data-stu-id="a063d-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a063d-106">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a063d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a063d-107">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a063d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a063d-108">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a063d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a063d-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="a063d-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a063d-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="a063d-110">Script explanation</span></span>

<span data-ttu-id="a063d-111">Esse script usa Olá comandos toocreate um grupo de recursos, aplicativo web e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a063d-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="a063d-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="a063d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a063d-113">Command</span><span class="sxs-lookup"><span data-stu-id="a063d-113">Command</span></span> | <span data-ttu-id="a063d-114">Observações</span><span class="sxs-lookup"><span data-stu-id="a063d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a063d-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a063d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a063d-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="a063d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a063d-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="a063d-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a063d-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a063d-118">Creates an App Service plan.</span></span> <span data-ttu-id="a063d-119">Isso é como um farm de servidores para seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a063d-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a063d-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="a063d-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a063d-121">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a063d-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a063d-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="a063d-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="a063d-123">Configura quais logs serão persistidos pelo aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a063d-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="a063d-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="a063d-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="a063d-125">Saudação de downloads faz Olá uma máquina local de tooyour de aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a063d-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a063d-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a063d-126">Next steps</span></span>

<span data-ttu-id="a063d-127">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a063d-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a063d-128">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a063d-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
