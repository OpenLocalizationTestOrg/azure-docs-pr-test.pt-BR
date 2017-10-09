---
title: "Tutorial: integração do Azure Active Directory com o SCC LifeCycle | Microsoft Docs"
description: "Saiba como toouse SCC LifeCycle com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="31ca8-103">Tutorial: Integração do Active Directory do Azure com o SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="31ca8-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="31ca8-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="31ca8-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="31ca8-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="31ca8-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="31ca8-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="31ca8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="31ca8-107">Uma assinatura do SCC LifeCycle com SSO (logon único) habilitado</span><span class="sxs-lookup"><span data-stu-id="31ca8-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="31ca8-108">Após concluir este tutorial, Olá AD do Azure usuários atribuídos tooSCC ciclo de vida será toosingle capaz de entrada para o aplicativo hello no site da empresa do SCC LifeCycle (serviço iniciado pelo provedor logon) ou usando Olá [Introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31ca8-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="31ca8-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="31ca8-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="31ca8-110">Habilitando Olá integração de aplicativos para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="31ca8-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="31ca8-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="31ca8-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="31ca8-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="31ca8-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="31ca8-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="31ca8-113">Assigning users</span></span>

<span data-ttu-id="31ca8-114">![Cenário](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="31ca8-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="31ca8-115">Habilitar Olá integração de aplicativos para SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="31ca8-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="31ca8-116">Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="31ca8-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="31ca8-117">**integração do aplicativo hello tooenable para SCC LifeCycle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="31ca8-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ca8-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="31ca8-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="31ca8-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="31ca8-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="31ca8-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="31ca8-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="31ca8-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="31ca8-122">![Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="31ca8-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="31ca8-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="31ca8-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="31ca8-124">![Adicionar aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="31ca8-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="31ca8-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="31ca8-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="31ca8-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="31ca8-127">Em Olá **caixa de pesquisa**, tipo **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="31ca8-128">![Galeria de Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="31ca8-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="31ca8-129">No painel de resultados de saudação, selecione **SCC LifeCycle**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="31ca8-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="31ca8-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="31ca8-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="31ca8-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="31ca8-131">Configure single sign-on</span></span>

<span data-ttu-id="31ca8-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSCC ciclo de vida com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="31ca8-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="31ca8-133">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="31ca8-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ca8-134">Em Olá portal clássico do Azure, em Olá **SCC LifeCycle** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31ca8-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="31ca8-135">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="31ca8-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="31ca8-136">Em Olá **como você gostaria usuários toosign no ciclo de vida de tooSCC** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="31ca8-137">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="31ca8-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="31ca8-138">Em Olá **configurar URL do aplicativo** página Olá **URL de logon** caixa de texto, digite a URL de saudação usado pelo seu toosign usuários em tooyour aplicativo SCC LifeCycle usando saudação padrão a seguir "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*"e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="31ca8-139">![Configurar URL do Aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="31ca8-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="31ca8-140">Em Olá **configurar logon único no SCC LifeCycle** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="31ca8-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="31ca8-141">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="31ca8-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="31ca8-142">Encaminhe esse arquivo de metadados tooSCC a equipe de suporte do ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="31ca8-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="31ca8-143">O logon único tem toobe habilitado por Olá, equipe de suporte do SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="31ca8-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="31ca8-144">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31ca8-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="31ca8-145">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="31ca8-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="31ca8-146">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="31ca8-146">Configure user provisioning</span></span>

<span data-ttu-id="31ca8-147">Ordem tooenable AD do Azure usuários toolog no SCC LifeCycle, eles devem ser provisionados no SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="31ca8-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="31ca8-148">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooSCC ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="31ca8-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="31ca8-149">Quando um toolog de tentativas de usuário atribuído no SCC LifeCycle, uma conta do SCC LifeCycle é criada automaticamente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="31ca8-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="31ca8-150">Você pode usar qualquer ferramenta de criação outros SCC LifeCycle usuário conta ou APIs fornecidas pelo SCC LifeCycle tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="31ca8-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="31ca8-151">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="31ca8-151">Assign users</span></span>
<span data-ttu-id="31ca8-152">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="31ca8-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="31ca8-153">**tooassign usuários tooSCC ciclo de vida, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="31ca8-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="31ca8-154">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="31ca8-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="31ca8-155">Em hello * * SCC LifeCycle * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="31ca8-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="31ca8-156">![Atribuir Usuários](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="31ca8-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="31ca8-157">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="31ca8-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="31ca8-158">![Sim](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="31ca8-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="31ca8-159">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="31ca8-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="31ca8-160">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31ca8-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

