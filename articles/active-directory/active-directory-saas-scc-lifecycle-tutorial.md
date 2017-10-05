---
title: "Tutorial: integração do Azure Active Directory com o SCC LifeCycle | Microsoft Docs"
description: "Saiba como usar o SCC LifeCycle com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="be18b-103">Tutorial: Integração do Active Directory do Azure com o SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="be18b-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="be18b-104">O objetivo deste tutorial é mostrar a integração do Azure com o SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="be18b-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="be18b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="be18b-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="be18b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="be18b-107">Uma assinatura do SCC LifeCycle com SSO (logon único) habilitado</span><span class="sxs-lookup"><span data-stu-id="be18b-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="be18b-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao SCC LifeCycle poderão fazer logon único no aplicativo em seu site de empresa do SCC LifeCycle (logon iniciado pelo provedor de serviços) ou usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be18b-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="be18b-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="be18b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="be18b-110">Habilitando a integração de aplicativos com o SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="be18b-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="be18b-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="be18b-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="be18b-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="be18b-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="be18b-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="be18b-113">Assigning users</span></span>

<span data-ttu-id="be18b-114">![Cenário](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="be18b-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="be18b-115">Habilitar a integração de aplicativos com o SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="be18b-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="be18b-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos com o SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="be18b-117">**Para habilitar a integração de aplicativos com o SCC LifeCycle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="be18b-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="be18b-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be18b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="be18b-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="be18b-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="be18b-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="be18b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="be18b-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="be18b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="be18b-122">![Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="be18b-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="be18b-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="be18b-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="be18b-124">![Adicionar aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="be18b-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="be18b-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="be18b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="be18b-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="be18b-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="be18b-127">Na **caixa de pesquisa**, digite **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="be18b-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="be18b-128">![Galeria de Aplicativos](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="be18b-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="be18b-129">No painel de resultados, selecione **SCC LifeCycle** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be18b-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="be18b-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="be18b-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="be18b-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="be18b-131">Configure single sign-on</span></span>

<span data-ttu-id="be18b-132">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no SCC LifeCycle com sua conta do AD do Azure usando federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="be18b-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="be18b-133">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="be18b-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="be18b-134">No Portal Clássico do Azure, na página de integração de aplicativos do **SCC LifeCycle**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="be18b-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="be18b-135">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="be18b-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="be18b-136">Na página **Como você deseja que os usuários façam logon no SCC LifeCycle**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="be18b-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="be18b-137">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="be18b-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="be18b-138">Na página **Configurar a URL do Aplicativo**, na caixa de texto **URL de Entrada**, digite a URL usada por seus usuários para fazer logon no aplicativo SCC LifeCycle usando o padrão "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*" e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="be18b-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="be18b-139">![Configurar URL do Aplicativo](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="be18b-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="be18b-140">Na página **Configurar logon único no SCC LifeCycle**, clique em **Baixar metadados** e salve o arquivo de metadados localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="be18b-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="be18b-141">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="be18b-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="be18b-142">Encaminhe esse arquivo de Metadados à equipe de Suporte do SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="be18b-143">O logon único deve ser habilitado pela equipe de suporte do SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="be18b-144">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="be18b-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="be18b-145">![Configurar Logon Único](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="be18b-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="be18b-146">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="be18b-146">Configure user provisioning</span></span>

<span data-ttu-id="be18b-147">Para permitir que os usuários do AD do Azure façam logon no SCC LifeCycle, eles deverão ser provisionados no SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="be18b-148">Não há nenhum item de ação para a configuração de provisionamento de usuário para o SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="be18b-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="be18b-149">Quando um usuário atribuído tentar fazer logon no SCC LifeCycle, uma conta do SCC LifeCycle será automaticamente criada, se necessário.</span><span class="sxs-lookup"><span data-stu-id="be18b-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="be18b-150">É possível usar qualquer outra ferramenta de criação da conta de usuário do SCC LifeCycle ou as APIs fornecidas pelo SCC LifeCycle para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="be18b-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="be18b-151">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="be18b-151">Assign users</span></span>
<span data-ttu-id="be18b-152">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="be18b-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="be18b-153">**Para atribuir usuários ao SCC LifeCycle, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="be18b-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="be18b-154">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="be18b-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="be18b-155">Na página de integração de aplicativos do **SCC LifeCycle**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="be18b-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="be18b-156">![Atribuir Usuários](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="be18b-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="be18b-157">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="be18b-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="be18b-158">![Sim](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="be18b-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="be18b-159">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="be18b-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="be18b-160">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be18b-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

