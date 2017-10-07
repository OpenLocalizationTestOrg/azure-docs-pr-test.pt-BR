---
title: "Tutorial: configurar o Workplace by Facebook para provisionamento de usuário | Microsoft Docs"
description: "Saiba como contas de usuário de provisionar e provisionar eliminação de tooautomatically do AD do Azure tooWorkplace pelo Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="0b615-103">Tutorial: configurar o Workplace by Facebook para provisionamento de usuário</span><span class="sxs-lookup"><span data-stu-id="0b615-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="0b615-104">Este tutorial mostra Olá tooautomatically necessárias etapas provisionar e desprovisionar contas de usuário do Azure Active Directory (AD do Azure) tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b615-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0b615-105">Prerequisites</span></span>

<span data-ttu-id="0b615-106">tooconfigure integração do AD do Azure com o local de trabalho pelo Facebook, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="0b615-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="0b615-107">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b615-107">An Azure AD subscription</span></span>
- <span data-ttu-id="0b615-108">Uma assinatura do Workplace by Facebook habilitada para SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="0b615-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="0b615-109">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0b615-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="0b615-110">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0b615-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b615-111">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma [oferta de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b615-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="0b615-112">Atribuir usuários tooWorkplace pelo Facebook</span><span class="sxs-lookup"><span data-stu-id="0b615-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="0b615-113">O AD do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0b615-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0b615-114">No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que receberam tooan aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b615-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="0b615-115">Antes de decidir Configurando e habilitando o Olá provisionamento de serviço, quais usuários e grupos no AD do Azure representam usuários de saudação que precisam acessar tooyour no local de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="0b615-116">Você pode atribuir essas tooyour de usuários local de trabalho pelo aplicativo do Facebook seguindo Olá instruções [atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0b615-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="0b615-117">Saudação de teste, configuração de provisionamento, atribuindo um único tooWorkplace de usuário do AD do Azure pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="0b615-118">Atribua usuários e grupos adicionais mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0b615-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="0b615-119">Quando você atribui um tooWorkplace usuário pelo Facebook, você deve selecionar uma função de usuário válido.</span><span class="sxs-lookup"><span data-stu-id="0b615-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="0b615-120">função de acesso padrão de saudação não funciona para o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0b615-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0b615-121">Habilitar o provisionamento automatizado de usuários</span><span class="sxs-lookup"><span data-stu-id="0b615-121">Enable automated user provisioning</span></span>

<span data-ttu-id="0b615-122">Esta seção orienta você por meio de conectar sua conta de usuário do AD do Azure toohello provisionamento API do local de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="0b615-123">Você também aprenderá como tooconfigure Olá provisionamento serviço toocreate, atualizar e desativar contas de usuário atribuído no local de trabalho pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="0b615-124">Isso se baseia na atribuição de usuários e grupos no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b615-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="0b615-125">Você também pode escolher tooenabled SSO baseado em SAML para o local de trabalho pelo Facebook, por seguindo as instruções de saudação fornecidas no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b615-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0b615-126">O SSO pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.</span><span class="sxs-lookup"><span data-stu-id="0b615-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="0b615-127">Configurar a conta de usuário provisionamento tooWorkplace pelo Facebook no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b615-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="0b615-128">Azure AD oferece suporte a saudação capacidade tooautomatically sincronizar detalhes da conta de saudação atribuído tooWorkplace usuários pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="0b615-129">A sincronização automática habilita o local de trabalho por precisa tooauthorize usuários para acessar, antes dos dados do Facebook tooget Olá-los de tentativa de toosign em para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="0b615-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="0b615-130">Ele também desprovisiona os usuários do Workplace by Facebook quando o acesso tiver sido revogado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b615-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="0b615-131">Em Olá [portal do Azure](https://portal.azure.com), selecione **Active Directory do Azure** > **aplicativos corporativos** > **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0b615-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="0b615-132">Se você já tiver configurado o local de trabalho pelo Facebook para SSO, procure sua instância do local de trabalho pelo Facebook usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b615-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="0b615-133">Caso contrário, selecione **adicionar** e procure **no local de trabalho pelo Facebook** na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0b615-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="0b615-134">Selecione **no local de trabalho pelo Facebook** de saudação resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0b615-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0b615-135">Selecione sua instância do local de trabalho pelo Facebook e, em seguida, selecione Olá **provisionamento** guia.</span><span class="sxs-lookup"><span data-stu-id="0b615-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0b615-136">Definir **modo de provisionamento** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="0b615-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Captura de tela das opções de provisionamento do Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0b615-138">Em Olá **credenciais de administrador** seção, digite Olá **segredo do Token** e hello **URL do locatário** do local de trabalho pelo administrador do Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="0b615-139">No portal do Azure de Olá, selecione **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour no local de trabalho pelo aplicativo do Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="0b615-140">Se conexão Olá falhar, certifique-se de que o seu local de trabalho por conta do Facebook tem permissões de administrador de equipe.</span><span class="sxs-lookup"><span data-stu-id="0b615-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="0b615-141">Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e marque a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b615-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="0b615-142">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0b615-142">Select **Save**.</span></span>

9. <span data-ttu-id="0b615-143">Em Olá mapeamentos, selecione **tooWorkplace sincronizar do Azure Active Directory Users pelo Facebook**.</span><span class="sxs-lookup"><span data-stu-id="0b615-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="0b615-144">Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="0b615-145">Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usada na área de trabalho pelo Facebook para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="0b615-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="0b615-146">Selecione de todas as alterações, toocommit **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0b615-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="0b615-147">tooenable Olá serviço de provisionamento do Azure AD para o local de trabalho pelo Facebook, no hello **configurações** seção, altere Olá **Status de provisionamento** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="0b615-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="0b615-148">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0b615-148">Select **Save**.</span></span>

<span data-ttu-id="0b615-149">Para obter mais informações sobre como tooconfigure automático de provisionamento, consulte [Olá Facebook documentação](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="0b615-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="0b615-150">Agora você pode criar uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="0b615-150">You can now create a test account.</span></span> <span data-ttu-id="0b615-151">Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooWorkplace pelo Facebook.</span><span class="sxs-lookup"><span data-stu-id="0b615-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b615-152">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0b615-152">Additional resources</span></span>

* [<span data-ttu-id="0b615-153">Gerenciamento do provisionamento de conta de usuário para aplicativos empresariais</span><span class="sxs-lookup"><span data-stu-id="0b615-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b615-154">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b615-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0b615-155">Configurar Logon Único</span><span class="sxs-lookup"><span data-stu-id="0b615-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

