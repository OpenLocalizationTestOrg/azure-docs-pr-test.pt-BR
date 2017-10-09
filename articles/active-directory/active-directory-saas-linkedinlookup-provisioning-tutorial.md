---
title: "Tutorial: configurar o LinkedIn Lookup para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooLinkedIn pesquisa."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="46205-103">Tutorial: configurar o LinkedIn Lookup para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="46205-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="46205-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no LinkedIn pesquisa e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="46205-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Lookup and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="46205-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46205-105">Prerequisites</span></span>

<span data-ttu-id="46205-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="46205-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="46205-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46205-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="46205-108">Um locatário do LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="46205-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="46205-109">Uma conta de administrador na pesquisa do LinkedIn com acesso toohello LinkedIn Centro de contas</span><span class="sxs-lookup"><span data-stu-id="46205-109">An administrator account in LinkedIn Lookup with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="46205-110">Active Directory do Azure integra LinkedIn pesquisa usando Olá [SCIM](http://www.simplecloud.info/) protocolo.</span><span class="sxs-lookup"><span data-stu-id="46205-110">Azure Active Directory integrates with LinkedIn Lookup using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-lookup"></a><span data-ttu-id="46205-111">Atribuir usuários tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="46205-111">Assigning users tooLinkedIn Lookup</span></span>

<span data-ttu-id="46205-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46205-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="46205-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="46205-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="46205-114">Antes de configurar e habilitar Olá provisionar um serviço, você precisará toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="46205-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Lookup.</span></span> <span data-ttu-id="46205-115">Depois de decidir, você pode atribuir essas tooLinkedIn usuários pesquisa seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="46205-115">Once decided, you can assign these users tooLinkedIn Lookup by following hello instructions here:</span></span>

[<span data-ttu-id="46205-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="46205-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a><span data-ttu-id="46205-117">Dicas importantes para atribuir usuários tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="46205-117">Important tips for assigning users tooLinkedIn Lookup</span></span>

*   <span data-ttu-id="46205-118">É recomendável que um único usuário do AD do Azure ser atribuído a saudação de tootest de pesquisa tooLinkedIn configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46205-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Lookup tootest hello provisioning configuration.</span></span> <span data-ttu-id="46205-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="46205-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="46205-120">Ao atribuir uma pesquisa de tooLinkedIn do usuário, você deve selecionar Olá **usuário** função na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="46205-120">When assigning a user tooLinkedIn Lookup, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="46205-121">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="46205-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a><span data-ttu-id="46205-122">Configurando tooLinkedIn pesquisa o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="46205-122">Configuring user provisioning tooLinkedIn Lookup</span></span>

<span data-ttu-id="46205-123">Esta seção orienta você conectar-se a conta de usuário SCIM da pesquisa de tooLinkedIn seu AD do Azure API de provisionamento e configuração Olá toocreate do serviço de provisionamento, atualizar e desativar contas na pesquisa do LinkedIn com base em usuários e grupos de usuário atribuído atribuição no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="46205-123">This section guides you through connecting your Azure AD tooLinkedIn Lookup's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="46205-124">Você também pode escolher tooenabled baseado no SAML SSO para pesquisa LinkedIn, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46205-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Lookup, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="46205-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="46205-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a><span data-ttu-id="46205-126">conta de usuário automático tooconfigure provisionamento tooLinkedIn pesquisa no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="46205-126">tooconfigure automatic user account provisioning tooLinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="46205-127">primeira etapa de saudação é tooretrieve seu token de acesso do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="46205-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="46205-128">Se você for um administrador corporativo, você poderá provisionar um token de acesso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="46205-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="46205-129">No Centro de sua conta, vá muito**configurações &gt; configurações globais** e abra hello **SCIM instalação** painel.</span><span class="sxs-lookup"><span data-stu-id="46205-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="46205-130">Se você estiver acessando o Centro de contas Olá diretamente em vez de através de um link, você pode acessar usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="46205-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="46205-131">Entrar no Centro de tooAccount.</span><span class="sxs-lookup"><span data-stu-id="46205-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="46205-132">Selecione **Administrador &gt; Configurações de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="46205-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="46205-133">Clique em **avançado integrações** na lateral esquerda da saudação.</span><span class="sxs-lookup"><span data-stu-id="46205-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="46205-134">Você é direcionado toohello Centro de contas.</span><span class="sxs-lookup"><span data-stu-id="46205-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="46205-135">Clique em **+ adicionar a nova configuração de SCIM** e siga o procedimento Olá preenchendo cada campo.</span><span class="sxs-lookup"><span data-stu-id="46205-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="46205-136">Quando a atribuição automática de licenças não está habilitada, isso significa que somente os dados de usuário estão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="46205-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Provisionamento do LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="46205-138">Quando a atribuição de autolicense estiver habilitada, você precisa toonote a instância do aplicativo e o tipo de licença.</span><span class="sxs-lookup"><span data-stu-id="46205-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="46205-139">Licenças são atribuídas para entrega, primeiro atender base até que todas as licenças de saudação são feitas.</span><span class="sxs-lookup"><span data-stu-id="46205-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Provisionamento do LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="46205-141">Clique em **Gerar token**.</span><span class="sxs-lookup"><span data-stu-id="46205-141">Click **Generate token**.</span></span> <span data-ttu-id="46205-142">Você deve ver o vídeo de token de acesso em Olá **token de acesso** campo.</span><span class="sxs-lookup"><span data-stu-id="46205-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="46205-143">Salve a área de transferência de tooyour de token de acesso ou o computador antes de sair da página hello.</span><span class="sxs-lookup"><span data-stu-id="46205-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="46205-144">Em seguida, entrar toohello [portal do Azure](https://portal.azure.com)e procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="46205-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="46205-145">Se você já tiver configurado a pesquisa LinkedIn para logon único, procure sua instância do LinkedIn pesquisa usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="46205-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using hello search field.</span></span> <span data-ttu-id="46205-146">Caso contrário, selecione **adicionar** e procure **LinkedIn pesquisa** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="46205-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in hello application gallery.</span></span> <span data-ttu-id="46205-147">Selecione LinkedIn pesquisa Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="46205-147">Select LinkedIn Lookup from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="46205-148">Selecione sua instância do LinkedIn pesquisa e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="46205-148">Select your instance of LinkedIn Lookup, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="46205-149">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="46205-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Provisionamento do LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="46205-151">Preencha Olá seguintes campos em **credenciais de administrador** :</span><span class="sxs-lookup"><span data-stu-id="46205-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="46205-152">Em Olá **URL do locatário** , digite https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="46205-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="46205-153">Em Olá **segredo do Token** campo, insira o token de acesso de saudação gerado na etapa 1 e clique em **Conexão de teste** .</span><span class="sxs-lookup"><span data-stu-id="46205-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="46205-154">Você verá uma notificação de êxito no lado de superiordireito de saudação do seu portal.</span><span class="sxs-lookup"><span data-stu-id="46205-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="46205-155">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="46205-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="46205-156">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46205-156">Click **Save**.</span></span> 

14) <span data-ttu-id="46205-157">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário e grupo Olá que serão sincronizados do AD do Azure tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="46205-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Lookup.</span></span> <span data-ttu-id="46205-158">Observe que Olá atributos selecionados como **correspondência** propriedades serão usados toomatch Olá as contas de usuário e grupos na pesquisa do LinkedIn para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="46205-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="46205-159">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="46205-159">Select hello Save button toocommit any changes.</span></span>

![Provisionamento do LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="46205-161">tooenable Olá serviço de provisionamento do AD do Azure para pesquisa LinkedIn, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="46205-161">tooenable hello Azure AD provisioning service for LinkedIn Lookup, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="46205-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46205-162">Click **Save**.</span></span> 

<span data-ttu-id="46205-163">Isso iniciará a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooLinkedIn pesquisa na seção usuários e grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="46205-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Lookup in hello Users and Groups section.</span></span> <span data-ttu-id="46205-164">Observe que a sincronização inicial Olá levará mais tooperform que sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="46205-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="46205-165">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo de pesquisa do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="46205-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="46205-166">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="46205-166">Additional Resources</span></span>

* [<span data-ttu-id="46205-167">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="46205-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="46205-168">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46205-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
