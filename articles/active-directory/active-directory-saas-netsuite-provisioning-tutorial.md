---
title: "Tutorial: Integração do Azure Active Directory com o NetSuite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="9d6a6-103">Tutorial: Configurando o Netsuite para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="9d6a6-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="9d6a6-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Netsuite e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d6a6-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9d6a6-105">Prerequisites</span></span>

<span data-ttu-id="9d6a6-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9d6a6-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9d6a6-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="9d6a6-108">Uma assinatura habilitada para logon único do Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="9d6a6-109">Uma conta de usuário no Netsuite com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="9d6a6-110">Atribuindo usuários ao Netsuite</span><span class="sxs-lookup"><span data-stu-id="9d6a6-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="9d6a6-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9d6a6-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9d6a6-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="9d6a6-114">Depois de decidir, atribua esses usuários ao aplicativo Netsuite seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="9d6a6-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="9d6a6-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="9d6a6-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="9d6a6-116">Dicas importantes para atribuir usuários ao Netsuite</span><span class="sxs-lookup"><span data-stu-id="9d6a6-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="9d6a6-117">Recomendamos a atribuição de um único usuário do Azure AD ao Netsuite para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="9d6a6-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9d6a6-119">Ao atribuir um usuário ao Netsuite, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="9d6a6-120">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="9d6a6-121">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="9d6a6-121">Enable User Provisioning</span></span>

<span data-ttu-id="9d6a6-122">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Netsuite e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Netsuite, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="9d6a6-123">Você também pode optar por habilitar o Logon Único baseado em SAML no Netsuite, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d6a6-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d6a6-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="9d6a6-125">Para configurar o provisionamento de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="9d6a6-125">To configure user account provisioning:</span></span>

<span data-ttu-id="9d6a6-126">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="9d6a6-127">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="9d6a6-128">Se você já tiver configurado o Netsuite para logon único, pesquise a instância do Netsuite usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="9d6a6-129">Caso contrário, selecione **Adicionar** e pesquise **Netsuite** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="9d6a6-130">Selecione o Netsuite nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="9d6a6-131">Selecione a instância do Netsuite e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="9d6a6-132">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9d6a6-134">Na seção **Credenciais de Administrador**, forneça as seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="9d6a6-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="9d6a6-135">a.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-135">a.</span></span> <span data-ttu-id="9d6a6-136">Na caixa de texto **Nome de Usuário Administrador**, digite um nome de conta do Netsuite que tem o perfil **Administrador do Sistema** atribuído no Netsuite.com.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="9d6a6-137">b.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-137">b.</span></span> <span data-ttu-id="9d6a6-138">Na caixa de texto **Senha do Administrador**, digite a senha dessa conta.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="9d6a6-139">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="9d6a6-140">No campo **Email de Notificação**, insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="9d6a6-141">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="9d6a6-141">Click **Save.**</span></span>

9. <span data-ttu-id="9d6a6-142">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Netsuite.**</span><span class="sxs-lookup"><span data-stu-id="9d6a6-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="9d6a6-143">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="9d6a6-144">Observe que os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Netsuite em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="9d6a6-145">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="9d6a6-146">Para habilitar o serviço de provisionamento do Azure AD no Netsuite, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="9d6a6-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="9d6a6-147">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="9d6a6-147">Click **Save.**</span></span>

<span data-ttu-id="9d6a6-148">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Netsuite na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="9d6a6-149">Observe que a sincronização inicial leva mais tempo do que as sincronizações posteriores, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="9d6a6-150">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="9d6a6-151">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-151">You can now create a test account.</span></span> <span data-ttu-id="9d6a6-152">Aguarde até 20 minutos para confirmar se a conta foi sincronizada com o Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9d6a6-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d6a6-153">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9d6a6-153">Additional resources</span></span>

* [<span data-ttu-id="9d6a6-154">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="9d6a6-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d6a6-155">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d6a6-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9d6a6-156">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="9d6a6-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)