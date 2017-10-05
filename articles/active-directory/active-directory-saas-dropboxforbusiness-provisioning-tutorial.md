---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="81e57-103">Tutorial: Configurando o Dropbox for Business para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="81e57-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="81e57-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Dropbox for Business e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81e57-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="81e57-105">Prerequisites</span></span>

<span data-ttu-id="81e57-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="81e57-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="81e57-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81e57-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="81e57-108">Uma assinatura habilitada para logon único do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="81e57-109">Uma conta de usuário no Dropbox for Business com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="81e57-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="81e57-110">Atribuindo usuários ao Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="81e57-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="81e57-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="81e57-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="81e57-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="81e57-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="81e57-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="81e57-114">Depois de decidir, atribua esses usuários ao aplicativo Dropbox for Business seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="81e57-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="81e57-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="81e57-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="81e57-116">Dicas importantes para atribuir usuários ao Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="81e57-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="81e57-117">Recomendamos a atribuição de um único usuário do Azure AD ao Dropbox for Business para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="81e57-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="81e57-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="81e57-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="81e57-119">Ao atribuir um usuário ao Dropbox for Business, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="81e57-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="81e57-120">A função “Acesso Padrão” não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="81e57-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="81e57-121">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="81e57-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="81e57-122">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Dropbox for Business e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Dropbox for Business, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81e57-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="81e57-123">Você também pode optar por habilitar o Logon Único baseado em SAML no Dropbox for Business, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81e57-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="81e57-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="81e57-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="81e57-125">Para configurar o provisionamento automático de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="81e57-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="81e57-126">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="81e57-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="81e57-127">Se você já tiver configurado o Dropbox for Business para logon único, pesquise a instância do Dropbox for Business usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="81e57-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="81e57-128">Caso contrário, selecione **Adicionar** e pesquise **Dropbox for Business** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="81e57-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="81e57-129">Selecione o Dropbox for Business nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="81e57-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="81e57-130">Selecione a instância do Dropbox for Business e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="81e57-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="81e57-131">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="81e57-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="81e57-133">Na seção **Credenciais de Administrador**, clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="81e57-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="81e57-134">Ela abre uma caixa de diálogo de logon do Dropbox for Business em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="81e57-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="81e57-135">Na caixa de diálogo **Entrar no Dropbox para vincular com o Azure AD**, entre no locatário do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="81e57-136">![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="81e57-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="81e57-137">Confirme se deseja conceder permissão ao Azure Active Directory para fazer alterações em seu locatário do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="81e57-138">Clique em **Permitir**.</span><span class="sxs-lookup"><span data-stu-id="81e57-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="81e57-139">![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="81e57-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="81e57-140">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="81e57-141">Se a conexão falhar, verifique se sua conta do Dropbox for Business tem permissões de Administrador de Equipe e repita a etapa **“Autorizar”**.</span><span class="sxs-lookup"><span data-stu-id="81e57-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="81e57-142">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="81e57-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="81e57-143">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="81e57-143">Click **Save.**</span></span>

11. <span data-ttu-id="81e57-144">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Dropbox for Business.**</span><span class="sxs-lookup"><span data-stu-id="81e57-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="81e57-145">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="81e57-146">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Dropbox for Business em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="81e57-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="81e57-147">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="81e57-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="81e57-148">Para habilitar o serviço de provisionamento do Azure AD no Dropbox for Business, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="81e57-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="81e57-149">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="81e57-149">Click **Save.**</span></span>

<span data-ttu-id="81e57-150">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Dropbox for Business na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="81e57-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="81e57-151">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="81e57-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="81e57-152">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="81e57-153">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="81e57-153">You can now create a test account.</span></span> <span data-ttu-id="81e57-154">Aguarde até 20 minutos para confirmar se a conta foi sincronizada com o Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="81e57-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="81e57-155">Um ciclo de provisionamento de usuário concluído com êxito é indicado por um status relacionado.</span><span class="sxs-lookup"><span data-stu-id="81e57-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="81e57-156">![Atribuir usuários](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="81e57-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="81e57-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="81e57-157">Additional resources</span></span>

* [<span data-ttu-id="81e57-158">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="81e57-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81e57-159">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81e57-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="81e57-160">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="81e57-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)