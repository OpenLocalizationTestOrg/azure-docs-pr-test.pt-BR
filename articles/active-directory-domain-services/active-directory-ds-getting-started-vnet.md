---
title: 'Azure Active Directory Domain Services: criar ou selecionar uma rede virtual | Microsoft Docs'
description: "Habilitar o Azure Active Directory Domain Services usando o portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="9328f-103">Criar ou selecionar uma rede virtual para o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="9328f-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="9328f-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="9328f-104">Before you begin</span></span>
<span data-ttu-id="9328f-105">Consulte as [Considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="9328f-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="9328f-106">Tarefa 2: criar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="9328f-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="9328f-107">A próxima tarefa de configuração é criar uma rede virtual do Azure e uma sub-rede dentro dela.</span><span class="sxs-lookup"><span data-stu-id="9328f-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="9328f-108">Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9328f-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="9328f-109">Se você tem uma rede virtual preferida, pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="9328f-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="9328f-110">Verifique se a rede virtual do Azure que você criar ou escolher usar com o Azure Active Directory Domain Services pertença a uma região do Azure com suporte pelo Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="9328f-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9328f-111">Para conhecer as regiões do Azure nas quais o Azure Active Directory Domain Services está disponível, confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="9328f-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="9328f-112">Anote o nome da rede virtual para selecionar a rede virtual correta ao habilitar o Azure Active Directory Domain Services em uma etapa de configuração subsequente.</span><span class="sxs-lookup"><span data-stu-id="9328f-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="9328f-113">Para criar uma rede virtual do Azure no qual você deseja habilitar o Azure Active Directory Domain Services, siga estas instruções de configuração:</span><span class="sxs-lookup"><span data-stu-id="9328f-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="9328f-114">Vá para o [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9328f-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9328f-115">No painel esquerdo, selecione **Redes**.</span><span class="sxs-lookup"><span data-stu-id="9328f-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="9328f-116">![Nó de redes](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="9328f-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="9328f-117">A janela **Redes Virtuais** é aberta.</span><span class="sxs-lookup"><span data-stu-id="9328f-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="9328f-118">No painel de tarefas na parte inferior da página, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="9328f-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="9328f-120">Clique em **Serviços de Rede**e selecione **Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="9328f-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Rede virtual - criação rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="9328f-122">Para criar uma rede virtual, clique em **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="9328f-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="9328f-123">Especifique um **nome** para sua rede virtual e considere o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9328f-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="9328f-124">Você pode optar por configurar o **Espaço de endereço** ou a **Contagem máxima de VMs** para essa rede.</span><span class="sxs-lookup"><span data-stu-id="9328f-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="9328f-125">Por enquanto, você pode deixar a configuração **Servidor DNS** definida como **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="9328f-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="9328f-126">Depois de habilitar o Azure Active Directory Domain Services, você pode atualizar a configuração.</span><span class="sxs-lookup"><span data-stu-id="9328f-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="9328f-127">Na lista suspensa **Local**, selecione uma região do Azure com suporte.</span><span class="sxs-lookup"><span data-stu-id="9328f-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="9328f-128">Para conhecer as regiões do Azure nas quais o Azure Active Directory Domain Services está disponível, confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="9328f-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="9328f-129">Para criar sua rede virtual, clique em **Criar uma Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="9328f-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Criar uma rede virtual para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="9328f-131">Depois de criar uma rede virtual, selecione o nome da rede virtual e clique na guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="9328f-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Criar uma sub-rede](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="9328f-133">Em **espaços de endereço de rede virtual**, clique em **adicionar sub-rede**e especifique uma sub-rede com o nome **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="9328f-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Criar uma sub-rede para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="9328f-135">Para criar a sub-rede, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9328f-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="9328f-136">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="9328f-136">Next step</span></span>
[<span data-ttu-id="9328f-137">Tarefa 3: habilitar o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="9328f-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
