---
title: "Tutorial: Integração do Azure Active Directory com o Replicon | Microsoft Docs"
description: "Saiba como usar o Replicon com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="07922-103">Tutorial: Integração do Active Directory do Azure com o Replicon</span><span class="sxs-lookup"><span data-stu-id="07922-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="07922-104">O objetivo deste tutorial é mostrar a integração do Azure com o Replicon.</span><span class="sxs-lookup"><span data-stu-id="07922-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="07922-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="07922-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="07922-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="07922-106">A valid Azure subscription</span></span>
* <span data-ttu-id="07922-107">Um locatário do Replicon</span><span class="sxs-lookup"><span data-stu-id="07922-107">A Replicon tenant</span></span>

<span data-ttu-id="07922-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao Replicon poderão fazer logon único no aplicativo em seu site de empresa do Replicon (logon iniciado pelo provedor de serviços) ou usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07922-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="07922-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="07922-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="07922-110">Habilitando a integração de aplicativos para Replicon</span><span class="sxs-lookup"><span data-stu-id="07922-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="07922-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="07922-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="07922-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="07922-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="07922-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="07922-113">Assigning users</span></span>

<span data-ttu-id="07922-114">![Cenário](./media/active-directory-saas-replicon-tutorial/IC777798.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="07922-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="07922-115">Habilitar a integração de aplicativos para Replicon</span><span class="sxs-lookup"><span data-stu-id="07922-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="07922-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos para o Replicon.</span><span class="sxs-lookup"><span data-stu-id="07922-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="07922-117">**Para habilitar a integração de aplicativos com o Replicon, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07922-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="07922-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07922-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="07922-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="07922-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="07922-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="07922-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="07922-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="07922-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="07922-122">![Aplicativos](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="07922-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="07922-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="07922-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="07922-124">![Adicionar aplicativo](./media/active-directory-saas-replicon-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="07922-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="07922-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="07922-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="07922-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-replicon-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="07922-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="07922-127">Na **caixa de pesquisa**, digite **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="07922-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="07922-128">![Galeria de aplicativos](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galeria de aplicativos")</span><span class="sxs-lookup"><span data-stu-id="07922-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="07922-129">No painel de resultados, selecione **Replicon** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07922-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="07922-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="07922-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="07922-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="07922-131">Configure single sign-on</span></span>

<span data-ttu-id="07922-132">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Replicon com sua conta do AD do Azure usando federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="07922-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="07922-133">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07922-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="07922-134">No Portal Clássico do Azure, na página de integração de aplicativos do **Replicon**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="07922-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="07922-135">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="07922-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="07922-136">Na página **Como você deseja que os usuários façam logon no Replicon**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="07922-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="07922-137">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="07922-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="07922-138">Na página **Configurar URL do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07922-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="07922-139">![Configurar URL do Aplicativo](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="07922-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="07922-140">Na caixa de texto **URL de Logon do Replicon**, digite a URL do locatário do Replicon (por exemplo: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="07922-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="07922-141">Na caixa de texto **URL de Resposta do Replicon**, digite a URL de **AssertionConsumerService** do Replicon (por exemplo: *https://global.replicon.com/!/saml2/company/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="07922-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="07922-142">Você pode obter a URL dos metadados do Replicon em: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="07922-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="07922-143">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="07922-143">Click **Next**.</span></span>

4. <span data-ttu-id="07922-144">Na página **Configurar logon único no Replicon**, para baixar os metadados, clique em **Baixar metadados** e salve os metadados no computador.</span><span class="sxs-lookup"><span data-stu-id="07922-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="07922-145">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="07922-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="07922-146">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="07922-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="07922-147">Para configurar o SAML 2.0, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07922-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="07922-148">![Habilitar autenticação de SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar autenticação de SAML")</span><span class="sxs-lookup"><span data-stu-id="07922-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="07922-149">Para exibir a caixa de diálogo **EnableSAML Authentication2**, acrescente o seguinte à URL, após a chave da empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="07922-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="07922-150">O código a seguir mostra o esquema da URL completa:</span><span class="sxs-lookup"><span data-stu-id="07922-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="07922-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="07922-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="07922-152">Clique em **+** para expandir a seção **v20Configuration**.</span><span class="sxs-lookup"><span data-stu-id="07922-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="07922-153">Clique em **+** para expandir a seção **metaDataConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="07922-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="07922-154">Clique em **Escolher Arquivo** para selecionar o arquivo XML de metadados de provedor de identidade e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="07922-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="07922-155">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="07922-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="07922-156">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="07922-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="07922-157">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="07922-157">Configure user provisioning</span></span>

<span data-ttu-id="07922-158">Para permitir que os usuários do AD do Azure façam logon no Replicon, eles deverão ser provisionados no Replicon.</span><span class="sxs-lookup"><span data-stu-id="07922-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="07922-159">No caso do Replicon, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="07922-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="07922-160">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="07922-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="07922-161">Em uma janela de navegador da Web, faça logon no site de sua empresa do Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="07922-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="07922-162">Vá para **Administração\>Usuários**.</span><span class="sxs-lookup"><span data-stu-id="07922-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="07922-163">![Usuários](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="07922-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="07922-164">Clique em **+Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="07922-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="07922-165">![Adicionar Usuário](./media/active-directory-saas-replicon-tutorial/IC777807.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="07922-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="07922-166">Na seção **Perfil de Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07922-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="07922-167">![Perfil de usuário](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuário")</span><span class="sxs-lookup"><span data-stu-id="07922-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="07922-168">Na caixa de texto **Nome de Logon** , digite o endereço de email do Azure AD do usuário do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="07922-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="07922-169">Para **Tipo de Autenticação**, selecione **SSO**.</span><span class="sxs-lookup"><span data-stu-id="07922-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="07922-170">Na caixa de texto **Departamento** , digite o departamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="07922-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="07922-171">Para **Tipo de Funcionário**, selecione **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="07922-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="07922-172">Clique em **Salvar Perfil do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="07922-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="07922-173">É possível usar qualquer outra ferramenta de criação da conta de usuário do Replicon ou as APIs fornecidas pelo Replicon para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="07922-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="07922-174">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="07922-174">Assign users</span></span>
<span data-ttu-id="07922-175">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07922-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="07922-176">**Para atribuir usuários ao Replicon, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="07922-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="07922-177">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="07922-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="07922-178">Na página de integração de aplicativos do **Replicon**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="07922-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="07922-179">![Atribuir usuários](./media/active-directory-saas-replicon-tutorial/IC777809.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="07922-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="07922-180">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="07922-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="07922-181">![Sim](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="07922-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="07922-182">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="07922-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="07922-183">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07922-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

