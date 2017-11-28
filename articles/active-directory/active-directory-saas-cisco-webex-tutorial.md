---
title: "Tutorial: integração do Azure Active Directory com o Cisco Webex | Microsoft Docs"
description: "Saiba como toouse Cisco Webex com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="06e89-103">Tutorial: integração do Active Directory do Azure ao Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="06e89-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="06e89-104">Olá objetivo deste tutorial é a integração do Azure e do Cisco Webex Olá tooshow.</span><span class="sxs-lookup"><span data-stu-id="06e89-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="06e89-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="06e89-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="06e89-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="06e89-106">A valid Azure subscription</span></span>
* <span data-ttu-id="06e89-107">Um locatário do Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="06e89-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="06e89-108">Após concluir este tutorial, Olá AD do Azure usuários atribuídos tooCisco Webex será toosingle capaz de entrada para o aplicativo hello no site da empresa do Cisco Webex (serviço iniciado pelo provedor logon) ou usando Olá [toohello de Introdução Acessar o painel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06e89-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="06e89-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="06e89-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="06e89-110">Habilitando Olá integração de aplicativos para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="06e89-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="06e89-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="06e89-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="06e89-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="06e89-112">Configuring user provisioning</span></span>
* <span data-ttu-id="06e89-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="06e89-113">Assigning users</span></span>

