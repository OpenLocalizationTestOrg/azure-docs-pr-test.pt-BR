---
title: "Azure AD Connect: próximas etapas e como gerenciar o Azure AD Connect | Microsoft Docs"
description: "Aprenda a estender configuração padrão e tarefas operacionais para o Azure AD Connect."
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
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="d3ce7-103">Próximas etapas e como gerenciar o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d3ce7-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="d3ce7-104">Use os procedimentos operacionais neste artigo para personalizar o Azure AD (Azure Active Directory) Connect para atender às necessidades e requisitos de sua organização.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="d3ce7-105">Adicionar administradores de sincronização adicionais</span><span class="sxs-lookup"><span data-stu-id="d3ce7-105">Add additional sync admins</span></span>
<span data-ttu-id="d3ce7-106">Por padrão, somente o usuário que fez a instalação e os administradores locais podem gerenciar o mecanismo de sincronização instalado.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="d3ce7-107">Para que outras pessoas possam acessar e gerenciar o mecanismo de sincronização, localize o grupo chamado ADSyncAdmins no servidor local e adicione-os a esse grupo.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="d3ce7-108">Atribuir licenças aos usuários do Azure AD Premium e do Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="d3ce7-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="d3ce7-109">Agora que os usuários foram sincronizados para a nuvem, você precisará atribuir uma licença para que eles possam começar a usar aplicativos de nuvem como o Office 365.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="d3ce7-110">Como atribuir uma licença do Enterprise Mobility Suite ou do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="d3ce7-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="d3ce7-111">Entre no Portal do Azure como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="d3ce7-112">Selecione **Active Directory**à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d3ce7-113">Na página do **Active Directory**, clique duas vezes no diretório que tem os usuários que você deseja configurar.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="d3ce7-114">Na parte superior da página do diretório, selecione **Licenças**.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="d3ce7-115">Na página **Licenças**, selecione **Active Directory Premium** ou **Enterprise Mobility Suite** e, em seguida, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="d3ce7-116">Na caixa de diálogo, selecione os usuários para os quais você deseja atribuir licenças e, em seguida, clique no ícone de marca de seleção para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="d3ce7-117">Verificar a tarefa de sincronização agendada</span><span class="sxs-lookup"><span data-stu-id="d3ce7-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="d3ce7-118">Use o Portal do Azure para verificar o status de uma sincronização.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="d3ce7-119">Como verificar a tarefa de sincronização agendada</span><span class="sxs-lookup"><span data-stu-id="d3ce7-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="d3ce7-120">Entre no Portal do Azure como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="d3ce7-121">Selecione **Active Directory**à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d3ce7-122">Na página do **Active Directory**, clique duas vezes no diretório que tem os usuários que você deseja configurar.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="d3ce7-123">Na parte superior da página do diretório, selecione **Integração de diretório**.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="d3ce7-124">Na **integração com o Active Directory local**, observe o horário da última sincronização.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="d3ce7-125"><center>![Horário de sincronização de diretórios](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="d3ce7-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="d3ce7-126">Iniciar uma tarefa de sincronização agendada</span><span class="sxs-lookup"><span data-stu-id="d3ce7-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="d3ce7-127">Se você precisar executar uma tarefa de sincronização, poderá fazer isso executando-a novamente por meio do assistente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="d3ce7-128">Você precisa fornecer suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="d3ce7-129">No assistente, selecione a tarefa **Personalizar opções de sincronização** e clique em **Avançar** para seguir pelo assistente.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="d3ce7-130">No final, certifique-se de que a caixa **Iniciar o processo de sincronização assim que a configuração for concluída** esteja selecionada.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="d3ce7-131"><center>![Iniciar a sincronização](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="d3ce7-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="d3ce7-132">Para obter mais informações sobre o Agendador de sincronização do Azure AD Connect, consulte [Agendador do Azure AD Connect](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="d3ce7-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="d3ce7-133">Tarefas adicionais disponíveis no Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d3ce7-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="d3ce7-134">Após a instalação inicial do Azure AD Connect, você pode sempre iniciar o assistente novamente de um atalho da área de trabalho ou da página inicial do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="d3ce7-135">Você observará que executar novamente o assistente fornece algumas novas opções na forma de tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="d3ce7-136">A tabela a seguir fornece um resumo dessas tarefas e uma breve descrição de cada uma delas.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lista de tarefas adicionais](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="d3ce7-138">Tarefa adicional</span><span class="sxs-lookup"><span data-stu-id="d3ce7-138">Additional task</span></span> | <span data-ttu-id="d3ce7-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="d3ce7-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3ce7-140">**Exibir o cenário selecionado**</span><span class="sxs-lookup"><span data-stu-id="d3ce7-140">**View the selected scenario**</span></span> |<span data-ttu-id="d3ce7-141">Exiba sua solução atual do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="d3ce7-142">Isso inclui configurações gerais, diretórios sincronizados e configurações de sincronização.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="d3ce7-143">**Personalizar opções de sincronização**</span><span class="sxs-lookup"><span data-stu-id="d3ce7-143">**Customize synchronization options**</span></span> |<span data-ttu-id="d3ce7-144">Altere a configuração atual, por exemplo adicionando florestas do Active Directory para a configuração ou habilitando opções de sincronização como usuário, grupo, dispositivo ou write-back de senha.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="d3ce7-145">**Habilitar o modo de preparo**</span><span class="sxs-lookup"><span data-stu-id="d3ce7-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="d3ce7-146">Informações de preparo que não são sincronizadas imediatamente e não são exportadas para o Azure AD ou o Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="d3ce7-147">Com esse recurso, você pode visualizar as sincronizações antes que elas ocorram.</span><span class="sxs-lookup"><span data-stu-id="d3ce7-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3ce7-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3ce7-148">Next steps</span></span>
<span data-ttu-id="d3ce7-149">Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d3ce7-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
