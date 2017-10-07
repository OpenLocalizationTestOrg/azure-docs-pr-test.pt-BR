---
title: "toocreate aaaUse 2.0 do CLI um aplicativo do AD do Azure e configurá-lo tooaccess API de serviços de mídia do Azure | Microsoft Docs"
description: "Este tópico mostra como toouse 2.0 do CLI toocreate um aplicativo do AD do Azure e configurá-lo tooaccess API de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="735fb-103">Use 2.0 do CLI toocreate um aplicativo AAD e configurá-lo tooaccess API de serviços de mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="735fb-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="735fb-104">Este tópico mostra como toouse 2.0 do CLI toocreate um aplicativo do Azure Active Directory (AD do Azure) e tooaccess principal do serviço do Azure Media Services recursos.</span><span class="sxs-lookup"><span data-stu-id="735fb-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="735fb-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="735fb-105">Prerequisites</span></span>

- <span data-ttu-id="735fb-106">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="735fb-106">An Azure account.</span></span> <span data-ttu-id="735fb-107">Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="735fb-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="735fb-108">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="735fb-108">A Media Services account.</span></span> <span data-ttu-id="735fb-109">Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="735fb-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="735fb-110">Saudação de usar o Shell de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="735fb-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="735fb-111">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="735fb-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="735fb-112">Inicie Olá nuvem Shell Olá superior no painel de navegação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="735fb-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="735fb-114">Para obter mais informações, consulte [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="735fb-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="735fb-115">Criar um aplicativo do AD do Azure e configurar a conta do media toohello acesso com 2.0 do CLI</span><span class="sxs-lookup"><span data-stu-id="735fb-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="735fb-116">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="735fb-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="735fb-117">Neste exemplo, Olá **escopo** é o caminho do recurso completo de saudação para mídia Olá conta dos serviços.</span><span class="sxs-lookup"><span data-stu-id="735fb-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="735fb-118">No entanto, Olá **escopo** pode estar em qualquer nível.</span><span class="sxs-lookup"><span data-stu-id="735fb-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="735fb-119">Por exemplo, pode ser uma saudação níveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="735fb-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="735fb-120">Olá **assinatura** nível.</span><span class="sxs-lookup"><span data-stu-id="735fb-120">hello **subscription** level.</span></span>
* <span data-ttu-id="735fb-121">Olá **grupo de recursos** nível.</span><span class="sxs-lookup"><span data-stu-id="735fb-121">hello **resource group** level.</span></span>
* <span data-ttu-id="735fb-122">Olá **recurso** nível (por exemplo, uma conta de mídia).</span><span class="sxs-lookup"><span data-stu-id="735fb-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="735fb-123">Para obter mais informações, consulte [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="735fb-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="735fb-124">Consulte também [Manage Role-Based o controle de acesso com hello Azure interface de linha de comando](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="735fb-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="735fb-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="735fb-125">Next steps</span></span>

<span data-ttu-id="735fb-126">Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="735fb-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
