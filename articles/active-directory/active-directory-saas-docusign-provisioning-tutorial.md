---
title: "Tutorial: integração do Azure Active Directory com o DocuSign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="49892-103">Tutorial: Configurando o DocuSign para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="49892-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="49892-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no DocuSign e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="49892-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49892-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49892-105">Prerequisites</span></span>

<span data-ttu-id="49892-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="49892-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="49892-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49892-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="49892-108">Uma assinatura habilitada para logon único do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="49892-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="49892-109">Uma conta de usuário no DocuSign com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="49892-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="49892-110">Atribuir usuários tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="49892-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="49892-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="49892-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="49892-112">No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="49892-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="49892-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour DocuSign aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49892-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="49892-114">Depois de decidir, você pode atribuir esses aplicativos de DocuSign tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="49892-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="49892-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="49892-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="49892-116">Dicas importantes para atribuir usuários tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="49892-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="49892-117">É recomendável que um único usuário do AD do Azure é atribuído tooDocuSign tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="49892-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="49892-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="49892-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="49892-119">Ao atribuir um usuário tooDocuSign, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="49892-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="49892-120">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="49892-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="49892-121">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="49892-121">Enable User Provisioning</span></span>

<span data-ttu-id="49892-122">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooDocuSign seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no DocuSign com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="49892-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="49892-123">Você também pode escolher tooenabled baseado no SAML SSO para DocuSign, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49892-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="49892-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="49892-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="49892-125">provisionamento de conta de usuário de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="49892-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="49892-126">Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="49892-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="49892-127">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="49892-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="49892-128">Se você já tiver configurado o DocuSign para logon único, procure sua instância do DocuSign usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="49892-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="49892-129">Caso contrário, selecione **adicionar** e procure **DocuSign** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49892-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="49892-130">Selecione DocuSign Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="49892-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="49892-131">Selecione sua instância do DocuSign, em seguida Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="49892-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="49892-132">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="49892-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="49892-134">Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="49892-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="49892-135">a.</span><span class="sxs-lookup"><span data-stu-id="49892-135">a.</span></span> <span data-ttu-id="49892-136">Em Olá **nome de usuário administrador** caixa de texto, tipo de um DocuSign nome de conta que tem Olá **administrador do sistema** perfil em DocuSign.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="49892-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="49892-137">b.</span><span class="sxs-lookup"><span data-stu-id="49892-137">b.</span></span> <span data-ttu-id="49892-138">Em Olá **senha do administrador** caixa de texto, digite a senha Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="49892-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="49892-139">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour DocuSign aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49892-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="49892-140">Em Olá **Email de notificação** , digite o endereço de email de saudação de uma pessoa ou grupo que deve receber notificações de erros de provisionamento e marque caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="49892-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="49892-141">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="49892-141">Click **Save.**</span></span>

9. <span data-ttu-id="49892-142">Em Olá mapeamentos, selecione **tooDocuSign sincronizar Azure usuários do Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="49892-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="49892-143">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooDocuSign do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="49892-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="49892-144">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no DocuSign para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="49892-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="49892-145">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="49892-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="49892-146">tooenable Olá serviço de provisionamento do AD do Azure para DocuSign, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="49892-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="49892-147">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="49892-147">Click **Save.**</span></span>

<span data-ttu-id="49892-148">Ele inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooDocuSign em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="49892-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="49892-149">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="49892-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="49892-150">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="49892-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="49892-151">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="49892-151">You can now create a test account.</span></span> <span data-ttu-id="49892-152">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="49892-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49892-153">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="49892-153">Additional resources</span></span>

* [<span data-ttu-id="49892-154">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="49892-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49892-155">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49892-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="49892-156">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="49892-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)