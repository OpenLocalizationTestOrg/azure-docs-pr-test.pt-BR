---
title: aaaCreate farms de servidores do SharePoint no Azure | Microsoft Docs
description: "Crie rapidamente um novo farm do SharePoint 2013 ou SharePoint 2016 no Azure usando Olá marketplace portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="6aff1-103">Criar farms de servidores do SharePoint usando Olá marketplace portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6aff1-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="6aff1-104">Farms do SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="6aff1-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="6aff1-105">Com a saudação Microsoft Azure portal do marketplace, você pode criar rapidamente farms do SharePoint Server 2013 pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="6aff1-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="6aff1-106">Isso pode economizar muito tempo quando você precisar de um farm do SharePoint básico ou de alta disponibilidade para um ambiente de desenvolvimento/teste, ou se estiver avaliando o SharePoint Server 2013 como uma solução de colaboração para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="6aff1-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="6aff1-107">Olá **Farm do SharePoint Server** item hello Azure Marketplace de saudação portal do Azure foi removido.</span><span class="sxs-lookup"><span data-stu-id="6aff1-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="6aff1-108">Ela foi substituída por hello **Farm do SharePoint 2013 não - HA** e **Farm do SharePoint 2013 HA** itens.</span><span class="sxs-lookup"><span data-stu-id="6aff1-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="6aff1-109">farm do SharePoint básico de saudação consiste em três máquinas virtuais nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="6aff1-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="6aff1-111">É possível usar esta configuração de farm para uma configuração simplificada para o desenvolvimento do aplicativo SharePoint na sua primeira avaliação do SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="6aff1-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="6aff1-112">toocreate Olá básica () do SharePoint farm de três servidores:</span><span class="sxs-lookup"><span data-stu-id="6aff1-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6aff1-113">Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="6aff1-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="6aff1-114">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="6aff1-115">Em Olá **Farm do SharePoint 2013 não - HA** painel, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6aff1-116">Especificar as configurações em etapas Olá Olá **criar Farm do SharePoint 2013 não - HA** painel e clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="6aff1-117">farm do SharePoint de alta disponibilidade Olá consiste em nove máquinas virtuais nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="6aff1-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="6aff1-119">Você pode usar este farm configuração tootest cargas mais elevadas de cliente, a alta disponibilidade do site do SharePoint externo de saudação e grupos de disponibilidade do AlwaysOn do SQL Server para um farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6aff1-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="6aff1-120">Também é possível usar esta configuração para a implementação do aplicativo SharePoint em um ambiente de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="6aff1-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="6aff1-121">farm de toocreate Olá alta disponibilidade (servidor de nove) do SharePoint:</span><span class="sxs-lookup"><span data-stu-id="6aff1-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6aff1-122">Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="6aff1-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="6aff1-123">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="6aff1-124">Em Olá **Farm do SharePoint 2013 HA** painel, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6aff1-125">Especificar as configurações em etapas Olá sete Olá **criar Farm do SharePoint 2013 HA** painel e clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="6aff1-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="6aff1-126">Não é possível criar hello **Farm do SharePoint 2013 não - HA** ou **Farm do SharePoint 2013 HA** com uma avaliação gratuita do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aff1-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="6aff1-127">Olá portal do Azure cria ambos esses farms de servidores em uma rede virtual somente em nuvem com uma presença da web para a Internet.</span><span class="sxs-lookup"><span data-stu-id="6aff1-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="6aff1-128">Não há nenhum site a site VPN ou rota expressa conexão back tooyour rede da organização.</span><span class="sxs-lookup"><span data-stu-id="6aff1-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="6aff1-129">Quando você cria Olá básica ou farms do SharePoint de alta disponibilidade usando Olá portal do Azure, você não pode especificar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="6aff1-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="6aff1-130">toowork com essa limitação, crie esses farms de servidores com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6aff1-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="6aff1-131">Para obter mais informações, consulte [Criar farms de desenvolvimento/teste do SharePoint 2013 com o Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="6aff1-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="6aff1-132">Farms do SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="6aff1-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="6aff1-133">Consulte [neste artigo](https://technet.microsoft.com/library/mt723354.aspx) para Olá Olá de toobuild de instruções a seguir de servidor único do SharePoint Server 2016 do farm.</span><span class="sxs-lookup"><span data-stu-id="6aff1-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="6aff1-135">Gerenciando farms do SharePoint Olá</span><span class="sxs-lookup"><span data-stu-id="6aff1-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="6aff1-136">Você pode administrar servidores Olá esses farms através de conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="6aff1-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="6aff1-137">Para obter mais informações, consulte [fazer logon na máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="6aff1-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="6aff1-138">No site do SharePoint de Administração Central hello, você pode configurar meus sites, aplicativos do SharePoint e outras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="6aff1-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="6aff1-139">Para saber mais, confira [Configurar o SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aff1-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aff1-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6aff1-140">Next steps</span></span>
* <span data-ttu-id="6aff1-141">Descubra as [configurações do SharePoint](https://technet.microsoft.com/library/dn635309.aspx) adicionais nos serviços de infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aff1-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
