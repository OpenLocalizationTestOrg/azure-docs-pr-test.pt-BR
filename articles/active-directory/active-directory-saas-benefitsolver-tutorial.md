---
title: "Tutorial: integração do Azure Active Directory ao Benefitsolver | Microsoft Docs"
description: "Saiba como toouse Benefitsolver com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="fbb99-103">Tutorial: Integração do Active Directory do Azure ao Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="fbb99-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="fbb99-104">Olá objetivo deste tutorial é a integração do Azure e Benefitsolver Olá tooshow.</span><span class="sxs-lookup"><span data-stu-id="fbb99-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="fbb99-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="fbb99-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="fbb99-106">A valid Azure subscription</span></span>
* <span data-ttu-id="fbb99-107">Uma assinatura habilitada para logon único (SSO) do Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="fbb99-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="fbb99-108">Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooBenefitsolver será toosingle capaz de usar o logon no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbb99-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="fbb99-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="fbb99-110">Habilitando a integração de aplicativos de saudação para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="fbb99-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="fbb99-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="fbb99-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="fbb99-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="fbb99-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="fbb99-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="fbb99-113">Assigning users</span></span>

<span data-ttu-id="fbb99-114">![Cenário](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="fbb99-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="fbb99-115">Habilitando a integração de aplicativos de saudação para Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="fbb99-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="fbb99-116">Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="fbb99-117">integração de aplicativos de saudação tooenable para Benefitsolver, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="fbb99-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="fbb99-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="fbb99-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="fbb99-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="fbb99-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="fbb99-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="fbb99-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="fbb99-122">![Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="fbb99-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="fbb99-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="fbb99-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="fbb99-124">![Adicionar aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="fbb99-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="fbb99-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="fbb99-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="fbb99-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="fbb99-127">Em Olá **caixa de pesquisa**, tipo **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="fbb99-128">![Galeria de Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="fbb99-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="fbb99-129">No painel de resultados de saudação, selecione **Benefitsolver**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fbb99-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="fbb99-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="fbb99-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="fbb99-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="fbb99-131">Configure single sign-on</span></span>

<span data-ttu-id="fbb99-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooBenefitsolver com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbb99-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="fbb99-133">Seu aplicativo de Benefitsolver espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens saml** configuração.</span><span class="sxs-lookup"><span data-stu-id="fbb99-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="fbb99-134">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="fbb99-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="fbb99-135">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="fbb99-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="fbb99-136">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="fbb99-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbb99-137">Em Olá portal clássico do Azure, em Olá **Benefitsolver** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fbb99-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="fbb99-138">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fbb99-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="fbb99-139">Em Olá **como você gostaria usuários toosign em tooBenefitsolver** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="fbb99-140">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fbb99-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="fbb99-141">Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="fbb99-142">![Definir Configurações de Aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Definir Configurações de Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="fbb99-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="fbb99-143">Em Olá **URL de logon** caixa de texto, tipo **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="fbb99-144">Em Olá **URL de resposta** caixa de texto, tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="fbb99-145">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-145">Click **Next**.</span></span>
4. <span data-ttu-id="fbb99-146">Em Olá **configurar logon único no Benefitsolver** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="fbb99-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="fbb99-147">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fbb99-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="fbb99-148">Envie a equipe de suporte do hello baixado metadados arquivo tooyour Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="fbb99-149">Sua equipe de suporte Benefitsolver tem toodo Olá configuração real do SSO.</span><span class="sxs-lookup"><span data-stu-id="fbb99-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="fbb99-150">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="fbb99-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="fbb99-151">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fbb99-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="fbb99-152">![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="fbb99-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="fbb99-153">No menu de saudação na parte superior de saudação, clique em **atributos** tooopen Olá **atributos de tokens SAML** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fbb99-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="fbb99-154">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="fbb99-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="fbb99-155">mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="fbb99-156">![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="fbb99-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="fbb99-157">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="fbb99-157">Attribute Name</span></span> | <span data-ttu-id="fbb99-158">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="fbb99-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fbb99-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="fbb99-159">ClientID</span></span> |<span data-ttu-id="fbb99-160">É necessário tooget esse valor de sua equipe de suporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="fbb99-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="fbb99-161">ClientKey</span></span> |<span data-ttu-id="fbb99-162">É necessário tooget esse valor de sua equipe de suporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="fbb99-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="fbb99-163">LogoutURL</span></span> |<span data-ttu-id="fbb99-164">É necessário tooget esse valor de sua equipe de suporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="fbb99-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="fbb99-165">EmployeeID</span></span> |<span data-ttu-id="fbb99-166">É necessário tooget esse valor de sua equipe de suporte de Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="fbb99-167">Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="fbb99-168">Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="fbb99-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="fbb99-169">Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="fbb99-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="fbb99-170">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-170">Click **Complete**.</span></span>
9. <span data-ttu-id="fbb99-171">Clique em **Aplicar alterações**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="fbb99-172">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="fbb99-172">Configure user provisioning</span></span>
<span data-ttu-id="fbb99-173">Em ordem tooenable AD do Azure usuários toolog em Benefitsolver, eles devem ser provisionados no Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="fbb99-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="fbb99-174">No caso de saudação de Benefitsolver, dados de funcionário estão em seu aplicativo preenchido por meio de um arquivo de censo do seu sistema HRIS (geralmente à noite).</span><span class="sxs-lookup"><span data-stu-id="fbb99-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="fbb99-175">Você pode usar qualquer ferramenta de criação outros Benefitsolver usuário conta ou APIs fornecidas pelo Benefitsolver tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="fbb99-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="fbb99-176">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="fbb99-176">Assigning users</span></span>
<span data-ttu-id="fbb99-177">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="fbb99-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="fbb99-178">tooassign usuários tooBenefitsolver, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbb99-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="fbb99-179">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="fbb99-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="fbb99-180">Em hello * * Benefitsolver * * página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="fbb99-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="fbb99-181">![Atribuir Usuários](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="fbb99-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="fbb99-182">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="fbb99-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="fbb99-183">![Sim](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="fbb99-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="fbb99-184">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fbb99-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="fbb99-185">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbb99-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

