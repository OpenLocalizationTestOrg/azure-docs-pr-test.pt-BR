---
title: "Tutorial: Integração do Azure Active Directory com o Replicon | Microsoft Docs"
description: "Saiba como toouse Replicon com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="95d38-103">Tutorial: Integração do Active Directory do Azure com o Replicon</span><span class="sxs-lookup"><span data-stu-id="95d38-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="95d38-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e Replicon.</span><span class="sxs-lookup"><span data-stu-id="95d38-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="95d38-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d38-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="95d38-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="95d38-106">A valid Azure subscription</span></span>
* <span data-ttu-id="95d38-107">Um locatário do Replicon</span><span class="sxs-lookup"><span data-stu-id="95d38-107">A Replicon tenant</span></span>

<span data-ttu-id="95d38-108">Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooReplicon será toosingle capaz de usar o logon no aplicativo hello em seu site da empresa do Replicon (serviço iniciado pelo provedor logon), ou por meio de saudação [Introdução toohello acesso Painel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95d38-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="95d38-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d38-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="95d38-110">Habilitando Olá integração de aplicativos para Replicon</span><span class="sxs-lookup"><span data-stu-id="95d38-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="95d38-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="95d38-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="95d38-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="95d38-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="95d38-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="95d38-113">Assigning users</span></span>

<span data-ttu-id="95d38-114">![Cenário](./media/active-directory-saas-replicon-tutorial/IC777798.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="95d38-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="95d38-115">Habilitar Olá integração de aplicativos para Replicon</span><span class="sxs-lookup"><span data-stu-id="95d38-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="95d38-116">Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Replicon.</span><span class="sxs-lookup"><span data-stu-id="95d38-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="95d38-117">**integração do aplicativo hello tooenable para Replicon, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95d38-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="95d38-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95d38-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="95d38-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="95d38-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="95d38-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="95d38-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="95d38-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="95d38-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="95d38-122">![Aplicativos](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="95d38-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="95d38-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="95d38-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="95d38-124">![Adicionar aplicativo](./media/active-directory-saas-replicon-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="95d38-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="95d38-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="95d38-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="95d38-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-replicon-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="95d38-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="95d38-127">Em Olá **caixa de pesquisa**, tipo **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="95d38-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="95d38-128">![Galeria de aplicativos](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galeria de aplicativos")</span><span class="sxs-lookup"><span data-stu-id="95d38-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="95d38-129">No painel de resultados de saudação, selecione **Replicon**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="95d38-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="95d38-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="95d38-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="95d38-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="95d38-131">Configure single sign-on</span></span>

<span data-ttu-id="95d38-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooReplicon com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="95d38-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="95d38-133">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95d38-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="95d38-134">Em Olá portal clássico do Azure, em Olá **Replicon** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95d38-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="95d38-135">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="95d38-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="95d38-136">Em Olá **como você gostaria usuários toosign em tooReplicon** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95d38-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="95d38-137">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="95d38-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="95d38-138">Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d38-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="95d38-139">![Configurar URL do Aplicativo](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="95d38-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="95d38-140">Em Olá **Replicon URL de logon** caixa de texto, digite a URL do locatário Replicon (por exemplo: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="95d38-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="95d38-141">Em Olá **URL de resposta do Replicon** caixa de texto, digite a URL **AssertionConsumerService** URL (por exemplo: *https://global.replicon.com/! / saml2/empresa/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="95d38-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="95d38-142">Você pode obter a URL de saudação do hello Replicon metadados em: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="95d38-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="95d38-143">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95d38-143">Click **Next**.</span></span>

4. <span data-ttu-id="95d38-144">Em Olá **configurar logon único no Replicon** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve os metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="95d38-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="95d38-145">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="95d38-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="95d38-146">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="95d38-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="95d38-147">tooconfigure SAML 2.0, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d38-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="95d38-148">![Habilitar autenticação de SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar autenticação de SAML")</span><span class="sxs-lookup"><span data-stu-id="95d38-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="95d38-149">Olá toodisplay **EnableSAML Authentication2** caixa de diálogo, acrescente Olá tooyour URL, a seguir após a chave da empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="95d38-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="95d38-150">seguir Olá mostra o esquema de saudação de URL completa hello:</span><span class="sxs-lookup"><span data-stu-id="95d38-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="95d38-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="95d38-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="95d38-152">Clique em Olá  **+**  tooexpand Olá **v20Configuration** seção.</span><span class="sxs-lookup"><span data-stu-id="95d38-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="95d38-153">Clique em Olá  **+**  tooexpand Olá **metaDataConfiguration** seção.</span><span class="sxs-lookup"><span data-stu-id="95d38-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="95d38-154">Clique em **Escolher arquivo**, tooselect seu arquivo XML de metadados de provedor de identidade e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="95d38-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="95d38-155">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="95d38-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="95d38-156">![Configurar logon único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="95d38-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="95d38-157">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="95d38-157">Configure user provisioning</span></span>

<span data-ttu-id="95d38-158">Em ordem tooenable AD do Azure usuários toolog no Replicon, eles devem ser provisionados no Replicon.</span><span class="sxs-lookup"><span data-stu-id="95d38-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="95d38-159">No caso de saudação do Replicon, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="95d38-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="95d38-160">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95d38-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="95d38-161">Em uma janela de navegador da Web, faça logon no site de sua empresa do Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="95d38-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="95d38-162">Vá muito**administração \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="95d38-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="95d38-163">![Usuários](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="95d38-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="95d38-164">Clique em **+Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="95d38-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="95d38-165">![Adicionar Usuário](./media/active-directory-saas-replicon-tutorial/IC777807.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="95d38-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="95d38-166">Em Olá **perfil de usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95d38-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="95d38-167">![Perfil de usuário](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuário")</span><span class="sxs-lookup"><span data-stu-id="95d38-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="95d38-168">Em Olá **nome de logon** caixa de texto, Olá tipo AD do Azure endereço de email do usuário de saudação do AD do Azure que você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="95d38-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="95d38-169">Para **Tipo de Autenticação**, selecione **SSO**.</span><span class="sxs-lookup"><span data-stu-id="95d38-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="95d38-170">Em Olá **departamento** caixa de texto, digite departamento saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="95d38-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="95d38-171">Para **Tipo de Funcionário**, selecione **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="95d38-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="95d38-172">Clique em **Salvar Perfil do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="95d38-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="95d38-173">Você pode usar qualquer ferramenta de criação outros Replicon usuário conta ou APIs fornecidas pelo Replicon tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="95d38-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="95d38-174">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="95d38-174">Assign users</span></span>
<span data-ttu-id="95d38-175">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="95d38-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="95d38-176">**tooassign usuários tooReplicon, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="95d38-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="95d38-177">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="95d38-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="95d38-178">Em Olá **Replicon** página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="95d38-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="95d38-179">![Atribuir usuários](./media/active-directory-saas-replicon-tutorial/IC777809.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="95d38-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="95d38-180">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="95d38-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="95d38-181">![Sim](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="95d38-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="95d38-182">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="95d38-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="95d38-183">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95d38-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

