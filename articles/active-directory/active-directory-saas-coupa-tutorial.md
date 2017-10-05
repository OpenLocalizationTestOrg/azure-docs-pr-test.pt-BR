---
title: "Tutorial: integração do Azure Active Directory ao Coupa | Microsoft Docs"
description: "Saiba como usar o Coupa com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="e6fcd-103">Tutorial: integração do Active Directory do Azure ao Coupa</span><span class="sxs-lookup"><span data-stu-id="e6fcd-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="e6fcd-104">O objetivo deste tutorial é mostrar a integração do Azure ao Coupa.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="e6fcd-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e6fcd-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="e6fcd-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="e6fcd-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e6fcd-107">Uma assinatura habilitada para SSO (logon único) do Coupa</span><span class="sxs-lookup"><span data-stu-id="e6fcd-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e6fcd-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao Coupa poderão fazer logon único no aplicativo usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e6fcd-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e6fcd-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e6fcd-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="e6fcd-110">Habilitando a integração de aplicativos para Coupa</span><span class="sxs-lookup"><span data-stu-id="e6fcd-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="e6fcd-111">Configurando o logon único</span><span class="sxs-lookup"><span data-stu-id="e6fcd-111">Configuring single sign-on</span></span>
* <span data-ttu-id="e6fcd-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="e6fcd-112">Configuring user provisioning</span></span>
* <span data-ttu-id="e6fcd-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="e6fcd-113">Assigning users</span></span>

<span data-ttu-id="e6fcd-114">![Cenário](./media/active-directory-saas-coupa-tutorial/IC791897.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="e6fcd-115">Habilitar a integração de aplicativos para Coupa</span><span class="sxs-lookup"><span data-stu-id="e6fcd-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="e6fcd-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos para o Coupa.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="e6fcd-117">**Para habilitar a integração de aplicativos para o Coupa, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e6fcd-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="e6fcd-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="e6fcd-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e6fcd-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e6fcd-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="e6fcd-122">![Aplicativos](./media/active-directory-saas-coupa-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e6fcd-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="e6fcd-124">![Adicionar aplicativo](./media/active-directory-saas-coupa-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e6fcd-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="e6fcd-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-coupa-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e6fcd-127">Na **caixa de pesquisa**, digite **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="e6fcd-128">![Galeria de Aplicativos](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="e6fcd-129">No painel de resultados, selecione **Coupa** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="e6fcd-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e6fcd-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="e6fcd-131">Configure single sign-on</span></span>

<span data-ttu-id="e6fcd-132">O objetivo desta seção é descrever como permitir que os usuários autentiquem no Coupa com a própria conta no Azure AD usando federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="e6fcd-133">Configurar o logon único para o Coupa exige que você recupere um valor de impressão digital de um certificado.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="e6fcd-134">Se você não estiver familiarizado com este procedimento, consulte [Como recuperar o valor de impressão digital do certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="e6fcd-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="e6fcd-135">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e6fcd-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="e6fcd-136">Faça logon em seu site de empresa do Coupa como administrador.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="e6fcd-137">Vá para **Configuração \> Controle de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="e6fcd-138">![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="e6fcd-139">Para baixar o arquivo de metadados do Coupa no computador, clique em **Baixar e importar metadados do SP**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="e6fcd-140">![Metadados SP do Coupa](./media/active-directory-saas-coupa-tutorial/IC791901.png "Metadados SP do Coupa")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="e6fcd-141">Em uma janela de navegador diferente, faça logon no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="e6fcd-142">Na página de integração do aplicativo **Coupa**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="e6fcd-143">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="e6fcd-144">Na página **Como você deseja que os usuários façam logon no Coupa**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="e6fcd-145">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="e6fcd-146">Na página **Configurar URL do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e6fcd-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="e6fcd-147">![Configurar URL do Aplicativo](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="e6fcd-148">Na caixa de texto **URL de Logon**, digite a URL usada pelos usuários para fazer logon no seu aplicativo Coupa (por exemplo: “*http://company.Coupa.com*”).</span><span class="sxs-lookup"><span data-stu-id="e6fcd-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="e6fcd-149">Abra o arquivo de metadados do Coupa baixado e copie o **Índice/URL de AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="e6fcd-150">Na caixa de texto **URL de Resposta do Coupa**, cole o valor de **Índice/URL de AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="e6fcd-151">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-151">Click **Next**.</span></span>
8. <span data-ttu-id="e6fcd-152">Na página **Configurar logon único no Coupa**, para baixar seu arquivo de metadados, clique em **Baixar metadados** e salve o arquivo localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="e6fcd-153">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="e6fcd-154">No site de empresa do Coupa, vá para **Configuração\> Controle de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="e6fcd-155">![Controles de Segurança](./media/active-directory-saas-coupa-tutorial/IC791900.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="e6fcd-156">Na seção **Fazer Logon usando as credenciais do Coupa** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e6fcd-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="e6fcd-157">![Logon usando as credenciais do Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Logon usando as credenciais do Coupa")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="e6fcd-158">Selecione **Fazer logon usando o SAML**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="e6fcd-159">Clique em **Procurar** para carregar seu arquivo de metadados baixado do Active do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="e6fcd-160">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-160">Click **Save**.</span></span>
11. <span data-ttu-id="e6fcd-161">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="e6fcd-162">![Configurar Logon Único](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="e6fcd-163">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="e6fcd-163">Configure user provisioning</span></span>

<span data-ttu-id="e6fcd-164">Para permitir que os usuários do Azure AD façam logon no Coupa, eles devem ser provisionados no Coupa.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="e6fcd-165">No caso do Coupa, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="e6fcd-166">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e6fcd-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e6fcd-167">Faça logon em seu site de empresa do **Coupa** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="e6fcd-168">No menu na parte superior, clique em **Configuração** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="e6fcd-169">![Usuários](./media/active-directory-saas-coupa-tutorial/IC791908.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="e6fcd-170">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-170">Click **Create**.</span></span>
   
   <span data-ttu-id="e6fcd-171">![Criar Usuários](./media/active-directory-saas-coupa-tutorial/IC791909.png "Criar Usuários")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="e6fcd-172">Na seção **Criação de Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e6fcd-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="e6fcd-173">![Detalhes do Usuário](./media/active-directory-saas-coupa-tutorial/IC791910.png "Detalhes do Usuário")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="e6fcd-174">Digite os atributos **Logon**, **Nome**, **Sobrenome**, **ID de Logon Único** e **Email** de uma conta válida do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="e6fcd-175">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="e6fcd-176">O titular da conta do Active Directory do Azure receberá um email com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="e6fcd-177">É possível usar qualquer outra ferramenta de criação da conta de usuário do Coupa ou as APIs fornecidas pelo Coupa para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="e6fcd-178">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="e6fcd-178">Assign users</span></span>
<span data-ttu-id="e6fcd-179">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="e6fcd-180">**Para atribuir usuários ao Coupa, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e6fcd-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="e6fcd-181">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="e6fcd-182">Sobre o * * Coupa * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="e6fcd-183">![Atribuir Usuários](./media/active-directory-saas-coupa-tutorial/IC791911.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="e6fcd-184">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="e6fcd-185">![Sim](./media/active-directory-saas-coupa-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="e6fcd-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e6fcd-186">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e6fcd-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e6fcd-187">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e6fcd-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

