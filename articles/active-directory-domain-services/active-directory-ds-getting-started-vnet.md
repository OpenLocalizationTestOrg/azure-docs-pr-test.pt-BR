---
title: 'Azure Active Directory Domain Services: criar ou selecionar uma rede virtual | Microsoft Docs'
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
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
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="eb968-103">Criar ou selecionar uma rede virtual para o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="eb968-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="eb968-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="eb968-104">Before you begin</span></span>
<span data-ttu-id="eb968-105">Consulte também[considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="eb968-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="eb968-106">Tarefa 2: criar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="eb968-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="eb968-107">a próxima tarefa de configuração Olá é toocreate uma rede virtual do Azure e uma sub-rede dentro dele.</span><span class="sxs-lookup"><span data-stu-id="eb968-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="eb968-108">Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="eb968-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="eb968-109">Se você tiver uma rede virtual existente que você prefere toouse, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="eb968-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="eb968-110">Certifique-se de que Olá rede virtual do Azure crie ou escolha toouse com o Azure Active Directory Domain Services pertence tooan região do Azure que é compatível com o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="eb968-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="eb968-111">tooascertain Olá regiões do Azure em que o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="eb968-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="eb968-112">Anote o nome de saudação do hello tooensure de rede virtual que você selecione a rede virtual à direita hello quando você habilitar o Azure Active Directory Domain Services em uma etapa de configuração subsequentes.</span><span class="sxs-lookup"><span data-stu-id="eb968-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="eb968-113">toocreate uma rede virtual do Azure no qual você deseja tooenable do Azure Active Directory Domain Services, siga estas instruções de configuração:</span><span class="sxs-lookup"><span data-stu-id="eb968-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="eb968-114">Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="eb968-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="eb968-115">No painel esquerdo do hello, selecione **redes**.</span><span class="sxs-lookup"><span data-stu-id="eb968-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="eb968-116">![Nó de redes](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="eb968-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="eb968-117">Olá **redes virtuais** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="eb968-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="eb968-118">No painel de tarefas de saudação na parte inferior da saudação da janela hello, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="eb968-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Janela Redes virtuais](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="eb968-120">Clique em **Serviços de Rede**e selecione **Rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="eb968-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Rede virtual - criação rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="eb968-122">toocreate uma rede virtual, clique em **criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="eb968-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="eb968-123">Especifique um **nome** para sua máquina virtual, rede e considere o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="eb968-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="eb968-124">Você pode escolher tooconfigure **espaço de endereço** ou **contagem máxima de VMs** para essa rede.</span><span class="sxs-lookup"><span data-stu-id="eb968-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="eb968-125">Você pode deixar Olá **servidor DNS** definindo como **nenhum** por enquanto.</span><span class="sxs-lookup"><span data-stu-id="eb968-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="eb968-126">Você pode atualizar a configuração de saudação depois de habilitar o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="eb968-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="eb968-127">Em Olá **local** lista suspensa, selecione uma região do Azure com suporte.</span><span class="sxs-lookup"><span data-stu-id="eb968-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="eb968-128">tooascertain Olá regiões do Azure em que o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="eb968-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="eb968-129">toocreate sua rede virtual, clique em **criar uma rede Virtual**.</span><span class="sxs-lookup"><span data-stu-id="eb968-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Criar uma rede virtual para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="eb968-131">Depois de criar uma rede virtual, selecione Olá nome de rede virtual Olá e clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="eb968-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Criar uma sub-rede](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="eb968-133">Em **espaços de endereço de rede virtual**, clique em **Adicionar sub-rede**e, em seguida, especifique uma sub-rede com nome hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="eb968-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Criar uma sub-rede para o Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="eb968-135">toocreate Olá sub-rede, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb968-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="eb968-136">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="eb968-136">Next step</span></span>
[<span data-ttu-id="eb968-137">Tarefa 3: habilitar o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="eb968-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
