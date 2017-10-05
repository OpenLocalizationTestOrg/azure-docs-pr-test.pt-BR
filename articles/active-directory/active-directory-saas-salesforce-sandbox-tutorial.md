---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como usar a Área Restrita Salesforce com o Active Directory do Azure para habilitar o logon único, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="2317b-103">Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce</span><span class="sxs-lookup"><span data-stu-id="2317b-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="2317b-104">O objetivo deste tutorial é mostrar a integração do Azure com a Área Restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="2317b-105">Para enviar comentários, consulte a [página de suporte do Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="2317b-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="2317b-106">As áreas restritas oferecem a capacidade de criar várias cópias da sua organização em ambientes separados por uma variedade de finalidades, como desenvolvimento, testes e treinamento, sem comprometer os dados e os aplicativos em sua organização de produção do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="2317b-107">Para obter mais detalhes, confira [Visão geral da área restrita](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="2317b-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="2317b-108">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2317b-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2317b-109">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="2317b-109">A valid Azure subscription</span></span>
* <span data-ttu-id="2317b-110">Uma área restrita no Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="2317b-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="2317b-111">Se você não tiver uma área restrita válida no Salesforce.com, precisará entrar em contato com o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="2317b-112">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2317b-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="2317b-113">Habilitando a integração de aplicativos para a Área Restrita Salesforce</span><span class="sxs-lookup"><span data-stu-id="2317b-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="2317b-114">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="2317b-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="2317b-115">Habilitando seu domínio</span><span class="sxs-lookup"><span data-stu-id="2317b-115">Enabling your domain</span></span>
4. <span data-ttu-id="2317b-116">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="2317b-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="2317b-117">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="2317b-117">Assigning users</span></span>

<span data-ttu-id="2317b-118">![Cenário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="2317b-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="2317b-119">Habilitar a integração de aplicativos para a Área Restrita do Salesforce</span><span class="sxs-lookup"><span data-stu-id="2317b-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="2317b-120">O objetivo desta seção é descrever como habilitar a integração de aplicativos para a área restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="2317b-121">**Para habilitar a integração de aplicativos para a área restrita Salesforce, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2317b-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="2317b-122">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2317b-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2317b-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2317b-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2317b-124">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="2317b-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2317b-125">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="2317b-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2317b-126">![Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="2317b-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2317b-127">Para abrir a **Galeria de Aplicativos**, clique em **Adicionar um Aplicativo** e em **Adicionar um aplicativo a ser utilizado pela minha organização**.</span><span class="sxs-lookup"><span data-stu-id="2317b-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="2317b-128">![O que você deseja fazer? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "O que você deseja fazer?")</span><span class="sxs-lookup"><span data-stu-id="2317b-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="2317b-129">Na **caixa de pesquisa**, digite **Área Restrita Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="2317b-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="2317b-130">![Galeria de Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="2317b-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="2317b-131">No painel de resultados, selecione **Área Restrita Salesforce** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2317b-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2317b-132">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="2317b-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="2317b-133">Configurar o SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="2317b-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="2317b-134">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Salesforce com a conta do AD do Azure usando federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="2317b-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2317b-135">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2317b-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2317b-136">No Portal Clássico do Azure, na página de integração de aplicativos da **Área Restrita do Salesforce**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="2317b-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2317b-137">![Configurar logon único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="2317b-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="2317b-138">Na página **Como você deseja que os usuários façam logon na Área Restrita Salesforce**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="2317b-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2317b-139">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="2317b-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="2317b-140">Na página **Configurar URL do Aplicativo**, na caixa de texto **URL de logon**, digite sua URL usando o seguinte padrão, `http://company.my.salesforce.com` e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="2317b-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="2317b-141">![Configurar URL do Aplicativo](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="2317b-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="2317b-142">Se já tiver configurado o logon único para outra instância de Área restrita do Salesforce em seu diretório, você também deve configurar o **Identificador** para ter o mesmo valor que a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="2317b-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="2317b-143">O campo **Identificador** pode ser encontrado marcando a caixa de seleção **Mostrar configurações avançadas** na página **Configurar URL do Aplicativo** do diálogo.</span><span class="sxs-lookup"><span data-stu-id="2317b-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="2317b-144">Na página **Configurar logon único na Área Restrita Salesforce**, clique em **Baixar o certificado** e salve o arquivo de certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2317b-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="2317b-145">![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2317b-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="2317b-146">Em outra janela do navegador da Web, faça logon em sua área restrita Salesforce como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2317b-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="2317b-147">No menu na parte superior, clique em **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="2317b-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="2317b-148">![Configuração](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="2317b-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="2317b-149">No painel de navegação à esquerda, clique em **Controles de Segurança** e clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="2317b-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="2317b-150">![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2317b-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="2317b-151">Na seção de Configurações de Logon Único, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2317b-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="2317b-152">![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2317b-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="2317b-153">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="2317b-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="2317b-154">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="2317b-154">Click **New**.</span></span>
10. <span data-ttu-id="2317b-155">Na seção Configurações de Logon Único de SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2317b-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="2317b-156">![Configurações de Logon Único do SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="2317b-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="2317b-157">Na caixa de texto Nome, digite o nome da configuração (por exemplo:*SPSSOWAAD\_Teste*).</span><span class="sxs-lookup"><span data-stu-id="2317b-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="2317b-158">No portal clássico do Azure, na página de diálogo **Configurar logon único na Área Restrita do Salesforce**, copie o valor de **URL do Emissor** e cole-o na caixa de texto **Emissor**.</span><span class="sxs-lookup"><span data-stu-id="2317b-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="2317b-159">Na caixa de texto **Id da Entidade**, digite **https://test.salesforce.com** se esta for a primeira instância de área restrita do Salesforce que você está adicionando ao seu diretório.</span><span class="sxs-lookup"><span data-stu-id="2317b-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="2317b-160">Se você já tiver adicionado uma instância da Área restrita do Salesforce, para a **ID da Entidade**, digite a **URL de Logon** que deve estar no seguinte formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="2317b-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="2317b-161">Clique em **Procurar** para carregar o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="2317b-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="2317b-162">Para o **Tipo de Identidade SAML**, selecione **A declaração contém a ID de Federação do objeto de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="2317b-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="2317b-163">Para **Local de Identidade SAML**, selecione **A identidade está no elemento NameIdentifier da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="2317b-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="2317b-164">No portal clássico do Azure, na página de diálogo **Configurar logon único na Área Restrita do Salesforce**, copie o valor de **URL de Logon Remoto** e cole-o na caixa de texto **URL de Logon do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="2317b-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="2317b-165">O SFDC não dá suporte a logout SAML.</span><span class="sxs-lookup"><span data-stu-id="2317b-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="2317b-166">Como alternativa, cole “https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0” na caixa de texto **URL de Logoff do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="2317b-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="2317b-167">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="2317b-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="2317b-168">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2317b-168">Click **Save**.</span></span>
11. <span data-ttu-id="2317b-169">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="2317b-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="2317b-170">![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="2317b-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="2317b-171">Habilitar seu domínio</span><span class="sxs-lookup"><span data-stu-id="2317b-171">Enable your domain</span></span>
<span data-ttu-id="2317b-172">Esta seção pressupõe que você já tenha criado um domínio.</span><span class="sxs-lookup"><span data-stu-id="2317b-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="2317b-173">Para obter mais detalhes, confira [Definindo seu nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="2317b-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="2317b-174">**Para habilitar seu domínio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2317b-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="2317b-175">No painel de navegação esquerdo, clique em **Gerenciamento de Domínio** e clique em **Meu Domínio.**</span><span class="sxs-lookup"><span data-stu-id="2317b-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="2317b-176">![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="2317b-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2317b-177">Verifique se o domínio foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2317b-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="2317b-178">Na seção **Configurações de Página de Logon**, clique em **Editar** e, para o **Serviço de Autenticação**, selecione o nome da Configuração de Logon Único SAML da seção anterior e, por fim, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2317b-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="2317b-179">![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="2317b-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="2317b-180">Assim que você tiver um domínio configurado, seus usuários deverão usar a URL do domínio para fazer logon na área restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="2317b-181">Para obter o valor da URL, clique no perfil SSO criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="2317b-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="2317b-182">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="2317b-182">Configure user provisioning</span></span>
<span data-ttu-id="2317b-183">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory na Área Restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="2317b-184">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2317b-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="2317b-185">No portal do Salesforce, na barra de navegação superior, selecione seu nome para expandir o seu menu de usuário:</span><span class="sxs-lookup"><span data-stu-id="2317b-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="2317b-186">![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Minhas configurações")</span><span class="sxs-lookup"><span data-stu-id="2317b-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="2317b-187">Do seu menu de usuário, selecione **Minhas Configurações** para abrir a página **Minhas Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2317b-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="2317b-188">No painel esquerdo, clique em **Pessoal** para expandir a seção Pessoal e clique em **Redefinir Meu Token de Segurança**:</span><span class="sxs-lookup"><span data-stu-id="2317b-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="2317b-189">![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Minhas configurações")</span><span class="sxs-lookup"><span data-stu-id="2317b-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="2317b-190">Na página **Redefinir meu Token de Segurança**, clique em **Redefinir Token de Segurança** para solicitar um email com seu token de segurança do Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="2317b-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="2317b-191">![Novo Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Novo token")</span><span class="sxs-lookup"><span data-stu-id="2317b-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="2317b-192">Marque a caixa de entrada de um email do Salesforce.com usando "**confirmação de segurança de salesforce.com.com**" como o assunto.</span><span class="sxs-lookup"><span data-stu-id="2317b-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="2317b-193">Leia o email e copie o valor do token de segurança.</span><span class="sxs-lookup"><span data-stu-id="2317b-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="2317b-194">No portal clássico do Azure, na página de integração do aplicativo **Área restrita do salesforce**, clique em **Configurar provisionamento do usuário** para abrir a caixa de diálogo **Configurar Provisionamento do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="2317b-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="2317b-195">![Configurar provisionamento do usuário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "configurar provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="2317b-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="2317b-196">Na página **Inserir suas credenciais da Área Restrita Salesforce para habilitar o provisionamento automático de usuários** , forneça as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="2317b-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="2317b-197">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="2317b-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="2317b-198">Na caixa de texto **Nome de Usuário Administrador da área restrita Salesforce**, digite o nome da conta de uma área restrita Salesforce com o perfil **Administrador de Sistema** do Salesforce.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="2317b-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="2317b-199">Na caixa de texto **Senha do Administrador da Área Restrita Salesforce** , digite a senha dessa conta.</span><span class="sxs-lookup"><span data-stu-id="2317b-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="2317b-200">Na caixa de texto **Token de Segurança do Usuário** , cole o valor do token de segurança.</span><span class="sxs-lookup"><span data-stu-id="2317b-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="2317b-201">Clique em **Validar** para verificar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="2317b-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="2317b-202">Clique no botão **Avançar** para abrir a página **Confirmação**.</span><span class="sxs-lookup"><span data-stu-id="2317b-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="2317b-203">Na página **Confirmação**, clique em **Concluir** para salvar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="2317b-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="2317b-204">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="2317b-204">Assigning users</span></span>

<span data-ttu-id="2317b-205">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2317b-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2317b-206">**Para atribuir usuários à Área Restrita Salesforce, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="2317b-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="2317b-207">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="2317b-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2317b-208">Na página de integração do aplicativo **Salesforce Sandbox**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="2317b-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2317b-209">![Atribuir usuários](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="2317b-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="2317b-210">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="2317b-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2317b-211">![Sim](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="2317b-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2317b-212">Agora você deve aguardar 10 minutos e verificar se a conta foi sincronizada com a Área Restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2317b-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="2317b-213">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2317b-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="2317b-214">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2317b-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

