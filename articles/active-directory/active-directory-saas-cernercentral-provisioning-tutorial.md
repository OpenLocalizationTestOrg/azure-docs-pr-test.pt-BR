---
title: "Tutorial: Configurar o Cerner Central para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar o Azure Active Directory para provisionar automaticamente usuários para uma lista no Cerner Central."
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
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="66c5a-103">Tutorial: Configurar o Cerner Central para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="66c5a-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="66c5a-104">O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Cerner Central e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para uma lista de usuários no Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="66c5a-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="66c5a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66c5a-105">Prerequisites</span></span>

<span data-ttu-id="66c5a-106">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="66c5a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="66c5a-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66c5a-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="66c5a-108">Um locatário do Cerner Central</span><span class="sxs-lookup"><span data-stu-id="66c5a-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="66c5a-109">O Azure Active Directory integra-se com o Cerner Central usando o protocolo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="66c5a-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="66c5a-110">Atribuir usuários ao Cerner Central</span><span class="sxs-lookup"><span data-stu-id="66c5a-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="66c5a-111">O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados.</span><span class="sxs-lookup"><span data-stu-id="66c5a-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="66c5a-112">No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="66c5a-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="66c5a-113">Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários e/ou grupos no Azure AD representam os usuários que precisam de acesso ao Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="66c5a-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="66c5a-114">Depois de decidir, atribua esses usuários ao Cerner Central seguindo estas instruções:</span><span class="sxs-lookup"><span data-stu-id="66c5a-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="66c5a-115">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="66c5a-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="66c5a-116">Dicas importantes para atribuir usuários ao Cerner Central</span><span class="sxs-lookup"><span data-stu-id="66c5a-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="66c5a-117">Recomendamos a atribuição de um único usuário do Azure AD ao Cerner Central para testar a configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="66c5a-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="66c5a-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="66c5a-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="66c5a-119">Depois que o teste inicial for concluído para um único usuário, o Cerner Central recomenda atribuir toda a lista de usuários que deve acessar qualquer solução Cerner (não apenas Cerner Central) para que esta seja provisionada para a lista do usuário do Cerner.</span><span class="sxs-lookup"><span data-stu-id="66c5a-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="66c5a-120">Outras soluções Cerner aproveitam essa lista de usuários na lista do usuário.</span><span class="sxs-lookup"><span data-stu-id="66c5a-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="66c5a-121">Ao atribuir um usuário ao Cerner Central, selecione a função **Usuário** na caixa de diálogo de atribuição.</span><span class="sxs-lookup"><span data-stu-id="66c5a-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="66c5a-122">Os usuários com a função de "Acesso Padrão" são excluídos do provisionamento.</span><span class="sxs-lookup"><span data-stu-id="66c5a-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="66c5a-123">Configurar o provisionamento de usuários no Cerner Central</span><span class="sxs-lookup"><span data-stu-id="66c5a-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="66c5a-124">Esta seção ensina como conectar o seu Azure AD à Lista do Usuário do Cerner Central à API de provisionamento de conta de usuário do SCIM do Cerner Central e também pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Cerner Central com base na atribuição de usuário e de grupo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66c5a-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="66c5a-125">Você também pode optar por habilitar o SSO baseado em SAML para o Cerner Central seguindo as instruções fornecidas no Portal do Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66c5a-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="66c5a-126">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="66c5a-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="66c5a-127">Para obter mais informações, consulte o [Tutorial de logon único do Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="66c5a-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="66c5a-128">Para configurar o provisionamento automático de usuário para o Cerner Central no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="66c5a-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="66c5a-129">Para provisionar contas de usuário no Cerner Central, você precisará solicitar uma conta de sistema do Cerner Central do Cerner e gerar um token de portador OAuth que o Azure AD pode usar para se conectar ao ponto de extremidade SCIM do Cerner.</span><span class="sxs-lookup"><span data-stu-id="66c5a-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="66c5a-130">Também recomendamos que a integração seja executada em um ambiente de área restrita do Cerner antes da implantação em produção.</span><span class="sxs-lookup"><span data-stu-id="66c5a-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="66c5a-131">A primeira etapa é garantir que as pessoas que gerenciam a integração do Cerner e do Azure AD tenham uma conta no CernerCare, que é exigida para acessar a documentação necessária para concluir as instruções.</span><span class="sxs-lookup"><span data-stu-id="66c5a-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="66c5a-132">Se for necessário, use as URLs abaixo para criar contas do CernerCare em cada ambiente aplicável.</span><span class="sxs-lookup"><span data-stu-id="66c5a-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="66c5a-133">Área restrita: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="66c5a-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="66c5a-134">Produção:  https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="66c5a-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="66c5a-135">Em seguida, será necessário criar uma conta do sistema para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66c5a-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="66c5a-136">Use as instruções a seguir para solicitar uma Conta do Sistema para seus ambientes de produção e de área restrita.</span><span class="sxs-lookup"><span data-stu-id="66c5a-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="66c5a-137">Instruções:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="66c5a-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="66c5a-138">Área restrita: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="66c5a-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="66c5a-139">Produção:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="66c5a-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="66c5a-140">Em seguida, gere um token de portador OAuth para cada uma de suas contas do sistema.</span><span class="sxs-lookup"><span data-stu-id="66c5a-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="66c5a-141">Para fazer isso, siga as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="66c5a-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="66c5a-142">Instruções: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="66c5a-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="66c5a-143">Área restrita: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="66c5a-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="66c5a-144">Produção:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="66c5a-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="66c5a-145">Por fim, você precisa adquirir as IDs de Realm da Lista do Usuário para ambientes de área restrita e de produção Cerner para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="66c5a-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="66c5a-146">Para saber mais sobre como adquirir isso, consulte: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="66c5a-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="66c5a-147">Agora você pode configurar o Azure AD para provisionar contas de usuário para o Cerner.</span><span class="sxs-lookup"><span data-stu-id="66c5a-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="66c5a-148">Entre no [Portal do Azure](https://portal.azure.com) e navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="66c5a-149">Se você já tiver configurado o Cerner Central para logon único, procure sua instância do Cerner Central usando o campo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="66c5a-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="66c5a-150">Caso contrário, selecione **Adicionar** e procure **Cerner Central** na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="66c5a-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="66c5a-151">Selecione o Cerner Central nos resultados da pesquisa e adicione-o à lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="66c5a-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="66c5a-152">Selecione sua instância do Cerner Central e selecione a guia **Provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="66c5a-153">Defina o **Modo de Provisionamento** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Provisionamento do Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="66c5a-155">Preencha os campos a seguir em **Credenciais de Administrador**:</span><span class="sxs-lookup"><span data-stu-id="66c5a-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="66c5a-156">No campo **URL do Locatário**, insira uma URL no formato abaixo, substituindo "User-Roster-Realm-ID" pela ID do realm que você adquiriu na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="66c5a-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="66c5a-157">Área restrita: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="66c5a-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="66c5a-158">Produção: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="66c5a-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="66c5a-159">No campo **Segredo do Token**, insira o token de portador OAuth gerado na etapa 3 e clique em **Testar Conexão**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="66c5a-160">Você verá uma notificação de êxito no lado do superior direito do seu Portal.</span><span class="sxs-lookup"><span data-stu-id="66c5a-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="66c5a-161">Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="66c5a-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="66c5a-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-162">Click **Save**.</span></span> 

12. <span data-ttu-id="66c5a-163">Na seção **Mapeamentos de Atributo**, examine os atributos de usuário e grupo que serão sincronizados do Azure AD para o Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="66c5a-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="66c5a-164">Os atributos selecionados como propriedades **Correspondentes** são usados para corresponder as contas de usuário e grupos no Cerner Central para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="66c5a-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="66c5a-165">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="66c5a-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="66c5a-166">Para habilitar o serviço de provisionamento do Azure AD para o Cerner Central, altere o **Status de Provisionamento** para **Ativado** na seção **Configurações**</span><span class="sxs-lookup"><span data-stu-id="66c5a-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="66c5a-167">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66c5a-167">Click **Save**.</span></span> 

<span data-ttu-id="66c5a-168">Isso inicia a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Cerner Central na seção Usuários e Grupos.</span><span class="sxs-lookup"><span data-stu-id="66c5a-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="66c5a-169">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço de provisionamento do Azure AD esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="66c5a-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="66c5a-170">Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="66c5a-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="66c5a-171">Para saber mais sobre como ler os logs de provisionamento do Azure AD, consulte [Relatórios sobre o provisionamento automático de contas de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="66c5a-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66c5a-172">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="66c5a-172">Additional resources</span></span>

* [<span data-ttu-id="66c5a-173">Cerner Central: Publicação de dados de identidade usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="66c5a-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="66c5a-174">Tutorial: Configurar o Cerner Central para logon único com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66c5a-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="66c5a-175">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="66c5a-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="66c5a-176">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66c5a-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="66c5a-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66c5a-177">Next steps</span></span>
* <span data-ttu-id="66c5a-178">[Saiba como fazer revisão de logs e obter relatórios sobre a atividade de provisionamento](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="66c5a-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
