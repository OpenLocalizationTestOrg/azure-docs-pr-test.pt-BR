---
title: aaaCreate um servidor do Analysis Services no Azure | Microsoft Docs
description: "Saiba como toocreate um servidor do Analysis Services da instância no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="99b57-103">Criar um servidor do Azure Analysis Services no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="99b57-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="99b57-104">Este artigo orienta você pela criação de um recurso de servidor do Analysis Services em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="99b57-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="99b57-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="99b57-105">Before you begin</span></span>
<span data-ttu-id="99b57-106">toocomplete este guia de início rápido, você precisa:</span><span class="sxs-lookup"><span data-stu-id="99b57-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="99b57-107">**Assinatura do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="99b57-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="99b57-108">**Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99b57-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="99b57-109">E, então, você precisa toobe tooAzure conectado com uma conta em que o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="99b57-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="99b57-110">Não há suporte para contas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="99b57-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="99b57-111">mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="99b57-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="99b57-112">**Grupo de recursos**: use um grupo de recursos que você já tem ou [crie um novo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99b57-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99b57-113">Criar um servidor pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="99b57-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="99b57-114">mais, consulte toolearn [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="99b57-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="99b57-115">toocreate um servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="99b57-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="99b57-116">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99b57-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="99b57-117">Clique em **+ Novo** > **Dados + Análise** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="99b57-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="99b57-118">Em Olá **Analysis Services** folha, preencha os campos de saudação necessárias e, em seguida, pressione **criar**.</span><span class="sxs-lookup"><span data-stu-id="99b57-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Criar servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="99b57-120">**Nome do servidor**: digite um servidor de saudação tooreference nome exclusivo usado.</span><span class="sxs-lookup"><span data-stu-id="99b57-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="99b57-121">**Assinatura**: selecione Olá assinatura neste servidor cobra para.</span><span class="sxs-lookup"><span data-stu-id="99b57-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="99b57-122">**Grupo de recursos**: esses contêineres são projetado toohelp você gerenciar uma coleção de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="99b57-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="99b57-123">mais, consulte toolearn [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99b57-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="99b57-124">**Local**: Olá de hosts de local do datacenter do Azure neste servidor.</span><span class="sxs-lookup"><span data-stu-id="99b57-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="99b57-125">Escolha um local mais próximo da sua maior base de usuários.</span><span class="sxs-lookup"><span data-stu-id="99b57-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="99b57-126">**Tipo de preço**: selecione um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="99b57-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="99b57-127">Há suporte para modelos de tabela para cima too400 GB.</span><span class="sxs-lookup"><span data-stu-id="99b57-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="99b57-128">mais, consulte toolearn [preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="99b57-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="99b57-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="99b57-129">Click **Create**.</span></span>

<span data-ttu-id="99b57-130">Normalmente, a criação demora menos de um minuto; com frequência, apenas alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="99b57-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="99b57-131">Se você selecionou **adicionar tooPortal**, navegar toosee portal tooyour o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="99b57-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="99b57-132">Ou, navegue muito**mais serviços** > **Analysis Services** toosee se seu servidor está pronto.</span><span class="sxs-lookup"><span data-stu-id="99b57-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Painel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="99b57-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99b57-134">Next steps</span></span>
<span data-ttu-id="99b57-135">Depois de criar seu servidor, você pode [implantar um modelo](analysis-services-deploy.md) tooit usando SSDT ou com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="99b57-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="99b57-136">Se um modelo que você implantar o servidor tooyour se conecta a fontes de dados tooon locais, você precisa tooinstall um [gateway de dados no local](analysis-services-gateway.md) em um computador em sua rede.</span><span class="sxs-lookup"><span data-stu-id="99b57-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

