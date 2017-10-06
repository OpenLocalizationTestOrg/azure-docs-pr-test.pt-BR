---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Secure | Microsoft Docs"
description: "Saiba como toouse TOPdesk - seguro com o Active Directory do Azure tooenable-logon único, o provisionamento automatizado e muito mais!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="48731-103">Tutorial: Integração do Active Directory do Azure ao TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="48731-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="48731-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e TOPdesk - seguro.</span><span class="sxs-lookup"><span data-stu-id="48731-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="48731-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="48731-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="48731-106">A valid Azure subscription</span></span>
* <span data-ttu-id="48731-107">Uma assinatura habilitada para logon único do TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="48731-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="48731-108">Depois de concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooTOPdesk - será seguro seja capaz de toosingle o logon no aplicativo hello no TOPdesk - seguro site da empresa (serviço iniciado pelo provedor logon) ou usando Olá [Introdução Painel de acesso de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48731-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="48731-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="48731-110">Habilitando Olá integração de aplicativos para TOPdesk - seguro</span><span class="sxs-lookup"><span data-stu-id="48731-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="48731-111">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="48731-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="48731-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="48731-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="48731-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="48731-113">Assigning users</span></span>

<span data-ttu-id="48731-114">![Cenário](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="48731-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="48731-115">Habilitando Olá integração de aplicativos para TOPdesk - seguro</span><span class="sxs-lookup"><span data-stu-id="48731-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="48731-116">Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para TOPdesk - seguro.</span><span class="sxs-lookup"><span data-stu-id="48731-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="48731-117">integração do aplicativo hello tooenable para TOPdesk - seguro, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="48731-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48731-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="48731-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="48731-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="48731-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="48731-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="48731-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="48731-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="48731-122">![Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="48731-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="48731-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="48731-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="48731-124">![Adicionar aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="48731-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="48731-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="48731-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="48731-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="48731-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="48731-127">Em Olá **caixa de pesquisa**, tipo **TOPdesk - seguro**.</span><span class="sxs-lookup"><span data-stu-id="48731-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="48731-128">![Galeria de Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="48731-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="48731-129">No painel de resultados de saudação, selecione **TOPdesk - seguro**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="48731-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="48731-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="48731-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="48731-131">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="48731-131">Configuring single sign-on</span></span>
<span data-ttu-id="48731-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooTOPdesk - seguro com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="48731-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="48731-133">Configurar logon único para TOPdesk - seguro requer que você tooupload um arquivo de ícone do logotipo.</span><span class="sxs-lookup"><span data-stu-id="48731-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="48731-134">arquivo de ícone tooget Olá, equipe de suporte do TOPdesk Olá contato.</span><span class="sxs-lookup"><span data-stu-id="48731-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="48731-135">tooconfigure o logon único, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="48731-136">Logon tooyour **TOPdesk - seguro** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="48731-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="48731-137">Em Olá **TOPdesk** menu, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="48731-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="48731-138">![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="48731-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="48731-139">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="48731-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="48731-140">![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="48731-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="48731-141">Expanda Olá **configurações de logon** menu e clique **geral**.</span><span class="sxs-lookup"><span data-stu-id="48731-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="48731-142">![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="48731-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="48731-143">Em Olá **seguro** seção Olá **logon SAML** configuração, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="48731-144">![Configurações técnicas](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configurações técnicas")</span><span class="sxs-lookup"><span data-stu-id="48731-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="48731-145">a.</span><span class="sxs-lookup"><span data-stu-id="48731-145">a.</span></span> <span data-ttu-id="48731-146">Clique em **baixar** toodownload Olá arquivo de metadados público e, em seguida, salve-o localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="48731-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="48731-147">b.</span><span class="sxs-lookup"><span data-stu-id="48731-147">b.</span></span> <span data-ttu-id="48731-148">Abra o arquivo de metadados hello e localize Olá **AssertionConsumerService** nó.</span><span class="sxs-lookup"><span data-stu-id="48731-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="48731-149">![Serviço de Declaração do Consumidor](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Serviço de Declaração do Consumidor")</span><span class="sxs-lookup"><span data-stu-id="48731-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="48731-150">c.</span><span class="sxs-lookup"><span data-stu-id="48731-150">c.</span></span> <span data-ttu-id="48731-151">Saudação de cópia **AssertionConsumerService** valor.</span><span class="sxs-lookup"><span data-stu-id="48731-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="48731-152">Será necessário Olá o valor em Olá **configurar URL do aplicativo** seção mais adiante neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="48731-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="48731-153">Em outra janela do navegador da Web, faça logon no **portal clássico do Azure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="48731-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="48731-154">Em Olá **TOPdesk - seguro** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48731-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="48731-155">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="48731-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="48731-156">Em Olá **como seria como usuários toosign em tooTOPdesk - Secure** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="48731-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="48731-157">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="48731-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="48731-158">Em Olá **configurar URL do aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="48731-159">![Configurar URL do Aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="48731-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="48731-160">a.</span><span class="sxs-lookup"><span data-stu-id="48731-160">a.</span></span> <span data-ttu-id="48731-161">Em Olá **TOPdesk - seguro URL de logon** caixa de texto, digite a URL Olá usada por seu usuários toosign em TOPdesk - seguro aplicativo (por exemplo: "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="48731-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="48731-162">b.</span><span class="sxs-lookup"><span data-stu-id="48731-162">b.</span></span> <span data-ttu-id="48731-163">Em hello **TOPdesk – URL de resposta pública** textbox, colar Olá **TOPdesk - seguro URL de AssertionConsumerService** (por exemplo: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="48731-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="48731-164">c.</span><span class="sxs-lookup"><span data-stu-id="48731-164">c.</span></span> <span data-ttu-id="48731-165">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="48731-165">Click **Next**.</span></span>

10. <span data-ttu-id="48731-166">Em Olá **configurar logon único no TOPdesk - seguro** página, toodownload o arquivo de metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="48731-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="48731-167">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="48731-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="48731-168">toocreate um arquivo de certificado, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="48731-169">![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="48731-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="48731-170">a.</span><span class="sxs-lookup"><span data-stu-id="48731-170">a.</span></span> <span data-ttu-id="48731-171">Arquivo de metadados baixado Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="48731-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="48731-172">b.</span><span class="sxs-lookup"><span data-stu-id="48731-172">b.</span></span> <span data-ttu-id="48731-173">Expanda Olá **RoleDescriptor** nó que possui um **xsi: Type** de **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="48731-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="48731-174">c.</span><span class="sxs-lookup"><span data-stu-id="48731-174">c.</span></span> <span data-ttu-id="48731-175">Copie o valor Olá Olá **X509Certificate** nó.</span><span class="sxs-lookup"><span data-stu-id="48731-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="48731-176">d.</span><span class="sxs-lookup"><span data-stu-id="48731-176">d.</span></span> <span data-ttu-id="48731-177">Salvar Olá copiado **X509Certificate** valor localmente no seu computador em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="48731-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="48731-178">No TOPdesk - proteger o site da empresa, em Olá **TOPdesk** menu, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="48731-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="48731-179">![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="48731-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="48731-180">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="48731-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="48731-181">![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="48731-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="48731-182">Expanda Olá **configurações de logon** menu e clique **geral**.</span><span class="sxs-lookup"><span data-stu-id="48731-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="48731-183">![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="48731-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="48731-184">Em Olá **pública** seção, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="48731-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="48731-185">![Adicionar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="48731-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="48731-186">Em Olá **Assistente de configuração SAML** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="48731-187">![Assistente de configuração SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistente de configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="48731-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="48731-188">a.</span><span class="sxs-lookup"><span data-stu-id="48731-188">a.</span></span> <span data-ttu-id="48731-189">tooupload arquivo seus metadados baixado, em **metadados de Federação**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="48731-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="48731-190">b.</span><span class="sxs-lookup"><span data-stu-id="48731-190">b.</span></span> <span data-ttu-id="48731-191">tooupload arquivo seu certificado, em **certificado (RSA)**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="48731-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="48731-192">c.</span><span class="sxs-lookup"><span data-stu-id="48731-192">c.</span></span> <span data-ttu-id="48731-193">arquivo de logotipo Olá tooupload você obteve da equipe de suporte do TOPdesk hello, em **ícone do logotipo**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="48731-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="48731-194">d.</span><span class="sxs-lookup"><span data-stu-id="48731-194">d.</span></span> <span data-ttu-id="48731-195">Em Olá **atributo de nome de usuário** caixa de texto, tipo **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="48731-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="48731-196">e.</span><span class="sxs-lookup"><span data-stu-id="48731-196">e.</span></span> <span data-ttu-id="48731-197">Em Olá **nome de exibição** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="48731-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="48731-198">f.</span><span class="sxs-lookup"><span data-stu-id="48731-198">f.</span></span> <span data-ttu-id="48731-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48731-199">Click **Save**.</span></span>

17. <span data-ttu-id="48731-200">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48731-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="48731-201">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="48731-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="48731-202">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="48731-202">Configuring user provisioning</span></span>
<span data-ttu-id="48731-203">Em ordem toolog de usuários tooenable AD do Azure no TOPdesk - seguro, eles devem ser provisionados no TOPdesk - seguro.</span><span class="sxs-lookup"><span data-stu-id="48731-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="48731-204">No caso de saudação do TOPdesk - seguro, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="48731-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="48731-205">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="48731-206">Logon tooyour **TOPdesk - seguro** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="48731-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="48731-207">No menu de saudação na parte superior de saudação, clique em **TOPdesk \> novo \> arquivos de suporte \> operador**.</span><span class="sxs-lookup"><span data-stu-id="48731-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="48731-208">![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")</span><span class="sxs-lookup"><span data-stu-id="48731-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="48731-209">Em Olá **novo operador** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="48731-210">![Novo operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Novo operador")</span><span class="sxs-lookup"><span data-stu-id="48731-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="48731-211">a.</span><span class="sxs-lookup"><span data-stu-id="48731-211">a.</span></span> <span data-ttu-id="48731-212">Clique em guia Geral hello.</span><span class="sxs-lookup"><span data-stu-id="48731-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="48731-213">b.</span><span class="sxs-lookup"><span data-stu-id="48731-213">b.</span></span> <span data-ttu-id="48731-214">Em Olá **Sobrenome** caixa de texto de saudação **geral** seção, digite Olá sobrenome de uma conta válida do Active Directory do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="48731-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="48731-215">c.</span><span class="sxs-lookup"><span data-stu-id="48731-215">c.</span></span> <span data-ttu-id="48731-216">Selecione um **Site** para conta Olá Olá **local** seção.</span><span class="sxs-lookup"><span data-stu-id="48731-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="48731-217">d.</span><span class="sxs-lookup"><span data-stu-id="48731-217">d.</span></span> <span data-ttu-id="48731-218">Em Olá **nome de logon** caixa de texto de saudação **logon do TOPdesk** seção, digite um nome de logon para o usuário.</span><span class="sxs-lookup"><span data-stu-id="48731-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="48731-219">e.</span><span class="sxs-lookup"><span data-stu-id="48731-219">e.</span></span> <span data-ttu-id="48731-220">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48731-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="48731-221">Você pode usar qualquer outra TOPdesk - conta de usuário segura ferramentas de criação ou APIs fornecidas pelo TOPdesk - seguro tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="48731-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="48731-222">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="48731-222">Assigning users</span></span>
<span data-ttu-id="48731-223">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="48731-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="48731-224">tooassign usuários tooTOPdesk - seguro, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48731-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="48731-225">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="48731-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="48731-226">Em hello * * TOPdesk - seguro * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="48731-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="48731-227">![Atribuir Usuários](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="48731-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="48731-228">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="48731-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="48731-229">![Sim](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="48731-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="48731-230">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="48731-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="48731-231">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48731-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

