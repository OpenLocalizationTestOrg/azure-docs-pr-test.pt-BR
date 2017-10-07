---
title: "Tutorial: Configurar o Slack para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooSlack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="7fed3-103">Tutorial: Configurar o Slack para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="7fed3-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="7fed3-104">Olá, o objetivo deste tutorial é tooshow Olá etapas precisam tooperform na margem de atraso e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSlack.</span><span class="sxs-lookup"><span data-stu-id="7fed3-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7fed3-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7fed3-105">Prerequisites</span></span>

<span data-ttu-id="7fed3-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7fed3-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="7fed3-107">Um locatário de diretório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fed3-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="7fed3-108">Margem de atraso de locatário com hello [Plus plano](https://aadsyncfabric.slack.com/pricing) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="7fed3-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="7fed3-109">Uma conta de usuário no Slack com permissões de Administrador de Equipe</span><span class="sxs-lookup"><span data-stu-id="7fed3-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="7fed3-110">Observação: Olá provisionamento integração do AD do Azure depende de saudação [Slack SCIM API](https://api.slack.com/scim) que é equipes tooSlack disponível em hello mais plano ou melhor.</span><span class="sxs-lookup"><span data-stu-id="7fed3-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="7fed3-111">Atribuir usuários tooSlack</span><span class="sxs-lookup"><span data-stu-id="7fed3-111">Assigning users tooSlack</span></span>

<span data-ttu-id="7fed3-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7fed3-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="7fed3-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="7fed3-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="7fed3-114">Antes de configurar e habilitar Olá provisionar um serviço, você precisará toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo de margem de atraso de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7fed3-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="7fed3-115">Depois de decidir, você pode atribuir esses aplicativos de margem de atraso de tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="7fed3-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="7fed3-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="7fed3-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="7fed3-117">Dicas importantes para atribuir usuários tooSlack</span><span class="sxs-lookup"><span data-stu-id="7fed3-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="7fed3-118">É recomendável que um único usuário do AD do Azure receberá tooSlack tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="7fed3-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="7fed3-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7fed3-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7fed3-120">Ao atribuir um usuário tooSlack, você deve selecionar Olá **usuário** ou uma função de "Grupo" na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="7fed3-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="7fed3-121">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="7fed3-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="7fed3-122">Configurando tooSlack de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="7fed3-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="7fed3-123">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooSlack seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído em atraso com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fed3-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="7fed3-124">**Dica:** você também pode escolher tooenabled baseado no SAML SSO para o Slack, seguindo instruções Olá fornecidas no (portal do Azure) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="7fed3-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="7fed3-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="7fed3-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="7fed3-126">conta de usuário automático tooconfigure provisionamento tooSlack no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="7fed3-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="7fed3-127">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="7fed3-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="7fed3-128">Se você já tiver configurado a margem de atraso para o logon único, pesquisa de sua instância de atraso usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="7fed3-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="7fed3-129">Caso contrário, selecione **adicionar** e procure **Slack** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7fed3-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="7fed3-130">Selecione a margem de atraso Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7fed3-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="7fed3-131">Selecione a instância de atraso, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="7fed3-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="7fed3-132">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Provisionamento do Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="7fed3-134">Em Olá **credenciais de administrador** seção, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="7fed3-135">Isso abre uma caixa de diálogo de autorização do Slack em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="7fed3-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="7fed3-136">Na nova janela de Olá, entre usando sua conta de administrador de equipe de margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="7fed3-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="7fed3-137">no diálogo de autorização resultante hello, selecione Olá atraso equipe que você deseja tooenable provisionamento para e, em seguida, selecione **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="7fed3-138">Saudação de toocomplete portal do Azure depois de concluído, retorne toohello configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="7fed3-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Caixa de diálogo Autorização](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="7fed3-140">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode conectar o aplicativo de margem de atraso de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7fed3-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="7fed3-141">Se a conexão de saudação falhar, certifique-se de que sua conta do Slack tem permissões de administrador de equipe e tente hello "Autorizar" etapa novamente.</span><span class="sxs-lookup"><span data-stu-id="7fed3-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="7fed3-142">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="7fed3-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="7fed3-143">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-143">Click **Save**.</span></span> 

10) <span data-ttu-id="7fed3-144">Em Olá mapeamentos, selecione **tooSlack sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="7fed3-145">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação serão sincronizados do AD do Azure tooSlack.</span><span class="sxs-lookup"><span data-stu-id="7fed3-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="7fed3-146">Observe que Olá atributos selecionados como **correspondência** propriedades serão contas de usuário de saudação toomatch usada na margem de atraso para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="7fed3-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="7fed3-147">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="7fed3-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="7fed3-148">tooenable Olá serviço de provisionamento do AD do Azure para o Slack, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="7fed3-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="7fed3-149">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-149">Click **Save**.</span></span> 

<span data-ttu-id="7fed3-150">Isso iniciará a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSlack em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="7fed3-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="7fed3-151">Observe que a sincronização inicial Olá levará mais tooperform que sincronizações subsequentes, que ocorrem aproximadamente a cada 10 minutos, desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="7fed3-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="7fed3-152">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo a margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="7fed3-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="7fed3-153">[Opcional] Configurar provisionamento tooSlack do objeto de grupo</span><span class="sxs-lookup"><span data-stu-id="7fed3-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="7fed3-154">Opcionalmente, você pode habilitar o provisionamento Olá dos objetos de grupo do AD do Azure tooSlack.</span><span class="sxs-lookup"><span data-stu-id="7fed3-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="7fed3-155">Isso é diferente de "atribuir grupos de usuários", no objeto do grupo real Olá além tooits membros serão replicados do tooSlack do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fed3-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="7fed3-156">Por exemplo, se você tiver um grupo chamado "Meu Grupo" no Azure AD, um grupo de idêntico chamado "Meu Grupos" será criado dentro do Slack.</span><span class="sxs-lookup"><span data-stu-id="7fed3-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="7fed3-157">tooenable provisionamento dos objetos de grupo:</span><span class="sxs-lookup"><span data-stu-id="7fed3-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="7fed3-158">Em Olá mapeamentos, selecione **tooSlack sincronizar Azure grupos do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="7fed3-159">Na folha de mapeamento de atributo hello, defina tooYes habilitado.</span><span class="sxs-lookup"><span data-stu-id="7fed3-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="7fed3-160">Em Olá **mapeamentos de atributo** seção, revise os atributos de grupo de saudação serão sincronizados do AD do Azure tooSlack.</span><span class="sxs-lookup"><span data-stu-id="7fed3-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="7fed3-161">Observe que Olá atributos selecionados como **correspondência** propriedades serão grupos de saudação do toomatch usada na margem de atraso para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="7fed3-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="7fed3-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7fed3-162">Click **Save**.</span></span>

<span data-ttu-id="7fed3-163">Esse resultado em qualquer tooSlack de objetos atribuídos do grupo no hello **usuários e grupos** seção totalmente sendo sincronizado tooSlack do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fed3-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="7fed3-164">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo a margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="7fed3-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7fed3-165">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7fed3-165">Additional Resources</span></span>

* [<span data-ttu-id="7fed3-166">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="7fed3-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="7fed3-167">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7fed3-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
