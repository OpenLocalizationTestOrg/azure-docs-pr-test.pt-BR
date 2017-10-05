---
title: "Tutorial: Configurando o Google Apps para o provisionamento automático de usuário no Azure | Microsoft Docs"
description: "Saiba como provisionar e desprovisionar automaticamente contas de usuário do Azure AD para o Google Apps."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="0c9e8-103">Tutorial: Configurando o Google Apps para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="0c9e8-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="0c9e8-104">O objetivo deste tutorial é mostrar as etapas que precisam ser realizadas no Google Apps e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c9e8-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c9e8-105">Prerequisites</span></span>

<span data-ttu-id="0c9e8-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0c9e8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0c9e8-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0c9e8-108">É necessário ter um locatário válido do Google Apps for Work ou do Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="0c9e8-109">Você pode usar uma conta de avaliação gratuita para qualquer serviço.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="0c9e8-110">Uma conta de usuário no Google Apps com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="0c9e8-111">Atribuindo usuários ao Google Apps</span><span class="sxs-lookup"><span data-stu-id="0c9e8-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="0c9e8-112">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0c9e8-113">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0c9e8-114">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao aplicativo Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="0c9e8-115">Depois de decidir, atribua esses usuários ao aplicativo Google Apps seguindo estas instruções: [Atribuir um usuário ou grupo a um aplicativo empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="0c9e8-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="0c9e8-116">Recomendamos a atribuição de um único usuário do Azure AD ao Google Apps para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="0c9e8-117">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="0c9e8-118">Ao atribuir um usuário ao Google Apps, é necessário selecionar a função Usuário ou “Grupo” na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="0c9e8-119">A função de "Acesso Padrão" não funciona para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0c9e8-120">Habilitar o provisionamento automatizado de usuários</span><span class="sxs-lookup"><span data-stu-id="0c9e8-120">Enable automated user provisioning</span></span>

