---
title: Exemplo de Script da CLI do Azure - Associar um certificado SSL personalizado a um aplicativo Web | Microsoft Docs
description: Exemplo de Script da CLI do Azure - Associar um certificado SSL personalizado a um aplicativo Web
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="e1fb3-103">Associar um certificado SSL personalizado a um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e1fb3-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="e1fb3-104">Este exemplo de script cria um aplicativo Web no Serviço de Aplicativo com seus recursos relacionados e associa o certificado SSL de um nome de domínio personalizado a ele.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="e1fb3-105">Para esta amostra, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="e1fb3-105">For this sample, you will need:</span></span>

* <span data-ttu-id="e1fb3-106">Acesso à página de configuração do DNS do registrador de seu domínio.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="e1fb3-107">Um arquivo .PFX válido e sua senha para o certificado SSL que você deseja carregar e associar.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e1fb3-108">Se você optar por instalar e usar a CLI localmente, este tópico exigirá que você esteja executando a CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e1fb3-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="e1fb3-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1fb3-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="e1fb3-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e1fb3-111">Sample script</span></span>

<span data-ttu-id="e1fb3-112">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associar um certificado SSL personalizado a um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="e1fb3-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e1fb3-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e1fb3-113">Script explanation</span></span>

<span data-ttu-id="e1fb3-114">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-114">This script uses the following commands.</span></span> <span data-ttu-id="e1fb3-115">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e1fb3-116">Command</span><span class="sxs-lookup"><span data-stu-id="e1fb3-116">Command</span></span> | <span data-ttu-id="e1fb3-117">Observações</span><span class="sxs-lookup"><span data-stu-id="e1fb3-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e1fb3-118">az group create</span><span class="sxs-lookup"><span data-stu-id="e1fb3-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e1fb3-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e1fb3-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e1fb3-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e1fb3-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e1fb3-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e1fb3-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e1fb3-123">Cria um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e1fb3-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="e1fb3-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="e1fb3-125">Mapeia um domínio personalizado para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="e1fb3-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="e1fb3-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="e1fb3-127">Carrega um certificado SSL em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="e1fb3-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="e1fb3-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="e1fb3-129">Associa um certificado SSL carregado a um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e1fb3-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e1fb3-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1fb3-130">Next steps</span></span>

<span data-ttu-id="e1fb3-131">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1fb3-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e1fb3-132">Os exemplos de script da CLI do Serviço de Aplicativo adicionais podem ser encontrados na [documentação do Serviço de Aplicativo do Azure](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e1fb3-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
