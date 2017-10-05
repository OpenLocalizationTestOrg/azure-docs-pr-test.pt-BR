---
title: "Tutorial: Integração do Azure Active Directory ao Central Desktop | Microsoft Docs"
description: "Saiba como usar o Central Desktop com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="ba4a0-103">Tutorial: Integração do Active Directory do Azure ao Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ba4a0-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="ba4a0-104">O objetivo deste tutorial é mostrar a integração do Azure ao Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="ba4a0-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ba4a0-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ba4a0-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="ba4a0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ba4a0-107">Uma assinatura habilitada para logon único do Central Desktop/locatário do Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ba4a0-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="ba4a0-108">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ba4a0-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="ba4a0-109">Habilitando a integração de aplicativos para o Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ba4a0-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="ba4a0-110">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="ba4a0-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="ba4a0-111">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="ba4a0-111">Configuring user provisioning</span></span>
* <span data-ttu-id="ba4a0-112">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="ba4a0-112">Assigning users</span></span>

<span data-ttu-id="ba4a0-113">![Cenário](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="ba4a0-114">Habilitar a integração de aplicativos para o Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ba4a0-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="ba4a0-115">O objetivo desta seção é descrever como habilitar a integração de aplicativos para o Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="ba4a0-116">**Para habilitar a integração de aplicativos para o Central Desktop, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba4a0-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a0-117">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ba4a0-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ba4a0-119">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ba4a0-120">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ba4a0-121">![Aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ba4a0-122">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ba4a0-123">![Adicionar aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ba4a0-124">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ba4a0-125">![Adicionar um aplicativo da galeria](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ba4a0-126">Na **caixa de pesquisa**, digite **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="ba4a0-127">![Galeria de aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galeria de aplicativos")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="ba4a0-128">No painel de resultados, selecione **Central Desktop** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ba4a0-129">![Área de Trabalho Central](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Área de Trabalho Central")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ba4a0-130">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="ba4a0-130">Configure single sign-on</span></span>

<span data-ttu-id="ba4a0-131">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Central Desktop com a respectiva conta do AD do Azure usando federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ba4a0-132">Como parte deste procedimento, é necessário carregar um certificado codificado em base 64 no locatário do Desktop Central.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="ba4a0-133">Se você não estiver familiarizado com este procedimento, consulte [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="ba4a0-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="ba4a0-134">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba4a0-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a0-135">No portal clássico do Azure, no **Central Desktop** página de integração de aplicativos, clique em **configurar logon único** para abrir o * * configurar logon único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="ba4a0-136">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ba4a0-137">Na página **Como você deseja que os usuários façam logon no Central Desktop**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ba4a0-138">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="ba4a0-139">Na página **Configurar URL do Aplicativo**, realize as etapas a seguir e clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="ba4a0-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="ba4a0-140">Na caixa de texto **URL de Logon do Central Desktop**, digite a URL do seu locatário do Central Desktop (por exemplo: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="ba4a0-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="ba4a0-141">Na caixa de texto URL de Resposta do Central Desktop, digite a URL AssertionConsumerService do Central Desktop (por exemplo:  https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="ba4a0-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ba4a0-142">Você pode obter o valor nos metadados do Central Desktop (por exemplo: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="ba4a0-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="ba4a0-143">![Configurar URL do Aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="ba4a0-144">Na página **Configurar logon único no Central Desktop**, para baixar seu certificado, clique em **Baixar certificado** e salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="ba4a0-145">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="ba4a0-146">Faça logon em seu locatário do **Central Desktop** .</span><span class="sxs-lookup"><span data-stu-id="ba4a0-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="ba4a0-147">Vá para **Configurações**, clique em **Avançadas** e em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="ba4a0-148">![Configuração – Avançada](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Configuração – Avançada")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="ba4a0-149">Na página **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba4a0-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="ba4a0-150">![Configurações de Logon Único](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="ba4a0-151">Selecione **Habilitar Logon Único do SAML v2**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="ba4a0-152">No portal clássico do Azure, na página **Configurar logon único no Central Desktop**, copie o valor da **URL do Emissor** e cole-o na caixa de texto **URL de SSO**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="ba4a0-153">No portal clássico do Azure, na página **Configurar logon único no Central Desktop**, copie o valor da **URL de Logon Remoto** e cole-o na caixa de texto **URL de SSO**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="ba4a0-154">No portal clássico do Azure, na página **Configurar logon único no Central Desktop**, copie o valor da **URL do Serviço de Saída Única** e cole-o na caixa de texto **URL de Logout de SSO**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="ba4a0-155">Na seção **Método de Verificação de Assinatura de Mensagem** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ba4a0-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ba4a0-156">![Método de Verificação de Assinatura da Mensagem](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de Verificação de Assinatura da Mensagem")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="ba4a0-157">Selecione **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="ba4a0-158">Na lista **Certificado de SSO**, selecione **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="ba4a0-159">Crie um arquivo de texto por meio do certificado baixado, copie o conteúdo do arquivo de texto e cole-o no campo **Certificado de SSO** .</span><span class="sxs-lookup"><span data-stu-id="ba4a0-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="ba4a0-160">Para obter mais detalhes, veja [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ba4a0-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="ba4a0-161">Selecione **Exibir um link para a sua página de logon do SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="ba4a0-162">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-162">Click **Update**.</span></span>
10. <span data-ttu-id="ba4a0-163">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="ba4a0-164">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="ba4a0-165">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="ba4a0-165">Configure user provisioning</span></span>

<span data-ttu-id="ba4a0-166">Para que os usuários do AAD possam fazer logon, eles devem ser provisionados no aplicativo Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="ba4a0-167">Esta seção descreve como criar contas de usuário do AAD no Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="ba4a0-168">**Para provisionar contas de usuário no Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="ba4a0-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="ba4a0-169">Faça logon no seu locatário do Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="ba4a0-170">Vá para **Pessoas \> Membros Internos**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="ba4a0-171">Clique em **Adicionar Membros Internos**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="ba4a0-172">![Pessoas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="ba4a0-173">Na caixa de texto **Endereço de Email dos Novos Membros**, digite uma conta do AAD que você deseja provisionar e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="ba4a0-174">![Endereços de Email de Novos Membros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Endereços de Email de Novos Membros")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="ba4a0-175">Clique em **Adicionar Membro(s) interno(s)**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="ba4a0-176">![Adicionar Membro Interno](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Adicionar Membro Interno")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ba4a0-177">Os usuários que você adicionou receberão um email com um link de confirmação em que eles precisam clicar para ativar a conta.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="ba4a0-178">É possível usar qualquer outra ferramenta de criação da conta de usuário do Central Desktop ou as APIs fornecidas pelo Central Desktop para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="ba4a0-179">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="ba4a0-179">Assign users</span></span>
<span data-ttu-id="ba4a0-180">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ba4a0-181">**Para atribuir usuários ao Central Desktop, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ba4a0-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="ba4a0-182">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ba4a0-183">Na página de integração de aplicativos do **Central Desktop**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ba4a0-184">![Atribuir usuários](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="ba4a0-185">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ba4a0-186">![Sim](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="ba4a0-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ba4a0-187">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ba4a0-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ba4a0-188">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba4a0-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

