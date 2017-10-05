---
title: "Exemplo de Script da CLI do Azure - Associar um certificado SSL personalizado a um aplicativo de funções | Microsoft Docs"
description: "Exemplo de Script da CLI do Azure - Associar um certificado SSL personalizado a um aplicativo de funções"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="22cfc-103">Associar um certificado SSL personalizado a um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="22cfc-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="22cfc-104">Este exemplo de script cria um aplicativo de funções no Serviço de Aplicativo com seus recursos relacionados e associa o certificado SSL de um nome de domínio personalizado a ele.</span><span class="sxs-lookup"><span data-stu-id="22cfc-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="22cfc-105">Neste exemplo, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="22cfc-105">For this sample, you need:</span></span>

* <span data-ttu-id="22cfc-106">Acesso à página de configuração do DNS do registrador de seu domínio.</span><span class="sxs-lookup"><span data-stu-id="22cfc-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="22cfc-107">Um arquivo .PFX válido e sua senha para o certificado SSL que você deseja carregar e associar.</span><span class="sxs-lookup"><span data-stu-id="22cfc-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="22cfc-108">Para associar um certificado SSL, seu aplicativo de funções deve ser criado em um Plano do Serviço de Aplicativo, e não em um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="22cfc-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="22cfc-109">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="22cfc-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="22cfc-110">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="22cfc-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="22cfc-111">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="22cfc-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="22cfc-112">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="22cfc-112">Sample script</span></span>

<span data-ttu-id="22cfc-113">[!code-azurecli-interactive[principal](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associar um certificado SSL personalizado a um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="22cfc-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="22cfc-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="22cfc-114">Script explanation</span></span>

<span data-ttu-id="22cfc-115">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="22cfc-115">This script uses the following commands.</span></span> <span data-ttu-id="22cfc-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="22cfc-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="22cfc-117">Command</span><span class="sxs-lookup"><span data-stu-id="22cfc-117">Command</span></span> | <span data-ttu-id="22cfc-118">Observações</span><span class="sxs-lookup"><span data-stu-id="22cfc-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="22cfc-119">az group create</span><span class="sxs-lookup"><span data-stu-id="22cfc-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="22cfc-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="22cfc-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="22cfc-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="22cfc-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="22cfc-122">Cria um Plano do Serviço de Aplicativo necessário para associar certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="22cfc-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="22cfc-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="22cfc-123">az functionapp create</span></span>]() | <span data-ttu-id="22cfc-124">Cria um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="22cfc-124">Creates a function app.</span></span> |
| [<span data-ttu-id="22cfc-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="22cfc-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="22cfc-126">Mapeia um domínio personalizado para o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="22cfc-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="22cfc-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="22cfc-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="22cfc-128">Carrega um certificado SSL em um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="22cfc-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="22cfc-129">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="22cfc-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="22cfc-130">Associa um certificado SSL carregado a um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="22cfc-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22cfc-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22cfc-131">Next steps</span></span>

<span data-ttu-id="22cfc-132">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22cfc-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="22cfc-133">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure]().</span><span class="sxs-lookup"><span data-stu-id="22cfc-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
