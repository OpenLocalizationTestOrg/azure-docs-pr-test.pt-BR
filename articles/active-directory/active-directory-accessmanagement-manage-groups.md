---
title: grupos de aaaManaging no Active Directory do Azure | Microsoft Docs
description: "Como toocreate e gerenciar grupos toomanage Azure usuários usando o Active Directory do Azure."
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
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="b4bca-103">Gerenciamento de grupos no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4bca-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4bca-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="b4bca-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="b4bca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4bca-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="b4bca-107">Um dos recursos de saudação do gerenciamento de usuários do Active Directory do Azure (AD do Azure) é grupos de toocreate de capacidade de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="b4bca-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="b4bca-108">Realizar tarefas de gerenciamento de tooperform um grupo como a atribuição de permissões ou licenças tooa o número de usuários de uma vez.</span><span class="sxs-lookup"><span data-stu-id="b4bca-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="b4bca-109">Você também pode usar grupos tooassign permissão de acesso</span><span class="sxs-lookup"><span data-stu-id="b4bca-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="b4bca-110">Recursos como objetos no diretório Olá</span><span class="sxs-lookup"><span data-stu-id="b4bca-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="b4bca-111">Diretório de toohello externo de recursos, como aplicativos SaaS, os serviços do Azure, sites do SharePoint ou recursos locais</span><span class="sxs-lookup"><span data-stu-id="b4bca-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="b4bca-112">Além disso, um proprietário do recurso também pode atribuir o grupo de AD do Azure tooan no acesso tooa recursos pertencente a outra pessoa.</span><span class="sxs-lookup"><span data-stu-id="b4bca-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="b4bca-113">Essa atribuição concede aos membros de saudação do recurso grupo acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="b4bca-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="b4bca-114">Em seguida, proprietário de saudação do grupo de saudação gerencia a associação no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4bca-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="b4bca-115">Efetivamente, Olá recurso proprietário delegados toohello proprietário do hello grupo Olá permissão tooassign usuários tootheir recurso.</span><span class="sxs-lookup"><span data-stu-id="b4bca-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4bca-116">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="b4bca-117">Para como toomanage os grupos no Centro de administração de saudação do AD do Azure, consulte [criar um grupo e adicionar membros no Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4bca-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="b4bca-118">Como faço para criar um grupo?</span><span class="sxs-lookup"><span data-stu-id="b4bca-118">How do I create a group?</span></span>
<span data-ttu-id="b4bca-119">Dependendo da saudação toowhich de serviços que sua organização tenha assinado, você pode criar um grupo usando uma das seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="b4bca-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="b4bca-120">Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-120">hello Azure classic portal</span></span>
* <span data-ttu-id="b4bca-121">portal de conta Olá Office 365</span><span class="sxs-lookup"><span data-stu-id="b4bca-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="b4bca-122">portal de conta do Windows Intune Olá</span><span class="sxs-lookup"><span data-stu-id="b4bca-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="b4bca-123">Descreveremos tarefas como executadas no hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4bca-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="b4bca-124">Para obter mais informações sobre como usar portais do Azure não toomanage seu diretório do AD do Azure, consulte [administrando seu diretório do AD do Azure](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="b4bca-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="b4bca-125">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.</span><span class="sxs-lookup"><span data-stu-id="b4bca-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="b4bca-126">Selecione Olá **grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="b4bca-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="b4bca-127">Selecione **Adicionar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="b4bca-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="b4bca-128">Em Olá **adicionar grupo** janela, especifique o nome de saudação e Olá descrição de um grupo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="b4bca-129">Como faço para adicionar ou remover usuários individuais em um grupo de segurança?</span><span class="sxs-lookup"><span data-stu-id="b4bca-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="b4bca-130">**tooadd um grupo de tooa de usuário individuais**</span><span class="sxs-lookup"><span data-stu-id="b4bca-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="b4bca-131">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.</span><span class="sxs-lookup"><span data-stu-id="b4bca-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="b4bca-132">Selecione Olá **grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="b4bca-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="b4bca-133">Abra Olá grupo toowhich tooadd membros.</span><span class="sxs-lookup"><span data-stu-id="b4bca-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="b4bca-134">Olá abrir **membros** guia da saudação grupo selecionado se ele ainda não estiver exibindo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="b4bca-135">Selecione **Adicionar Membros**.</span><span class="sxs-lookup"><span data-stu-id="b4bca-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="b4bca-136">Em Olá **adicionar membros** página, o nome de saudação select de Olá usuário ou grupo que você deseja tooadd como um membro desse grupo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="b4bca-137">Certifique-se de que esse nome está adicionado toohello **selecionados** painel.</span><span class="sxs-lookup"><span data-stu-id="b4bca-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="b4bca-138">**tooremove um usuário individual de um grupo**</span><span class="sxs-lookup"><span data-stu-id="b4bca-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="b4bca-139">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.</span><span class="sxs-lookup"><span data-stu-id="b4bca-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="b4bca-140">Selecione Olá **grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="b4bca-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="b4bca-141">Abra o grupo de saudação do qual você deseja tooremove membros.</span><span class="sxs-lookup"><span data-stu-id="b4bca-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="b4bca-142">Selecione Olá **membros** guia, nome selecione Olá Olá membro que você deseja tooremove deste grupo e, em seguida, clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="b4bca-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="b4bca-143">No prompt de hello, confirme se deseja tooremove esse membro do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4bca-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="b4bca-144">Como gerenciar a associação de saudação de um grupo dinamicamente?</span><span class="sxs-lookup"><span data-stu-id="b4bca-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="b4bca-145">No AD do Azure, você pode facilmente configurar um toodetermine regra simples quais usuários são membros de toobe do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4bca-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="b4bca-146">Uma regra simples é aquele que faz uma única comparação.</span><span class="sxs-lookup"><span data-stu-id="b4bca-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="b4bca-147">Por exemplo, se um grupo for atribuído tooa aplicativo SaaS, você pode configurar uma regra tooadd os usuários que têm um cargo de "Representante de vendas".</span><span class="sxs-lookup"><span data-stu-id="b4bca-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="b4bca-148">Essa regra, em seguida, concede acesso toothis usuários de tooall de aplicativos SaaS com esse cargo em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="b4bca-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="b4bca-149">Quando os atributos de uma alteração de usuário, sistema Olá avalia todas as regras de grupo dinâmico em um toosee de diretório se a alteração de atributo de saudação do usuário Olá dispararia qualquer grupo adiciona ou remove.</span><span class="sxs-lookup"><span data-stu-id="b4bca-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="b4bca-150">Se um usuário satisfizer uma regra em um grupo, eles são adicionados como um membro do grupo toothat.</span><span class="sxs-lookup"><span data-stu-id="b4bca-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="b4bca-151">Se eles não atendem mais regra Olá de um grupo, de que ele é membro, eles serão removidos como um membros desse grupo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="b4bca-152">Você pode configurar uma regra de associação dinâmica em grupos de segurança ou em grupos do Office 365.</span><span class="sxs-lookup"><span data-stu-id="b4bca-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="b4bca-153">Atualmente não há suporte a associações de grupo aninhado para tooapplications atribuição baseada em grupo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="b4bca-154">Associações dinâmicas para grupos requerem uma toobe de licença do Azure AD Premium atribuída a</span><span class="sxs-lookup"><span data-stu-id="b4bca-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="b4bca-155">administrador de saudação que gerencia a regra Olá em um grupo</span><span class="sxs-lookup"><span data-stu-id="b4bca-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="b4bca-156">Todos os membros do grupo de saudação</span><span class="sxs-lookup"><span data-stu-id="b4bca-156">All members of hello group</span></span>
>
>

<span data-ttu-id="b4bca-157">**associação dinâmica tooenable para um grupo**</span><span class="sxs-lookup"><span data-stu-id="b4bca-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="b4bca-158">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e selecione o nome de saudação do diretório de saudação de sua organização.</span><span class="sxs-lookup"><span data-stu-id="b4bca-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="b4bca-159">Selecione Olá **grupos** guia e grupo Olá abrir deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="b4bca-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="b4bca-160">Selecione Olá **configurar** guia e, em seguida, defina **habilitar associações dinâmicas** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="b4bca-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="b4bca-161">Configurar uma única regra simple para Olá grupo toocontrol a associação dinâmica para funções desse grupo.</span><span class="sxs-lookup"><span data-stu-id="b4bca-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="b4bca-162">Verifique se Olá **adicionar usuários onde** opção está selecionada e, em seguida, selecione uma propriedade de usuário na lista de hello (por exemplo, departamento, jobTitle, etc.)</span><span class="sxs-lookup"><span data-stu-id="b4bca-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="b4bca-163">Em seguida, selecione uma condição (Não É Igual a, Igual a, Não Começa com, Começa com, Não Contém, Contém, Não Corresponde, Corresponde).</span><span class="sxs-lookup"><span data-stu-id="b4bca-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="b4bca-164">Especifique um valor de comparação para a propriedade de usuário de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="b4bca-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="b4bca-165">toolearn sobre como toocreate *avançados* regra (regras que podem conter várias comparações) para a associação de grupo dinâmico, consulte [usar atributos toocreate regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="b4bca-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="b4bca-166">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="b4bca-166">Additional information</span></span>
<span data-ttu-id="b4bca-167">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4bca-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="b4bca-168">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="b4bca-169">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="b4bca-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="b4bca-170">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b4bca-171">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="b4bca-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="b4bca-172">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b4bca-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
