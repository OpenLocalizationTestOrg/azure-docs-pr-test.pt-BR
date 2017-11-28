---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="07db9-103">Tutorial: Configurar o Citrix GoToMeeting para provisionamento automático de usuário</span><span class="sxs-lookup"><span data-stu-id="07db9-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="07db9-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Citrix GoToMeeting e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07db9-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07db9-105">Prerequisites</span></span>

<span data-ttu-id="07db9-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="07db9-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="07db9-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07db9-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="07db9-108">Uma assinatura do Citrix GoToMeeting habilitada para logon único.</span><span class="sxs-lookup"><span data-stu-id="07db9-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="07db9-109">Uma conta de usuário no Citrix GoToMeeting com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="07db9-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="07db9-110">Atribuir usuários tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="07db9-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="07db9-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07db9-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="07db9-112">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="07db9-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="07db9-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="07db9-114">Depois de decidir, você pode atribuir essas tooyour usuários Citrix GoToMeeting aplicativo seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="07db9-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="07db9-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="07db9-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="07db9-116">Dicas importantes para atribuir usuários tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="07db9-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="07db9-117">É recomendável que um único usuário do AD do Azure é atribuído tooCitrix GoToMeeting tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="07db9-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="07db9-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="07db9-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="07db9-119">Ao atribuir um usuário tooCitrix GoToMeeting, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="07db9-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="07db9-120">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="07db9-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="07db9-121">Habilitar o Provisionamento Automatizado de Usuários</span><span class="sxs-lookup"><span data-stu-id="07db9-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="07db9-122">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do GoToMeeting tooCitrix seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas no Citrix GoToMeeting com base em usuários e grupos de usuário atribuído atribuição no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07db9-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="07db9-123">Você também pode escolher tooenabled baseado no SAML SSO para Citrix GoToMeeting, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07db9-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="07db9-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="07db9-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="07db9-125">provisionamento de conta de usuário automático de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="07db9-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="07db9-126">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="07db9-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="07db9-127">Se você já tiver configurado o Citrix GoToMeeting para logon único, procure sua instância do usando o campo de pesquisa de saudação do Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="07db9-128">Caso contrário, selecione **adicionar** e procure **Citrix GoToMeeting** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="07db9-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="07db9-129">Selecione o Citrix GoToMeeting Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07db9-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="07db9-130">Selecione sua instância do Citrix GoToMeeting, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="07db9-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="07db9-131">Saudação de conjunto **provisionamento** modo muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="07db9-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="07db9-133">Na seção de credenciais de administrador do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07db9-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="07db9-134">a.</span><span class="sxs-lookup"><span data-stu-id="07db9-134">a.</span></span> <span data-ttu-id="07db9-135">Em Olá **nome de usuário de administrador do Citrix GoToMeeting** caixa de texto, nome de usuário de saudação do tipo de um administrador.</span><span class="sxs-lookup"><span data-stu-id="07db9-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="07db9-136">b.</span><span class="sxs-lookup"><span data-stu-id="07db9-136">b.</span></span> <span data-ttu-id="07db9-137">Em Olá **senha do administrador do Citrix GoToMeeting** texto, a senha do administrador do hello.</span><span class="sxs-lookup"><span data-stu-id="07db9-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="07db9-138">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour aplicativo Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="07db9-139">Se a conexão de saudação falhar, certifique-se de que sua conta do Citrix GoToMeeting tem permissões de administrador de equipe e tente Olá **"Credenciais de administrador"** etapa novamente.</span><span class="sxs-lookup"><span data-stu-id="07db9-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="07db9-140">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="07db9-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="07db9-141">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="07db9-141">Click **Save.**</span></span>

9. <span data-ttu-id="07db9-142">Em Olá mapeamentos, selecione **sincronizar do Azure Active Directory Users tooCitrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="07db9-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="07db9-143">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="07db9-144">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Citrix GoToMeeting para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="07db9-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="07db9-145">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="07db9-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="07db9-146">tooenable Olá serviço de provisionamento do AD do Azure para Citrix GoToMeeting, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="07db9-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="07db9-147">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="07db9-147">Click **Save.**</span></span>

<span data-ttu-id="07db9-148">Iniciar a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooCitrix GoToMeeting na seção usuários e grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="07db9-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="07db9-149">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="07db9-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="07db9-150">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo da Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="07db9-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07db9-151">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="07db9-151">Additional resources</span></span>

* [<span data-ttu-id="07db9-152">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="07db9-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07db9-153">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07db9-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="07db9-154">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="07db9-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


