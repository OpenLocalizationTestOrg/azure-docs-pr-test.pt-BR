---
title: "Tutorial: Configurando o GitHub para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooGitHub."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="0be20-103">Tutorial: Configurando o GitHub para o provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="0be20-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="0be20-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no GitHub e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="0be20-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0be20-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0be20-105">Prerequisites</span></span>

<span data-ttu-id="0be20-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0be20-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0be20-107">Um locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0be20-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="0be20-108">Um locatário Github com hello [plano de negócios](https://help.github.com/articles/organization-billing-plans/#business-plan) ou melhor habilitado</span><span class="sxs-lookup"><span data-stu-id="0be20-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="0be20-109">Uma conta de usuário no GitHub com permissões de Administrador</span><span class="sxs-lookup"><span data-stu-id="0be20-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="0be20-110">Olá provisionamento integração do AD do Azure depende de saudação [GitHub SCIM API](https://developer.github.com/v3/scim/), que é equipes tooGithub disponíveis no plano de negócios hello ou superior.</span><span class="sxs-lookup"><span data-stu-id="0be20-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="0be20-111">Atribuir usuários tooGitHub</span><span class="sxs-lookup"><span data-stu-id="0be20-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="0be20-112">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0be20-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0be20-113">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="0be20-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="0be20-114">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo do GitHub tooyour.</span><span class="sxs-lookup"><span data-stu-id="0be20-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="0be20-115">Depois de decidir, você pode atribuir esses aplicativos de GitHub tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="0be20-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="0be20-116">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="0be20-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="0be20-117">Dicas importantes para atribuir usuários tooGitHub</span><span class="sxs-lookup"><span data-stu-id="0be20-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="0be20-118">É recomendável que um único usuário do AD do Azure é atribuído tooGitHub tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0be20-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="0be20-119">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0be20-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0be20-120">Ao atribuir um usuário tooGitHub, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="0be20-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="0be20-121">Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.</span><span class="sxs-lookup"><span data-stu-id="0be20-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="0be20-122">Configurando tooGitHub de provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="0be20-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="0be20-123">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooGitHub seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no GitHub com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0be20-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0be20-124">Você também pode escolher tooenabled baseado no SAML SSO para o GitHub, seguir Olá instruções fornecidas na [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0be20-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0be20-125">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="0be20-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="0be20-126">Configurar conta de usuário automático provisionamento tooGitHub no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0be20-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="0be20-127">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="0be20-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="0be20-128">Se você já tiver configurado o GitHub para logon único, procure sua instância do usando o campo de pesquisa de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0be20-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="0be20-129">Caso contrário, selecione **adicionar** e procure **GitHub** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0be20-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="0be20-130">Selecione GitHub Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0be20-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0be20-131">Selecione sua instância do GitHub, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="0be20-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0be20-132">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="0be20-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisionamento do GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="0be20-134">Em Olá **credenciais de administrador** seção, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="0be20-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="0be20-135">Essa operação abre uma caixa de diálogo de autorização do GitHub em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="0be20-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="0be20-136">Na nova janela de hello, entre no GitHub usando sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="0be20-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="0be20-137">No diálogo de autorização resultante hello, selecione o agrupamento de GitHub de saudação que você deseja tooenable provisionamento para e, em seguida, selecione **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="0be20-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="0be20-138">Saudação de toocomplete portal do Azure depois de concluído, retorne toohello configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0be20-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Caixa de diálogo Autorização](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="0be20-140">No portal do Azure de Olá, entrada **URL do locatário** e clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour GitHub aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0be20-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="0be20-141">Se a conexão de saudação falhar, certifique-se de sua conta do GitHub tem permissões de administrador e **URl do locatário** for inserido corretamente e tente hello "Autorizar" etapa novamente (podem provocar **URL do locatário** pela regra: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", você pode encontrar as organizações em sua conta do GitHub: **configurações** > **organizações**).</span><span class="sxs-lookup"><span data-stu-id="0be20-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Caixa de diálogo Autorização](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="0be20-143">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."</span><span class="sxs-lookup"><span data-stu-id="0be20-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="0be20-144">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0be20-144">Click **Save**.</span></span> 

10. <span data-ttu-id="0be20-145">Em Olá mapeamentos, selecione **tooGitHub sincronizar do Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="0be20-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="0be20-146">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooGitHub do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0be20-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="0be20-147">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no GitHub para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="0be20-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="0be20-148">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="0be20-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="0be20-149">tooenable Olá serviço de provisionamento do AD do Azure para o GitHub, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="0be20-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="0be20-150">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0be20-150">Click **Save**.</span></span> 

<span data-ttu-id="0be20-151">Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooGitHub em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="0be20-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="0be20-152">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="0be20-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="0be20-153">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="0be20-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="0be20-154">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0be20-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0be20-155">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0be20-155">Additional resources</span></span>

* [<span data-ttu-id="0be20-156">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="0be20-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0be20-157">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0be20-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="0be20-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0be20-158">Next steps</span></span>

* [<span data-ttu-id="0be20-159">Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento</span><span class="sxs-lookup"><span data-stu-id="0be20-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
