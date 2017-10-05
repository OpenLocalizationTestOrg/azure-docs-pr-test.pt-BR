---
title: "Tutorial: integração do Azure Active Directory ao Benefitsolver | Microsoft Docs"
description: "Saiba como usar o Benefitsolver com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="b29ea-103">Tutorial: Integração do Active Directory do Azure ao Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="b29ea-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="b29ea-104">O objetivo deste tutorial é mostrar a integração do Azure ao Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="b29ea-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b29ea-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="b29ea-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="b29ea-106">A valid Azure subscription</span></span>
* <span data-ttu-id="b29ea-107">Uma assinatura habilitada para logon único (SSO) do Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="b29ea-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="b29ea-108">Depois de concluir este tutorial, os usuários do AD do Azure atribuídos ao Benefitsolver poderão fazer logon único no aplicativo usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b29ea-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="b29ea-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b29ea-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="b29ea-110">Habilitando a integração de aplicativos para o Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="b29ea-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="b29ea-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="b29ea-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="b29ea-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="b29ea-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="b29ea-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="b29ea-113">Assigning users</span></span>

<span data-ttu-id="b29ea-114">![Cenário](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="b29ea-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="b29ea-115">Habilitando a integração de aplicativos para o Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="b29ea-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="b29ea-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos para o Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="b29ea-117">Para habilitar a integração de aplicativos para o Benefitsolver, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b29ea-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="b29ea-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="b29ea-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="b29ea-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="b29ea-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="b29ea-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b29ea-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="b29ea-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="b29ea-122">![Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="b29ea-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="b29ea-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="b29ea-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="b29ea-124">![Adicionar aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="b29ea-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="b29ea-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="b29ea-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="b29ea-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="b29ea-127">Na **caixa de pesquisa**, digite **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="b29ea-128">![Galeria de Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="b29ea-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="b29ea-129">No painel de resultados, selecione **Benefitsolver** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b29ea-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="b29ea-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="b29ea-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="b29ea-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="b29ea-131">Configure single sign-on</span></span>

<span data-ttu-id="b29ea-132">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Benefitsolver com a respectiva conta do AD do Azure usando federação baseada no protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="b29ea-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="b29ea-133">Seu aplicativo Benefitsolver espera as declarações do SAML em um formato específico, o que exige a adição de mapeamentos de atributo personalizados de acordo com a sua configuração de **atributos do token SAML** .</span><span class="sxs-lookup"><span data-stu-id="b29ea-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="b29ea-134">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="b29ea-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="b29ea-135">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="b29ea-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="b29ea-136">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b29ea-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="b29ea-137">No Portal clássico do Azure, na página de integração do aplicativo **Benefitsolver**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="b29ea-138">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b29ea-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="b29ea-139">Na página **Como você deseja que os usuários façam logon no Benefitsolver**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="b29ea-140">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b29ea-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="b29ea-141">Na página **Definir Configurações do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b29ea-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="b29ea-142">![Definir Configurações de Aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Definir Configurações de Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="b29ea-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="b29ea-143">Na caixa de texto **URL de Logon**, digite **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="b29ea-144">Na caixa de texto **URL de Resposta**, digite **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="b29ea-145">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-145">Click **Next**.</span></span>
4. <span data-ttu-id="b29ea-146">Na página **Configurar logon único no Benefitsolver**, para baixar os metadados, clique em **Baixar metadados** e salve o arquivo de metadados localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="b29ea-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="b29ea-147">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b29ea-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="b29ea-148">Envie o arquivo de metadados baixado para a equipe de suporte do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="b29ea-149">A equipe de suporte do Benefitsolver precisa fazer a configuração real do SSO.</span><span class="sxs-lookup"><span data-stu-id="b29ea-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="b29ea-150">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b29ea-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="b29ea-151">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="b29ea-152">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b29ea-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="b29ea-153">Na parte superior do menu, clique em **Atributos** to open the **SAML Token Atributos** .</span><span class="sxs-lookup"><span data-stu-id="b29ea-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="b29ea-154">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="b29ea-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="b29ea-155">Para adicionar os mapeamentos de atributo necessários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b29ea-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="b29ea-156">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="b29ea-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="b29ea-157">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="b29ea-157">Attribute Name</span></span> | <span data-ttu-id="b29ea-158">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="b29ea-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b29ea-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="b29ea-159">ClientID</span></span> |<span data-ttu-id="b29ea-160">Você precisa obter esse valor com a equipe de suporte do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="b29ea-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="b29ea-161">ClientKey</span></span> |<span data-ttu-id="b29ea-162">Você precisa obter esse valor com a equipe de suporte do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="b29ea-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="b29ea-163">LogoutURL</span></span> |<span data-ttu-id="b29ea-164">Você precisa obter esse valor com a equipe de suporte do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="b29ea-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="b29ea-165">EmployeeID</span></span> |<span data-ttu-id="b29ea-166">Você precisa obter esse valor com a equipe de suporte do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="b29ea-167">Para cada linha de dados na tabela acima, clique em **adicionar atributo do usuário**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="b29ea-168">Na caixa de texto **Nome do Atributo** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="b29ea-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="b29ea-169">Na caixa de texto **Valor do Atributo** , selecione o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="b29ea-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="b29ea-170">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-170">Click **Complete**.</span></span>
9. <span data-ttu-id="b29ea-171">Clique em **Aplicar alterações**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="b29ea-172">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="b29ea-172">Configure user provisioning</span></span>
<span data-ttu-id="b29ea-173">Para permitir que os usuários do AD do Azure façam logon no Benefitsolver, eles deverão ser provisionados no Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="b29ea-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="b29ea-174">No caso do Benefitsolver, os dados de funcionários são preenchidos em seu aplicativo por meio de um arquivo de censo do sistema HRIS (geralmente à noite).</span><span class="sxs-lookup"><span data-stu-id="b29ea-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="b29ea-175">É possível usar qualquer outra ferramenta de criação da conta de usuário do Benefitsolver ou as APIs fornecidas pelo Benefitsolver para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="b29ea-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="b29ea-176">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="b29ea-176">Assigning users</span></span>
<span data-ttu-id="b29ea-177">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b29ea-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="b29ea-178">Para atribuir usuários ao Benefitsolver, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b29ea-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="b29ea-179">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="b29ea-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="b29ea-180">Sobre o * * Benefitsolver * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="b29ea-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="b29ea-181">![Atribuir Usuários](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="b29ea-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="b29ea-182">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="b29ea-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="b29ea-183">![Sim](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="b29ea-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="b29ea-184">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b29ea-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b29ea-185">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b29ea-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

