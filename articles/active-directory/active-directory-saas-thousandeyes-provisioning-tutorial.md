---
title: "Tutorial: configurar o ThousandEyes para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooThousandEyes."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="dd9d2-103">Tutorial: configurar o ThousandEyes para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="dd9d2-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="dd9d2-104">Olá objetivo deste tutorial é tooshow que Olá etapas necessárias tooperform no provisionamento de tooautomatically ThousandEyes e o Azure AD e desprovisionar contas de usuário do AD do Azure tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dd9d2-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dd9d2-105">Prerequisites</span></span>

<span data-ttu-id="dd9d2-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd9d2-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="dd9d2-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd9d2-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="dd9d2-108">Um locatário ThousandEyes com hello [plano padrão](https://www.thousandeyes.com/pricing) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="dd9d2-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="dd9d2-109">Uma conta de usuário no ThousandEyes com permissões de administrador</span><span class="sxs-lookup"><span data-stu-id="dd9d2-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="dd9d2-110">Olá provisionamento integração do AD do Azure depende de saudação [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), que é equipes tooThousandEyes disponíveis no plano de saudação padrão ou superior.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="dd9d2-111">Atribuir usuários tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dd9d2-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="dd9d2-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="dd9d2-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="dd9d2-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour ThousandEyes aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="dd9d2-115">Depois de decidir, você pode atribuir esses aplicativos de ThousandEyes tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="dd9d2-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="dd9d2-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="dd9d2-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="dd9d2-117">Dicas importantes para atribuir usuários tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="dd9d2-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="dd9d2-118">É recomendável que um único usuário do AD do Azure é atribuído tooThousandEyes tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="dd9d2-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="dd9d2-120">Ao atribuir um usuário tooThousandEyes, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="dd9d2-121">Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="dd9d2-122">Configurando tooThousandEyes de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="dd9d2-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="dd9d2-123">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooThousandEyes seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no ThousandEyes com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="dd9d2-124">Você também pode escolher tooenabled baseado no SAML SSO para ThousandEyes, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd9d2-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dd9d2-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="dd9d2-126">Configurar conta de usuário automático provisionamento tooThousandEyes no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="dd9d2-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="dd9d2-127">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="dd9d2-128">Se você já tiver configurado ThousandEyes para logon único, procure sua instância do ThousandEyes usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="dd9d2-129">Caso contrário, selecione **adicionar** e procure **ThousandEyes** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="dd9d2-130">Selecione ThousandEyes Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="dd9d2-131">Selecione sua instância do ThousandEyes, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="dd9d2-132">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="dd9d2-134">Em Olá **credenciais de administrador** seção, Olá entrada **segredo do Token** gerado pela conta do ThousandEyes (token Olá pode ser encontrado em sua conta ThousandEyes: **segurança & Autenticação**).</span><span class="sxs-lookup"><span data-stu-id="dd9d2-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="dd9d2-136">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour ThousandEyes aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="dd9d2-137">Se a conexão de saudação falhar, certifique-se de que sua conta ThousandEyes tem permissões de administrador e repita a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="dd9d2-138">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="dd9d2-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="dd9d2-139">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-139">Click **Save**.</span></span> 

9. <span data-ttu-id="dd9d2-140">Em Olá mapeamentos, selecione **tooThousandEyes sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="dd9d2-141">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooThousandEyes do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="dd9d2-142">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no ThousandEyes para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="dd9d2-143">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="dd9d2-144">tooenable Olá serviço de provisionamento do AD do Azure para ThousandEyes, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="dd9d2-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="dd9d2-145">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-145">Click **Save**.</span></span> 

<span data-ttu-id="dd9d2-146">Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooThousandEyes em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="dd9d2-147">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="dd9d2-148">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dd9d2-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="dd9d2-149">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="dd9d2-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dd9d2-150">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dd9d2-150">Additional resources</span></span>

* [<span data-ttu-id="dd9d2-151">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="dd9d2-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="dd9d2-152">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd9d2-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="dd9d2-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd9d2-153">Next steps</span></span>

* [<span data-ttu-id="dd9d2-154">Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="dd9d2-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
