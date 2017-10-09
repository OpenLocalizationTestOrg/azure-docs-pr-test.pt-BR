---
title: "Tutorial: Configurando o Samanage para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooSamanage."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="1ae8a-103">Tutorial: Configurando o Samanage para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="1ae8a-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="1ae8a-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Samanage e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1ae8a-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ae8a-105">Prerequisites</span></span>

<span data-ttu-id="1ae8a-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ae8a-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1ae8a-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ae8a-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="1ae8a-108">Um locatário do Samanage com hello [profissional plano](https://www.samanage.com/pricing/) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="1ae8a-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="1ae8a-109">Uma conta de usuário no Samanage com permissões de Administrador</span><span class="sxs-lookup"><span data-stu-id="1ae8a-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="1ae8a-110">Olá provisionamento integração do AD do Azure depende de saudação [API REST do Samanage](https://www.samanage.com/api/), que é equipes tooSamanage disponível em Olá profissional plano ou melhor.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="1ae8a-111">Atribuir usuários tooSamanage</span><span class="sxs-lookup"><span data-stu-id="1ae8a-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="1ae8a-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1ae8a-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="1ae8a-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour Samanage aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="1ae8a-115">Depois de decidir, você pode atribuir esses aplicativos de Samanage tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="1ae8a-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="1ae8a-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="1ae8a-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="1ae8a-117">Dicas importantes para atribuir usuários tooSamanage</span><span class="sxs-lookup"><span data-stu-id="1ae8a-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="1ae8a-118">É recomendável que um único usuário do AD do Azure é atribuído tooSamanage tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="1ae8a-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1ae8a-120">Ao atribuir um usuário tooSamanage, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="1ae8a-121">Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="1ae8a-122">Como um recurso adicionado, Olá provisionar um serviço lê qualquer funções personalizadas definidas no Samanage e as importa para onde pode ser selecionadas na caixa de diálogo Olá Selecionar função do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="1ae8a-123">Essas funções ficará visíveis no portal do Azure de saudação após Olá provisionamento de serviço está habilitado e um ciclo de sincronização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="1ae8a-124">Configurando tooSamanage de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="1ae8a-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="1ae8a-125">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooSamanage seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Samanage com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1ae8a-126">Você também pode escolher tooenabled baseado no SAML SSO para Samanage, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ae8a-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1ae8a-127">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="1ae8a-128">Configure a conta de usuário automático provisionamento tooSamanage no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="1ae8a-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="1ae8a-129">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="1ae8a-130">Se você já tiver configurado o Samanage para logon único, procure sua instância do Samanage usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="1ae8a-131">Caso contrário, selecione **adicionar** e procure **Samanage** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="1ae8a-132">Selecione Samanage Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1ae8a-133">Selecione sua instância do Samanage, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1ae8a-134">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisionamento do Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="1ae8a-136">Em Olá **credenciais de administrador** seção, Olá entrada **Admin Username & senha do administrador** da conta do Samanage.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="1ae8a-137">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Samanage aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="1ae8a-138">Se a conexão de saudação falhar, certifique-se de que sua conta Samanage tem permissões de administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="1ae8a-139">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="1ae8a-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="1ae8a-140">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-140">Click **Save**.</span></span> 

9. <span data-ttu-id="1ae8a-141">Em Olá mapeamentos, selecione **tooSamanage sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="1ae8a-142">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooSamanage do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="1ae8a-143">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Samanage para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="1ae8a-144">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="1ae8a-145">tooenable Olá serviço de provisionamento do AD do Azure para Samanage, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="1ae8a-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="1ae8a-146">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-146">Click **Save**.</span></span> 

<span data-ttu-id="1ae8a-147">Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSamanage em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="1ae8a-148">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="1ae8a-149">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="1ae8a-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="1ae8a-150">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="1ae8a-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1ae8a-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1ae8a-151">Additional resources</span></span>

* [<span data-ttu-id="1ae8a-152">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="1ae8a-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="1ae8a-153">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ae8a-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="1ae8a-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ae8a-154">Next steps</span></span>

* [<span data-ttu-id="1ae8a-155">Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="1ae8a-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
