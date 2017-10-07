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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="27284-103">Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="27284-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="27284-104">Este artigo mostra como tooenable do Azure Active Directory serviços de domínio (do Azure AD DS) usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27284-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="27284-105">Olá toolaunch **serviços de domínio de AD do Azure permitem** Olá assistente, concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27284-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="27284-106">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27284-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27284-107">No painel esquerdo do hello, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="27284-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="27284-108">Em Olá **novo** folha, digite **dos serviços de domínio** na barra de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="27284-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Pesquisa pelo Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="27284-110">Clique em tooselect **serviços de domínio do AD do Azure** de lista de saudação de sugestões de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="27284-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="27284-111">Em Olá **serviços de domínio do AD do Azure** folha, clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="27284-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Folha do Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="27284-113">Olá **serviços de domínio de AD do Azure permitem** assistente é iniciado.</span><span class="sxs-lookup"><span data-stu-id="27284-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="27284-114">Tarefa 1: definir as configurações básicas</span><span class="sxs-lookup"><span data-stu-id="27284-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="27284-115">Em Olá **Noções básicas sobre** página do Assistente para Olá, você pode especificar o nome de domínio DNS Olá para o domínio gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="27284-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="27284-116">Você também pode escolher o grupo de recursos de saudação e domínio gerenciado de saudação do local do Azure toowhich deve ser implantado.</span><span class="sxs-lookup"><span data-stu-id="27284-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Configurar os aspectos básicos](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="27284-118">Escolha Olá **nome de domínio DNS** para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="27284-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="27284-119">nome de domínio saudação padrão do diretório de saudação (com um **. c o m** sufixo) é especificada por padrão.</span><span class="sxs-lookup"><span data-stu-id="27284-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="27284-120">Você também pode inserir um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="27284-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="27284-121">Neste exemplo, é o nome de domínio personalizado Olá *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="27284-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="27284-122">prefixo de saudação do seu nome de domínio especificado (por exemplo, *contoso100* em Olá *contoso100.com* nome de domínio) deve conter a 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="27284-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="27284-123">Você não pode criar um domínio gerenciado com um prefixo de mais de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="27284-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="27284-124">Verifique se esse nome de domínio DNS Olá escolhido para Olá gerenciado domínio ainda não existir na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="27284-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="27284-125">Especificamente, verifique se:</span><span class="sxs-lookup"><span data-stu-id="27284-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="27284-126">Você já tiver um domínio com hello mesmo nome de domínio DNS na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="27284-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="27284-127">rede virtual Hello, onde você planeja tooenable Olá gerenciado domínio tem uma conexão VPN com a sua rede local.</span><span class="sxs-lookup"><span data-stu-id="27284-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="27284-128">Nesse cenário, verifique se você não tiver um domínio com hello mesmo nome de domínio DNS na rede local.</span><span class="sxs-lookup"><span data-stu-id="27284-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="27284-129">Você tem um serviço de nuvem existente com esse nome na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="27284-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="27284-130">Escolha Olá **tipo de rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="27284-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="27284-131">Por padrão, Olá **Gerenciador de recursos** tipo de rede virtual está selecionado.</span><span class="sxs-lookup"><span data-stu-id="27284-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="27284-132">Recomendamos o uso desse tipo de rede virtual para todos os domínios gerenciados recém-criados.</span><span class="sxs-lookup"><span data-stu-id="27284-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="27284-133">Selecione hello Azure **assinatura** em que você gostaria que toocreate Olá gerenciado domínio.</span><span class="sxs-lookup"><span data-stu-id="27284-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="27284-134">Selecione Olá **grupo de recursos** toowhich Olá gerenciado domínio deve pertencer.</span><span class="sxs-lookup"><span data-stu-id="27284-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="27284-135">Você pode escolher qualquer Olá **criar novo** ou **usar existente** grupo de recursos opções tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="27284-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="27284-136">Escolha hello Azure **local** em qual Olá domínio gerenciado deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="27284-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="27284-137">Em Olá **rede** página do Assistente de saudação, você ver as redes virtuais só pertencem toohello local selecionado.</span><span class="sxs-lookup"><span data-stu-id="27284-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="27284-138">Quando terminar, clique em **Okey** toomove na toohello **rede** página do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="27284-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="27284-139">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="27284-139">Next step</span></span>
[<span data-ttu-id="27284-140">Tarefa 2: definir as configurações de rede</span><span class="sxs-lookup"><span data-stu-id="27284-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
