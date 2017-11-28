---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Dropbox for Business."
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
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="f86f2-103">Tutorial: Configurando o Dropbox for Business para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="f86f2-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="f86f2-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Dropbox para negócios e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="f86f2-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f86f2-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f86f2-105">Prerequisites</span></span>

<span data-ttu-id="f86f2-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f86f2-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="f86f2-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f86f2-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f86f2-108">Uma assinatura habilitada para logon único do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="f86f2-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="f86f2-109">Uma conta de usuário no Dropbox for Business com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="f86f2-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="f86f2-110">Atribuir usuários tooDropbox para empresas</span><span class="sxs-lookup"><span data-stu-id="f86f2-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="f86f2-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f86f2-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="f86f2-112">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="f86f2-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="f86f2-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour Dropbox para o aplicativo de negócios.</span><span class="sxs-lookup"><span data-stu-id="f86f2-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="f86f2-114">Depois de decidir, você pode atribuir essas tooyour usuários Dropbox para o aplicativo de negócios seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="f86f2-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="f86f2-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="f86f2-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="f86f2-116">Dicas importantes para atribuir usuários tooDropbox de negócios</span><span class="sxs-lookup"><span data-stu-id="f86f2-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="f86f2-117">É recomendável que um único usuário do AD do Azure é atribuído tooDropbox de saudação do negócio tootest configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="f86f2-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="f86f2-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f86f2-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f86f2-119">Ao atribuir um usuário tooDropbox para empresas, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="f86f2-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="f86f2-120">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="f86f2-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="f86f2-121">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="f86f2-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="f86f2-122">Esta seção orienta você conectar seu tooDropbox do AD do Azure para a API de provisionamento de conta de usuário da empresa e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído em Dropbox for Business com base no usuário e grupo atribuição no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f86f2-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="f86f2-123">Você também pode escolher tooenabled baseado no SAML logon único para Dropbox for Business, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f86f2-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f86f2-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="f86f2-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="f86f2-125">provisionamento de conta de usuário automático de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="f86f2-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="f86f2-126">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="f86f2-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="f86f2-127">Se você já tiver configurado o Dropbox for Business para logon único, procure sua instância do Dropbox for Business usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86f2-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="f86f2-128">Caso contrário, selecione **adicionar** e procure **Dropbox for Business** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f86f2-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="f86f2-129">Selecione Dropbox for Business dos resultados da pesquisa hello e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f86f2-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="f86f2-130">Selecione sua instância do Dropbox for Business e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="f86f2-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="f86f2-131">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="f86f2-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="f86f2-133">Em Olá **credenciais de administrador** seção, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="f86f2-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="f86f2-134">Ela abre uma caixa de diálogo de logon do Dropbox for Business em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="f86f2-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="f86f2-135">Em Olá **entrar tooDropbox toolink com o Azure AD** caixa de diálogo, tooyour Dropbox para o locatário de negócios de entrada.</span><span class="sxs-lookup"><span data-stu-id="f86f2-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="f86f2-136">![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="f86f2-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="f86f2-137">Confirme que deseja toogive Active Directory do Azure permissão toomake alterações tooyour Dropbox para o locatário de negócios.</span><span class="sxs-lookup"><span data-stu-id="f86f2-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="f86f2-138">Clique em **Permitir**.</span><span class="sxs-lookup"><span data-stu-id="f86f2-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="f86f2-139">![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="f86f2-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="f86f2-140">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Dropbox para o aplicativo de negócios.</span><span class="sxs-lookup"><span data-stu-id="f86f2-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="f86f2-141">Se a conexão de saudação falhar, verifique seu Dropbox para conta de negócios tem permissões de administrador de equipe e tente Olá **"Autorizar"** etapa novamente.</span><span class="sxs-lookup"><span data-stu-id="f86f2-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="f86f2-142">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="f86f2-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="f86f2-143">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="f86f2-143">Click **Save.**</span></span>

11. <span data-ttu-id="f86f2-144">Em Olá mapeamentos, selecione **tooDropbox sincronizar Azure usuários do Active Directory para a empresa.**</span><span class="sxs-lookup"><span data-stu-id="f86f2-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="f86f2-145">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="f86f2-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="f86f2-146">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Dropbox for Business para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="f86f2-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="f86f2-147">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="f86f2-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="f86f2-148">tooenable Olá serviço de provisionamento do AD do Azure para Dropbox for Business, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="f86f2-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="f86f2-149">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="f86f2-149">Click **Save.**</span></span>

<span data-ttu-id="f86f2-150">Ele inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooDropbox para empresas no hello usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="f86f2-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="f86f2-151">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="f86f2-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="f86f2-152">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço no seu Dropbox para o aplicativo de negócios.</span><span class="sxs-lookup"><span data-stu-id="f86f2-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="f86f2-153">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="f86f2-153">You can now create a test account.</span></span> <span data-ttu-id="f86f2-154">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooDropbox para empresas.</span><span class="sxs-lookup"><span data-stu-id="f86f2-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="f86f2-155">Um ciclo de provisionamento de usuário concluído com êxito é indicado por um status relacionado.</span><span class="sxs-lookup"><span data-stu-id="f86f2-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="f86f2-156">![Atribuir usuários](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="f86f2-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f86f2-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f86f2-157">Additional resources</span></span>

* [<span data-ttu-id="f86f2-158">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="f86f2-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f86f2-159">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f86f2-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f86f2-160">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="f86f2-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)