---
title: Gerenciamento de grupos no Azure Active Directory | Microsoft Docs
description: "Como criar e gerenciar grupos para gerenciar usuários do Azure usando o Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="07908-103">Gerenciamento de grupos no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07908-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07908-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="07908-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="07908-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07908-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="07908-107">Um dos recursos de gerenciamento de usuários do Azure AD (Azure Active Directory) é a capacidade de criar grupos de usuários.</span><span class="sxs-lookup"><span data-stu-id="07908-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="07908-108">Você pode usar um grupo para executar tarefas de gerenciamento, como a atribuição de licenças ou permissões a vários usuários de uma vez.</span><span class="sxs-lookup"><span data-stu-id="07908-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="07908-109">Você também pode usar grupos para atribuir a permissão de acesso a</span><span class="sxs-lookup"><span data-stu-id="07908-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="07908-110">Recursos como objetos no diretório</span><span class="sxs-lookup"><span data-stu-id="07908-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="07908-111">Recursos externos para o diretório, como aplicativos SaaS, serviços do Azure, sites do SharePoint ou recursos locais</span><span class="sxs-lookup"><span data-stu-id="07908-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="07908-112">Além disso, o proprietário do recurso também pode atribuir acesso a um recurso a um grupo do Azure AD pertencente a outra pessoa.</span><span class="sxs-lookup"><span data-stu-id="07908-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="07908-113">Essa atribuição concede acesso ao recurso aos membros desse grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="07908-114">Em seguida, o proprietário do grupo gerencia a associação ao grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="07908-115">Efetivamente, o proprietário do recurso delega ao proprietário do grupo a permissão de atribuir usuários aos seus recursos.</span><span class="sxs-lookup"><span data-stu-id="07908-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07908-116">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="07908-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="07908-117">Para saber como gerenciar grupos no Centro de administração do Azure AD, confira [Criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07908-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="07908-118">Como faço para criar um grupo?</span><span class="sxs-lookup"><span data-stu-id="07908-118">How do I create a group?</span></span>
<span data-ttu-id="07908-119">Dependendo dos serviços que sua organização assinou, você pode criar um grupo usando um dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="07908-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="07908-120">o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-120">the Azure classic portal</span></span>
* <span data-ttu-id="07908-121">o portal da conta do Office 365</span><span class="sxs-lookup"><span data-stu-id="07908-121">the Office 365 account portal</span></span>
* <span data-ttu-id="07908-122">o portal da conta do Windows Intune</span><span class="sxs-lookup"><span data-stu-id="07908-122">the Windows Intune account portal</span></span>

<span data-ttu-id="07908-123">Descreveremos as tarefas da forma como são realizadas no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="07908-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="07908-124">Para saber mais sobre como usar portais que não são do Azure para gerenciar seu diretório do Azure AD, confira [Administrar seu diretório do Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="07908-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="07908-125">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e o nome do diretório de sua organização.</span><span class="sxs-lookup"><span data-stu-id="07908-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="07908-126">Selecione a guia **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="07908-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="07908-127">Selecione **Adicionar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="07908-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="07908-128">Na janela **Adicionar grupo** , especifique o nome e a descrição de um grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="07908-129">Como faço para adicionar ou remover usuários individuais em um grupo de segurança?</span><span class="sxs-lookup"><span data-stu-id="07908-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="07908-130">**Para adicionar um usuário individual a um grupo**</span><span class="sxs-lookup"><span data-stu-id="07908-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="07908-131">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e o nome do diretório de sua organização.</span><span class="sxs-lookup"><span data-stu-id="07908-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="07908-132">Selecione a guia **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="07908-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="07908-133">Abra o grupo ao qual você deseja adicionar membros.</span><span class="sxs-lookup"><span data-stu-id="07908-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="07908-134">Abra a guia **Membros** do grupo selecionado, se ela ainda não estiver sendo exibida.</span><span class="sxs-lookup"><span data-stu-id="07908-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="07908-135">Selecione **Adicionar Membros**.</span><span class="sxs-lookup"><span data-stu-id="07908-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="07908-136">Na página **Adicionar Membros** , selecione o nome do usuário ou um grupo que você deseja adicionar como membro do grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="07908-137">Verifique se esse nome é adicionado ao painel **Selecionados** .</span><span class="sxs-lookup"><span data-stu-id="07908-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="07908-138">**Para remover um usuário individual de um grupo**</span><span class="sxs-lookup"><span data-stu-id="07908-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="07908-139">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e o nome do diretório de sua organização.</span><span class="sxs-lookup"><span data-stu-id="07908-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="07908-140">Selecione a guia **Grupos** .</span><span class="sxs-lookup"><span data-stu-id="07908-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="07908-141">Abra o grupo do qual deseja remover membros.</span><span class="sxs-lookup"><span data-stu-id="07908-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="07908-142">Selecione a guia **Membros** e o nome do membro que você deseja remover do grupo e clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="07908-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="07908-143">No prompt, confirme que você deseja remover esse membro do grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="07908-144">Como posso gerenciar a associação de um grupo dinamicamente?</span><span class="sxs-lookup"><span data-stu-id="07908-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="07908-145">No Azure AD, você pode configurar com facilidade uma regra simples para determinar quais usuários devem ser membros do grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="07908-146">Uma regra simples é aquele que faz uma única comparação.</span><span class="sxs-lookup"><span data-stu-id="07908-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="07908-147">Por exemplo, se um grupo for atribuído a um aplicativo SaaS, você poderá configurar uma regra para adicionar usuários que têm o cargo de "Representante de Vendas".</span><span class="sxs-lookup"><span data-stu-id="07908-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="07908-148">Essa regra concede então acesso ao aplicativo SaaS para todos os usuários com esse cargo no diretório.</span><span class="sxs-lookup"><span data-stu-id="07908-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="07908-149">Quando os atributos de um usuário são alterados, o sistema avalia todas as regras de grupo dinâmicas em um diretório para ver se a alteração do atributo do usuário dispararia adições ou remoções de grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="07908-150">Se um usuário atender a uma regra em um grupo, ele será adicionado como membro a esse grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="07908-151">Se ele não satisfizer mais à regra de um grupo do qual é membro, será removido do grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="07908-152">Você pode configurar uma regra de associação dinâmica em grupos de segurança ou em grupos do Office 365.</span><span class="sxs-lookup"><span data-stu-id="07908-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="07908-153">Atualmente não há suporte a associações de grupo aninhadas para atribuição com base em grupo para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07908-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="07908-154">As associações dinâmicas de grupos exigem que uma licença do Azure AD Premium seja atribuída a</span><span class="sxs-lookup"><span data-stu-id="07908-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="07908-155">O administrador que gerencia a regra em um grupo</span><span class="sxs-lookup"><span data-stu-id="07908-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="07908-156">Todos os membros do grupo</span><span class="sxs-lookup"><span data-stu-id="07908-156">All members of the group</span></span>
>
>

<span data-ttu-id="07908-157">**Para habilitar a associação dinâmica a um grupo**</span><span class="sxs-lookup"><span data-stu-id="07908-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="07908-158">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e o nome do diretório de sua organização.</span><span class="sxs-lookup"><span data-stu-id="07908-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="07908-159">Selecione a guia **Grupos** e abra o grupo que você deseja editar.</span><span class="sxs-lookup"><span data-stu-id="07908-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="07908-160">Selecione a guia **Configurar** e defina **Habilitar Associações Dinâmicas** como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="07908-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="07908-161">Configure uma única regra simples para que o grupo controle o funcionamento da associação dinâmica para esse grupo.</span><span class="sxs-lookup"><span data-stu-id="07908-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="07908-162">Verifique se a opção **Adicionar usuários em que** está marcada e selecione uma propriedade de usuário na lista (por exemplo, departamento, jobTitle, etc.)</span><span class="sxs-lookup"><span data-stu-id="07908-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="07908-163">Em seguida, selecione uma condição (Não É Igual a, Igual a, Não Começa com, Começa com, Não Contém, Contém, Não Corresponde, Corresponde).</span><span class="sxs-lookup"><span data-stu-id="07908-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="07908-164">Especifique um valor de comparação para a propriedade de usuário selecionada.</span><span class="sxs-lookup"><span data-stu-id="07908-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="07908-165">Para saber mais sobre como criar regras *avançadas* (regras que podem conter várias comparações) para a associação dinâmica de grupo, confira [Uso de atributos para criar regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="07908-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="07908-166">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="07908-166">Additional information</span></span>
<span data-ttu-id="07908-167">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="07908-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="07908-168">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="07908-169">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="07908-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="07908-170">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="07908-171">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="07908-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="07908-172">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="07908-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
