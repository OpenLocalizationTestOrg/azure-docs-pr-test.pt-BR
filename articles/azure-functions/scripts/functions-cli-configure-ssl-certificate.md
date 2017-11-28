---
title: "aaaAzure exemplo de Script CLI - associar um aplicativo de função do tooa de certificado SSL personalizado | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - Bind um SSL certificado tooa função aplicativo personalizado no Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="50aad-103">Associar um aplicativo de função do tooa de certificado SSL personalizado</span><span class="sxs-lookup"><span data-stu-id="50aad-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="50aad-104">Esse script de exemplo cria um aplicativo de função no serviço de aplicativo com seus recursos relacionados, em seguida, associa o certificado SSL de saudação de um tooit de nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="50aad-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="50aad-105">Neste exemplo, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="50aad-105">For this sample, you need:</span></span>

* <span data-ttu-id="50aad-106">Acesse a página de configuração de DNS do registrador de domínio tooyour.</span><span class="sxs-lookup"><span data-stu-id="50aad-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="50aad-107">Válido. Arquivo PFX e sua senha para Olá SSL certificado que você deseja tooupload e estabeleça uma ligação.</span><span class="sxs-lookup"><span data-stu-id="50aad-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="50aad-108">toobind um certificado SSL, seu aplicativo de função deve ser criado em um plano de serviço de aplicativo e não em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="50aad-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="50aad-109">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="50aad-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="50aad-110">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="50aad-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="50aad-111">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="50aad-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="50aad-112">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="50aad-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="50aad-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="50aad-113">Script explanation</span></span>

<span data-ttu-id="50aad-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="50aad-114">This script uses hello following commands.</span></span> <span data-ttu-id="50aad-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="50aad-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="50aad-116">Command</span><span class="sxs-lookup"><span data-stu-id="50aad-116">Command</span></span> | <span data-ttu-id="50aad-117">Observações</span><span class="sxs-lookup"><span data-stu-id="50aad-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50aad-118">az group create</span><span class="sxs-lookup"><span data-stu-id="50aad-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="50aad-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="50aad-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50aad-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="50aad-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="50aad-121">Cria um toobind é necessário um plano de serviço de aplicativo certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="50aad-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="50aad-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="50aad-122">az functionapp create</span></span>]() | <span data-ttu-id="50aad-123">Cria um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="50aad-123">Creates a function app.</span></span> |
| [<span data-ttu-id="50aad-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="50aad-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="50aad-125">Mapeia um aplicativo de função toohello domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="50aad-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="50aad-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="50aad-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="50aad-127">Carrega um aplicativo de função de tooa de certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="50aad-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="50aad-128">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="50aad-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="50aad-129">Associa um aplicativo de função tooa de certificado carregado SSL.</span><span class="sxs-lookup"><span data-stu-id="50aad-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50aad-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50aad-130">Next steps</span></span>

<span data-ttu-id="50aad-131">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50aad-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="50aad-132">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure]().</span><span class="sxs-lookup"><span data-stu-id="50aad-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
