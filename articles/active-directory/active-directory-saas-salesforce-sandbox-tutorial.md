---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como toouse área restrita do Salesforce com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!."
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
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="fcc98-103">Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce</span><span class="sxs-lookup"><span data-stu-id="fcc98-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="fcc98-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e a área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="fcc98-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="fcc98-105">Comentários, consulte Olá [página de suporte do Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="fcc98-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="fcc98-106">Forneça as áreas restritas Olá capacidade toocreate várias cópias de sua organização em ambientes separados para uma variedade de propósitos, como desenvolvimento, teste e treinamento, sem comprometer Olá dados e aplicativos em sua equipe de vendas de produção organização.</span><span class="sxs-lookup"><span data-stu-id="fcc98-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="fcc98-107">Para obter mais detalhes, confira [Visão geral da área restrita](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="fcc98-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="fcc98-108">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc98-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="fcc98-109">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="fcc98-109">A valid Azure subscription</span></span>
* <span data-ttu-id="fcc98-110">Uma área restrita no Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="fcc98-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="fcc98-111">Se você ainda não tem uma área restrita válida no Salesforce.com, será necessário toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="fcc98-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="fcc98-112">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc98-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="fcc98-113">Habilitando Olá integração de aplicativos de área restrita do Salesforce</span><span class="sxs-lookup"><span data-stu-id="fcc98-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="fcc98-114">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="fcc98-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="fcc98-115">Habilitando seu domínio</span><span class="sxs-lookup"><span data-stu-id="fcc98-115">Enabling your domain</span></span>
4. <span data-ttu-id="fcc98-116">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="fcc98-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="fcc98-117">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="fcc98-117">Assigning users</span></span>

