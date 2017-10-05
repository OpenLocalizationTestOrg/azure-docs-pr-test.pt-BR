---
title: "Tutorial: integração do Azure Active Directory com o Box | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9f061f3f5a0a4825854b893150ceccc8951487de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a><span data-ttu-id="b46d6-103">Tutorial: Configurar o Box para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="b46d6-103">Tutorial: Configuring Box for Automatic User Provisioning</span></span>

<span data-ttu-id="b46d6-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Box e no Azure AD para provisionar e desprovisionar automaticamente contas de usuário do Azure AD no Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b46d6-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b46d6-105">Prerequisites</span></span>

<span data-ttu-id="b46d6-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b46d6-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="b46d6-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b46d6-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b46d6-108">Uma assinatura do Box habilitada para logon único.</span><span class="sxs-lookup"><span data-stu-id="b46d6-108">A Box single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b46d6-109">Uma conta de usuário do Box com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="b46d6-109">A user account in Box with Team Admin permissions.</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="b46d6-110">Atribuindo usuários ao Box</span><span class="sxs-lookup"><span data-stu-id="b46d6-110">Assigning users to Box</span></span> 

<span data-ttu-id="b46d6-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="b46d6-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b46d6-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="b46d6-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b46d6-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos do Azure AD representam os usuários que precisam de acesso ao aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="b46d6-114">Depois de decidir, você pode atribuir esses usuários ao aplicativo Box seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="b46d6-114">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="b46d6-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="b46d6-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="b46d6-116">Atribuir usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="b46d6-116">Assign users and groups</span></span>
<span data-ttu-id="b46d6-117">A guia **Box > Usuários e Grupos** no portal do Azure permite especificar quais usuários e grupos devem ter acesso ao Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-117">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="b46d6-118">A atribuição de um usuário ou grupo faz com que as seguintes ações ocorram:</span><span class="sxs-lookup"><span data-stu-id="b46d6-118">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="b46d6-119">O Azure AD permite que o usuário atribuído (seja por atribuição direta ou associação de grupo) realize a autenticação no Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-119">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="b46d6-120">Se um usuário não for atribuído, o Azure AD não permitirá que ele entre no Box e retornará um erro na página de entrada do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b46d6-120">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="b46d6-121">Um bloco de aplicativo do Box é adicionado ao [iniciador do aplicativo](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)do usuário.</span><span class="sxs-lookup"><span data-stu-id="b46d6-121">An app tile for Box is added to the user's [application launcher](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="b46d6-122">Se o provisionamento automático estiver habilitado, os usuários e/ou grupos atribuídos serão adicionados à fila de provisionamento para serem provisionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b46d6-122">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="b46d6-123">Se apenas objetos de usuário tiverem sido configurados para serem provisionados, todos os usuários atribuídos diretamente e todos os usuários que são membros de grupos atribuídos serão colocados na fila de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b46d6-123">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="b46d6-124">Se os objetos de grupo tiverem sido configurados para serem provisionados, todos os objetos de grupo atribuídos serão provisionados para o Box, bem como todos os usuários que são membros desses grupos.</span><span class="sxs-lookup"><span data-stu-id="b46d6-124">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="b46d6-125">As associações de grupo e usuário são preservadas ao serem gravadas no Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-125">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="b46d6-126">Você pode usar a guia **Atributos > Logon único** para configurar quais atributos de usuário (ou declarações) são apresentadas ao Box durante a autenticação baseada em SAML e a guia **Atributos > Provisionamento** para configurar como os atributos de usuário e grupo fluem do Azure AD para o Box durante as operações de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b46d6-126">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="b46d6-127">Dicas importantes para atribuir usuários ao Box</span><span class="sxs-lookup"><span data-stu-id="b46d6-127">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="b46d6-128">Recomendamos atribuir um único usuário do Azure AD ao Box para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b46d6-128">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="b46d6-129">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b46d6-129">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b46d6-130">Ao atribuir um usuário ao Box, você precisa selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="b46d6-130">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="b46d6-131">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b46d6-131">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b46d6-132">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="b46d6-132">Enable Automated User Provisioning</span></span>

