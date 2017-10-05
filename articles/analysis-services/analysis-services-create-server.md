---
title: Criar um servidor do Analysis Services no Azure | Microsoft Docs
description: "Saiba como criar uma instância do servidor do Analysis Services no Azure."
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
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="6088c-103">Criar um servidor do Azure Analysis Services no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6088c-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="6088c-104">Este artigo orienta você pela criação de um recurso de servidor do Analysis Services em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6088c-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6088c-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6088c-105">Before you begin</span></span>
<span data-ttu-id="6088c-106">Para concluir este início rápido, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="6088c-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="6088c-107">**Assinatura do Azure**: visite a [Avaliação Gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) para criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="6088c-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="6088c-108">**Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6088c-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="6088c-109">Também é preciso estar conectado ao Azure com uma conta no Azure Active Directory em questão.</span><span class="sxs-lookup"><span data-stu-id="6088c-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="6088c-110">Não há suporte para contas da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6088c-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="6088c-111">Para obter mais informações, confira [Autenticação e permissões de usuário](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="6088c-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="6088c-112">**Grupo de recursos**: use um grupo de recursos que você já tem ou [crie um novo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6088c-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6088c-113">Criar um servidor pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="6088c-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="6088c-114">Para saber mais, veja [Preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="6088c-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="6088c-115">Para criar um servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6088c-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="6088c-116">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6088c-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="6088c-117">Clique em **+ Novo** > **Dados + Análise** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="6088c-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="6088c-118">Na folha **Analysis Services**, preencha os campos obrigatórios e pressione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6088c-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Criar servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="6088c-120">**Nome do servidor**: digite um nome exclusivo usado para fazer referência ao servidor.</span><span class="sxs-lookup"><span data-stu-id="6088c-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="6088c-121">**Assinatura**: selecione a assinatura para a qual este servidor é cobrado.</span><span class="sxs-lookup"><span data-stu-id="6088c-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="6088c-122">**Grupo de recursos**: esses contêineres são projetados para ajudar você a gerenciar uma coleção de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6088c-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="6088c-123">Para saber mais, veja [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6088c-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="6088c-124">**Local**: local do datacenter do Azure que hospeda o servidor.</span><span class="sxs-lookup"><span data-stu-id="6088c-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="6088c-125">Escolha um local mais próximo da sua maior base de usuários.</span><span class="sxs-lookup"><span data-stu-id="6088c-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="6088c-126">**Tipo de preço**: selecione um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="6088c-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="6088c-127">Há suporte para modelos tabulares até de 400 GB.</span><span class="sxs-lookup"><span data-stu-id="6088c-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="6088c-128">Para saber mais, veja [Preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="6088c-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="6088c-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6088c-129">Click **Create**.</span></span>

<span data-ttu-id="6088c-130">Normalmente, a criação demora menos de um minuto; com frequência, apenas alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="6088c-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="6088c-131">Se você tiver selecionado **Adicionar ao Portal**, navegue até o portal para ver o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="6088c-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="6088c-132">Ou navegue até **Mais serviços** > **Analysis Services** para ver se o servidor está pronto.</span><span class="sxs-lookup"><span data-stu-id="6088c-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Painel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="6088c-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6088c-134">Next steps</span></span>
<span data-ttu-id="6088c-135">Depois de ter criado seu servidor, você poderá [implantar um modelo](analysis-services-deploy.md) a ele usando o SSDT ou com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="6088c-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="6088c-136">Se um modelo implantado em seu servidor se conectar às fontes de dados locais, você precisará instalar um [Gateway de dados local](analysis-services-gateway.md) em um computador em sua rede.</span><span class="sxs-lookup"><span data-stu-id="6088c-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

