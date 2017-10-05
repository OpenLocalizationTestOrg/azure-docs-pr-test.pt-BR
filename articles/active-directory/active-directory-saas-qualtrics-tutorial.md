---
title: "Tutorial: Integração do Azure Active Directory com o Qualtrics | Microsoft Docs"
description: "Saiba como usar o Qualtrics com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
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
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="29b48-103">Tutorial: Integração do Active Directory do Azure com o Qualtrics</span><span class="sxs-lookup"><span data-stu-id="29b48-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="29b48-104">O objetivo deste tutorial é mostrar a integração do Azure com o Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="29b48-105">O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="29b48-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="29b48-106">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="29b48-106">A valid Azure subscription</span></span>
* <span data-ttu-id="29b48-107">Uma assinatura do Qualtrics com SSO (logon único) habilitado</span><span class="sxs-lookup"><span data-stu-id="29b48-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="29b48-108">Depois de concluir este tutorial, os usuários do Azure AD atribuídos ao Qualtrics poderão fazer logon único no aplicativo em seu site de empresa do Qualtrics (logon iniciado pelo provedor de serviços) ou usando a [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29b48-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="29b48-109">O cenário descrito neste tutorial consiste nos seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="29b48-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="29b48-110">Habilitando a integração de aplicativos para o Qualtrics</span><span class="sxs-lookup"><span data-stu-id="29b48-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="29b48-111">Configuração do SSO (logon único)</span><span class="sxs-lookup"><span data-stu-id="29b48-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="29b48-112">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="29b48-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="29b48-113">Atribuindo usuários</span><span class="sxs-lookup"><span data-stu-id="29b48-113">Assigning users</span></span>

<span data-ttu-id="29b48-114">![Cenário](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="29b48-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="29b48-115">Habilitando a integração de aplicativos para o Qualtrics</span><span class="sxs-lookup"><span data-stu-id="29b48-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="29b48-116">O objetivo desta seção é descrever como habilitar a integração de aplicativos com o Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="29b48-117">**Para habilitar a integração de aplicativos com o Qualtrics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="29b48-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="29b48-118">No Portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29b48-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="29b48-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="29b48-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="29b48-120">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="29b48-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="29b48-121">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="29b48-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="29b48-122">![Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="29b48-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="29b48-123">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="29b48-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="29b48-124">![Adicionar aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Adicionar aplicativo")</span><span class="sxs-lookup"><span data-stu-id="29b48-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="29b48-125">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="29b48-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="29b48-126">![Adicionar um aplicativo da galeria](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Adicionar um aplicativo da galeria")</span><span class="sxs-lookup"><span data-stu-id="29b48-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="29b48-127">Na **caixa de pesquisa**, digite **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="29b48-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="29b48-128">![Galeria de Aplicativos](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galeria de Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="29b48-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="29b48-129">No painel de resultados, selecione **Qualtrics** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29b48-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="29b48-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="29b48-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="29b48-131">Configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="29b48-131">Configure single sign-on</span></span>

<span data-ttu-id="29b48-132">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no Qualtrics com sua conta do AD do Azure usando federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="29b48-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="29b48-133">**Para configurar o logon único, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="29b48-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="29b48-134">No Portal Clássico do Azure, na página de integração de aplicativos do **Qualtrics**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="29b48-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="29b48-135">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29b48-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="29b48-136">Na página **Como você deseja que os usuários façam logon no Qualtrics**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="29b48-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="29b48-137">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29b48-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="29b48-138">Na página **Configurar a URL do Aplicativo**, na caixa de texto **URL de Entrada do Qualtrics**, digite a URL (por exemplo "*https://ssotest2ut1.qualtrics.com*") e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="29b48-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="29b48-139">![Configurar URL do Aplicativo](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="29b48-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="29b48-140">Na página **Configurar logon único no Qualtrics**, clique em **Baixar metadados** e salve o arquivo de metadados no computador.</span><span class="sxs-lookup"><span data-stu-id="29b48-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="29b48-141">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29b48-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="29b48-142">Envie o metadatafile para a equipe de suporte do Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="29b48-143">A configuração de SSO deve ser executada pela equipe de suporte do Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="29b48-144">Assim que a configuração for concluída, você receberá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="29b48-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="29b48-145">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="29b48-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="29b48-146">![Configurar Logon Único](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29b48-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="29b48-147">Configurar provisionamento do usuário</span><span class="sxs-lookup"><span data-stu-id="29b48-147">Configure user provisioning</span></span>

<span data-ttu-id="29b48-148">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="29b48-149">Quando um usuário atribuído tenta fazer logon no Qualtrics usando o painel de acesso, o Qualtrics verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="29b48-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="29b48-150">Se ainda não houver uma conta de usuário disponível, ela será automaticamente criada pelo Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="29b48-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="29b48-151">Atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="29b48-151">Assign users</span></span>
<span data-ttu-id="29b48-152">Para testar sua configuração, é necessário conceder acesso ao aplicativo aos usuários do Azure AD que você deseja que usem seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29b48-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="29b48-153">**Para atribuir usuários ao Qualtrics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="29b48-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="29b48-154">No Portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="29b48-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="29b48-155">Na página de integração de aplicativos do **Qualtrics**, clique em **Atribuir usuários**.</span><span class="sxs-lookup"><span data-stu-id="29b48-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="29b48-156">![Atribuir Usuários](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Atribuir Usuários")</span><span class="sxs-lookup"><span data-stu-id="29b48-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="29b48-157">Selecione seu usuário de teste, clique em **Atribuir** e, em seguida, clique em **Sim** para confirmar a atribuição.</span><span class="sxs-lookup"><span data-stu-id="29b48-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="29b48-158">![Sim](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="29b48-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="29b48-159">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="29b48-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="29b48-160">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29b48-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

