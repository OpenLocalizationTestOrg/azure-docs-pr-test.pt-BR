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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="6ebc3-103">Habilite o Azure Active Directory Domain Services usando o portal do Azure (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="6ebc3-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="6ebc3-104">Este artigo mostra como habilitar o Azure AD DS (Azure Active Directory Domain Services) usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="6ebc3-105">Para iniciar o assistente **Habilitar Azure AD Domain Services**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6ebc3-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="6ebc3-106">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6ebc3-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6ebc3-107">No painel esquerdo, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="6ebc3-108">Na folha **Novo**, digite **Domain Services** na barra de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Pesquisa pelo Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="6ebc3-110">Clique para selecionar o **Azure AD Domain Services** na lista de sugestões de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="6ebc3-111">Na folha **Azure AD Domain Services**, clique no botão **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Folha do Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="6ebc3-113">O assistente **Habilitar Azure AD Domain Services** é iniciado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="6ebc3-114">Tarefa 1: definir as configurações básicas</span><span class="sxs-lookup"><span data-stu-id="6ebc3-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="6ebc3-115">Na página **Básico** do assistente, você pode especificar o nome de domínio DNS para o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="6ebc3-116">Você também pode escolher o grupo de recursos e o local do Azure no qual o domínio gerenciado deve ser implantado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Configurar os aspectos básicos](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="6ebc3-118">Escolha o **nome de domínio DNS** para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="6ebc3-119">O nome de domínio padrão do diretório (com um sufixo **.onmicrosoft.com**) é selecionado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="6ebc3-120">Você também pode inserir um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="6ebc3-121">Neste exemplo, o nome de domínio personalizado é *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="6ebc3-122">O prefixo do nome do domínio especificado (por exemplo, *contoso100* no nome de domínio *contoso100.com*) deve conter 15 caracteres ou menos.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="6ebc3-123">Você não pode criar um domínio gerenciado com um prefixo de mais de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="6ebc3-124">Garanta que o nome de domínio DNS escolhido para o domínio gerenciado ainda não exista na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="6ebc3-125">Especificamente, verifique se:</span><span class="sxs-lookup"><span data-stu-id="6ebc3-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="6ebc3-126">Você já tiver um domínio com o mesmo nome de domínio DNS na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="6ebc3-127">A rede virtual em que você planeja habilitar o domínio gerenciado tem uma conexão VPN com sua rede local.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="6ebc3-128">Nesse cenário, verifique se você não tem um domínio com o mesmo nome de domínio DNS na rede local.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="6ebc3-129">Você tiver um serviço de nuvem existente com esse nome na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="6ebc3-130">Escolha o **tipo de rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="6ebc3-131">Por padrão, o tipo de rede virtual **Gerenciador de Recursos** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="6ebc3-132">Recomendamos o uso desse tipo de rede virtual para todos os domínios gerenciados recém-criados.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="6ebc3-133">Selecione a **Assinatura** do Azure na qual você deseja criar o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="6ebc3-134">Selecione o **Grupo de recursos** a que o domínio gerenciado deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="6ebc3-135">Você pode escolher as opções **Criar novo** ou **Usar existente** para selecionar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="6ebc3-136">Escolha o **Local** do Azure no qual o domínio gerenciado deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="6ebc3-137">Na página **Rede** do assistente, você vê somente redes virtuais que pertencem ao local selecionado.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="6ebc3-138">Quando terminar, clique em **OK** para ir para a página **Rede** do assistente.</span><span class="sxs-lookup"><span data-stu-id="6ebc3-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="6ebc3-139">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6ebc3-139">Next step</span></span>
[<span data-ttu-id="6ebc3-140">Tarefa 2: definir as configurações de rede</span><span class="sxs-lookup"><span data-stu-id="6ebc3-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