<span data-ttu-id="fcc98-118">![Cenário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="fcc98-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="fcc98-119">Habilitar a integração de área restrita do Salesforce aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="fcc98-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="fcc98-120">Olá objetivo desta seção é toooutline como tooenable Olá integração de área restrita do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="fcc98-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="fcc98-121">**tooenable Olá integração de área restrita do Salesforce, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fcc98-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcc98-122">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="fcc98-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="fcc98-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="fcc98-124">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="fcc98-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="fcc98-125">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="fcc98-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="fcc98-126">![Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="fcc98-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="fcc98-127">Olá tooopen **Galeria de aplicativos**, clique em **adicionar um aplicativo**e, em seguida, clique em **adicionar um aplicativo para minha organização toouse**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="fcc98-128">![O que fazer você deseja toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "o que fazer você deseja toodo?")</span><span class="sxs-lookup"><span data-stu-id="fcc98-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="fcc98-129">Em Olá **caixa de pesquisa**, tipo **área restrita do Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="fcc98-130">![Galeria de Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="fcc98-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="fcc98-131">No painel de resultados de saudação, selecione **área restrita do Salesforce**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fcc98-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="fcc98-132">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="fcc98-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="fcc98-133">Configurar o SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="fcc98-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="fcc98-134">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSalesforce com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcc98-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="fcc98-135">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fcc98-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcc98-136">Em Olá portal clássico do Azure, em Olá **área restrita do Salesforce** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcc98-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="fcc98-137">![Configurar logon único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="fcc98-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="fcc98-138">Em Olá **como você gostaria toosign usuários em área restrita do tooSalesforce** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="fcc98-139">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="fcc98-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="fcc98-140">Em Olá **configurar URL do aplicativo** página Olá **URL de logon** caixa de texto, digite sua URL usando o saudação padrão a seguir `http://company.my.salesforce.com`e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="fcc98-141">![Configurar URL do Aplicativo](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="fcc98-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="fcc98-142">Se você já tiver configurado logon único para outra instância de área restrita do Salesforce em seu diretório, você também deve configurar Olá **identificador** toohave Olá mesmo valor Olá **URL de entrada**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="fcc98-143">Olá **identificador** campo pode ser encontrado verificando Olá **Mostrar configurações avançadas** caixa de seleção na Olá **configurar URL do aplicativo** página da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcc98-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="fcc98-144">Em Olá **configurar logon único no Salesforce Sandbox** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fcc98-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="fcc98-145">![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fcc98-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="fcc98-146">Em outra janela do navegador da Web, faça logon em sua área restrita Salesforce como um administrador.</span><span class="sxs-lookup"><span data-stu-id="fcc98-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="fcc98-147">No menu de saudação na parte superior de saudação, clique em **instalação**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="fcc98-148">![Configuração](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="fcc98-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="fcc98-149">No painel de navegação Olá Olá esquerda, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="fcc98-150">![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fcc98-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="fcc98-151">Na seção configurações de logon único do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc98-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="fcc98-152">![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fcc98-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="fcc98-153">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="fcc98-154">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-154">Click **New**.</span></span>
10. <span data-ttu-id="fcc98-155">Na seção configurações de logon único SAML do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc98-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="fcc98-156">![Configurações de Logon Único do SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="fcc98-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="fcc98-157">Na caixa de texto de nome hello, digite o nome de saudação da configuração de saudação (por exemplo: *SPSSOWAAD\_teste*).</span><span class="sxs-lookup"><span data-stu-id="fcc98-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="fcc98-158">Em Olá portal clássico do Azure, em Olá **configurar logon único no Salesforce Sandbox** página da caixa de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o em Olá **emissor**caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fcc98-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="fcc98-159">Em Olá **Id da entidade** caixa de texto, tipo **https://test.salesforce.com** se Olá primeira instância de área restrita do Salesforce que você está adicionando tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="fcc98-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="fcc98-160">Se você já tiver adicionado uma instância de área restrita do Salesforce, em seguida, para Olá **ID da entidade** tipo no hello **URL de logon**, que deveriam estar neste formato:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="fcc98-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="fcc98-161">Clique em **procurar** Olá tooupload baixado o certificado.</span><span class="sxs-lookup"><span data-stu-id="fcc98-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="fcc98-162">Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="fcc98-163">Como **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="fcc98-164">Em Olá portal clássico do Azure, em Olá **configurar logon único no Salesforce Sandbox** página da caixa de diálogo, Olá cópia **URL de logon remoto** valor e, em seguida, cole-o em Olá **provedor de identidade URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fcc98-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="fcc98-165">O SFDC não dá suporte a logout SAML.</span><span class="sxs-lookup"><span data-stu-id="fcc98-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="fcc98-166">Como alternativa, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'-o na Olá **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fcc98-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="fcc98-167">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="fcc98-168">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-168">Click **Save**.</span></span>
11. <span data-ttu-id="fcc98-169">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcc98-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="fcc98-170">![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fcc98-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="fcc98-171">Habilitar seu domínio</span><span class="sxs-lookup"><span data-stu-id="fcc98-171">Enable your domain</span></span>
<span data-ttu-id="fcc98-172">Esta seção pressupõe que você já tenha criado um domínio.</span><span class="sxs-lookup"><span data-stu-id="fcc98-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="fcc98-173">Para obter mais detalhes, confira [Definindo seu nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="fcc98-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="fcc98-174">**tooenable seu domínio, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fcc98-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcc98-175">No painel de navegação esquerdo hello, clique em **gerenciamento de domínio**e, em seguida, clique em **meu domínio.**</span><span class="sxs-lookup"><span data-stu-id="fcc98-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="fcc98-176">![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="fcc98-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="fcc98-177">Verifique se o domínio foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="fcc98-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="fcc98-178">Em Olá **configurações de página de logon** seção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome de saudação do hello configuração de logon único SAML de saudação anterior seção e, finalmente, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="fcc98-179">![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="fcc98-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="fcc98-180">Assim que você tiver um domínio configurado, seus usuários devem usar a área restrita do Salesforce Olá domínio URL toologin toohello.</span><span class="sxs-lookup"><span data-stu-id="fcc98-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="fcc98-181">valor tooget Olá Olá URL, clique em perfil Olá SSO que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="fcc98-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="fcc98-182">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="fcc98-182">Configure user provisioning</span></span>
<span data-ttu-id="fcc98-183">Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooSalesforce área restrita.</span><span class="sxs-lookup"><span data-stu-id="fcc98-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="fcc98-184">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fcc98-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcc98-185">No portal do Salesforce hello, na barra de navegação superior hello, selecione seu nome tooexpand seu menu de usuário:</span><span class="sxs-lookup"><span data-stu-id="fcc98-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="fcc98-186">![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Minhas configurações")</span><span class="sxs-lookup"><span data-stu-id="fcc98-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="fcc98-187">No seu menu de usuário, selecione **minhas configurações** tooopen sua **minhas configurações** página.</span><span class="sxs-lookup"><span data-stu-id="fcc98-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="fcc98-188">No painel esquerdo do hello, clique em **pessoal** tooexpand Olá seção pessoal e, em seguida, clique em **redefinir meu Token de segurança**:</span><span class="sxs-lookup"><span data-stu-id="fcc98-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="fcc98-189">![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Minhas configurações")</span><span class="sxs-lookup"><span data-stu-id="fcc98-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="fcc98-190">Em Olá **redefinir meu Token de segurança** , clique em **redefinir Token de segurança** toorequest um email que contém o token de segurança do Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="fcc98-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="fcc98-191">![Novo Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Novo token")</span><span class="sxs-lookup"><span data-stu-id="fcc98-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="fcc98-192">Marque a caixa de entrada de um email do Salesforce.com usando "**confirmação de segurança de salesforce.com.com**" como o assunto.</span><span class="sxs-lookup"><span data-stu-id="fcc98-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="fcc98-193">Revise este valor de token de segurança cópia e de email, para o hello.</span><span class="sxs-lookup"><span data-stu-id="fcc98-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="fcc98-194">Em Olá portal clássico do Azure, em Olá **área restrita do salesforce** página de integração de aplicativos, clique em **configurar provisionamento de usuário** tooopen Olá **configurar provisionamento do usuário**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fcc98-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="fcc98-195">![Configurar provisionamento do usuário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "configurar provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="fcc98-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="fcc98-196">Em Olá **Insira sua área restrita do Salesforce credenciais tooenable provisionamento automático de usuário** , forneça Olá definições de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcc98-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="fcc98-197">![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Área restrita do Salesforce")</span><span class="sxs-lookup"><span data-stu-id="fcc98-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="fcc98-198">Em Olá **nome de usuário de administrador de área restrita do Salesforce** caixa de texto, tipo de uma área restrita do Salesforce nome de conta que tem Olá **administrador do sistema** perfil em Salesforce.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="fcc98-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="fcc98-199">Em Olá **senha do administrador do Salesforce Sandbox** caixa de texto, digite a senha Olá para esta conta.</span><span class="sxs-lookup"><span data-stu-id="fcc98-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="fcc98-200">Em Olá **o Token de segurança do usuário** texto, o valor do token de segurança do hello colar.</span><span class="sxs-lookup"><span data-stu-id="fcc98-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="fcc98-201">Clique em **validar** tooverify sua configuração.</span><span class="sxs-lookup"><span data-stu-id="fcc98-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="fcc98-202">Clique em Olá **próximo** saudação do botão tooopen **confirmação** página.</span><span class="sxs-lookup"><span data-stu-id="fcc98-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="fcc98-203">Em Olá **confirmação** , clique em **concluir** toosave sua configuração.</span><span class="sxs-lookup"><span data-stu-id="fcc98-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="fcc98-204">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="fcc98-204">Assigning users</span></span>

<span data-ttu-id="fcc98-205">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="fcc98-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="fcc98-206">**tooassign usuários tooSalesforce área restrita, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fcc98-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="fcc98-207">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="fcc98-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="fcc98-208">Em hello * * área restrita do Salesforce * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="fcc98-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="fcc98-209">![Atribuir usuários](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="fcc98-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="fcc98-210">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="fcc98-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="fcc98-211">![Sim](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="fcc98-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="fcc98-212">Agora você deve aguardar 10 minutos e verificar se a conta Olá foi sincronizada tooSalesforce área restrita.</span><span class="sxs-lookup"><span data-stu-id="fcc98-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="fcc98-213">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fcc98-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="fcc98-214">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="fcc98-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

