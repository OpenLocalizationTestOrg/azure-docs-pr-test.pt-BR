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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="0e1f6-103">Habilitar o Azure Active Directory Domain Services usando Olá portal do Azure (visualização)</span><span class="sxs-lookup"><span data-stu-id="0e1f6-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="0e1f6-104">Tarefa 3: configurar um grupo administrativo</span><span class="sxs-lookup"><span data-stu-id="0e1f6-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="0e1f6-105">Nesta tarefa de configuração, você cria um grupo administrativo em seu diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="0e1f6-106">Este grupo administrativo especial é chamado *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="0e1f6-107">Os membros deste grupo recebem permissões administrativas nos computadores com domínio gerenciado toohello ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="0e1f6-108">Em computadores que ingressaram no domínio, esse grupo é adicionado toohello grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="0e1f6-109">Além disso, os membros desse grupo podem usar a área de trabalho remota tooconnect remotamente toodomain-computadores que ingressaram no.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="0e1f6-110">Você não tem permissões de administrador de domínio ou administrador corporativo no hello domínio gerenciado que você criou usando o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="0e1f6-111">Em domínios gerenciados, essas permissões são reservadas pelo serviço hello em não ficam disponíveis toousers dentro do locatário hello.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="0e1f6-112">No entanto, você pode usar o grupo administrativo especial Olá criado no tooperform de tarefa configuração algumas operações privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="0e1f6-113">Essas operações incluem ingressar em domínio toohello dos computadores que pertencem a grupo de administração de toohello em computadores que ingressaram no domínio e configurar política de grupo.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="0e1f6-114">Assistente de saudação cria automaticamente o grupo administrativo Olá em seu diretório do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="0e1f6-115">Esse grupo se chama "Administradores do AAD DC".</span><span class="sxs-lookup"><span data-stu-id="0e1f6-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="0e1f6-116">Se você tiver um grupo existente com esse nome no diretório do AD do Azure, o Assistente de saudação seleciona esse grupo.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="0e1f6-117">Você pode configurar a associação de grupo usando Olá **grupo administrador** página do assistente.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="0e1f6-118">associação de grupo tooconfigure, clique em **AAD DC administradores**.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurar associação ao grupo](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="0e1f6-120">Clique em Olá **adicionar membros** botão tooadd usuários do seu grupo de administradores do AD do Azure diretório toohello.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="0e1f6-121">Quando terminar, clique em **Okey** toomove na toohello **resumo** página do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="0e1f6-122">Em Olá **resumo** página do Assistente de saudação, examine Olá configurações de domínio gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="0e1f6-123">Você pode voltar tooany etapa do assistente toomake altera o hello, se necessário.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="0e1f6-124">Quando terminar, clique em **Okey** toocreate Olá gerenciados novo domínio.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Resumo](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="0e1f6-126">Você verá uma notificação que mostra o andamento da saudação da sua implantação de serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="0e1f6-127">Clique em notificação Olá toosee detalhadas progresso para a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Notificação – implantação em andamento](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="0e1f6-129">Provisionar o domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="0e1f6-129">Provision your managed domain</span></span>
<span data-ttu-id="0e1f6-130">Olá processo de provisionamento de seu domínio gerenciado pode levar horas tooan.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="0e1f6-131">Durante a implantação está em andamento, você pode procurar 'Serviços de domínio' hello **pesquisar recursos** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="0e1f6-132">Selecione **serviços de domínio do AD do Azure** Olá resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="0e1f6-133">Olá **serviços de domínio do AD do Azure** folha lista Olá domínio gerenciado que está sendo provisionado.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="0e1f6-135">Clique o nome de saudação do hello gerenciado toosee de domínio (por exemplo, ' contoso100.com') mais detalhes sobre o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="0e1f6-137">Olá **visão geral** guia mostra esse domínio hello está atualmente sendo provisionado.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="0e1f6-138">Você não pode configurar o domínio gerenciado Olá até que ele está totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="0e1f6-139">Pode levar até horas tooan para sua toobe domínio gerenciado totalmente provisionado.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="0e1f6-140">Serviços de domínio - guia de visão geral durante a saudação estado de provisionamento</span><span class="sxs-lookup"><span data-stu-id="0e1f6-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="0e1f6-141">Quando o domínio gerenciado hello está totalmente provisionado, Olá **visão geral** guia mostra o status de domínio hello como **executando**.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services - guia Visão geral depois de totalmente provisionado](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="0e1f6-143">Em Olá **propriedades** guia, você ver dois endereços IP no qual domínio os controladores estão disponíveis para rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="0e1f6-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Serviços de domínio – guia Propriedades após a conclusão do provisionado](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="0e1f6-145">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="0e1f6-145">Next step</span></span>
[<span data-ttu-id="0e1f6-146">Tarefa 4: atualizar configurações de DNS Olá Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0e1f6-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
