---
title: "Tutorial: Configurando o Google Apps para o provisionamento automático de usuário no Azure | Microsoft Docs"
description: "Saiba como contas de usuário de provisionar e provisionar eliminação de tooautomatically do AD do Azure tooGoogle aplicativos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="42798-103">Tutorial: Configurando o Google Apps para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="42798-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="42798-104">Olá objetivo deste tutorial é tooshow que Olá etapas necessárias tooperform no Google Apps e o Azure AD provisão de tooautomatically e desprovisionar contas de usuário do AD do Azure tooGoogle aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42798-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42798-105">Prerequisites</span></span>

<span data-ttu-id="42798-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="42798-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="42798-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42798-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="42798-108">É necessário ter um locatário válido do Google Apps for Work ou do Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="42798-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="42798-109">Você pode usar uma conta de avaliação gratuita para qualquer serviço.</span><span class="sxs-lookup"><span data-stu-id="42798-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="42798-110">Uma conta de usuário no Google Apps com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="42798-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="42798-111">Atribuir usuários tooGoogle aplicativos</span><span class="sxs-lookup"><span data-stu-id="42798-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="42798-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="42798-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="42798-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="42798-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar o aplicativo do Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="42798-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="42798-115">Depois de decidir, você pode atribuir esses aplicativos do usuários tooyour Google Apps, seguindo as instruções de saudação aqui: [atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="42798-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="42798-116">É recomendável que um único usuário do AD do Azure ser atribuído a saudação de tootest aplicativos de tooGoogle configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="42798-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="42798-117">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="42798-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="42798-118">Ao atribuir um usuário tooGoogle aplicativos, você deve selecionar Olá usuário ou função de "Grupo" na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="42798-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="42798-119">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="42798-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="42798-120">Habilitar o provisionamento automatizado de usuários</span><span class="sxs-lookup"><span data-stu-id="42798-120">Enable automated user provisioning</span></span>

<span data-ttu-id="42798-121">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do aplicativos tooGoogle seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Google Apps com base na atribuição de usuário e grupo no AD do Azure .</span><span class="sxs-lookup"><span data-stu-id="42798-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="42798-122">Você também pode escolher tooenabled baseado no SAML SSO para o Google Apps, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42798-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="42798-123">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="42798-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="42798-124">Configurar o provisionamento automático de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="42798-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="42798-125">Outra opção viável para automatizar o provisionamento de tooGoogle aplicativos de usuário é toouse [sincronização de diretório de aplicativos da Google (GADS)](https://support.google.com/a/answer/106368?hl=en) que provisiona seu tooGoogle de identidades do Active Directory local aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="42798-126">Por outro lado, a solução Olá neste tutorial provisiona usuários do Active Directory do Azure (nuvem) e grupos habilitados para email tooGoogle aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="42798-127">O logon no hello [Console de administração do Google Apps](http://admin.google.com/) usando sua conta de administrador e, em seguida, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="42798-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="42798-128">Se você não vir o link hello, podem estar ocultos em Olá **mais controles** menu na parte inferior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="42798-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Clique em Segurança.][10]

2. <span data-ttu-id="42798-130">Em Olá **segurança** , clique em **referência da API**.</span><span class="sxs-lookup"><span data-stu-id="42798-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Clique em Referência de API.][15]

3. <span data-ttu-id="42798-132">Selecione **Habilitar o acesso à API**.</span><span class="sxs-lookup"><span data-stu-id="42798-132">Select **Enable API access**.</span></span>
   
    ![Clique em Referência de API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="42798-134">Para cada usuário que você pretende tooprovision tooGoogle aplicativos, seu nome de usuário no Active Directory do Azure *deve* ser domínio personalizado tooa associado.</span><span class="sxs-lookup"><span data-stu-id="42798-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="42798-135">Por exemplo, nomes de usuários parecidos com bob@contoso.onmicrosoft.com não são aceitos pelo Google Apps, enquanto bob@contoso.com é aceito.</span><span class="sxs-lookup"><span data-stu-id="42798-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="42798-136">É possível alterar o domínio de um usuário existente editando as propriedades dele no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="42798-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="42798-137">Instruções de como tooset um domínio personalizado para o Active Directory do Azure e o Google Apps inclusos nos seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="42798-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="42798-138">Se você ainda não adicionou um nome de domínio personalizado tooyour Active Directory do Azure, siga Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="42798-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="42798-139">a.</span><span class="sxs-lookup"><span data-stu-id="42798-139">a.</span></span> <span data-ttu-id="42798-140">Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42798-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="42798-141">Na lista de diretório hello, selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="42798-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="42798-142">b.</span><span class="sxs-lookup"><span data-stu-id="42798-142">b.</span></span> <span data-ttu-id="42798-143">Clique em **nome dos domínios** Olá painel de navegação esquerdo e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="42798-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![adição de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="42798-146">c.</span><span class="sxs-lookup"><span data-stu-id="42798-146">c.</span></span> <span data-ttu-id="42798-147">Digite seu nome de domínio em Olá **nome de domínio** campo.</span><span class="sxs-lookup"><span data-stu-id="42798-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="42798-148">Esse nome de domínio deve ser Olá mesmo nome de domínio que você pretende toouse Google Apps.</span><span class="sxs-lookup"><span data-stu-id="42798-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="42798-149">Quando estiver pronto, clique em Olá **Adicionar domínio** botão.</span><span class="sxs-lookup"><span data-stu-id="42798-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![nome de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="42798-151">d.</span><span class="sxs-lookup"><span data-stu-id="42798-151">d.</span></span> <span data-ttu-id="42798-152">Clique em **próximo** toogo página de verificação de toohello.</span><span class="sxs-lookup"><span data-stu-id="42798-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="42798-153">tooverify que você possui este domínio, você deve editar registros DNS do domínio de saudação de acordo com os valores de toohello fornecidos nessa página.</span><span class="sxs-lookup"><span data-stu-id="42798-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="42798-154">Você pode escolher tooverify usando **registros MX** ou **registros TXT**, dependendo do que você selecionar Olá **tipo de registro** opção.</span><span class="sxs-lookup"><span data-stu-id="42798-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="42798-155">Para obter instruções mais abrangentes sobre como nome de domínio de tooverify com o AD do Azure, consulte [adicionar seu próprio nome de domínio tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="42798-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="42798-157">e.</span><span class="sxs-lookup"><span data-stu-id="42798-157">e.</span></span> <span data-ttu-id="42798-158">Repita Olá etapas para todos os domínios de saudação que você pretende tooadd tooyour directory anteriores.</span><span class="sxs-lookup"><span data-stu-id="42798-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="42798-159">Agora que você confirmou todos os domínios com o Azure AD, agora deve confirmá-los novamente com o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="42798-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="42798-160">Para cada domínio que já não está registrado com o Google Apps, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="42798-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="42798-161">a.</span><span class="sxs-lookup"><span data-stu-id="42798-161">a.</span></span> <span data-ttu-id="42798-162">Em Olá [Console de administração do Google Apps](http://admin.google.com/), clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="42798-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Clique em Domínios][20]

    <span data-ttu-id="42798-164">b.</span><span class="sxs-lookup"><span data-stu-id="42798-164">b.</span></span> <span data-ttu-id="42798-165">Clique em **Adicionar um domínio ou um alias de domínio**.</span><span class="sxs-lookup"><span data-stu-id="42798-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Adicione um novo domínio][21]

    <span data-ttu-id="42798-167">c.</span><span class="sxs-lookup"><span data-stu-id="42798-167">c.</span></span> <span data-ttu-id="42798-168">Selecione **adicionar outro domínio**e digite o nome de saudação do domínio Olá que deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="42798-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Digite o nome de domínio][22]

    <span data-ttu-id="42798-170">d.</span><span class="sxs-lookup"><span data-stu-id="42798-170">d.</span></span> <span data-ttu-id="42798-171">Clique em **Continuar e confirmar a propriedade do domínio**.</span><span class="sxs-lookup"><span data-stu-id="42798-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="42798-172">Siga Olá tooverify de etapas que você possui o nome de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="42798-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="42798-173">Para obter instruções abrangentes sobre como tooverify seu domínio com o Google Apps, consulte.</span><span class="sxs-lookup"><span data-stu-id="42798-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="42798-174">[Confirmar a propriedade do site com o Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="42798-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="42798-175">e.</span><span class="sxs-lookup"><span data-stu-id="42798-175">e.</span></span> <span data-ttu-id="42798-176">Repita Olá etapas para todos os domínios adicionais que você pretende tooadd tooGoogle aplicativos anteriores.</span><span class="sxs-lookup"><span data-stu-id="42798-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="42798-177">Se você alterar domínio primário Olá para seu locatário do Google Apps, e se você já tiver configurado o logon único com o Azure AD, você tem toorepeat etapa #3 em [etapa 2: Habilitar logon único](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="42798-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="42798-178">Em Olá [Console de administração do Google Apps](http://admin.google.com/), clique em **funções de administrador**.</span><span class="sxs-lookup"><span data-stu-id="42798-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Clique em Google Apps][26]

7. <span data-ttu-id="42798-180">Determine qual administrador de conta que você deseja que o provisionamento de usuário toomanage toouse.</span><span class="sxs-lookup"><span data-stu-id="42798-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="42798-181">Para Olá **função admin** dessa conta, editar Olá **privilégios** para essa função.</span><span class="sxs-lookup"><span data-stu-id="42798-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="42798-182">Verifique se ele tem todos os Olá **privilégios de API de administração** habilitado para que essa conta pode ser usada para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="42798-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Clique em Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="42798-184">Se você estiver configurando um ambiente de produção, Olá melhor prática é toocreate uma conta de administrador no Google Apps especificamente para essa etapa.</span><span class="sxs-lookup"><span data-stu-id="42798-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="42798-185">Essas contas devem ter associada a ele uma função de administrador que tem os privilégios necessários API hello.</span><span class="sxs-lookup"><span data-stu-id="42798-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="42798-186">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="42798-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="42798-187">Se você já tiver configurado o Google Apps para o logon único, procure sua instância do usando o campo de pesquisa de saudação do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="42798-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="42798-188">Caso contrário, selecione **adicionar** e procure **Google Apps** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="42798-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="42798-189">Selecione o Google Apps Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="42798-190">Selecione sua instância do Google Apps e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="42798-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="42798-191">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="42798-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![provisionamento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="42798-193">Em Olá **credenciais de administrador** seção, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="42798-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="42798-194">Isso abre uma caixa de diálogo de autorização do Google Apps em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="42798-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="42798-195">Confirme que deseja toogive Active Directory do Azure toomake as alterações de permissão de locatário tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="42798-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="42798-196">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="42798-196">Click **Accept**.</span></span>
    
     ![Confirme permissões.][28]

14. <span data-ttu-id="42798-198">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a aplicativos do Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="42798-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="42798-199">Se a conexão de saudação falhar, certifique-se de que sua conta do Google Apps tem permissões de administrador de equipe e tente Olá **"Autorizar"** etapa novamente.</span><span class="sxs-lookup"><span data-stu-id="42798-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="42798-200">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="42798-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="42798-201">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="42798-201">Click **Save.**</span></span>

17. <span data-ttu-id="42798-202">Em Olá mapeamentos, selecione **sincronizar do Azure Active Directory Users tooGoogle aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="42798-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="42798-203">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooGoogle aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42798-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="42798-204">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Google Apps para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="42798-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="42798-205">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="42798-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="42798-206">tooenable Olá serviço de provisionamento do AD do Azure para Google Apps, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="42798-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="42798-207">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="42798-207">Click **Save.**</span></span>

<span data-ttu-id="42798-208">Iniciar a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos aplicativos tooGoogle na seção usuários e grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="42798-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="42798-209">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="42798-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="42798-210">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="42798-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42798-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="42798-211">Additional resources</span></span>

* [<span data-ttu-id="42798-212">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="42798-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42798-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42798-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="42798-214">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="42798-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png