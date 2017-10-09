---
title: "Tutorial: Configurando o LucidChart para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooLucidChart."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="b208b-103">Tutorial: Configurando o LucidChart para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="b208b-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="b208b-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no LucidChart e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="b208b-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b208b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b208b-105">Prerequisites</span></span>

<span data-ttu-id="b208b-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b208b-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b208b-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b208b-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="b208b-108">Um locatário LucidChart com hello [plano empresarial](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="b208b-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="b208b-109">Uma conta de usuário no LucidChart com permissões de Administrador</span><span class="sxs-lookup"><span data-stu-id="b208b-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="b208b-110">Atribuir usuários tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="b208b-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="b208b-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b208b-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b208b-112">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="b208b-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="b208b-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour LucidChart aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b208b-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="b208b-114">Depois de decidir, você pode atribuir esses aplicativos de LucidChart tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="b208b-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="b208b-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="b208b-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="b208b-116">Dicas importantes para atribuir usuários tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="b208b-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="b208b-117">É recomendável que um único usuário do AD do Azure é atribuído tooLucidChart tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b208b-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="b208b-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b208b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b208b-119">Ao atribuir um usuário tooLucidChart, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="b208b-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="b208b-120">Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="b208b-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="b208b-121">Configurando tooLucidChart de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="b208b-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="b208b-122">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooLucidChart seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no LucidChart com base na atribuição de usuário e grupo no AD do Azure .</span><span class="sxs-lookup"><span data-stu-id="b208b-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b208b-123">Você também pode escolher tooenabled baseado no SAML SSO para o LucidChart, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b208b-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b208b-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="b208b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="b208b-125">Configurar conta de usuário automático provisionamento tooLucidChart no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b208b-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="b208b-126">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="b208b-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="b208b-127">Se você já tiver configurado o LucidChart para logon único, procure sua instância do LucidChart usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b208b-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="b208b-128">Caso contrário, selecione **adicionar** e procure **LucidChart** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b208b-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="b208b-129">Selecione o LucidChart Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b208b-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b208b-130">Selecione sua instância do LucidChart, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="b208b-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b208b-131">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="b208b-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisionamento do LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="b208b-133">Em Olá **credenciais de administrador** seção, Olá entrada **segredo do Token** gerado pela conta do LucidChart (token Olá pode ser encontrado em sua conta: **equipe**  >  **Integração de aplicativo** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="b208b-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Provisionamento do LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="b208b-135">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour LucidChart aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b208b-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="b208b-136">Se a conexão de saudação falhar, certifique-se de que sua conta LucidChart tem permissões de administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="b208b-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="b208b-137">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="b208b-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="b208b-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b208b-138">Click **Save**.</span></span> 

9. <span data-ttu-id="b208b-139">Em Olá mapeamentos, selecione **tooLucidChart sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="b208b-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="b208b-140">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooLucidChart do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b208b-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="b208b-141">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no LucidChart para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="b208b-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="b208b-142">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="b208b-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="b208b-143">tooenable Olá serviço de provisionamento do AD do Azure para o LucidChart, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="b208b-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="b208b-144">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b208b-144">Click **Save**.</span></span> 

<span data-ttu-id="b208b-145">Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooLucidChart em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="b208b-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="b208b-146">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="b208b-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b208b-147">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="b208b-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="b208b-148">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="b208b-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b208b-149">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b208b-149">Additional resources</span></span>

* [<span data-ttu-id="b208b-150">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="b208b-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="b208b-151">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b208b-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="b208b-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b208b-152">Next steps</span></span>

* [<span data-ttu-id="b208b-153">Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="b208b-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
