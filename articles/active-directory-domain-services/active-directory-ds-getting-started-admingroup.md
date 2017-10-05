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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="c4831-103">Habilite o Azure Active Directory Domain Services usando o portal do Azure (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="c4831-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="c4831-104">Tarefa 3: configurar um grupo administrativo</span><span class="sxs-lookup"><span data-stu-id="c4831-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="c4831-105">Nesta tarefa de configuração, você cria um grupo administrativo em seu diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4831-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="c4831-106">Este grupo administrativo especial é chamado *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="c4831-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="c4831-107">Os membros desse grupo recebem permissões administrativas nos computadores ingressados no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c4831-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="c4831-108">Em computadores ingressados no domínio, esse grupo é adicionado ao grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="c4831-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="c4831-109">Além disso, os membros desse grupo também poderão usar a Área de Trabalho Remota para se conectar remotamente a computadores ingressados no domínio.</span><span class="sxs-lookup"><span data-stu-id="c4831-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="c4831-110">Você não tem permissões de Administrador de Domínio nem de Administrador Enterprise no domínio gerenciado criado com o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c4831-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="c4831-111">Em domínios gerenciados, essas permissões são reservadas pelo serviço e não são disponibilizadas aos usuários dentro do locatário.</span><span class="sxs-lookup"><span data-stu-id="c4831-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="c4831-112">No entanto, você poderá usar o grupo administrativo especial criado nesta tarefa de configuração para executar algumas operações privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="c4831-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="c4831-113">Essas operações incluem ingressar os computadores no domínio, pertencer ao grupo de administração em computadores ingressados no domínio e configurar a Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="c4831-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="c4831-114">O assistente cria automaticamente o grupo administrativo em seu diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4831-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="c4831-115">Esse grupo se chama "Administradores do AAD DC".</span><span class="sxs-lookup"><span data-stu-id="c4831-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="c4831-116">Se houver um grupo existente com esse nome em seu diretório do Azure AD, o assistente o selecionará.</span><span class="sxs-lookup"><span data-stu-id="c4831-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="c4831-117">Você pode configurar a associação ao grupo usando a página do assistente **Grupo de administradores**.</span><span class="sxs-lookup"><span data-stu-id="c4831-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="c4831-118">Para configurar a associação ao grupo, clique em **Administradores do AAD DC**.</span><span class="sxs-lookup"><span data-stu-id="c4831-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurar associação ao grupo](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="c4831-120">Clique no botão **Adicionar membros** para adicionar usuários de seu diretório do Azure AD ao grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="c4831-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="c4831-121">Quando terminar, clique em **OK** para ir para a página **Resumo** do assistente.</span><span class="sxs-lookup"><span data-stu-id="c4831-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="c4831-122">Na página **Resumo** do assistente, examine as definições de configuração do domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c4831-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="c4831-123">Você pode voltar para qualquer etapa do assistente para fazer alterações se for necessário.</span><span class="sxs-lookup"><span data-stu-id="c4831-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="c4831-124">Quando terminar, clique em **OK** para criar o novo domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c4831-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Resumo](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="c4831-126">Você verá uma notificação que mostra o andamento da implantação do Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c4831-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="c4831-127">Clique na notificação para ver detalhes do andamento da implantação.</span><span class="sxs-lookup"><span data-stu-id="c4831-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Notificação – implantação em andamento](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="c4831-129">Provisionar o domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="c4831-129">Provision your managed domain</span></span>
<span data-ttu-id="c4831-130">O processo de provisionamento de seu domínio gerenciado pode levar até uma hora.</span><span class="sxs-lookup"><span data-stu-id="c4831-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="c4831-131">Enquanto a implantação está em andamento, você pode pesquisar por "domain services" na caixa de pesquisa **Pesquisar recursos**.</span><span class="sxs-lookup"><span data-stu-id="c4831-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="c4831-132">Selecione **Azure AD Domain Services** nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c4831-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="c4831-133">A folha **Azure AD Domain Services** lista o domínio gerenciado que está sendo provisionado.</span><span class="sxs-lookup"><span data-stu-id="c4831-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="c4831-135">Clique no nome do domínio gerenciado (por exemplo, "contoso100.com") para ver mais detalhes sobre ele.</span><span class="sxs-lookup"><span data-stu-id="c4831-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="c4831-137">A guia **Visão Geral** mostra que o domínio está sendo provisionado.</span><span class="sxs-lookup"><span data-stu-id="c4831-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="c4831-138">Você não pode configurar o domínio gerenciado até que ele esteja totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="c4831-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="c4831-139">Pode levar até uma hora para que o domínio gerenciado seja totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="c4831-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="c4831-140">Serviços de domínio – guia Visão Geral no estado de provisionamento</span><span class="sxs-lookup"><span data-stu-id="c4831-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="c4831-141">Quando o domínio gerenciado está totalmente provisionado, a guia **Visão Geral** mostra o status do domínio como **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="c4831-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="c4831-143">Na guia **Propriedades**, você vê dois endereços IP nos quais controladores de domínio estão disponíveis para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c4831-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Serviços de domínio – guia Propriedades após a conclusão do provisionado](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="c4831-145">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="c4831-145">Next step</span></span>
<span data-ttu-id="c4831-146">Tarefa 4: [atualizar as configurações do DNS para a rede virtual do Azure](active-directory-ds-getting-started-dns.md)</span><span class="sxs-lookup"><span data-stu-id="c4831-146">[Task 4: update the DNS settings for the Azure virtual network](active-directory-ds-getting-started-dns.md)</span></span>
