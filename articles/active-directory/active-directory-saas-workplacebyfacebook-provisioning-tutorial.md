---
title: "Tutorial: Integração do Azure Active Directory com o Workplace by Facebook| Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o local de trabalho pelo Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="1c338-103">Tutorial: configurar o Workplace by Facebook para o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="1c338-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="1c338-104">Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no local de trabalho pelo Facebook e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c338-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1c338-105">Prerequisites</span></span>

<span data-ttu-id="1c338-106">tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c338-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="1c338-107">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c338-107">An Azure AD subscription</span></span>
- <span data-ttu-id="1c338-108">Uma assinatura do Workplace by Facebook habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1c338-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c338-109">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1c338-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c338-110">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1c338-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c338-111">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1c338-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c338-112">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c338-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="1c338-113">Atribuir usuários tooWorkplace pelo Facebook</span><span class="sxs-lookup"><span data-stu-id="1c338-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="1c338-114">Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1c338-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1c338-115">No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="1c338-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1c338-116">Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour no local de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="1c338-117">Depois de decidir, você pode atribuir essas tooyour de usuários local de trabalho pelo aplicativo do Facebook, seguindo as instruções de saudação aqui:</span><span class="sxs-lookup"><span data-stu-id="1c338-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="1c338-118">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="1c338-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="1c338-119">Dicas importantes para atribuir usuários tooWorkplace pelo Facebook</span><span class="sxs-lookup"><span data-stu-id="1c338-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="1c338-120">É recomendável que um único usuário do AD do Azure é atribuído tooWorkplace pelo Facebook tootest Olá configuração de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="1c338-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="1c338-121">Outros usuários e/ou grupos podem ser atribuídos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1c338-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1c338-122">Ao atribuir tooWorkplace um usuário pelo Facebook, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="1c338-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="1c338-123">função de "Acesso padrão" Hello não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="1c338-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="1c338-124">Habilitar o provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="1c338-124">Enable User Provisioning</span></span>

<span data-ttu-id="1c338-125">Esta seção orienta você conectar seu AD do Azure tooWorkplace pela API de provisionamento de conta de usuário do Facebook e configurando Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no local de trabalho pelo Facebook com base no usuário e grupo atribuição no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c338-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="1c338-126">Você também pode escolher tooenabled baseado no SAML SSO para o local de trabalho pelo Facebook, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c338-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1c338-127">O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="1c338-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="1c338-128">conta de usuário tooconfigure provisionamento tooWorkplace pelo Facebook no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="1c338-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="1c338-129">Olá o objetivo desta seção é toooutline como tooenable provisionamento de usuário do Active Directory contas tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="1c338-130">Azure AD oferece suporte a saudação capacidade tooautomatically sincronizar detalhes da conta de saudação atribuído tooWorkplace usuários pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="1c338-131">A sincronização automática habilita o local de trabalho por precisa tooauthorize usuários para acessar, antes dos dados do Facebook tooget Olá-los de tentativa de toosign em para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="1c338-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="1c338-132">Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c338-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="1c338-133">Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure** > **aplicativos corporativos** > **detodososaplicativos** seção.</span><span class="sxs-lookup"><span data-stu-id="1c338-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="1c338-134">Se você já tiver configurado o local de trabalho pelo Facebook para logon único, procure sua instância do local de trabalho pelo Facebook usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c338-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="1c338-135">Caso contrário, selecione **adicionar** e procure **no local de trabalho pelo Facebook** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1c338-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="1c338-136">Selecione o local de trabalho pelo Facebook Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1c338-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="1c338-137">Selecione sua instância do local de trabalho pelo Facebook e selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="1c338-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="1c338-138">Saudação de conjunto **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="1c338-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisionamento](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="1c338-140">Em Olá **credenciais de administrador** seção, digite Olá segredo do Token e Olá URL do locatário da área de trabalho pelo administrador do Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="1c338-141">No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour no local de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="1c338-142">Se a conexão de saudação falhar, certifique-se de que seu local de trabalho por conta do Facebook tem permissões de administrador de equipe.</span><span class="sxs-lookup"><span data-stu-id="1c338-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="1c338-143">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c338-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="1c338-144">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="1c338-144">Click **Save.**</span></span>

9. <span data-ttu-id="1c338-145">Em Olá mapeamentos, selecione **tooWorkplace sincronizar do Azure Active Directory Users pelo Facebook.**</span><span class="sxs-lookup"><span data-stu-id="1c338-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="1c338-146">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="1c338-147">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usada na área de trabalho pelo Facebook para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="1c338-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="1c338-148">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="1c338-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="1c338-149">tooenable Olá serviço de provisionamento do AD do Azure para o local de trabalho pelo Facebook, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção</span><span class="sxs-lookup"><span data-stu-id="1c338-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="1c338-150">Clique em **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="1c338-150">Click **Save.**</span></span>

<span data-ttu-id="1c338-151">Para obter mais informações sobre como tooconfigure automático de provisionamento, consulte [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="1c338-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="1c338-152">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="1c338-152">You can now create a test account.</span></span> <span data-ttu-id="1c338-153">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="1c338-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c338-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1c338-154">Additional resources</span></span>

* [<span data-ttu-id="1c338-155">Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="1c338-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c338-156">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c338-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1c338-157">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="1c338-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

