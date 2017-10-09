---
title: "Azure AD Connect: Próximas etapas e como toomanage do Azure AD Connect | Microsoft Docs"
description: "Saiba como tooextend Olá tarefas operacionais e configuração padrão para o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="d666d-103">Próximas etapas e como toomanage do Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d666d-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="d666d-104">Use procedimentos operacionais Olá toomeet de conectar do Azure Active Directory (AD do Azure) de toocustomize este artigo necessidades e requisitos de sua organização.</span><span class="sxs-lookup"><span data-stu-id="d666d-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="d666d-105">Adicionar administradores de sincronização adicionais</span><span class="sxs-lookup"><span data-stu-id="d666d-105">Add additional sync admins</span></span>
<span data-ttu-id="d666d-106">Por padrão, o único usuário a saudação Olá administradores locais e instalação são toomanage capaz de mecanismo de sincronização de saudação instalado.</span><span class="sxs-lookup"><span data-stu-id="d666d-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="d666d-107">Para outras pessoas toobe capaz de tooaccess e gerenciar o mecanismo de sincronização Olá, localize Olá grupo denominado ADSyncAdmins no servidor de local de saudação e adicioná-los toothis grupo.</span><span class="sxs-lookup"><span data-stu-id="d666d-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="d666d-108">Atribuir licenças tooAzure os usuários do AD Premium e Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="d666d-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="d666d-109">Agora que os usuários tenham sido sincronizadas toohello nuvem, você precisa tooassign-los uma licença para eles podem começar a usar aplicativos de nuvem como o Office 365.</span><span class="sxs-lookup"><span data-stu-id="d666d-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="d666d-110">tooassign um Azure AD Premium ou Enterprise Mobility Suite licença</span><span class="sxs-lookup"><span data-stu-id="d666d-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="d666d-111">Entrar toohello portal do Azure como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d666d-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="d666d-112">Olá esquerda, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d666d-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d666d-113">Em Olá **do Active Directory** página, clique duas vezes no diretório Olá com usuários Olá desejar tooset.</span><span class="sxs-lookup"><span data-stu-id="d666d-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="d666d-114">Na parte superior de saudação da página de diretório Olá, selecione **licenças**.</span><span class="sxs-lookup"><span data-stu-id="d666d-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="d666d-115">Em Olá **licenças** página, selecione **Active Directory Premium** ou **Enterprise Mobility Suite**e, em seguida, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="d666d-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="d666d-116">Na caixa de diálogo Olá, selecione os usuários de saudação que deseja tooassign licenças para e, em seguida, clique em Olá marca de seleção ícone toosave Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="d666d-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="d666d-117">Verifique se a tarefa de sincronização agendada Olá</span><span class="sxs-lookup"><span data-stu-id="d666d-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="d666d-118">Use o status de saudação do hello toocheck portal do Azure de uma sincronização.</span><span class="sxs-lookup"><span data-stu-id="d666d-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="d666d-119">tarefa de sincronização agendada Olá tooverify</span><span class="sxs-lookup"><span data-stu-id="d666d-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="d666d-120">Entrar toohello portal do Azure como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d666d-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="d666d-121">Olá esquerda, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d666d-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d666d-122">Em Olá **do Active Directory** página, clique duas vezes no diretório Olá com usuários Olá desejar tooset.</span><span class="sxs-lookup"><span data-stu-id="d666d-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="d666d-123">Na parte superior de saudação da página de diretório Olá, selecione **integração de diretórios**.</span><span class="sxs-lookup"><span data-stu-id="d666d-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="d666d-124">Em **integração com o active directory local**, Olá Observação hora da última sincronização.</span><span class="sxs-lookup"><span data-stu-id="d666d-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="d666d-125"><center>![Horário de sincronização de diretórios](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="d666d-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="d666d-126">Iniciar uma tarefa de sincronização agendada</span><span class="sxs-lookup"><span data-stu-id="d666d-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="d666d-127">Se você precisar toorun uma tarefa de sincronização, você pode fazer isso executando o Assistente de conexão do AD do Azure Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="d666d-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="d666d-128">É necessário tooprovide suas credenciais do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d666d-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="d666d-129">No Assistente de saudação, selecione Olá **personalizar opções de sincronização** de tarefas e, em seguida, clique em **próximo** toomove por meio do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="d666d-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="d666d-130">No final da saudação, certifique-se de que Olá **iniciar o processo de sincronização de saudação assim que concluir a configuração inicial Olá** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="d666d-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="d666d-131"><center>![Iniciar a sincronização](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="d666d-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="d666d-132">Para obter mais informações sobre a sincronização do hello Azure AD Connect Agendador, consulte [o Agendador de conectar-se de AD do Azure](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="d666d-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="d666d-133">Tarefas adicionais disponíveis no Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d666d-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="d666d-134">Após a instalação inicial do Azure AD Connect, você pode sempre iniciar assistente Olá novamente de saudação do Azure AD Connect iniciar página ou área de trabalho um atalho.</span><span class="sxs-lookup"><span data-stu-id="d666d-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="d666d-135">Você observará que entrar novamente por meio do Assistente de saudação fornece algumas novas opções na forma de saudação de tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="d666d-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="d666d-136">Olá tabela a seguir fornece um resumo dessas tarefas e uma breve descrição de cada tarefa.</span><span class="sxs-lookup"><span data-stu-id="d666d-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lista de tarefas adicionais](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="d666d-138">Tarefa adicional</span><span class="sxs-lookup"><span data-stu-id="d666d-138">Additional task</span></span> | <span data-ttu-id="d666d-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="d666d-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d666d-140">**Cenário do modo de exibição Olá selecionado**</span><span class="sxs-lookup"><span data-stu-id="d666d-140">**View hello selected scenario**</span></span> |<span data-ttu-id="d666d-141">Exiba sua solução atual do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d666d-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="d666d-142">Isso inclui configurações gerais, diretórios sincronizados e configurações de sincronização.</span><span class="sxs-lookup"><span data-stu-id="d666d-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="d666d-143">**Personalizar opções de sincronização**</span><span class="sxs-lookup"><span data-stu-id="d666d-143">**Customize synchronization options**</span></span> |<span data-ttu-id="d666d-144">Alterar a configuração atual hello como adicionar configuração adicional de toohello de florestas do Active Directory ou habilitar as opções de sincronização, como usuário, grupo, dispositivo ou write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="d666d-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="d666d-145">**Habilitar o modo de preparo**</span><span class="sxs-lookup"><span data-stu-id="d666d-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="d666d-146">Informações de estágio que não estão sincronizadas imediatamente e não é exportado tooAzure AD ou do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="d666d-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="d666d-147">Com esse recurso, você pode visualizar as sincronizações Olá antes que eles ocorram.</span><span class="sxs-lookup"><span data-stu-id="d666d-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d666d-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d666d-148">Next steps</span></span>
<span data-ttu-id="d666d-149">Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d666d-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