<span data-ttu-id="0c9e8-121">Esta seção explica como conectar o Azure AD à API de provisionamento de conta de usuário do Google Apps e como configurar o serviço de provisionamento para criar, atualizar e desabilitar contas de usuário atribuídas no Google Apps, com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="0c9e8-122">Você também pode optar por habilitar o Logon Único baseado em SAML no Google Apps, seguindo as instruções fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c9e8-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c9e8-123">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="0c9e8-124">Configurar o provisionamento automático de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="0c9e8-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="0c9e8-125">Outra opção viável para automatizar o provisionamento de usuários para o Google Apps é usar a [Ferramenta de Sincronização do Google Apps (GADS)](https://support.google.com/a/answer/106368?hl=en) , que provisiona suas identidades do Active Directory local para o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="0c9e8-126">Por outro lado, a solução neste tutorial provisiona seus usuários do Active Directory do Azure (nuvem) e grupos habilitados para email para o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="0c9e8-127">Entre no [Console de Admin do Google Apps](http://admin.google.com/) usando sua conta de administrador e clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="0c9e8-128">Se você não enxergar o link, ele pode estar oculto sob o menu **Mais Controles** , na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Clique em Segurança.][10]

2. <span data-ttu-id="0c9e8-130">Na página **Segurança**, clique em **Referência de API**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![Clique em Referência de API.][15]

3. <span data-ttu-id="0c9e8-132">Selecione **Habilitar o acesso à API**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-132">Select **Enable API access**.</span></span>
   
    ![Clique em Referência de API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="0c9e8-134">Para cada usuário que você pretende provisionar para o Google Apps, seu nome de usuário no Active Directory do Azure *deve* estar vinculado a um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="0c9e8-135">Por exemplo, nomes de usuários parecidos com bob@contoso.onmicrosoft.com não são aceitos pelo Google Apps, enquanto bob@contoso.com é aceito.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="0c9e8-136">É possível alterar o domínio de um usuário existente editando as propriedades dele no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="0c9e8-137">Instruções sobre como definir um domínio personalizado para o Azure Active Directory e o Google Apps estão incluídas nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="0c9e8-138">Se você ainda não adicionou um nome de domínio personalizado ao Azure Active Directory, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0c9e8-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="0c9e8-139">a.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-139">a.</span></span> <span data-ttu-id="0c9e8-140">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="0c9e8-141">Na lista de diretórios, selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="0c9e8-142">b.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-142">b.</span></span> <span data-ttu-id="0c9e8-143">Clique em **Nome de domínios** no painel de navegação à esquerda e, depois, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![adição de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="0c9e8-146">c.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-146">c.</span></span> <span data-ttu-id="0c9e8-147">Digite seu nome de domínio no campo **Nome de domínio** .</span><span class="sxs-lookup"><span data-stu-id="0c9e8-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="0c9e8-148">Esse nome de domínio deve ser o mesmo nome de domínio que você pretende usar para o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="0c9e8-149">Quando estiver pronto, clique no botão **Adicionar Domínio**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-149">When ready, click the **Add Domain** button.</span></span>
     
     ![nome de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="0c9e8-151">d.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-151">d.</span></span> <span data-ttu-id="0c9e8-152">Clique em **Avançar** para ir até a página de verificação.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="0c9e8-153">Para verificar se você possui esse domínio, é preciso editar os registros DNS do domínio de acordo com os valores fornecidos nesta página.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="0c9e8-154">É possível optar por verificar usando **Registros MX** ou **Registros TXT**, dependendo do que você selecionar na opção **Tipo de Registro**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="0c9e8-155">Para obter instruções mais abrangentes sobre como confirmar o nome de domínio com o Azure AD, consulte [Adicionar seu próprio nome de domínio ao Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0c9e8-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="0c9e8-157">e.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-157">e.</span></span> <span data-ttu-id="0c9e8-158">Repita as etapas anteriores para todos os domínios que você pretende adicionar ao diretório.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="0c9e8-159">Agora que você confirmou todos os domínios com o Azure AD, agora deve confirmá-los novamente com o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="0c9e8-160">Para cada domínio que já não estiver registrado com o Google Apps, realize as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c9e8-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="0c9e8-161">a.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-161">a.</span></span> <span data-ttu-id="0c9e8-162">No [Console de Administrador do Google Apps](http://admin.google.com/), clique em **Domínios**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Clique em Domínios][20]

    <span data-ttu-id="0c9e8-164">b.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-164">b.</span></span> <span data-ttu-id="0c9e8-165">Clique em **Adicionar um domínio ou um alias de domínio**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Adicione um novo domínio][21]

    <span data-ttu-id="0c9e8-167">c.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-167">c.</span></span> <span data-ttu-id="0c9e8-168">Selecione **Adicionar outro domínio**e digite o nome do domínio que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![Digite o nome de domínio][22]

    <span data-ttu-id="0c9e8-170">d.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-170">d.</span></span> <span data-ttu-id="0c9e8-171">Clique em **Continuar e confirmar a propriedade do domínio**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="0c9e8-172">Em seguida, siga as etapas para verificar se você possui o nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="0c9e8-173">Para obter instruções abrangentes sobre como confirmar seu domínio com o Google Apps, consulte.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="0c9e8-174">[Confirmar a propriedade do site com o Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="0c9e8-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="0c9e8-175">e.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-175">e.</span></span> <span data-ttu-id="0c9e8-176">Repita as etapas anteriores para os domínios adicionais que você pretende adicionar ao Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="0c9e8-177">Se você alterar o domínio primário do locatário do Google Apps e já tiver configurado o logon único com o Azure AD, precisará repetir a etapa 3 em [Etapa 2: Habilitar Logon Único](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0c9e8-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="0c9e8-178">No [Console de Administrador do Google Apps](http://admin.google.com/), clique em **Funções de Administrador**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Clique em Google Apps][26]

7. <span data-ttu-id="0c9e8-180">Determine a conta de administrador que você gostaria de usar para gerenciar o provisionamento de usuários.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="0c9e8-181">Para a **função de administrador** dessa conta, edite os **Privilégios** para essa função.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="0c9e8-182">Verifique se ela tem todos os **Privilégios de API de Administrador** habilitados, para que essa conta possa ser usada para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Clique em Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="0c9e8-184">Se estiver configurando um ambiente de produção, a melhor prática será criar uma conta do administrador no Google Apps especificamente para esta etapa.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="0c9e8-185">Essas contas devem ter uma função de administrador associada a elas que tem os privilégios de API necessários.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="0c9e8-186">No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="0c9e8-187">Se você já tiver configurado o Google Apps para logon único, pesquise a instância do Google Apps usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="0c9e8-188">Caso contrário, selecione **Adicionar** e pesquise **Google Apps** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="0c9e8-189">Selecione o Google Apps nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="0c9e8-190">Selecione a instância do Google Apps e, depois, a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="0c9e8-191">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![provisionamento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="0c9e8-193">Na seção **Credenciais de Administrador**, clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="0c9e8-194">Isso abre uma caixa de diálogo de autorização do Google Apps em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="0c9e8-195">Confirme que você deseja dar permissão ao Active Directory do Azure para fazer alterações em seu locatário do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="0c9e8-196">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-196">Click **Accept**.</span></span>
    
     ![Confirme permissões.][28]

14. <span data-ttu-id="0c9e8-198">No portal do Azure, clique em **Testar Conectividade** para garantir que o Azure AD pode se conectar ao aplicativo Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="0c9e8-199">Se a conexão falhar, verifique se sua conta do Google Apps tem permissões de Administrador de Equipe e repita a etapa **“Autorizar”**.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="0c9e8-200">Insira o endereço de email de uma pessoa ou um grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="0c9e8-201">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="0c9e8-201">Click **Save.**</span></span>

17. <span data-ttu-id="0c9e8-202">Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Google Apps.**</span><span class="sxs-lookup"><span data-stu-id="0c9e8-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="0c9e8-203">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário que são sincronizados do Azure AD para o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="0c9e8-204">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário do Google Apps em operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="0c9e8-205">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="0c9e8-206">Para habilitar o serviço de provisionamento do Azure AD no Google Apps, altere o **Status de Provisionamento** para **Ativado** na seção Configurações</span><span class="sxs-lookup"><span data-stu-id="0c9e8-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="0c9e8-207">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="0c9e8-207">Click **Save.**</span></span>

<span data-ttu-id="0c9e8-208">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Google Apps na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="0c9e8-209">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0c9e8-210">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento no aplicativo Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0c9e8-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c9e8-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0c9e8-211">Additional resources</span></span>

* [<span data-ttu-id="0c9e8-212">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="0c9e8-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c9e8-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c9e8-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0c9e8-214">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="0c9e8-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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