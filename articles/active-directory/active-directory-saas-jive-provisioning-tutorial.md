---
title: "Tutorial: Integração do Azure Active Directory com o Jive | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="b95e3-103">Tutorial: Configurando o Jive para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="b95e3-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="b95e3-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform em Jive e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooJive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b95e3-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b95e3-105">Prerequisites</span></span>

<span data-ttu-id="b95e3-106">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b95e3-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="b95e3-107">Um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b95e3-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b95e3-108">Uma assinatura habilitada para logon único do Jive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b95e3-109">Uma conta de usuário no Jive com permissões de Administrador de Equipe.</span><span class="sxs-lookup"><span data-stu-id="b95e3-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="b95e3-110">Atribuir usuários tooJive</span><span class="sxs-lookup"><span data-stu-id="b95e3-110">Assigning users tooJive</span></span>

<span data-ttu-id="b95e3-111">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e3-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="b95e3-112">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="b95e3-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b95e3-113">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour Jive aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e3-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="b95e3-114">Depois de decidir, você pode atribuir esses aplicativos de Jive tooyour usuários, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="b95e3-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="b95e3-115">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="b95e3-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="b95e3-116">Dicas importantes para atribuir usuários tooJive</span><span class="sxs-lookup"><span data-stu-id="b95e3-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="b95e3-117">É recomendável que um único usuário do AD do Azure receberá tooJive tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b95e3-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="b95e3-118">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b95e3-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b95e3-119">Ao atribuir um usuário tooJive, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="b95e3-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="b95e3-120">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b95e3-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="b95e3-121">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="b95e3-121">Enable User Provisioning</span></span>

<span data-ttu-id="b95e3-122">Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooJive seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído em Jive com base na atribuição de usuário e grupo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b95e3-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b95e3-123">Você também pode escolher tooenabled baseado no SAML SSO para Jive, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b95e3-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b95e3-124">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="b95e3-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="b95e3-125">provisionamento de conta de usuário de tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="b95e3-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="b95e3-126">Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooJive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="b95e3-127">Como parte desse procedimento, será necessário tooprovide um token de segurança do usuário é necessário toorequest em Jive.com.</span><span class="sxs-lookup"><span data-stu-id="b95e3-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="b95e3-128">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="b95e3-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b95e3-129">Se você já tiver configurado o Jive para logon único, procure sua instância do usando o campo de pesquisa de saudação do Jive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="b95e3-130">Caso contrário, selecione **adicionar** e procure **Jive** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b95e3-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="b95e3-131">Selecione Jive Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b95e3-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="b95e3-132">Selecione sua instância do Jive e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="b95e3-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="b95e3-133">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="b95e3-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b95e3-135">Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="b95e3-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="b95e3-136">a.</span><span class="sxs-lookup"><span data-stu-id="b95e3-136">a.</span></span> <span data-ttu-id="b95e3-137">Em Olá **nome de usuário administrador Jive** caixa de texto, tipo de um Jive nome de conta que tem Olá **administrador do sistema** perfil atribuído no Jive.com.</span><span class="sxs-lookup"><span data-stu-id="b95e3-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="b95e3-138">b.</span><span class="sxs-lookup"><span data-stu-id="b95e3-138">b.</span></span> <span data-ttu-id="b95e3-139">Em Olá **senha do administrador do Jive** caixa de texto, digite a senha Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="b95e3-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="b95e3-140">c.</span><span class="sxs-lookup"><span data-stu-id="b95e3-140">c.</span></span> <span data-ttu-id="b95e3-141">Em Olá **URL de locatário Jive** caixa de texto URL de locatário do tipo hello Jive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b95e3-142">URL de locatário Jive Olá é usado pelo toolog sua organização em tooJive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="b95e3-143">Normalmente, a saudação URL tem Olá formato a seguir: **www.\< organização\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="b95e3-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="b95e3-144">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Jive aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b95e3-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="b95e3-145">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.</span><span class="sxs-lookup"><span data-stu-id="b95e3-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="b95e3-146">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b95e3-146">Click **Save.**</span></span>

9. <span data-ttu-id="b95e3-147">Em Olá mapeamentos, selecione **tooJive sincronizar Azure usuários do Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="b95e3-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="b95e3-148">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooJive do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b95e3-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="b95e3-149">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usados em Jive para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="b95e3-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="b95e3-150">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="b95e3-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="b95e3-151">tooenable Olá serviço de provisionamento do AD do Azure para Jive, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação</span><span class="sxs-lookup"><span data-stu-id="b95e3-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="b95e3-152">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="b95e3-152">Click **Save.**</span></span>

<span data-ttu-id="b95e3-153">Ele inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooJive em Olá usuários e a seção de grupos.</span><span class="sxs-lookup"><span data-stu-id="b95e3-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="b95e3-154">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="b95e3-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="b95e3-155">Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo do Jive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="b95e3-156">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b95e3-156">You can now create a test account.</span></span> <span data-ttu-id="b95e3-157">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooJive.</span><span class="sxs-lookup"><span data-stu-id="b95e3-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b95e3-158">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b95e3-158">Additional resources</span></span>

* [<span data-ttu-id="b95e3-159">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="b95e3-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b95e3-160">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b95e3-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b95e3-161">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="b95e3-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)