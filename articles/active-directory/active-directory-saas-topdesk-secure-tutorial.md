---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Secure | Microsoft Docs"
description: "Saiba como usar o TOPdesk - Secure com o Active Directory do Azure para habilitar logon único, provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="b2211-103">Tutorial: Integração do Active Directory do Azure ao TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="b2211-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="b2211-104">O objetivo deste tutorial é mostrar a integração do Azure com o TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="b2211-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="b2211-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b2211-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b2211-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="b2211-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b2211-107">Uma assinatura habilitada para logon único do TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="b2211-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="b2211-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao TOPdesk - Secure poderão fazer logon único no aplicativo em seu site de empresa do TOPdesk - Secure (logon iniciado pelo provedor de serviços) ou usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2211-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="b2211-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b2211-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="b2211-110">Habilitando a integração de aplicativos com o TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="b2211-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="b2211-111">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="b2211-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="b2211-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="b2211-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="b2211-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="b2211-113">Assigning users</span></span>

<span data-ttu-id="b2211-114">![Cenário](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="b2211-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="b2211-115">Habilitando a integração de aplicativos com o TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="b2211-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="b2211-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos com o TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="b2211-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="b2211-117">Para habilitar a integração de aplicativos com o TOPdesk - Secure, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="b2211-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b2211-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="b2211-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b2211-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="b2211-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="b2211-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="b2211-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="b2211-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="b2211-122">![Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="b2211-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="b2211-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="b2211-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="b2211-124">![Adicionar aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="b2211-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="b2211-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="b2211-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="b2211-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="b2211-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="b2211-127">Na **caixa de pesquisa**, digite **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="b2211-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="b2211-128">![Galeria de Aplicativos](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="b2211-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="b2211-129">No painel de resultados, selecione **TOPdesk - Secure** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2211-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="b2211-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="b2211-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="b2211-131">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="b2211-131">Configuring single sign-on</span></span>
<span data-ttu-id="b2211-132">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no TOPdesk - Secure com sua conta do AD do Azure usando federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="b2211-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="b2211-133">Configurar o logon único para o TOPdesk - Secure requer que você carregue um arquivo de ícone de logotipo.</span><span class="sxs-lookup"><span data-stu-id="b2211-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="b2211-134">Para obter o arquivo do ícone, entre em contato com a equipe de suporte do TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="b2211-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="b2211-135">Para configurar o logon único, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="b2211-136">Faça logon em seu site de empresa do **TOPdesk - Secure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b2211-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="b2211-137">No menu **TOPdesk**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b2211-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="b2211-138">![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b2211-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="b2211-139">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="b2211-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="b2211-140">![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="b2211-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="b2211-141">Expanda o menu **Configurações de Logon** e clique em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="b2211-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="b2211-142">![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="b2211-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="b2211-143">Na seção **Seguro** da seção de configuração de **Logon do SAML**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="b2211-144">![Configurações técnicas](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configurações técnicas")</span><span class="sxs-lookup"><span data-stu-id="b2211-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="b2211-145">a.</span><span class="sxs-lookup"><span data-stu-id="b2211-145">a.</span></span> <span data-ttu-id="b2211-146">Clique em **Baixar** para baixar o arquivo de metadados públicos e salve-o localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="b2211-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="b2211-147">b.</span><span class="sxs-lookup"><span data-stu-id="b2211-147">b.</span></span> <span data-ttu-id="b2211-148">Abra o arquivo de metadados e localize o nó **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="b2211-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="b2211-149">![Serviço de Declaração do Consumidor](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Serviço de Declaração do Consumidor")</span><span class="sxs-lookup"><span data-stu-id="b2211-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="b2211-150">c.</span><span class="sxs-lookup"><span data-stu-id="b2211-150">c.</span></span> <span data-ttu-id="b2211-151">Copie o valor de **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="b2211-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="b2211-152">Você precisará do valor na seção **Configurar URL do Aplicativo** mais adiante neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b2211-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="b2211-153">Em outra janela do navegador da Web, faça logon no **portal clássico do Azure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b2211-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="b2211-154">No **TOPdesk - seguro** página de integração de aplicativos, clique em **configurar logon único** para abrir o * * configurar logon único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2211-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="b2211-155">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b2211-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="b2211-156">Na página **Como você deseja que os usuários façam logon no TOPdesk - Secure**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b2211-157">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b2211-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="b2211-158">Na página **Configurar URL do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="b2211-159">![Configurar URL do Aplicativo](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="b2211-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="b2211-160">a.</span><span class="sxs-lookup"><span data-stu-id="b2211-160">a.</span></span> <span data-ttu-id="b2211-161">Na caixa de texto **URL de Logon do TOPdesk - Secure**, digite a URL usada pelos usuários para entrar no aplicativo TOPdesk - Secure (por exemplo, "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="b2211-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="b2211-162">b.</span><span class="sxs-lookup"><span data-stu-id="b2211-162">b.</span></span> <span data-ttu-id="b2211-163">Na caixa de texto **TOPdesk – URL de Resposta Pública**, cole **TOPdesk - URL AssertionConsumerService Protegida** (por exemplo, "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="b2211-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="b2211-164">c.</span><span class="sxs-lookup"><span data-stu-id="b2211-164">c.</span></span> <span data-ttu-id="b2211-165">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-165">Click **Next**.</span></span>

10. <span data-ttu-id="b2211-166">Na página **Configurar logon único no TOPdesk - Secure**, para baixar o arquivo de metadados, clique em **Baixar metadados** e salve o arquivo localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="b2211-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="b2211-167">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b2211-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="b2211-168">Execute as seguintes etapas para criar um arquivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="b2211-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="b2211-169">![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="b2211-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="b2211-170">a.</span><span class="sxs-lookup"><span data-stu-id="b2211-170">a.</span></span> <span data-ttu-id="b2211-171">Abra o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="b2211-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="b2211-172">b.</span><span class="sxs-lookup"><span data-stu-id="b2211-172">b.</span></span> <span data-ttu-id="b2211-173">Expanda o nó **RoleDescriptor** que contém um **xsi:type** de **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="b2211-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="b2211-174">c.</span><span class="sxs-lookup"><span data-stu-id="b2211-174">c.</span></span> <span data-ttu-id="b2211-175">Copie o valor do nó **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="b2211-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="b2211-176">d.</span><span class="sxs-lookup"><span data-stu-id="b2211-176">d.</span></span> <span data-ttu-id="b2211-177">Salve o valor copiado de **X509Certificate** localmente no computador em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="b2211-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="b2211-178">Em seu site de empresa do TOPdesk - Secure, no menu **TOPdesk**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b2211-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="b2211-179">![Configurações](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="b2211-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="b2211-180">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="b2211-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="b2211-181">![Configurações de logon](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="b2211-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="b2211-182">Expanda o menu **Configurações de Logon** e clique em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="b2211-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="b2211-183">![Geral](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="b2211-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="b2211-184">Na seção **Público**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="b2211-185">![Adicionar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="b2211-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="b2211-186">Na página do diálogo **Assistente de configuração do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="b2211-187">![Assistente de configuração SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistente de configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="b2211-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="b2211-188">a.</span><span class="sxs-lookup"><span data-stu-id="b2211-188">a.</span></span> <span data-ttu-id="b2211-189">Para carregar o arquivo de metadados baixado, em **Metadados de Federação**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="b2211-190">b.</span><span class="sxs-lookup"><span data-stu-id="b2211-190">b.</span></span> <span data-ttu-id="b2211-191">Para carregar o arquivo de certificado, em **Certificado (RSA)**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="b2211-192">c.</span><span class="sxs-lookup"><span data-stu-id="b2211-192">c.</span></span> <span data-ttu-id="b2211-193">Para carregar o arquivo de logotipo que você recebeu da equipe de suporte do TOPdesk, em **Ícone do logotipo**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="b2211-194">d.</span><span class="sxs-lookup"><span data-stu-id="b2211-194">d.</span></span> <span data-ttu-id="b2211-195">Na caixa de texto **Atributo de nome de usuário**, digite **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="b2211-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="b2211-196">e.</span><span class="sxs-lookup"><span data-stu-id="b2211-196">e.</span></span> <span data-ttu-id="b2211-197">Na caixa de texto **Nome de exibição** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="b2211-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="b2211-198">f.</span><span class="sxs-lookup"><span data-stu-id="b2211-198">f.</span></span> <span data-ttu-id="b2211-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-199">Click **Save**.</span></span>

17. <span data-ttu-id="b2211-200">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="b2211-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="b2211-201">![Configurar Logon Único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b2211-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="b2211-202">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="b2211-202">Configuring user provisioning</span></span>
<span data-ttu-id="b2211-203">Para permitir que os usuários do AD do Azure façam logon no TOPdesk - Secure, eles deverão ser provisionados no TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="b2211-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="b2211-204">No caso do TOPdesk - Secure, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b2211-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b2211-205">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="b2211-206">Faça logon em seu site de empresa do **TOPdesk - Secure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="b2211-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="b2211-207">No menu na parte superior, clique em **TOPdesk \> Novo \> Arquivos de Suporte \> Operador**.</span><span class="sxs-lookup"><span data-stu-id="b2211-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="b2211-208">![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")</span><span class="sxs-lookup"><span data-stu-id="b2211-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="b2211-209">No diálogo **Novo Operador** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b2211-210">![Novo operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Novo operador")</span><span class="sxs-lookup"><span data-stu-id="b2211-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="b2211-211">a.</span><span class="sxs-lookup"><span data-stu-id="b2211-211">a.</span></span> <span data-ttu-id="b2211-212">Clique na guia Geral.</span><span class="sxs-lookup"><span data-stu-id="b2211-212">Click the General tab.</span></span>
   
    <span data-ttu-id="b2211-213">b.</span><span class="sxs-lookup"><span data-stu-id="b2211-213">b.</span></span> <span data-ttu-id="b2211-214">Na caixa de texto **Sobrenome** na seção **Geral**, digite o sobrenome referente a uma conta válida do Azure Active Directory que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="b2211-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="b2211-215">c.</span><span class="sxs-lookup"><span data-stu-id="b2211-215">c.</span></span> <span data-ttu-id="b2211-216">Selecione um **Site** para a conta na seção **Local**.</span><span class="sxs-lookup"><span data-stu-id="b2211-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="b2211-217">d.</span><span class="sxs-lookup"><span data-stu-id="b2211-217">d.</span></span> <span data-ttu-id="b2211-218">Na caixa de texto **Nome de Logon** da seção **Logon no TOPdesk**, digite um nome de logon para o usuário.</span><span class="sxs-lookup"><span data-stu-id="b2211-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="b2211-219">e.</span><span class="sxs-lookup"><span data-stu-id="b2211-219">e.</span></span> <span data-ttu-id="b2211-220">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b2211-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="b2211-221">É possível usar qualquer outra ferramenta de criação da conta de usuário do TOPdesk - Secure ou APIs fornecidas pelo TOPdesk - Secure para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="b2211-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="b2211-222">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="b2211-222">Assigning users</span></span>
<span data-ttu-id="b2211-223">Para testar sua configuração, é necessário conceder aos usuários do AD do Azure que você deseja que usem seu aplicativo acesso a ele.</span><span class="sxs-lookup"><span data-stu-id="b2211-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="b2211-224">Para atribuir usuários ao TOPdesk - Secure, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b2211-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="b2211-225">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b2211-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="b2211-226">Sobre o * * TOPdesk - seguro * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="b2211-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="b2211-227">![Atribuir Usuários](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="b2211-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="b2211-228">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="b2211-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="b2211-229">![Sim](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="b2211-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b2211-230">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b2211-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b2211-231">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b2211-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

