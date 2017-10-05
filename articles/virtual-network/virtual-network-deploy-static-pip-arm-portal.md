---
title: "Criar uma máquina virtual com um endereço IP público estático - Portal do Azure | Microsoft Docs"
description: "Saiba como criar uma VM com um endereço IP público estático usando o Portal do Azure."
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
ms.openlocfilehash: 233e4eea8439320c1c7446e2c2b2e9d379351a3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-portal"></a><span data-ttu-id="eca71-103">Como criar uma VM com um endereço IP público estático usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eca71-103">Create a VM with a static public IP address using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eca71-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eca71-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="eca71-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eca71-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="eca71-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="eca71-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="eca71-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="eca71-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="eca71-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="eca71-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="eca71-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eca71-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eca71-110">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="eca71-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a><span data-ttu-id="eca71-111">Criar uma VM com um IP público estático</span><span class="sxs-lookup"><span data-stu-id="eca71-111">Create a VM with a static public IP</span></span>

<span data-ttu-id="eca71-112">Para criar uma VM com um endereço IP público estático no Portal do Azure, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="eca71-112">To create a VM with a static public IP address in the Azure portal, complete the following steps:</span></span>

1. <span data-ttu-id="eca71-113">Em um navegador, navegue até o [portal do Azure](https://portal.azure.com) e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="eca71-113">From a browser, navigate to the [Azure portal](https://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="eca71-114">No canto superior esquerdo do portal, clique em **Novo**>>**Computação**>**Windows Server 2012 R2 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="eca71-114">On the top left hand corner of the portal, click **New**>>**Compute**>**Windows Server 2012 R2 Datacenter**.</span></span>
3. <span data-ttu-id="eca71-115">Na lista **Selecionar um modelo de implantação**, selecione **Gerenciador de Recursos** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eca71-115">In the **Select a deployment model** list, select **Resource Manager** and click **Create**.</span></span>
4. <span data-ttu-id="eca71-116">Na folha **Noções Básicas**, insira as informações da VM conforme mostrado abaixo e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca71-116">In the **Basics** blade, enter the VM information as shown below, and then click **OK**.</span></span>
   
    ![Portal do Azure - Noções básicas](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. <span data-ttu-id="eca71-118">Na folha **Escolha um tamanho**, clique em **A1 Standard** conforme mostrado abaixo e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="eca71-118">In the **Choose a size** blade, click **A1 Standard** as shown below, and then click **Select**.</span></span>
   
    ![Portal do Azure - Escolha um tamanho](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. <span data-ttu-id="eca71-120">Na folha **Configurações**, clique em **Endereço IP público**, em seguida na folha **Criar endereço IP público** em **Atribuição**, clique em **Estático** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="eca71-120">In the **Settings** blade, click **Public IP address**, then in the **Create public IP address** blade, under **Assignment**, click **Static** as shown below.</span></span> <span data-ttu-id="eca71-121">E em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca71-121">And then click **OK**.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. <span data-ttu-id="eca71-123">Na folha **Configurações**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca71-123">In the **Settings** blade, click **OK**.</span></span>
8. <span data-ttu-id="eca71-124">Examine a folha **Resumo** conforme mostrado abaixo e então clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca71-124">Review the **Summary** blade, as shown below, and then click **OK**.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. <span data-ttu-id="eca71-126">Observe o novo bloco no seu painel.</span><span class="sxs-lookup"><span data-stu-id="eca71-126">Notice the new tile in your dashboard.</span></span>
   
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. <span data-ttu-id="eca71-128">Depois que a VM é criada, a folha **Configurações** será exibida conforme mostrado abaixo</span><span class="sxs-lookup"><span data-stu-id="eca71-128">Once the VM is created, the **Settings** blade will be displayed as shown below</span></span>
    
    ![Portal do Azure - Criar endereço IP público](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

