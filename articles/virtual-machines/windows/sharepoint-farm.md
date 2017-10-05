---
title: Criar farms de servidores do SharePoint no Azure | Microsoft Docs
description: Crie rapidamente um novo farm do SharePoint 2013 ou SharePoint 2016 no Azure usando o Marketplace no portal do Azure.
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
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="2caf4-103">Criar farms de servidores do SharePoint usando o Marketplace no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2caf4-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="2caf4-104">Farms do SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2caf4-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="2caf4-105">Com o Marketplace do portal do Microsoft Azure, você pode criar rapidamente farms pré-configurados do SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="2caf4-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="2caf4-106">Isso pode economizar muito tempo quando você precisar de um farm do SharePoint básico ou de alta disponibilidade para um ambiente de desenvolvimento/teste, ou se estiver avaliando o SharePoint Server 2013 como uma solução de colaboração para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="2caf4-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="2caf4-107">O item **Farm do SharePoint Server** no Azure Marketplace do portal do Azure foi removido.</span><span class="sxs-lookup"><span data-stu-id="2caf4-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="2caf4-108">Ele foi substituído pelos itens **Farm de não HA do SharePoint 2013** e **Farm HA do SharePoint 2013**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="2caf4-109">O farm do SharePoint básico consiste em três máquinas virtuais nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="2caf4-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="2caf4-111">É possível usar esta configuração de farm para uma configuração simplificada para o desenvolvimento do aplicativo SharePoint na sua primeira avaliação do SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="2caf4-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="2caf4-112">Para criar o farm básico (três servidores) do SharePoint:</span><span class="sxs-lookup"><span data-stu-id="2caf4-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="2caf4-113">Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span><span class="sxs-lookup"><span data-stu-id="2caf4-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="2caf4-114">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="2caf4-115">No painel **Farm de não HA do SharePoint 2013**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="2caf4-116">Especifique as configurações nas etapas do painel **Criar farm não HA do SharePoint 2013** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="2caf4-117">O farm do SharePoint de alta disponibilidade consiste em nove máquinas virtuais nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="2caf4-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="2caf4-119">É possível usar essa configuração de farm para testar cargas de clientes maiores, alta disponibilidade do site externo do SharePoint e Grupos de Disponibilidade AlwaysOn do SQL Server para um farm do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2caf4-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="2caf4-120">Também é possível usar esta configuração para a implementação do aplicativo SharePoint em um ambiente de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2caf4-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="2caf4-121">Para criar o farm de alta disponibilidade (nove servidores) do SharePoint:</span><span class="sxs-lookup"><span data-stu-id="2caf4-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="2caf4-122">Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span><span class="sxs-lookup"><span data-stu-id="2caf4-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="2caf4-123">Clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="2caf4-124">No painel **Farm de HA do SharePoint 2013**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="2caf4-125">Especifique as configurações nas sete etapas do painel **Criar Farm de HA do SharePoint 2013** e, então, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2caf4-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="2caf4-126">Não é possível criar o **Farm de não HA do SharePoint 2013** ou o **Farm de HA do SharePoint 2013** com uma Avaliação Gratuita do Azure.</span><span class="sxs-lookup"><span data-stu-id="2caf4-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="2caf4-127">O portal do Azure cria ambos os farms em uma rede virtual somente em nuvem com a presença da web voltada para a Internet.</span><span class="sxs-lookup"><span data-stu-id="2caf4-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="2caf4-128">Não há nenhuma conexão de VPN site a site ou de ExpressRoute para a rede da sua organização.</span><span class="sxs-lookup"><span data-stu-id="2caf4-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="2caf4-129">Quando você cria farms básicos ou de alta disponibilidade do SharePoint usando o portal do Azure, não é possível especificar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2caf4-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="2caf4-130">Para contornar essa limitação, crie esses farms com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2caf4-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="2caf4-131">Para obter mais informações, consulte [Criar farms de desenvolvimento/teste do SharePoint 2013 com o Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span><span class="sxs-lookup"><span data-stu-id="2caf4-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="2caf4-132">Farms do SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="2caf4-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="2caf4-133">Confira [este artigo](https://technet.microsoft.com/library/mt723354.aspx) para obter instruções sobre como criar o seguinte farm de servidor único do SharePoint Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2caf4-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="2caf4-135">Gerenciando os farms do SharePoint</span><span class="sxs-lookup"><span data-stu-id="2caf4-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="2caf4-136">É possível administrar os servidores desses farms por meio de conexões da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="2caf4-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="2caf4-137">Para saber mais, veja [Fazer logon na máquina virtual](quick-create-portal.md#connect-to-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="2caf4-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="2caf4-138">No site Administração central do SharePoint, é possível configurar o My sites, os aplicativos SharePoint e outra funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="2caf4-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="2caf4-139">Para saber mais, confira [Configurar o SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span><span class="sxs-lookup"><span data-stu-id="2caf4-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2caf4-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2caf4-140">Next steps</span></span>
* <span data-ttu-id="2caf4-141">Descubra as [configurações do SharePoint](https://technet.microsoft.com/library/dn635309.aspx) adicionais nos serviços de infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2caf4-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
