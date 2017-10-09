---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="4ba2b-103">Tutorial: configurar o Salesforce para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="4ba2b-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="4ba2b-104">Olá objetivo deste tutorial é tooshow Olá etapas necessárias tooperform na equipe de vendas e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-104">hello objective of this tutorial is tooshow hello steps required tooperform in Salesforce and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ba2b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ba2b-105">Prerequisites</span></span>

<span data-ttu-id="4ba2b-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba2b-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4ba2b-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4ba2b-108">É preciso ter um locatário válido para o Salesforce for Work ou Salesforce for Education.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="4ba2b-109">Você pode usar uma conta de avaliação gratuita para qualquer serviço.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="4ba2b-110">Uma conta de usuário no Salesforce com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce"></a><span data-ttu-id="4ba2b-111">Atribuir usuários tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="4ba2b-111">Assigning users tooSalesforce</span></span>

<span data-ttu-id="4ba2b-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4ba2b-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4ba2b-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo do Salesforce tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce app.</span></span> <span data-ttu-id="4ba2b-115">Depois de decidir, você pode atribuir esses usuários tooyour o aplicativo do Salesforce, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="4ba2b-115">Once decided, you can assign these users tooyour Salesforce app by following hello instructions here:</span></span>

[<span data-ttu-id="4ba2b-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="4ba2b-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a><span data-ttu-id="4ba2b-117">Dicas importantes para atribuir usuários tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="4ba2b-117">Important tips for assigning users tooSalesforce</span></span>

*   <span data-ttu-id="4ba2b-118">É recomendável que um único usuário do AD do Azure é atribuído tooSalesforce tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-118">It is recommended that a single Azure AD user is assigned tooSalesforce tootest hello provisioning configuration.</span></span> <span data-ttu-id="4ba2b-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="4ba2b-120">Ao atribuir um usuário tooSalesforce, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-120">When assigning a user tooSalesforce, you must select a valid user role.</span></span> <span data-ttu-id="4ba2b-121">função de "Acesso padrão" Hello não funciona para provisionamento</span><span class="sxs-lookup"><span data-stu-id="4ba2b-121">hello "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ba2b-122">Este aplicativo importa funções personalizadas do Salesforce como parte da saudação qual cliente Olá seja tooselect durante a atribuição de usuários no processo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="4ba2b-122">This app imports custom roles from Salesforce as part of hello provisioning process, which hello customer may want tooselect when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4ba2b-123">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="4ba2b-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="4ba2b-124">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooSalesforce seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Salesforce com base na atribuição de usuário e grupo no AD do Azure .</span><span class="sxs-lookup"><span data-stu-id="4ba2b-124">This section guides you through connecting your Azure AD tooSalesforce's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4ba2b-125">Você também pode escolher tooenabled baseado no SAML SSO para Salesforce, seguindo as instruções de saudação fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ba2b-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4ba2b-126">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="4ba2b-127">provisionamento de conta de usuário automático de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="4ba2b-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="4ba2b-128">Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce.</span></span>

1. <span data-ttu-id="4ba2b-129">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="4ba2b-130">Se você já tiver configurado a equipe de vendas para o logon único, procure sua instância do Salesforce usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using hello search field.</span></span> <span data-ttu-id="4ba2b-131">Caso contrário, selecione **adicionar** e procure **Salesforce** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-131">Otherwise, select **Add** and search for **Salesforce** in hello application gallery.</span></span> <span data-ttu-id="4ba2b-132">Selecione a equipe de vendas dos resultados da pesquisa hello e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-132">Select Salesforce from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4ba2b-133">Selecione sua instância do Salesforce, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-133">Select your instance of Salesforce, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4ba2b-134">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
<span data-ttu-id="4ba2b-135">![provisionamento](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="4ba2b-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="4ba2b-136">Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ba2b-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="4ba2b-137">a.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-137">a.</span></span> <span data-ttu-id="4ba2b-138">Em Olá **nome de usuário administrador** caixa de texto, digite nome que tem Olá de conta do Salesforce **administrador do sistema** perfil em Salesforce.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-138">In hello **Admin User Name** textbox, type a Salesforce account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="4ba2b-139">b.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-139">b.</span></span> <span data-ttu-id="4ba2b-140">Em Olá **senha do administrador** caixa de texto, digite a senha Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="4ba2b-141">tooget seu token de segurança do Salesforce, abra uma nova guia e entrar Olá mesma conta de administrador do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-141">tooget your Salesforce security token, open a new tab and sign into hello same Salesforce admin account.</span></span> <span data-ttu-id="4ba2b-142">No hello canto superior direito da página de saudação, clique no nome e, em seguida, clique em **minhas configurações**.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="4ba2b-143">![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Habilitar o provisionamento de usuário automático")</span><span class="sxs-lookup"><span data-stu-id="4ba2b-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="4ba2b-144">No painel de navegação esquerdo hello, clique em **pessoal** tooexpand Olá seção relacionada e, em seguida, clique em **redefinir meu Token de segurança**.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="4ba2b-145">![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Habilitar o provisionamento de usuário automático")</span><span class="sxs-lookup"><span data-stu-id="4ba2b-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="4ba2b-146">Em Olá **redefinir meu Token de segurança** , clique em **redefinir Token de segurança** botão.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-146">On hello **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="4ba2b-147">![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Habilitar o provisionamento de usuário automático")</span><span class="sxs-lookup"><span data-stu-id="4ba2b-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="4ba2b-148">Verifique a caixa de entrada de email de Olá associada a essa conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="4ba2b-149">Procure um email do Salesforce.com que contém o novo token de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-149">Look for an email from Salesforce.com that contains hello new security token.</span></span>
10. <span data-ttu-id="4ba2b-150">Copiar Olá token, vá tooyour janela do AD do Azure e cole-a saudação **soquete Token** campo.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="4ba2b-151">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar o aplicativo do Salesforce tooyour.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce app.</span></span>

12. <span data-ttu-id="4ba2b-152">Em Olá **Email de notificação** , digite o endereço de email de saudação de uma pessoa ou grupo que deve receber as notificações de erro de provisionamento e marque Olá caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox below.</span></span>

13. <span data-ttu-id="4ba2b-153">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="4ba2b-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="4ba2b-154">Em Olá mapeamentos, selecione **tooSalesforce sincronizar Azure usuários do Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="4ba2b-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce.**</span></span>

15. <span data-ttu-id="4ba2b-155">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooSalesforce do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce.</span></span> <span data-ttu-id="4ba2b-156">Observe que Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado na equipe de vendas para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-156">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="4ba2b-157">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="4ba2b-158">tooenable Olá serviço de provisionamento do AD do Azure para Salesforce, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="4ba2b-158">tooenable hello Azure AD provisioning service for Salesforce, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="4ba2b-159">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="4ba2b-159">Click **Save.**</span></span>

<span data-ttu-id="4ba2b-160">Isso inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSalesforce em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-160">This starts hello initial synchronization of any users and/or groups assigned tooSalesforce in hello Users and Groups section.</span></span> <span data-ttu-id="4ba2b-161">Observe que a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-161">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4ba2b-162">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo com a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="4ba2b-163">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-163">You can now create a test account.</span></span> <span data-ttu-id="4ba2b-164">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="4ba2b-164">Wait for up too20 minutes tooverify that hello account has been synchronized tooSalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ba2b-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4ba2b-165">Additional resources</span></span>

* [<span data-ttu-id="4ba2b-166">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="4ba2b-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ba2b-167">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ba2b-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4ba2b-168">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="4ba2b-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)