---
title: "Azure Active Directory Domain Services: introdução | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)"
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
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="e3ebc-103">Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="e3ebc-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="e3ebc-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e3ebc-104">Before you begin</span></span>
<span data-ttu-id="e3ebc-105">Consulte também[considerações de rede para o Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="e3ebc-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="e3ebc-106">Tarefa 2: definir as configurações de rede</span><span class="sxs-lookup"><span data-stu-id="e3ebc-106">Task 2: configure network settings</span></span>
<span data-ttu-id="e3ebc-107">a próxima tarefa de configuração Olá é toocreate uma rede virtual do Azure e uma sub-rede dedicada dentro dele.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="e3ebc-108">Você pode habilitar o Azure Active Directory Domain Services nessa sub-rede dentro de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="e3ebc-109">Você também pode escolher uma rede virtual existente e criar hello dedicado sub-rede dentro dele.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="e3ebc-110">Clique em **rede Virtual** tooselect uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="e3ebc-111">Em Olá **rede virtual escolha** folha, você vê todas as redes virtuais existentes.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="e3ebc-112">Consulte somente Olá redes virtuais que pertencem toohello grupo de recursos e local do Azure que você selecionou na Olá **Noções básicas sobre** página do assistente.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="e3ebc-113">Escolha Olá rede virtual no qual os serviços de domínio do AD do Azure devem ser habilitados.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="e3ebc-114">Clique em **criar novo**, se você preferir toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="e3ebc-115">É altamente recomendável usar uma sub-rede dedicada para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="e3ebc-116">Se você escolher uma rede virtual existente, [criar uma sub-rede dedicada usando a extensão de redes virtuais Olá](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e, em seguida, selecione nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Escolher rede virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="e3ebc-118">Clique em **sub-rede** toopick Olá sub-rede dedicada nessa rede virtual, no qual tooenable o domínio gerenciado seu novo.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="e3ebc-119">Em Olá **criar sub-rede** folha, especifique um nome para a sub-rede hello e clique em **Okey** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="e3ebc-120">Por exemplo, crie uma sub-rede com o nome de saudação 'DomainServices', tornando mais fácil para outros administradores toounderstand o que é implantado na sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Selecione a sub-rede na rede virtual Olá](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="e3ebc-122">**Diretrizes para selecionar uma sub-rede**</span><span class="sxs-lookup"><span data-stu-id="e3ebc-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="e3ebc-123">Use uma sub-rede dedicada para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="e3ebc-124">Não implante nenhuma outra sub-rede toothis de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="e3ebc-125">Essa configuração permite que você tooconfigure grupos de segurança de rede (NSGs) para as máquinas virtuais/cargas de trabalho sem interromper seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="e3ebc-126">Para obter detalhes, consulte as [Considerações de rede do Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="e3ebc-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="e3ebc-127">Não selecione a sub-rede de Gateway Olá para implantar serviços de domínio do AD do Azure, porque ele não é uma configuração com suporte.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="e3ebc-128">Certifique-se de sub-rede Olá selecionado tem espaço de endereço disponível suficiente - pelo menos 3 a 5 endereços IP.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="e3ebc-129">Quando terminar, clique em **Okey** toomove na toohello **grupo administrador** página do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3ebc-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="e3ebc-130">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="e3ebc-130">Next step</span></span>
[<span data-ttu-id="e3ebc-131">Tarefa 3: configurar o grupo administrativo e habilitar o Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="e3ebc-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
