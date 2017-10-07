---
title: "Tutorial: Configurar o Cerner Central para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como tooautomatically do Active Directory do Azure tooconfigure provisionar a lista de tooa de usuários em Cerner Central."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="3dd96-103">Tutorial: Configurar o Cerner Central para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="3dd96-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="3dd96-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform em Cerner Central e o Azure AD tooautomatically provisão de provisionar contas de usuário e da lista de usuário do AD do Azure tooa no Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="3dd96-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3dd96-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3dd96-105">Prerequisites</span></span>

<span data-ttu-id="3dd96-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3dd96-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="3dd96-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dd96-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="3dd96-108">Um locatário do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="3dd96-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="3dd96-109">Active Directory do Azure se integra ao centro Cerner usando Olá [SCIM](http://www.simplecloud.info/) protocolo.</span><span class="sxs-lookup"><span data-stu-id="3dd96-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="3dd96-110">Atribuir usuários tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="3dd96-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="3dd96-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3dd96-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="3dd96-112">No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd96-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="3dd96-113">Antes de configurar e habilitar Olá provisionar um serviço, você deve decidir quais usuários e/ou grupos no AD do Azure representam usuários Olá que precisam acessar tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="3dd96-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="3dd96-114">Depois de decidir, você pode atribuir essas tooCerner usuários Central seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="3dd96-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="3dd96-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="3dd96-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="3dd96-116">Dicas importantes para atribuir usuários tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="3dd96-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="3dd96-117">É recomendável que um único usuário do AD do Azure receberá tooCerner tootest Central Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="3dd96-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="3dd96-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3dd96-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="3dd96-119">Depois que o teste inicial for concluída para um único usuário, centro Cerner recomenda atribuir toda a lista de usuários devem tooaccess Olá lista de usuário de qualquer toobe provisionado tooCerner Cerner solução (não apenas Cerner Central).</span><span class="sxs-lookup"><span data-stu-id="3dd96-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="3dd96-120">Outras soluções Cerner aproveitam essa lista de usuários na lista de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="3dd96-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="3dd96-121">Ao atribuir um usuário tooCerner Central, você deve selecionar Olá **usuário** função na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dd96-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="3dd96-122">Os usuários com função de "Acesso padrão" hello são excluídos do provisionamento.</span><span class="sxs-lookup"><span data-stu-id="3dd96-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="3dd96-123">Configurando tooCerner Central de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="3dd96-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="3dd96-124">Esta seção orienta você conectar-se a lista de usuários do AD do Azure tooCerner Central com conta de usuário SCIM da Cerner API de provisionamento e configuração Olá toocreate do serviço de provisionamento, atualizar e desabilitar o usuário atribuído com base em contas em Cerner Central atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd96-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="3dd96-125">Você também pode escolher tooenabled baseado no SAML SSO Cerner centrais, seguindo instruções Olá fornecidas no [portal do Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3dd96-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="3dd96-126">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="3dd96-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="3dd96-127">Para obter mais informações, consulte Olá [tutorial do logon único centro Cerner](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3dd96-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="3dd96-128">conta de usuário automático tooconfigure provisionamento tooCerner Central no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="3dd96-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="3dd96-129">Em ordem tooprovision usuário contas tooCerner Central, será necessário toorequest uma conta do sistema Cerner Central de Cerner e gerar um token de portador OAuth que o AD do Azure pode usar o ponto de extremidade do tooconnect tooCerner SCIM.</span><span class="sxs-lookup"><span data-stu-id="3dd96-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="3dd96-130">Também é recomendável que a integração Olá executada em um ambiente de área restrita Cerner antes de implantar tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3dd96-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="3dd96-131">Olá primeira etapa é tooensure pessoas de saudação Gerenciando Olá Cerner e integração do AD do Azure tem uma conta de CernerCare, que é necessário tooaccess Olá documentação toocomplete necessário Olá instruções.</span><span class="sxs-lookup"><span data-stu-id="3dd96-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="3dd96-132">Se necessário, use Olá URLs abaixo toocreate CernerCare contas em cada ambiente aplicável.</span><span class="sxs-lookup"><span data-stu-id="3dd96-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="3dd96-133">Área restrita: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="3dd96-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="3dd96-134">Produção:  https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="3dd96-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="3dd96-135">Em seguida, será necessário criar uma conta do sistema para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dd96-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="3dd96-136">Use as instruções de saudação abaixo toorequest uma conta do sistema para seus ambientes de produção e de área restrita.</span><span class="sxs-lookup"><span data-stu-id="3dd96-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="3dd96-137">Instruções:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="3dd96-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="3dd96-138">Área restrita: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3dd96-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="3dd96-139">Produção:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3dd96-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="3dd96-140">Em seguida, gere um token de portador OAuth para cada uma de suas contas do sistema.</span><span class="sxs-lookup"><span data-stu-id="3dd96-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="3dd96-141">toodo isso, siga Olá as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="3dd96-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="3dd96-142">Instruções: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="3dd96-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="3dd96-143">Área restrita: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3dd96-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="3dd96-144">Produção:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="3dd96-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="3dd96-145">Finalmente, você precisa tooacquire usuário lista Realm IDs para ambos os ambientes de área restrita e de produção de hello na configuração de saudação do Cerner toocomplete.</span><span class="sxs-lookup"><span data-stu-id="3dd96-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="3dd96-146">Para obter informações sobre como tooacquire isso, consulte: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="3dd96-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="3dd96-147">Agora você pode configurar tooCerner de contas de usuário do AD do Azure tooprovision.</span><span class="sxs-lookup"><span data-stu-id="3dd96-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="3dd96-148">Entrar toohello [portal do Azure](https://portal.azure.com)e procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="3dd96-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="3dd96-149">Se você já tiver configurado Cerner Central para o logon único, pesquisa de sua instância do Cerner Central usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dd96-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="3dd96-150">Caso contrário, selecione **adicionar** e procure **Cerner Central** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3dd96-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="3dd96-151">Selecione Cerner Central Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3dd96-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="3dd96-152">Selecione a instância do Cerner Central, selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="3dd96-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="3dd96-153">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="3dd96-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Provisionamento do Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="3dd96-155">Preencha Olá seguintes campos em **credenciais de administrador**:</span><span class="sxs-lookup"><span data-stu-id="3dd96-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="3dd96-156">Em Olá **URL do locatário** campo, digite uma URL no formato Olá abaixo, substituindo "Lista-Realm-ID de usuário" com a ID do território Olá você copiou na etapa &#4;.</span><span class="sxs-lookup"><span data-stu-id="3dd96-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="3dd96-157">Área restrita: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="3dd96-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="3dd96-158">Produção: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="3dd96-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="3dd96-159">Em Olá **segredo do Token** campo, insira o token de portador OAuth Olá gerado na etapa &#3; e clique em **Conexão de teste**.</span><span class="sxs-lookup"><span data-stu-id="3dd96-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="3dd96-160">Você verá uma notificação de êxito no lado de superiordireito de saudação do seu portal.</span><span class="sxs-lookup"><span data-stu-id="3dd96-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="3dd96-161">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="3dd96-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="3dd96-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3dd96-162">Click **Save**.</span></span> 

12. <span data-ttu-id="3dd96-163">Em Olá **mapeamentos de atributo** seção, examine o usuário hello e toobe de atributos de grupo sincronizado do AD do Azure tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="3dd96-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="3dd96-164">Olá atributos selecionados como **correspondência** propriedades são usados toomatch Olá as contas de usuário e grupos no Centro de Cerner para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="3dd96-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="3dd96-165">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="3dd96-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="3dd96-166">tooenable Olá serviço de provisionamento do AD do Azure Cerner centrais, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="3dd96-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="3dd96-167">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3dd96-167">Click **Save**.</span></span> 

<span data-ttu-id="3dd96-168">Isso inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooCerner Central, na seção usuários e grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3dd96-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="3dd96-169">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde Olá serviço de provisionamento do AD do Azure está em execução.</span><span class="sxs-lookup"><span data-stu-id="3dd96-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="3dd96-170">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="3dd96-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="3dd96-171">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3dd96-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dd96-172">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3dd96-172">Additional resources</span></span>

* [<span data-ttu-id="3dd96-173">Cerner Central: Publicação de dados de identidade usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dd96-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="3dd96-174">Tutorial: Configurar o Cerner Central para logon único com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dd96-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="3dd96-175">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="3dd96-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="3dd96-176">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3dd96-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="3dd96-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3dd96-177">Next steps</span></span>
* <span data-ttu-id="3dd96-178">[Saiba como tooreview registra e obter relatórios sobre a atividade de provisionamento](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="3dd96-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
