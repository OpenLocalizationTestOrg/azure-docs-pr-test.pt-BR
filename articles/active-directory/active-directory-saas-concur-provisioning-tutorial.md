---
title: "Tutorial: integração do Azure Active Directory ao Concur | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="d7e31-103">Tutorial: configurar o Concur para provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="d7e31-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="d7e31-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Concur e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooConcur.</span><span class="sxs-lookup"><span data-stu-id="d7e31-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7e31-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7e31-105">Prerequisites</span></span>

<span data-ttu-id="d7e31-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d7e31-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="d7e31-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7e31-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="d7e31-108">Uma assinatura habilitada para logon único do Concur.</span><span class="sxs-lookup"><span data-stu-id="d7e31-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="d7e31-109">Uma conta de usuário no Concur com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="d7e31-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="d7e31-110">Atribuir usuários tooConcur</span><span class="sxs-lookup"><span data-stu-id="d7e31-110">Assigning users tooConcur</span></span>

<span data-ttu-id="d7e31-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d7e31-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="d7e31-112">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="d7e31-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="d7e31-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour Concur aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7e31-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="d7e31-114">Depois de decidir, você pode atribuir esses aplicativos de Concur tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="d7e31-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="d7e31-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="d7e31-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="d7e31-116">Dicas importantes para atribuir usuários tooConcur</span><span class="sxs-lookup"><span data-stu-id="d7e31-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="d7e31-117">É recomendável que um único usuário do AD do Azure receberá tooConcur tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d7e31-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="d7e31-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d7e31-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="d7e31-119">Ao atribuir um usuário tooConcur, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="d7e31-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="d7e31-120">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="d7e31-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="d7e31-121">Permitir provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="d7e31-121">Enable user provisioning</span></span>

