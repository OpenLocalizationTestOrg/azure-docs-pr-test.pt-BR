---
title: "Tutorial: Integração do Azure Active Directory com o Jive | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="2c9ee-103">Tutorial: Configurando o Jive para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="2c9ee-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="2c9ee-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Jive e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c9ee-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c9ee-105">Prerequisites</span></span>

<span data-ttu-id="2c9ee-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2c9ee-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="2c9ee-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="2c9ee-108">Uma assinatura habilitada para logon único do Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="2c9ee-109">Uma conta de usuário no Jive com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="2c9ee-110">Atribuindo usuários ao Jive</span><span class="sxs-lookup"><span data-stu-id="2c9ee-110">Assigning users to Jive</span></span>

<span data-ttu-id="2c9ee-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="2c9ee-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="2c9ee-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="2c9ee-114">Depois de decidir, atribua esses usuários ao aplicativo Jive seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="2c9ee-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="2c9ee-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="2c9ee-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="2c9ee-116">Dicas importantes para atribuir usuários ao Jive</span><span class="sxs-lookup"><span data-stu-id="2c9ee-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="2c9ee-117">Recomendamos a atribuição de um único usuário do Azure AD ao Jive para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="2c9ee-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="2c9ee-119">Ao atribuir um usuário ao Jive, você deve selecionar uma função de usuário válida.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="2c9ee-120">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="2c9ee-121">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="2c9ee-121">Enable User Provisioning</span></span>

<span data-ttu-id="2c9ee-122">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Jive e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Jive, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="2c9ee-123">Você também pode optar por habilitar o Logon Único baseado em SAML no Jive, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c9ee-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2c9ee-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="2c9ee-125">Para configurar o provisionamento de conta de usuário:</span><span class="sxs-lookup"><span data-stu-id="2c9ee-125">To configure user account provisioning:</span></span>

<span data-ttu-id="2c9ee-126">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="2c9ee-127">Como parte desse procedimento, é necessário fornecer um token de segurança do usuário que será necessário solicitar em Jive.com.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="2c9ee-128">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="2c9ee-129">Se você já tiver configurado o Jive para logon único, pesquise a instância do Jive usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="2c9ee-130">Caso contrário, selecione **Adicionar** e pesquise **Jive** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="2c9ee-131">Selecione o Jive nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="2c9ee-132">Selecione a instância do Jive e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="2c9ee-133">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="2c9ee-135">Na seção **Credenciais de Administrador**, forneça as seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="2c9ee-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="2c9ee-136">a.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-136">a.</span></span> <span data-ttu-id="2c9ee-137">Na caixa de texto **Nome do Usuário Administrador do Jive**, digite o nome da conta do Jive que tem o perfil do **Administrador de Sistema** atribuído no Jive.com.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="2c9ee-138">b.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-138">b.</span></span> <span data-ttu-id="2c9ee-139">Na caixa de texto **Senha do Administrador do Jive** , digite a senha desta conta.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="2c9ee-140">c.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-140">c.</span></span> <span data-ttu-id="2c9ee-141">Na caixa de texto **URL de Locatário do Jive** , digite a URL de locatário do Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="2c9ee-142">A URL de locatário do Jive é a URL usada por sua organização para fazer logon no Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="2c9ee-143">Normalmente, a URL tem o seguinte formato: **www.\<organização\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="2c9ee-144">No portal do Azure, clique em **Testar conectividade** para garantir que o Azure AD pode se conectar ao aplicativo Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="2c9ee-145">Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="2c9ee-146">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2c9ee-146">Click **Save.**</span></span>

9. <span data-ttu-id="2c9ee-147">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Jive.**</span><span class="sxs-lookup"><span data-stu-id="2c9ee-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="2c9ee-148">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="2c9ee-149">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Jive em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="2c9ee-150">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="2c9ee-151">Para habilitar o serviço de provisionamento do Azure AD no Jive, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="2c9ee-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="2c9ee-152">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="2c9ee-152">Click **Save.**</span></span>

<span data-ttu-id="2c9ee-153">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Jive na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="2c9ee-154">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="2c9ee-155">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="2c9ee-156">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-156">You can now create a test account.</span></span> <span data-ttu-id="2c9ee-157">Aguarde até 20 minutos para confirmar se a conta foi sincronizada com o Jive.</span><span class="sxs-lookup"><span data-stu-id="2c9ee-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2c9ee-158">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2c9ee-158">Additional resources</span></span>

* [<span data-ttu-id="2c9ee-159">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="2c9ee-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2c9ee-160">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2c9ee-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2c9ee-161">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="2c9ee-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)