<span data-ttu-id="06e89-114">![Cenário](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="06e89-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="06e89-115">Habilitar Olá integração de aplicativos para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="06e89-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="06e89-116">Olá objetivo desta seção é toooutline como integração de aplicativos tooenable Olá para Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="06e89-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="06e89-117">**integração do aplicativo hello tooenable para Cisco Webex, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="06e89-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="06e89-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="06e89-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="06e89-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="06e89-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="06e89-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="06e89-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="06e89-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="06e89-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="06e89-122">![Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="06e89-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="06e89-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="06e89-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="06e89-124">![Adicionar aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="06e89-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="06e89-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="06e89-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="06e89-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="06e89-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="06e89-127">Em Olá **caixa de pesquisa**, tipo **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="06e89-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="06e89-128">![Galeria de Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="06e89-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="06e89-129">No painel de resultados de saudação, selecione **Cisco Webex**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="06e89-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="06e89-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="06e89-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="06e89-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="06e89-131">Configure single sign-on</span></span>

<span data-ttu-id="06e89-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCisco Webex com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="06e89-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="06e89-133">Como parte desse procedimento, será necessário toocreate um certificado codificado em base 64.</span><span class="sxs-lookup"><span data-stu-id="06e89-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="06e89-134">Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="06e89-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="06e89-135">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="06e89-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="06e89-136">Em Olá portal clássico do Azure, em Olá **Cisco Webex** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="06e89-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="06e89-137">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="06e89-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="06e89-138">Em Olá **como você gostaria usuários toosign em tooCisco Webex** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="06e89-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="06e89-139">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="06e89-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="06e89-140">Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="06e89-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="06e89-141">![Configurar URL do Aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="06e89-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="06e89-142">Em Olá **URL de logon** caixa de texto, digite a URL do locatário Cisco Webex (por exemplo: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="06e89-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="06e89-143">Em hello **URL de resposta do Cisco Webex** caixa de texto, tipo de sua **URL Cisco Webex AssertionConsumerService** (por exemplo: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="06e89-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="06e89-144">Em Olá **configurar logon único no Cisco Webex** página, toodownload seu certificado, clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="06e89-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="06e89-145">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="06e89-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="06e89-146">Em uma janela diferente do navegador da Web, faça logon em seu site de empresa do Cisco Webex como administrador.</span><span class="sxs-lookup"><span data-stu-id="06e89-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="06e89-147">No menu de saudação na parte superior de saudação, clique em **administração de Site**.</span><span class="sxs-lookup"><span data-stu-id="06e89-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="06e89-148">![Administração de Site](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administração de Site")</span><span class="sxs-lookup"><span data-stu-id="06e89-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="06e89-149">Em Olá **Gerenciar Site** seção, clique em **configuração SSO**.</span><span class="sxs-lookup"><span data-stu-id="06e89-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="06e89-150">![Configuração de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="06e89-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="06e89-151">Na seção de configuração de SSO da Web federado do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="06e89-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="06e89-152">![Configuração de SSO Federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuração de SSO Federado")</span><span class="sxs-lookup"><span data-stu-id="06e89-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="06e89-153">De saudação **protocolo Federation** lista, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="06e89-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="06e89-154">Crie um arquivo **codificado em base 64** usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="06e89-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="06e89-155">Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="06e89-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="06e89-156">Abra seu certificado codificado em base 64 no bloco de notas e, em seguida, Olá de copiar conteúdo dele.</span><span class="sxs-lookup"><span data-stu-id="06e89-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="06e89-157">Clique em **Importar Metadados do SAML**e cole o certificado codificado em Base 64.</span><span class="sxs-lookup"><span data-stu-id="06e89-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="06e89-158">Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-Olá **emissor para SAML (ID IdP)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="06e89-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="06e89-159">Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL de logon remoto** valor e, em seguida, cole-Olá **logon de serviço de SSO do cliente URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="06e89-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="06e89-160">De saudação **formato NameID** lista, selecione **endereço de Email**.</span><span class="sxs-lookup"><span data-stu-id="06e89-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="06e89-161">Em Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: nomes: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="06e89-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="06e89-162">Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página de diálogo, Olá cópia **URL de Logout remoto** valor e, em seguida, cole-Olá **Logout de serviço de SSO do cliente URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="06e89-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="06e89-163">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="06e89-163">Click **Update**.</span></span>
9. <span data-ttu-id="06e89-164">Em Olá portal clássico do Azure, em Olá **configurar logon único no Cisco Webex** página da caixa de diálogo, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="06e89-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="06e89-165">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="06e89-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="06e89-166">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="06e89-166">Configure user provisioning</span></span>

<span data-ttu-id="06e89-167">Em ordem tooenable AD do Azure usuários toolog no Cisco Webex, eles devem ser provisionados no Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="06e89-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="06e89-168">No caso de saudação do Cisco Webex, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="06e89-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="06e89-169">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="06e89-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="06e89-170">Faça logon no tooyour **Cisco Webex** locatário.</span><span class="sxs-lookup"><span data-stu-id="06e89-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="06e89-171">Vá muito**gerenciar usuários \> adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="06e89-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="06e89-172">![Adicionar Usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="06e89-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="06e89-173">Na seção Adicionar usuário do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="06e89-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="06e89-174">![Adicionar Usuário](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="06e89-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="06e89-175">Para **Tipo de Conta**, selecione **Host**.</span><span class="sxs-lookup"><span data-stu-id="06e89-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="06e89-176">Digite as informações de saudação de um usuário existente do AD do Azure em Olá caixas de texto a seguir: **nome, Sobrenome**, **nome de usuário**, **Email**, **senha**, **Confirmar senha**.</span><span class="sxs-lookup"><span data-stu-id="06e89-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="06e89-177">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="06e89-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="06e89-178">Você pode usar qualquer ferramenta de criação outros Cisco Webex usuário conta ou APIs fornecidas pelo Cisco Webex tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="06e89-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="06e89-179">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="06e89-179">Assign users</span></span>
<span data-ttu-id="06e89-180">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="06e89-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="06e89-181">**tooassign usuários tooCisco Webex, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="06e89-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="06e89-182">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="06e89-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="06e89-183">Em Olá **Cisco Webex** página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="06e89-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="06e89-184">![Atribuir usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="06e89-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="06e89-185">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="06e89-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="06e89-186">![Sim](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="06e89-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="06e89-187">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="06e89-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="06e89-188">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06e89-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

