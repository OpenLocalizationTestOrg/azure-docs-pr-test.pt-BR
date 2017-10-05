---
title: "Tutorial: integração do Azure Active Directory com o Cisco Webex | Microsoft Docs"
description: "Saiba como usar o Cisco Webex com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="5943b-103">Tutorial: integração do Active Directory do Azure ao Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="5943b-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="5943b-104">O objetivo deste tutorial é mostrar a integração do Azure ao Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="5943b-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="5943b-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5943b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5943b-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="5943b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5943b-107">Um locatário do Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="5943b-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="5943b-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao Cisco Webex poderão fazer logon único no aplicativo em seu site de empresa do Cisco Webex (logon iniciado pelo provedor de serviços) ou usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5943b-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5943b-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5943b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="5943b-110">Habilitando a integração de aplicativos para o Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="5943b-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="5943b-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="5943b-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="5943b-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="5943b-112">Configuring user provisioning</span></span>
* <span data-ttu-id="5943b-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="5943b-113">Assigning users</span></span>

<span data-ttu-id="5943b-114">![Cenário](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="5943b-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="5943b-115">Habilitar a integração de aplicativos para o Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="5943b-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="5943b-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos para o Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="5943b-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="5943b-117">**Para habilitar a integração de aplicativos para o Cisco Webex, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5943b-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="5943b-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5943b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5943b-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5943b-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5943b-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="5943b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5943b-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="5943b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5943b-122">![Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="5943b-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5943b-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="5943b-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5943b-124">![Adicionar aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="5943b-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5943b-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="5943b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5943b-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="5943b-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5943b-127">Na **caixa de pesquisa**, digite **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="5943b-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="5943b-128">![Galeria de Aplicativos](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="5943b-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="5943b-129">No painel de resultados, selecione **Cisco Webex** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5943b-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5943b-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="5943b-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5943b-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="5943b-131">Configure single sign-on</span></span>

<span data-ttu-id="5943b-132">O objetivo desta seção é descrever como permitir que os usuários autentiquem no Cisco Webex com a própria conta do Azure AD usando a federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="5943b-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="5943b-133">Como parte deste procedimento, será necessário criar um certificado codificado em base-64.</span><span class="sxs-lookup"><span data-stu-id="5943b-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="5943b-134">Se você não estiver familiarizado com esse procedimento, veja [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="5943b-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="5943b-135">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5943b-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5943b-136">No Portal Clássico do Azure, na página de integração do aplicativo **Cisco Webex**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="5943b-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5943b-137">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5943b-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="5943b-138">Na página **Como você deseja que os usuários façam logon no Cisco Webex**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5943b-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5943b-139">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5943b-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="5943b-140">Na página **Configurar URL do Aplicativo**, realize as etapas a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5943b-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="5943b-141">![Configurar URL do Aplicativo](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="5943b-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="5943b-142">Na caixa de texto **URL de Logon**, digite a URL de locatário do Cisco Webex (por exemplo, *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="5943b-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="5943b-143">Na caixa de texto **URL de resposta do Cisco Webex**, digite sua **URL do AssertionConsumerService do Cisco Webex** (por exemplo, *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="5943b-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="5943b-144">Na página **Configurar logon único no Cisco Webex**, para baixar seu certificado, clique em **Baixar certificado** e salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="5943b-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="5943b-145">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5943b-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="5943b-146">Em uma janela diferente do navegador da Web, faça logon em seu site de empresa do Cisco Webex como administrador.</span><span class="sxs-lookup"><span data-stu-id="5943b-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="5943b-147">No menu na parte superior, clique em **Administração de Site**.</span><span class="sxs-lookup"><span data-stu-id="5943b-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="5943b-148">![Administração de Site](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Administração de Site")</span><span class="sxs-lookup"><span data-stu-id="5943b-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="5943b-149">Na seção **Gerenciar Site**, clique em **Configuração de SSO**.</span><span class="sxs-lookup"><span data-stu-id="5943b-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="5943b-150">![Configuração de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="5943b-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="5943b-151">Na seção Configuração de SSO da Web Federado, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5943b-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="5943b-152">![Configuração de SSO Federado](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuração de SSO Federado")</span><span class="sxs-lookup"><span data-stu-id="5943b-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="5943b-153">Na lista **Protocolo de Federação**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5943b-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="5943b-154">Crie um arquivo **codificado em base 64** usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="5943b-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="5943b-155">Para obter mais detalhes, veja [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="5943b-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="5943b-156">Abra seu certificado codificado em base-64 no bloco de notas e copie o conteúdo dele.</span><span class="sxs-lookup"><span data-stu-id="5943b-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="5943b-157">Clique em **Importar Metadados do SAML**e cole o certificado codificado em Base 64.</span><span class="sxs-lookup"><span data-stu-id="5943b-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="5943b-158">No portal clássico do Azure, na página do diálogo **Configurar logon único no Cisco Webex**, copie o valor da **URL do Emissor** e cole-o na caixa de texto **Emissor para SAML (ID do IdP)**.</span><span class="sxs-lookup"><span data-stu-id="5943b-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="5943b-159">No portal clássico do Azure, na página do diálogo **Configurar logon único no Cisco Webex**, copie o valor da **URL de Logon Remoto** e cole-o na caixa de texto **URL de Logon do Serviço SSO do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="5943b-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="5943b-160">Na lista **Formato de NameID**, selecione **Endereço de Email**.</span><span class="sxs-lookup"><span data-stu-id="5943b-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="5943b-161">Na caixa de texto **AuthnContextClassRef**, digite **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="5943b-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="5943b-162">No portal clássico do Azure, na página do diálogo **Configurar logon único no Cisco Webex**, copie o valor da **URL de Logout Remoto** e cole-o na caixa de texto **URL de Logout do Serviço SSO do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="5943b-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="5943b-163">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="5943b-163">Click **Update**.</span></span>
9. <span data-ttu-id="5943b-164">No portal clássico do Azure, na página do diálogo **Configurar logon único no Cisco Webex**, escolha a confirmação de configuração de logon único e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="5943b-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="5943b-165">![Configurar logon único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="5943b-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="5943b-166">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="5943b-166">Configure user provisioning</span></span>

<span data-ttu-id="5943b-167">Para permitir que os usuários do Azure AD façam logon no Cisco Webex, eles devem ser provisionados no Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="5943b-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="5943b-168">No caso do Cisco Webex, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="5943b-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="5943b-169">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5943b-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5943b-170">Faça logon em seu locatário do **Cisco Webex** .</span><span class="sxs-lookup"><span data-stu-id="5943b-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="5943b-171">Vá para **Gerenciar Usuários \> Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="5943b-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="5943b-172">![Adicionar Usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="5943b-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="5943b-173">Na seção Adicionar Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5943b-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="5943b-174">![Adicionar Usuário](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="5943b-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="5943b-175">Para **Tipo de Conta**, selecione **Host**.</span><span class="sxs-lookup"><span data-stu-id="5943b-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="5943b-176">Digite as informações de um usuário existente do Azure AD nas seguintes caixas de texto: **Nome, Sobrenome**, **Nome de usuário**, **Email**, **Senha** e **Confirmar Senha**.</span><span class="sxs-lookup"><span data-stu-id="5943b-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="5943b-177">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5943b-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="5943b-178">É possível usar qualquer outra ferramenta de criação da conta de usuário do Cisco Webex ou APIs fornecidas pelo Cisco Webex para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="5943b-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="5943b-179">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="5943b-179">Assign users</span></span>
<span data-ttu-id="5943b-180">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5943b-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="5943b-181">**Para atribuir usuários ao Cisco Webex, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5943b-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="5943b-182">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="5943b-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5943b-183">Na página de integração do aplicativo **Cisco Webex**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="5943b-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5943b-184">![Atribuir usuários](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="5943b-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="5943b-185">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="5943b-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5943b-186">![Sim](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="5943b-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5943b-187">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5943b-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5943b-188">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5943b-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