<span data-ttu-id="d7e31-122">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooConcur seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Concur com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e31-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="d7e31-123">Você também pode escolher tooenabled baseado no SAML SSO para Concur, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7e31-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d7e31-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="d7e31-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="d7e31-125">provisionamento de conta de usuário de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="d7e31-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="d7e31-126">Olá o objetivo desta seção é toooutline como tooenable provisionamento de usuário do Active Directory contas tooConcur.</span><span class="sxs-lookup"><span data-stu-id="d7e31-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="d7e31-127">aplicativos tooenable Olá serviço de despesas, é toobe configuração e uso apropriados de um perfil de administrador de serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="d7e31-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="d7e31-128">Não adicione Olá administrador WS função tooyour perfil de administrador existente que você usa para funções administrativas T & E.</span><span class="sxs-lookup"><span data-stu-id="d7e31-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="d7e31-129">Os consultores concur ou administrador de saudação do cliente deve criar um perfil de administrador de serviços Web distinto e administrador de saudação do cliente deve usar esse perfil para as funções de administrador de serviços Web da saudação (por exemplo, a habilitação de aplicativos).</span><span class="sxs-lookup"><span data-stu-id="d7e31-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="d7e31-130">Esses perfis devem ser mantidos separados de diário T & E perfil de administrador do administrador do cliente Olá (Olá T & perfil de administrador E não devem ter função de administrador de serviços Web hello atribuída).</span><span class="sxs-lookup"><span data-stu-id="d7e31-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="d7e31-131">Ao criar Olá perfil toobe usado para habilitar o aplicativo hello, insira o nome do administrador do cliente de saudação em campos de perfil de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7e31-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="d7e31-132">Isso atribuirá o perfil de toohello de propriedade.</span><span class="sxs-lookup"><span data-stu-id="d7e31-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="d7e31-133">Depois de criar um ou mais perfis, cliente Olá deve fazer logon com essa Olá tooclick de perfil "*habilitar*" botão para um aplicativo parceiro no menu de serviços Web hello.</span><span class="sxs-lookup"><span data-stu-id="d7e31-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="d7e31-134">Para Olá motivos a seguir, essa ação não deve ser feita com perfil Olá usam para administração T & E normal.</span><span class="sxs-lookup"><span data-stu-id="d7e31-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="d7e31-135">Olá cliente tiver toobe Olá que clica em "*Sim*" na janela de caixa de diálogo de saudação é exibida depois que um aplicativo está habilitado.</span><span class="sxs-lookup"><span data-stu-id="d7e31-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="d7e31-136">Esse clique confirma que o cliente Olá é disposto para Olá parceiro aplicativo tooaccess seus dados, para que você ou hello parceiro não é possível clicar botão Sim.</span><span class="sxs-lookup"><span data-stu-id="d7e31-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="d7e31-137">Se um administrador do cliente que habilitou um aplicativo usando Olá T & perfil de administrador E deixa a empresa hello (resultando em perfil hello está sendo desativado), quaisquer aplicativos habilitados usando o perfil não funcionará até que o aplicativo hello está habilitado com outro administrador WS active perfil.</span><span class="sxs-lookup"><span data-stu-id="d7e31-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="d7e31-138">É por isso devem toocreate distintos perfis de administrador de serviços Web.</span><span class="sxs-lookup"><span data-stu-id="d7e31-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="d7e31-139">Se um administrador deixa a empresa Olá, nome de saudação associada toohello perfil de administrador de serviços Web pode ser o administrador de substituição de toohello alterados se desejar sem afetar a saudação habilitada aplicativo desativado porque não é necessário que esse perfil.</span><span class="sxs-lookup"><span data-stu-id="d7e31-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="d7e31-140">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d7e31-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7e31-141">Faça logon no tooyour **Concur** locatário.</span><span class="sxs-lookup"><span data-stu-id="d7e31-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="d7e31-142">De saudação **administração** menu, selecione **serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="d7e31-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="d7e31-143">![Locatário do Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Locatário do Concur")</span><span class="sxs-lookup"><span data-stu-id="d7e31-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="d7e31-144">Em Olá deixados de lado, da saudação **serviços Web** painel, selecione **habilitar aplicativo parceiro**.</span><span class="sxs-lookup"><span data-stu-id="d7e31-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="d7e31-145">![Habilitar Aplicativo do Parceiro](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar Aplicativo do Parceiro")</span><span class="sxs-lookup"><span data-stu-id="d7e31-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="d7e31-146">De saudação **habilitar aplicativo** lista, selecione **Active Directory do Azure**e, em seguida, clique em **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="d7e31-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="d7e31-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d7e31-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="d7e31-148">Clique em **Sim** tooclose Olá **Confirmar ação** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7e31-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="d7e31-149">![Confirmar Ação](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar Ação")</span><span class="sxs-lookup"><span data-stu-id="d7e31-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="d7e31-150">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="d7e31-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="d7e31-151">Se você já tiver configurado o Concur para SSO, procure sua instância do Concur usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7e31-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="d7e31-152">Caso contrário, selecione **adicionar** e procure **Concur** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7e31-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="d7e31-153">Selecione Concur Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d7e31-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="d7e31-154">Selecione sua instância do Concur e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="d7e31-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="d7e31-155">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="d7e31-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![provisionamento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="d7e31-157">Em Olá **credenciais de administrador** seção, digite Olá **nome de usuário** e hello **senha** do administrador do Concur.</span><span class="sxs-lookup"><span data-stu-id="d7e31-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="d7e31-158">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Concur aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7e31-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="d7e31-159">Se a conexão de saudação falhar, certifique-se de que sua conta Concur tem permissões de administrador de equipe.</span><span class="sxs-lookup"><span data-stu-id="d7e31-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="d7e31-160">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7e31-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="d7e31-161">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="d7e31-161">Click **Save.**</span></span>

14. <span data-ttu-id="d7e31-162">Em Olá mapeamentos, selecione **tooConcur sincronizar Azure usuários do Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="d7e31-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="d7e31-163">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooConcur do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e31-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="d7e31-164">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Concur para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="d7e31-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="d7e31-165">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d7e31-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="d7e31-166">tooenable Olá serviço de provisionamento do AD do Azure para Concur, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="d7e31-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="d7e31-167">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="d7e31-167">Click **Save.**</span></span>

<span data-ttu-id="d7e31-168">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="d7e31-168">You can now create a test account.</span></span> <span data-ttu-id="d7e31-169">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooConcur.</span><span class="sxs-lookup"><span data-stu-id="d7e31-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7e31-170">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d7e31-170">Additional resources</span></span>

* [<span data-ttu-id="d7e31-171">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="d7e31-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7e31-172">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7e31-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d7e31-173">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="d7e31-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

