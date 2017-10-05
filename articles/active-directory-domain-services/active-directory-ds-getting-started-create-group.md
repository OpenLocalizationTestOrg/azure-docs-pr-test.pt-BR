---
title: "Azure Active Directory Domain Services: Criar o grupo de administradores de controladores de domínio do Azure AD | Microsoft Docs"
description: "Habilitar o Azure Active Directory Domain Services usando o portal clássico do Azure"
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="6b3e1-103">Habilitar o Azure Active Directory Domain Services usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6b3e1-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="6b3e1-104">Este artigo descreve e explica em detalhes as tarefas de configuração necessárias para habilitar o Azure AD DS (Azure Active Directory Domain Services) para seu locatário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6b3e1-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="6b3e1-105">[**Teste a experiência do novo portal do Azure (Versão prévia)**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b3e1-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="6b3e1-106">Tarefa 1: Criar o grupo de administradores de controladores de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b3e1-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="6b3e1-107">A primeira tarefa é criar um grupo administrativo em seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="6b3e1-108">Este grupo administrativo especial é chamado *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="6b3e1-109">Os membros desse grupo recebem permissões administrativas nos computadores ingressados no domínio ao domínio gerenciado pelo Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="6b3e1-110">Em computadores ingressados no domínio, esse grupo é adicionado ao grupo de administradores.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="6b3e1-111">Além disso, os membros desse grupo também poderão usar a Área de Trabalho Remota para se conectar remotamente a computadores ingressados no domínio.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="6b3e1-112">Você não tem permissões de Administrador de Domínio nem de Administrador Enterprise no domínio gerenciado criado com o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6b3e1-113">Em domínios gerenciados, essas permissões são reservadas pelo serviço e não são disponibilizadas aos usuários dentro do locatário.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="6b3e1-114">No entanto, você poderá usar o grupo administrativo especial criado nesta tarefa de configuração para executar algumas operações privilegiadas.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="6b3e1-115">Essas operações incluem ingressar os computadores no domínio, pertencer ao grupo de administração em computadores ingressados no domínio e configurar a Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="6b3e1-116">Nessa tarefa de configuração, você cria o grupo administrativo e adicionará um ou mais usuários em seu diretório ao grupo.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="6b3e1-117">Para criar o grupo administrativo para o Azure Active Directory Domain Services, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6b3e1-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="6b3e1-118">Acesse o [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6b3e1-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="6b3e1-119">No painel esquerdo, selecione o botão **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="6b3e1-120">Selecione o locatário do Azure AD (diretório) para o qual você deseja habilitar o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6b3e1-121">Você pode criar apenas um domínio para cada diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selecionar um diretório do Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="6b3e1-123">Na página **Diretório de visualização**, clique na guia **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="6b3e1-124">Para adicionar um grupo ao seu locatário do Azure AD, no painel de tarefas na parte inferior da página, clique em **Adicionar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![O botão Adicionar Grupo](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="6b3e1-126">Na caixa de diálogo **Adicionar Grupo**, crie um grupo chamado **Administradores de controladores de domínio do AAD** e, em seguida, defina **Tipo do Grupo** como **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="6b3e1-127">Para habilitar o acesso no domínio gerenciado pelo Azure Active Directory Domain Services, crie um grupo com esse mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![A caixa de diálogo Adicionar Grupo](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="6b3e1-129">Na caixa **Descrição**, insira uma descrição que permite que outras pessoas entendam que esse grupo concede permissões administrativas no Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="6b3e1-130">Depois de criar o grupo, clique no nome do grupo para exibir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="6b3e1-131">Para adicionar usuários como membros do grupo, na parte inferior da janela, clique no botão **Adicionar Membros**.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Botão Adicionar membros do grupo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="6b3e1-133">Na caixa de diálogo **Adicionar membros**, selecione os usuários que devem ser membros desse grupo e, em seguida, clique no ícone de marca de seleção no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="6b3e1-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Adicionar usuários ao grupo de administradores](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="6b3e1-135">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="6b3e1-135">Next step</span></span>
[<span data-ttu-id="6b3e1-136">Tarefa 2: Criar ou selecionar uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="6b3e1-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
