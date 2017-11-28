---
title: "aaaCreate uma VM com um endereço IP público estático - portal do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com um estático público endereço IP usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a><span data-ttu-id="5f290-103">Criar uma VM com um endereço IP público estático usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5f290-103">Create a VM with a static public IP address using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f290-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5f290-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="5f290-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f290-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="5f290-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5f290-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="5f290-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="5f290-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="5f290-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="5f290-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5f290-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5f290-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5f290-110">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="5f290-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="5f290-111">Criar uma VM com um IP público estático</span><span class="sxs-lookup"><span data-stu-id="5f290-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="5f290-112">endereço de uma VM com um endereço IP público estático toocreate em Olá portal do Azure, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f290-112">toocreate a VM with a static public IP address in hello Azure portal, complete hello following steps:</span></span>

1. <span data-ttu-id="5f290-113">Em um navegador, navegue toohello [portal do Azure](https://portal.azure.com) e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f290-113">From a browser, navigate toohello [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="5f290-114">No canto superior esquerdo de saudação do portal de saudação, clique em **novo**>>**de computação**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="5f290-114">On hello top left hand corner of hello portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="5f290-115">Em Olá **selecionar um modelo de implantação** , selecione **Gerenciador de recursos de** e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="5f290-115">In hello **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="5f290-116">Em Olá **Noções básicas de** folha, insira informações de VM Olá, conforme mostrado abaixo e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5f290-116">In hello **Basics** blade, enter hello VM information as shown below, and then click **OK**.</span></span>
   
    ![Portal do Azure - Noções básicas](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="5f290-118">Em Olá **escolher um tamanho de** folha, clique em **A1 padrão** conforme mostrado abaixo e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="5f290-118">In hello **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portal do Azure - Escolha um tamanho](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="5f290-120">Em hello **configurações** folha, clique em **endereço IP público**, em seguida, em hello **criar endereço IP público** folha, em **atribuição**, clique em **Estático** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5f290-120">In hello **Settings** blade, click **Public IP address**, then in hello **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="5f290-121">E em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f290-121">And then click **OK**.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="5f290-123">Em Olá **configurações** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5f290-123">In hello **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="5f290-124">Saudação de revisão **resumo** folha, conforme mostrado abaixo e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5f290-124">Review hello **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="5f290-126">Observe o novo bloco Olá no seu painel.</span><span class="sxs-lookup"><span data-stu-id="5f290-126">Notice hello new tile in your dashboard.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="5f290-128">Quando Olá VM é criada, Olá **configurações** folha será exibida conforme mostrado abaixo</span><span class="sxs-lookup"><span data-stu-id="5f290-128">Once hello VM is created, hello **Settings** blade will be displayed as shown below</span></span>
    
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

