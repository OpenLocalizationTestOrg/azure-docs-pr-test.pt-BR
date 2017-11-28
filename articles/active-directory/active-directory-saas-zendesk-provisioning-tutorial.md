---
title: "Tutorial: configurar o ZenDesk para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooZenDesk."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="eb73f-103">Tutorial: configurar o ZenDesk para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="eb73f-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="eb73f-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no ZenDesk e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooZenDesk.</span><span class="sxs-lookup"><span data-stu-id="eb73f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb73f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb73f-105">Prerequisites</span></span>

<span data-ttu-id="eb73f-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb73f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="eb73f-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb73f-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="eb73f-108">Um locatário do ZenDesk com hello [plano empresarial](https://www.zendesk.com/product/pricing/) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="eb73f-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="eb73f-109">Uma conta de usuário no ZenDesk com permissões de administrador</span><span class="sxs-lookup"><span data-stu-id="eb73f-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="eb73f-110">Olá provisionamento integração do AD do Azure depende de saudação [API REST do ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), que é equipes tooZenDesk disponíveis no plano essencial hello ou superior.</span><span class="sxs-lookup"><span data-stu-id="eb73f-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="eb73f-111">Atribuir usuários tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="eb73f-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="eb73f-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="eb73f-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="eb73f-113">No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb73f-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="eb73f-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour ZenDesk aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb73f-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="eb73f-115">Depois de decidir, você pode atribuir esses aplicativos de ZenDesk de tooyour de usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="eb73f-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="eb73f-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="eb73f-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="eb73f-117">Dicas importantes para atribuir usuários tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="eb73f-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="eb73f-118">É recomendável que um único usuário do AD do Azure é atribuído tooZenDesk tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="eb73f-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="eb73f-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="eb73f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="eb73f-120">Ao atribuir um usuário tooZenDesk, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb73f-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="eb73f-121">Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="eb73f-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="eb73f-122">Como um recurso adicionado, Olá provisionar um serviço lê qualquer funções personalizadas definidas no Zendesk e as importa para onde pode ser selecionadas na caixa de diálogo Olá Selecionar função do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb73f-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="eb73f-123">Essas funções ficará visíveis no portal do Azure de saudação após Olá provisionamento de serviço está habilitado e um ciclo de sincronização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="eb73f-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="eb73f-124">Configurando tooZenDesk de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="eb73f-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="eb73f-125">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooZenDesk seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no ZenDesk com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb73f-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="eb73f-126">Você também pode escolher tooenabled baseado no SAML SSO para o ZenDesk, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eb73f-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eb73f-127">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="eb73f-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="eb73f-128">Configurar conta de usuário automático provisionamento tooZenDesk no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb73f-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="eb73f-129">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="eb73f-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="eb73f-130">Se você já tiver configurado o ZenDesk para o logon único, procure sua instância do ZenDesk usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb73f-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="eb73f-131">Caso contrário, selecione **adicionar** e procure **ZenDesk** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="eb73f-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="eb73f-132">Selecione ZenDesk Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="eb73f-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="eb73f-133">Selecione sua instância do ZenDesk, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="eb73f-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="eb73f-134">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="eb73f-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisionamento do ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="eb73f-136">Em Olá **credenciais de administrador** seção, Olá entrada **Admin Username tokenkey & domínio** gerado pela conta do ZenDesk (token Olá pode ser encontrado em sua conta: **Admin**   >  **API** > **configurações**).</span><span class="sxs-lookup"><span data-stu-id="eb73f-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Provisionamento do ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="eb73f-138">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour ZenDesk aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb73f-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="eb73f-139">Se a conexão de saudação falhar, certifique-se de que sua conta do ZenDesk tem permissões de administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="eb73f-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="eb73f-140">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="eb73f-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="eb73f-141">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb73f-141">Click **Save**.</span></span> 

9. <span data-ttu-id="eb73f-142">Em Olá mapeamentos, selecione **tooZenDesk sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="eb73f-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="eb73f-143">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooZenDesk do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb73f-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="eb73f-144">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no ZenDesk para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="eb73f-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="eb73f-145">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="eb73f-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="eb73f-146">tooenable Olá serviço de provisionamento do AD do Azure para o ZenDesk, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="eb73f-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="eb73f-147">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="eb73f-147">Click **Save**.</span></span> 

<span data-ttu-id="eb73f-148">Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooZenDesk em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="eb73f-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="eb73f-149">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="eb73f-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="eb73f-150">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="eb73f-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="eb73f-151">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="eb73f-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="eb73f-152">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eb73f-152">Additional resources</span></span>

* [<span data-ttu-id="eb73f-153">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="eb73f-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="eb73f-154">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb73f-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="eb73f-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb73f-155">Next steps</span></span>

* [<span data-ttu-id="eb73f-156">Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="eb73f-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
