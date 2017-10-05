---
title: "Azure Active Directory Domain Services: introdução | Microsoft Docs"
description: "Habilite o Azure Active Directory Domain Services usando o portal do Azure (Versão prévia)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="d7aff-103">Habilite o Azure Active Directory Domain Services usando o portal do Azure (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="d7aff-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d7aff-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d7aff-104">Before you begin</span></span>
<span data-ttu-id="d7aff-105">Consulte as [Considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="d7aff-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="d7aff-106">Tarefa 2: definir as configurações de rede</span><span class="sxs-lookup"><span data-stu-id="d7aff-106">Task 2: configure network settings</span></span>
<span data-ttu-id="d7aff-107">A próxima tarefa de configuração é criar uma rede virtual do Azure e uma sub-rede dedicada dentro dela.</span><span class="sxs-lookup"><span data-stu-id="d7aff-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="d7aff-108">Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d7aff-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="d7aff-109">Você também pode escolher uma rede virtual existente e criar a sub-rede dedicada dentro dela.</span><span class="sxs-lookup"><span data-stu-id="d7aff-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="d7aff-110">Clique em **Rede virtual** para selecionar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d7aff-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="d7aff-111">Na folha **Escolher rede virtual**, você vê todas as redes virtuais desejadas.</span><span class="sxs-lookup"><span data-stu-id="d7aff-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="d7aff-112">Você vê somente as redes virtuais que pertencem ao grupo de recursos e ao local do Azure que selecionou na página do assistente **Básico**.</span><span class="sxs-lookup"><span data-stu-id="d7aff-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="d7aff-113">Selecione a rede virtual na qual o Azure AD Domain Services deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="d7aff-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="d7aff-114">Clique em **Criar novo** se preferir criar uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d7aff-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="d7aff-115">É altamente recomendável usar uma sub-rede dedicada para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d7aff-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="d7aff-116">Se você escolher uma rede virtual existente, [crie uma sub-rede dedicada usando a extensão de redes virtuais](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e, em seguida, selecione essa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d7aff-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Escolher rede virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="d7aff-118">Clique em **Sub-rede** para escolher a sub-rede dedicada nessa rede virtual, na qual você deseja habilitar o novo domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d7aff-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="d7aff-119">Na folha **Criar sub-rede**, especifique um nome para a sub-rede e clique em **OK** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="d7aff-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="d7aff-120">Por exemplo, crie uma sub-rede com o nome "DomainServices", tornando mais fácil para outros administradores entender o que está implantado dentro da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d7aff-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Escolher sub-rede na rede virtual](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="d7aff-122">**Diretrizes para selecionar uma sub-rede**</span><span class="sxs-lookup"><span data-stu-id="d7aff-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="d7aff-123">Use uma sub-rede dedicada para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d7aff-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="d7aff-124">Não implante nenhuma outra máquina virtual nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d7aff-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="d7aff-125">Essa configuração permite que você configure NSGs (grupos de segurança de rede) para suas máquinas virtuais/cargas de trabalho sem interromper seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d7aff-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="d7aff-126">Para obter detalhes, consulte as [Considerações de rede do Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="d7aff-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="d7aff-127">Não selecione a sub-rede do Gateway para implantar o Azure AD Domain Services, pois essa não é uma configuração com suporte.</span><span class="sxs-lookup"><span data-stu-id="d7aff-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="d7aff-128">Verifique se a sub-rede que você selecionou tem espaço de endereço disponível suficiente – pelo menos 3 a 5 endereços IP.</span><span class="sxs-lookup"><span data-stu-id="d7aff-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="d7aff-129">Quando terminar, clique em **OK** para ir para a página **Grupo de administradores** do assistente.</span><span class="sxs-lookup"><span data-stu-id="d7aff-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="d7aff-130">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="d7aff-130">Next step</span></span>
[<span data-ttu-id="d7aff-131">Tarefa 3: configurar o grupo administrativo e habilitar o Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="d7aff-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