<span data-ttu-id="b46d6-133">Esta seção orienta você quanto à conexão do Azure AD com a API de provisionamento de conta de usuário do Box e à configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Box com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b46d6-133">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="b46d6-134">Se o provisionamento automático estiver habilitado, os usuários e/ou grupos atribuídos serão adicionados à fila de provisionamento para serem provisionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b46d6-134">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="b46d6-135">Se apenas objetos de usuário tiverem sido configurados para serem provisionados, os usuários atribuídos diretamente e os usuários que são membros de grupos atribuídos serão colocados na fila de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b46d6-135">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="b46d6-136">Se os objetos de grupo tiverem sido configurados para serem provisionados, todos os objetos de grupo atribuídos serão provisionados para o Box, bem como todos os usuários que são membros desses grupos.</span><span class="sxs-lookup"><span data-stu-id="b46d6-136">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="b46d6-137">As associações de grupo e usuário são preservadas ao serem gravadas no Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-137">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="b46d6-138">Você também pode optar por habilitar o Logon único baseado em SAML para o Box seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b46d6-138">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b46d6-139">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="b46d6-139">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="b46d6-140">Para configurar o provisionamento automático de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="b46d6-140">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="b46d6-141">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-141">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="b46d6-142">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-142">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b46d6-143">Se já tiver configurado o Box para logon único, pesquise sua instância do Box usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b46d6-143">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="b46d6-144">Caso contrário, selecione **Adicionar** e pesquise o **Box** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b46d6-144">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="b46d6-145">Selecione o Box nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b46d6-145">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b46d6-146">Selecione sua instância do Box e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-146">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b46d6-147">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-147">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b46d6-149">Na seção **Credenciais de Administrador**, clique em **Autorizar** para abrir uma caixa de diálogo de logon do Box em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="b46d6-149">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="b46d6-150">Na página **Fazer logon para conceder acesso ao Box**, forneça as credenciais necessárias e clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-150">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="b46d6-151">![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Habilitar o provisionamento de usuário automático")</span><span class="sxs-lookup"><span data-stu-id="b46d6-151">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="b46d6-152">Clique em **Conceder acesso ao Box** para autorizar essa operação e retornar ao portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b46d6-152">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="b46d6-153">![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Habilitar o provisionamento de usuário automático")</span><span class="sxs-lookup"><span data-stu-id="b46d6-153">![Enable automatic user provisioning](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="b46d6-154">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD possa se conectar ao aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-154">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="b46d6-155">Se a conexão falhar, verifique se sua conta do Box tem permissões de Administrador de Equipe e repita a etapa **"Autorizar"**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-155">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="b46d6-156">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="b46d6-156">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="b46d6-157">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b46d6-157">Click **Save.**</span></span>

11. <span data-ttu-id="b46d6-158">Na seção Mapeamentos, selecione **Sincronizar usuários do Azure Active Directory com o Box**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="b46d6-159">Na seção **Mapeamentos de Atributo**, revise os atributos de usuário que serão sincronizados do Azure AD com o Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="b46d6-160">Os atributos selecionados como propriedades **Correspondentes** serão usados para fazer a correspondência entre as contas de usuário no Box para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="b46d6-160">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="b46d6-161">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="b46d6-161">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="b46d6-162">Para habilitar o serviço de provisionamento do Azure AD para o Box, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="b46d6-162">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="b46d6-163">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b46d6-163">Click **Save.**</span></span>

<span data-ttu-id="b46d6-164">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Box na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="b46d6-164">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="b46d6-165">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="b46d6-165">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="b46d6-166">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="b46d6-167">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b46d6-167">You can now create a test account.</span></span> <span data-ttu-id="b46d6-168">Aguarde até 20 minutos para confirmar se a conta foi sincronizada com o Box.</span><span class="sxs-lookup"><span data-stu-id="b46d6-168">Wait for up to 20 minutes to verify that the account has been synchronized to box.</span></span>

<span data-ttu-id="b46d6-169">Em seu locatário do Box, os usuários sincronizados estão listados em **Usuários Gerenciados** no **Console do Administrador**.</span><span class="sxs-lookup"><span data-stu-id="b46d6-169">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="b46d6-170">![Status da integração](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Status da integração")</span><span class="sxs-lookup"><span data-stu-id="b46d6-170">![Integration status](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b46d6-171">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b46d6-171">Additional resources</span></span>

* [<span data-ttu-id="b46d6-172">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="b46d6-172">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b46d6-173">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b46d6-173">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b46d6-174">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="b46d6-174">Configure Single Sign-on</span></span>](active-directory-saas-box-tutorial.md)