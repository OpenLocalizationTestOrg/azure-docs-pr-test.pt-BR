---
title: "Tutorial: Integração do Azure Active Directory ao Central Desktop | Microsoft Docs"
description: "Saiba como toouse Central Desktop com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="05b13-103">Tutorial: Integração do Active Directory do Azure ao Central Desktop</span><span class="sxs-lookup"><span data-stu-id="05b13-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="05b13-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e área de trabalho Central.</span><span class="sxs-lookup"><span data-stu-id="05b13-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="05b13-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="05b13-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="05b13-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="05b13-106">A valid Azure subscription</span></span>
* <span data-ttu-id="05b13-107">Uma assinatura habilitada para logon único do Central Desktop/locatário do Central Desktop</span><span class="sxs-lookup"><span data-stu-id="05b13-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="05b13-108">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="05b13-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="05b13-109">Habilitando Olá integração de aplicativos de área de trabalho Central</span><span class="sxs-lookup"><span data-stu-id="05b13-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="05b13-110">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="05b13-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="05b13-111">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="05b13-111">Configuring user provisioning</span></span>
* <span data-ttu-id="05b13-112">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="05b13-112">Assigning users</span></span>

<span data-ttu-id="05b13-113">![Cenário](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="05b13-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="05b13-114">Habilitar a integração de aplicativo hello para área de trabalho Central</span><span class="sxs-lookup"><span data-stu-id="05b13-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="05b13-115">Olá objetivo desta seção é toooutline como tooenable Olá integração de área de trabalho Central.</span><span class="sxs-lookup"><span data-stu-id="05b13-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="05b13-116">**integração de aplicativos de saudação tooenable para área de trabalho Central, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05b13-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="05b13-117">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05b13-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="05b13-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="05b13-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="05b13-119">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="05b13-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="05b13-120">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="05b13-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="05b13-121">![Aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="05b13-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="05b13-122">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="05b13-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="05b13-123">![Adicionar aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="05b13-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="05b13-124">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="05b13-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="05b13-125">![Adicionar um aplicativo da galeria](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="05b13-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="05b13-126">Em Olá **caixa de pesquisa**, tipo **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="05b13-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="05b13-127">![Galeria de aplicativos](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galeria de aplicativos")</span><span class="sxs-lookup"><span data-stu-id="05b13-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="05b13-128">No painel de resultados de saudação, selecione **Central Desktop**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="05b13-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="05b13-129">![Área de Trabalho Central](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Área de Trabalho Central")</span><span class="sxs-lookup"><span data-stu-id="05b13-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="05b13-130">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="05b13-130">Configure single sign-on</span></span>

<span data-ttu-id="05b13-131">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooCentral área de trabalho com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="05b13-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="05b13-132">Como parte desse procedimento, será necessário tooupload um locatário de área de trabalho Central tooyour certificado codificado em base 64.</span><span class="sxs-lookup"><span data-stu-id="05b13-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="05b13-133">Se você não estiver familiarizado com esse procedimento, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="05b13-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="05b13-134">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05b13-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="05b13-135">Em Olá portal clássico do Azure, em Olá **Central Desktop** página de integração de aplicativos, clique em **configurar logon único** tooopen hello * * configurar logon único * * caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05b13-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="05b13-136">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="05b13-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="05b13-137">Em Olá **como você gostaria toosign usuários na área de trabalho de tooCentral** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="05b13-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="05b13-138">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="05b13-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="05b13-139">Em Olá **configurar URL do aplicativo** página executar Olá etapas a seguir e, em seguida, clique em **próximo**:</span><span class="sxs-lookup"><span data-stu-id="05b13-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="05b13-140">Em Olá **Central Desktop URL de entrada** caixa de texto, digite a URL do seu locatário Central Desktop saudação (por exemplo: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="05b13-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="05b13-141">Na caixa de texto de URL de resposta do Central Desktop hello, digite a URL de AssertionConsumerService de área de trabalho Central (por exemplo: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="05b13-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="05b13-142">Você pode obter o valor de saudação do hello metadados de área de trabalho central (por exemplo: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="05b13-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="05b13-143">![Configurar URL do Aplicativo](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="05b13-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="05b13-144">Em Olá **configurar logon único no Central Desktop** página, toodownload seu certificado, clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="05b13-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="05b13-145">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="05b13-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="05b13-146">Faça logon no tooyour **Central Desktop** locatário.</span><span class="sxs-lookup"><span data-stu-id="05b13-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="05b13-147">Vá muito**configurações**, clique em **avançado**e, em seguida, clique em **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="05b13-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="05b13-148">![Configuração – Avançada](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Configuração – Avançada")</span><span class="sxs-lookup"><span data-stu-id="05b13-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="05b13-149">Em Olá **logon único** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05b13-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="05b13-150">![Configurações de Logon Único](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="05b13-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="05b13-151">Selecione **Habilitar Logon Único do SAML v2**.</span><span class="sxs-lookup"><span data-stu-id="05b13-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="05b13-152">Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL do emissor** valor e, em seguida, cole-Olá **URL SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="05b13-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="05b13-153">Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL de logon remoto** valor e, em seguida, cole-o em Olá **URL de logon SSO**caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="05b13-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="05b13-154">Em Olá portal clássico do Azure, em Olá **configurar logon único no Central Desktop** página, Olá cópia **URL do serviço de logon único** valor e, em seguida, cole-Olá **URL de logoff SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="05b13-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="05b13-155">Em Olá **método de verificação de assinatura de mensagens** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05b13-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="05b13-156">![Método de Verificação de Assinatura da Mensagem](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Método de Verificação de Assinatura da Mensagem")</span><span class="sxs-lookup"><span data-stu-id="05b13-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="05b13-157">Selecione **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="05b13-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="05b13-158">De saudação **certificado SSO** lista, selecione **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="05b13-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="05b13-159">Criar um arquivo de texto do certificado Olá baixado, Olá de copiar conteúdo de arquivo de texto de saudação e, em seguida, cole-Olá **certificado SSO** campo.</span><span class="sxs-lookup"><span data-stu-id="05b13-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="05b13-160">Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="05b13-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="05b13-161">Selecione **exibir uma página de logon do link tooyour SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="05b13-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="05b13-162">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="05b13-162">Click **Update**.</span></span>
10. <span data-ttu-id="05b13-163">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05b13-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="05b13-164">![Configurar logon único](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="05b13-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="05b13-165">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="05b13-165">Configure user provisioning</span></span>

<span data-ttu-id="05b13-166">Para AAD usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo de área de trabalho Central.</span><span class="sxs-lookup"><span data-stu-id="05b13-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="05b13-167">Esta seção descreve como contas de usuário do AAD toocreate na área de trabalho Central.</span><span class="sxs-lookup"><span data-stu-id="05b13-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="05b13-168">**tooCentral de contas de usuário do tooprovision área de trabalho:**</span><span class="sxs-lookup"><span data-stu-id="05b13-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="05b13-169">Faça logon no tooyour locatário Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="05b13-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="05b13-170">Vá muito**pessoas \> membros internos**.</span><span class="sxs-lookup"><span data-stu-id="05b13-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="05b13-171">Clique em **Adicionar Membros Internos**.</span><span class="sxs-lookup"><span data-stu-id="05b13-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="05b13-172">![Pessoas](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="05b13-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="05b13-173">Em Olá **endereço de Email dos membros novos** caixa de texto, digite uma conta do AAD você deseja tooprovision e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="05b13-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="05b13-174">![Endereços de Email de Novos Membros](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Endereços de Email de Novos Membros")</span><span class="sxs-lookup"><span data-stu-id="05b13-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="05b13-175">Clique em **Adicionar Membro(s) interno(s)**.</span><span class="sxs-lookup"><span data-stu-id="05b13-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="05b13-176">![Adicionar Membro Interno](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Adicionar Membro Interno")</span><span class="sxs-lookup"><span data-stu-id="05b13-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="05b13-177">usuários de Olá que você adicionou receberão um email que inclui um link de confirmação que precisam de conta de saudação do tooclick tooactivate.</span><span class="sxs-lookup"><span data-stu-id="05b13-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="05b13-178">Você pode usar qualquer outra área de trabalho Central usuário conta ferramenta de criação ou APIs fornecidas pela área de trabalho Central tooprovision contas de usuário do AAD</span><span class="sxs-lookup"><span data-stu-id="05b13-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="05b13-179">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="05b13-179">Assign users</span></span>
<span data-ttu-id="05b13-180">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="05b13-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="05b13-181">**tooassign usuários tooCentral área de trabalho, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="05b13-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="05b13-182">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="05b13-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="05b13-183">Em Olá **Central Desktop** página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="05b13-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="05b13-184">![Atribuir usuários](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Atribuir usuários")</span><span class="sxs-lookup"><span data-stu-id="05b13-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="05b13-185">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="05b13-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="05b13-186">![Sim](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="05b13-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="05b13-187">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="05b13-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="05b13-188">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05b13-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

