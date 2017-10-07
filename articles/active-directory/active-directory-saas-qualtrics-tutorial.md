---
title: "Tutorial: Integração do Azure Active Directory com o Qualtrics | Microsoft Docs"
description: "Saiba como toouse Qualtrics com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="dc6be-103">Tutorial: Integração do Active Directory do Azure com o Qualtrics</span><span class="sxs-lookup"><span data-stu-id="dc6be-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="dc6be-104">Olá objetivo deste tutorial é tooshow integração de saudação do Azure e Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="dc6be-105">cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc6be-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="dc6be-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="dc6be-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dc6be-107">Uma assinatura do Qualtrics com SSO (logon único) habilitado</span><span class="sxs-lookup"><span data-stu-id="dc6be-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="dc6be-108">Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooQualtrics será toosingle capaz de usar o logon no aplicativo hello em seu site da empresa do Qualtrics (serviço iniciado pelo provedor logon), ou por meio de saudação [toohello de Introdução Acessar o painel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc6be-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dc6be-109">cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc6be-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="dc6be-110">Habilitando a integração de aplicativos de saudação para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="dc6be-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="dc6be-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="dc6be-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="dc6be-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="dc6be-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="dc6be-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="dc6be-113">Assigning users</span></span>

<span data-ttu-id="dc6be-114">![Cenário](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="dc6be-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="dc6be-115">Habilitando a integração de aplicativos de saudação para Qualtrics</span><span class="sxs-lookup"><span data-stu-id="dc6be-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="dc6be-116">Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="dc6be-117">**integração de aplicativos de saudação tooenable para Qualtrics, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc6be-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc6be-118">No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="dc6be-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dc6be-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dc6be-120">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="dc6be-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="dc6be-121">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="dc6be-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="dc6be-122">![Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="dc6be-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dc6be-123">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="dc6be-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="dc6be-124">![Adicionar aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="dc6be-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dc6be-125">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="dc6be-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="dc6be-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dc6be-127">Em Olá **caixa de pesquisa**, tipo **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="dc6be-128">![Galeria de Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="dc6be-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="dc6be-129">No painel de resultados de saudação, selecione **Qualtrics**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dc6be-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="dc6be-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="dc6be-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dc6be-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="dc6be-131">Configure single sign-on</span></span>

<span data-ttu-id="dc6be-132">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooQualtrics com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc6be-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="dc6be-133">**tooconfigure o logon único, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc6be-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc6be-134">Em Olá portal clássico do Azure, em Olá **Qualtrics** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc6be-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dc6be-135">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="dc6be-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="dc6be-136">Em Olá **como você gostaria usuários toosign em tooQualtrics** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="dc6be-137">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="dc6be-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="dc6be-138">Em Olá **configurar URL do aplicativo** página Olá **Qualtrics URL de logon** caixa de texto, digite a URL (por exemplo: "*https://ssotest2ut1.qualtrics.com*") e, em seguida, clique em **Próxima**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="dc6be-139">![Configurar URL do Aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="dc6be-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="dc6be-140">Em Olá **configurar logon único no Qualtrics** , clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="dc6be-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="dc6be-141">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="dc6be-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="dc6be-142">Envie toohello de arquivo de metadados de saudação equipe de suporte do Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dc6be-143">a configuração de SSO Olá tem toobe executada pelo Olá, equipe de suporte do Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="dc6be-144">Você receberá uma notificação assim Olá configuração foi concluída.</span><span class="sxs-lookup"><span data-stu-id="dc6be-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="dc6be-145">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc6be-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dc6be-146">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="dc6be-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="dc6be-147">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="dc6be-147">Configure user provisioning</span></span>

<span data-ttu-id="dc6be-148">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="dc6be-149">Quando um usuário atribuído tenta toolog no Qualtrics usando o painel de acesso hello, Qualtrics verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="dc6be-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="dc6be-150">Se ainda não houver uma conta de usuário disponível, ela será automaticamente criada pelo Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="dc6be-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="dc6be-151">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="dc6be-151">Assign users</span></span>
<span data-ttu-id="dc6be-152">tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.</span><span class="sxs-lookup"><span data-stu-id="dc6be-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="dc6be-153">**tooassign tooQualtrics de usuários, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="dc6be-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc6be-154">No hello portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="dc6be-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dc6be-155">Em Olá **Qualtrics** página de integração de aplicativos, clique em **atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="dc6be-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dc6be-156">![Atribuir Usuários](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="dc6be-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="dc6be-157">Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.</span><span class="sxs-lookup"><span data-stu-id="dc6be-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="dc6be-158">![Sim](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="dc6be-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dc6be-159">Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="dc6be-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="dc6be-160">Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc6be-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

