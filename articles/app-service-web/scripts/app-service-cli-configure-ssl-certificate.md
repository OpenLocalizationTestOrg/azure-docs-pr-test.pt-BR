---
title: aaaAzure exemplo de Script CLI - associar um certificado SSL personalizado, tooa aplicativo da web | Microsoft Docs
description: Exemplo de Script CLI do Azure - associar um certificado SSL personalizado, tooa aplicativo da web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="6ca9b-103">Associar um certificado SSL personalizado, tooa aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="6ca9b-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="6ca9b-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com seus recursos relacionados, em seguida, associa o certificado SSL de saudação de um tooit de nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="6ca9b-105">Para esta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="6ca9b-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6ca9b-106">Acesse a página de configuração de DNS do registrador de domínio tooyour.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="6ca9b-107">Válido. Arquivo PFX e sua senha para Olá SSL certificado que você deseja tooupload e estabeleça uma ligação.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6ca9b-108">Se você escolher tooinstall e usa o hello CLI localmente, este tópico requer que você está executando a versão do CLI do Azure Olá 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6ca9b-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6ca9b-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ca9b-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="6ca9b-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6ca9b-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6ca9b-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6ca9b-112">Script explanation</span></span>

<span data-ttu-id="6ca9b-113">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-113">This script uses hello following commands.</span></span> <span data-ttu-id="6ca9b-114">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6ca9b-115">Command</span><span class="sxs-lookup"><span data-stu-id="6ca9b-115">Command</span></span> | <span data-ttu-id="6ca9b-116">Observações</span><span class="sxs-lookup"><span data-stu-id="6ca9b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ca9b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6ca9b-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6ca9b-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ca9b-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6ca9b-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6ca9b-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6ca9b-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6ca9b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6ca9b-122">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6ca9b-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="6ca9b-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="6ca9b-124">Mapeia um aplicativo de web tooa domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="6ca9b-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="6ca9b-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="6ca9b-126">Carrega um aplicativo web de tooa de certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="6ca9b-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="6ca9b-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="6ca9b-128">Associa um certificado SSL carregado, tooa aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="6ca9b-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ca9b-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ca9b-129">Next steps</span></span>

<span data-ttu-id="6ca9b-130">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ca9b-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6ca9b-131">Exemplos de script CLI do serviço de aplicativo adicionais podem ser encontrados no hello [documentação do serviço de aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6ca9b-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
