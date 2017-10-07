---
title: "Serviços do Azure Active Directory domínio: Criar o grupo de administradores do controlador de domínio de saudação do AD do Azure | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="6583d-103">Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6583d-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="6583d-104">Este artigo descreve e orienta durante as tarefas de configuração de saudação que são necessárias para você tooenable do Azure Active Directory serviços de domínio (Azure AD DS) para seu locatário do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="6583d-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="6583d-105">[**Tente a nova experiência do portal (visualização) do Azure Olá em vez disso,**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6583d-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="6583d-106">Tarefa 1: criar o grupo de administradores do controlador de domínio de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6583d-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="6583d-107">Olá primeira tarefa é toocreate um grupo administrativo em seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6583d-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="6583d-108">Este grupo administrativo especial é chamado *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="6583d-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="6583d-109">Os membros deste grupo recebem permissões administrativas nos computadores que ingressaram no domínio toohello gerenciado do Azure Active Directory Domain Services domínio.</span><span class="sxs-lookup"><span data-stu-id="6583d-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="6583d-110">Em computadores que ingressaram no domínio, esse grupo é adicionado toohello grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="6583d-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="6583d-111">Além disso, os membros desse grupo podem usar a área de trabalho remota tooconnect remotamente toodomain-computadores que ingressaram no.</span><span class="sxs-lookup"><span data-stu-id="6583d-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="6583d-112">Você não tem permissões de administrador de domínio ou administrador corporativo no hello domínio gerenciado que você criou usando o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6583d-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6583d-113">Em domínios gerenciados, essas permissões são reservadas pelo serviço hello em não ficam disponíveis toousers dentro do locatário hello.</span><span class="sxs-lookup"><span data-stu-id="6583d-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="6583d-114">No entanto, você pode usar o grupo administrativo especial Olá criado no tooperform de tarefa configuração algumas operações privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="6583d-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="6583d-115">Essas operações incluem ingressar em domínio toohello dos computadores que pertencem a grupo de administração de toohello em computadores que ingressaram no domínio e configurar política de grupo.</span><span class="sxs-lookup"><span data-stu-id="6583d-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="6583d-116">Esta tarefa de configuração, criar grupo administrativo hello e adicionar um ou mais usuários no grupo de toohello de diretório.</span><span class="sxs-lookup"><span data-stu-id="6583d-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="6583d-117">grupo administrativo do toocreate Olá para o Azure Active Directory Domain Services, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="6583d-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="6583d-118">Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6583d-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6583d-119">No painel esquerdo do hello, selecione Olá **do Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="6583d-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="6583d-120">Selecione o locatário de AD do Azure hello (diretório) para o qual você deseja que o Azure tooenable serviços de domínio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6583d-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6583d-121">Você pode criar apenas um domínio para cada diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6583d-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selecionar um diretório do Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="6583d-123">Em Olá **directory visualização** , clique em Olá **grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="6583d-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="6583d-124">clique de um locatário de grupo tooyour AD do Azure, no painel de tarefas de saudação na parte inferior da saudação da janela de saudação tooadd **adicionar grupo**.</span><span class="sxs-lookup"><span data-stu-id="6583d-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![botão Adicionar grupo de saudação](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="6583d-126">Em Olá **adicionar grupo** caixa de diálogo caixa, crie um grupo chamado **AAD DC administradores**e, em seguida, defina **tipo de grupo** muito**segurança**.</span><span class="sxs-lookup"><span data-stu-id="6583d-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="6583d-127">acesso de tooenable em seu domínio gerenciado do Azure Active Directory Domain Services, crie um grupo com esse nome exato.</span><span class="sxs-lookup"><span data-stu-id="6583d-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![caixa de diálogo Adicionar grupo Olá](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="6583d-129">Em Olá **descrição** , digite uma descrição que permite que outras pessoas toounderstand neste grupo concede permissões administrativas no Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6583d-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="6583d-130">Depois de criar o grupo de hello, clique em tooview de nome de grupo Olá suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6583d-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="6583d-131">tooadd usuários como membros do grupo de hello, na parte inferior da saudação da janela de saudação, clique em Olá **adicionar membros** botão.</span><span class="sxs-lookup"><span data-stu-id="6583d-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Botão Adicionar membros do grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="6583d-133">Em Olá **adicionar membros** caixa de diálogo, os usuários de saudação select que devem ser membros desse grupo e clique no ícone de marca de seleção de saudação em hello inferior direito.</span><span class="sxs-lookup"><span data-stu-id="6583d-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Adicionar grupo de usuários do tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="6583d-135">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6583d-135">Next step</span></span>
[<span data-ttu-id="6583d-136">Tarefa 2: Criar ou selecionar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="6583d-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
