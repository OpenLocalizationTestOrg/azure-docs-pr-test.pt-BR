---
title: aaaConsume o aplicativo gerenciado no marketplace do Azure | Microsoft Docs
description: "Describeshow toocreate um aplicativo gerenciado do Azure que está disponível por meio de saudação Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="27b96-103">Consumir Azure aplicativos em Olá Marketplace gerenciados</span><span class="sxs-lookup"><span data-stu-id="27b96-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="27b96-104">Conforme discutido em Olá [visão geral de aplicativos gerenciados](managed-application-overview.md) artigo, há dois cenários Olá final tooend experiência.</span><span class="sxs-lookup"><span data-stu-id="27b96-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="27b96-105">Um é publicador hello ou fornecedor que deseja toocreate um aplicativo gerenciado para uso por clientes.</span><span class="sxs-lookup"><span data-stu-id="27b96-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="27b96-106">Olá segundo é cliente do final de saudação ou consumidor de saudação do aplicativo hello gerenciado.</span><span class="sxs-lookup"><span data-stu-id="27b96-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="27b96-107">Este artigo aborda o segundo cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="27b96-107">This article covers hello second scenario.</span></span> <span data-ttu-id="27b96-108">Descreve como você pode implantar um aplicativo gerenciado de saudação do Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="27b96-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="27b96-109">Criar a partir de saudação Marketplace</span><span class="sxs-lookup"><span data-stu-id="27b96-109">Create from hello Marketplace</span></span>

<span data-ttu-id="27b96-110">Implantar um aplicativo gerenciado de saudação Marketplace é semelhante toodeploying qualquer tipo de recursos de saudação Marketplace.</span><span class="sxs-lookup"><span data-stu-id="27b96-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="27b96-111">No portal de saudação, selecione **+ novo** e pesquisa para o tipo de saudação do toodeploy da solução.</span><span class="sxs-lookup"><span data-stu-id="27b96-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="27b96-112">Selecione opções disponíveis de Olá, Olá um que é necessário.</span><span class="sxs-lookup"><span data-stu-id="27b96-112">From hello available options, select hello one you need.</span></span>

![pesquisar soluções](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="27b96-114">Examine o resumo de saudação do aplicativo hello e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="27b96-114">Review hello summary of hello application, and select **Create**.</span></span>

![criar aplicativo gerenciado](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="27b96-116">Como qualquer outra solução, você verá campos tooprovide valores para.</span><span class="sxs-lookup"><span data-stu-id="27b96-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="27b96-117">Esses campos variam por tipo de saudação do aplicativo gerenciado que você criar.</span><span class="sxs-lookup"><span data-stu-id="27b96-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="27b96-118">Exibir informações de suporte</span><span class="sxs-lookup"><span data-stu-id="27b96-118">View support information</span></span>

<span data-ttu-id="27b96-119">Após ter implantado seu aplicativo gerenciado, exiba informações de suporte de saudação para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="27b96-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="27b96-120">Na folha de aplicativo gerenciado hello, informações de suporte de saudação são listadas.</span><span class="sxs-lookup"><span data-stu-id="27b96-120">In hello managed application blade, hello support information is listed.</span></span>

![suporte](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="27b96-122">Exibir permissões de publicador</span><span class="sxs-lookup"><span data-stu-id="27b96-122">View publisher permissions</span></span>

<span data-ttu-id="27b96-123">fornecedor Olá que gerencia seu aplicativo é concedido acesso tooyour recursos.</span><span class="sxs-lookup"><span data-stu-id="27b96-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="27b96-124">toosee essas permissões, selecione **autorizações**.</span><span class="sxs-lookup"><span data-stu-id="27b96-124">toosee those permissions, select **Authorizations**.</span></span>

![autorizações](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="27b96-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27b96-126">Next steps</span></span>

* <span data-ttu-id="27b96-127">Para obter informações sobre como publicar um aplicativo gerenciado no hello Marketplace, consulte [aplicativos gerenciados do Azure no Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="27b96-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="27b96-128">toopublish aplicativos gerenciados que são somente toousers disponíveis em sua organização, consulte [criar e publicar o aplicativo gerenciado do catálogo do serviço](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="27b96-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="27b96-129">tooconsume aplicativos gerenciados que são somente toousers disponíveis em sua organização, consulte [consumir um aplicativo gerenciado do serviço de catálogo](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="27b96-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
