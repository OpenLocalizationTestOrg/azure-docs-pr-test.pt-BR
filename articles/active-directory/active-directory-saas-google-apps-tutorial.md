---
title: "Tutorial: Integração do Azure Active Directory ao Google Apps no Azure | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="3e79b-103">Tutorial: integração do Azure Active Directory ao Google Apps</span><span class="sxs-lookup"><span data-stu-id="3e79b-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="3e79b-104">Neste tutorial, você aprende a integrar o Google Apps ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3e79b-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e79b-105">A integração do Google Apps ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3e79b-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3e79b-106">No Azure AD, é possível controlar quem tem acesso ao Google Apps</span><span class="sxs-lookup"><span data-stu-id="3e79b-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="3e79b-107">É possível permitir que os usuários se conectem automaticamente ao Google Apps (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e79b-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e79b-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3e79b-109">Caso deseje obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e79b-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e79b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3e79b-110">Prerequisites</span></span>

<span data-ttu-id="3e79b-111">Para configurar a integração do Azure AD ao Google Apps, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3e79b-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="3e79b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e79b-113">Uma assinatura habilitada para logon único do Google Apps</span><span class="sxs-lookup"><span data-stu-id="3e79b-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e79b-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3e79b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e79b-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3e79b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e79b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3e79b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e79b-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e79b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="3e79b-118">Tutorial em vídeo</span><span class="sxs-lookup"><span data-stu-id="3e79b-118">Video tutorial</span></span>
<span data-ttu-id="3e79b-119">Como habilitar o logon único no Google Apps em dois minutos:</span><span class="sxs-lookup"><span data-stu-id="3e79b-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="3e79b-120">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="3e79b-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="3e79b-121">**P: Os Chromebooks e outros dispositivos Chrome são compatíveis com o logon único do AD do AD do Azure?**</span><span class="sxs-lookup"><span data-stu-id="3e79b-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="3e79b-122">R: Sim. Os usuários podem entrar em seus dispositivos Chromebook usando suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e79b-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="3e79b-123">Confira este [artigo de suporte do Google Apps](https://support.google.com/chrome/a/answer/6060880) para saber mais sobre o motivo de os usuários receberem uma solicitação por credenciais duas vezes.</span><span class="sxs-lookup"><span data-stu-id="3e79b-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="3e79b-124">**P: Se eu habilitar o logon único, os usuários conseguirão usar suas credenciais do Azure AD para entrar em qualquer produto do Google, como Google Sala de aula, GMail, Google Drive, YouTube e assim por diante?**</span><span class="sxs-lookup"><span data-stu-id="3e79b-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="3e79b-125">R: Sim, dependendo de [quais aplicativos do Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) você optar por habilitar ou desabilitar para sua organização.</span><span class="sxs-lookup"><span data-stu-id="3e79b-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="3e79b-126">**P: Posso habilitar o logon único apenas para um subconjunto de meus usuários do Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="3e79b-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="3e79b-127">R: Não. A ativação do logon único exige imediatamente que todos os usuários do Google Apps se autentiquem com suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e79b-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="3e79b-128">Como o Google Apps não oferece suporte a vários provedores de identidade, o provedor de identidade para seu ambiente do Google Apps pode ser o AD do Azure ou o Google, mas não ambos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="3e79b-129">**P: Se um usuário se conectar por meio do Windows, ele será autenticado automaticamente no Google Apps sem que uma senha seja solicitada?**</span><span class="sxs-lookup"><span data-stu-id="3e79b-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="3e79b-130">R: Há duas opções para este cenário.</span><span class="sxs-lookup"><span data-stu-id="3e79b-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="3e79b-131">Primeiro, os usuários podem entrar em dispositivos com Windows 10 por meio do [Ingresso no Active Directory do Azure](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e79b-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="3e79b-132">Como alternativa, os usuários podem entrar em dispositivos com Windows que ingressaram em um domínio para um Active Directory local com logon único habilitado no AD do Azure por meio de uma implantação dos [Serviços de Federação do Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) .</span><span class="sxs-lookup"><span data-stu-id="3e79b-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="3e79b-133">Ambas as opções exigem que você realize as etapas no tutorial a seguir para habilitar o logon único entre o Azure AD e o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="3e79b-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e79b-134">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3e79b-134">Scenario description</span></span>
<span data-ttu-id="3e79b-135">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3e79b-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e79b-136">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3e79b-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e79b-137">Adicionando o Google Apps por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="3e79b-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="3e79b-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="3e79b-139">Adicionando o Google Apps por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="3e79b-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="3e79b-140">Para configurar a integração do Google Apps ao Azure AD, é necessário adicionar o Google Apps à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="3e79b-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3e79b-141">**Para adicionar o Google Apps por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3e79b-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3e79b-142">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e79b-144">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3e79b-145">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-145">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3e79b-147">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3e79b-149">Na caixa de pesquisa, digite **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-149">In the search box, type **Google Apps**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="3e79b-151">No painel de resultados, selecione **Google Apps** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e79b-153">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e79b-154">Nesta seção, você configura e testa o logon único do Azure AD com o Google Apps, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3e79b-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3e79b-155">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Google Apps é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e79b-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="3e79b-156">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="3e79b-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="3e79b-157">Essa relação de vínculo é estabelecida com a atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Google Apps.</span><span class="sxs-lookup"><span data-stu-id="3e79b-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="3e79b-158">Para configurar e testar o logon único do Azure AD com o Google Apps, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3e79b-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3e79b-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3e79b-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3e79b-160">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3e79b-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e79b-161">**[Criando um usuário de teste do Google Apps](#creating-a-google-apps-test-user)** – para ter um equivalente de Brenda Fernandes no Google Apps que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e79b-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e79b-162">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e79b-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e79b-163">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3e79b-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e79b-164">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e79b-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e79b-165">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Google Apps.</span><span class="sxs-lookup"><span data-stu-id="3e79b-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="3e79b-166">**Para configurar o logon único do Azure AD com o Google Apps, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3e79b-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="3e79b-167">No portal do Azure, na página de integração do aplicativo **Google Apps**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3e79b-169">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3e79b-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="3e79b-171">Na seção **Domínio e URLs do Google Apps**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3e79b-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="3e79b-173">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="3e79b-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e79b-174">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3e79b-174">This value is not real.</span></span> <span data-ttu-id="3e79b-175">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="3e79b-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="3e79b-176">Contate a [equipe de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="3e79b-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="3e79b-177">Na seção **Certificado de Autenticação SAML**, clique em **Certificado** e, em seguida, salve o certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3e79b-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="3e79b-179">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3e79b-179">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e79b-181">Na seção **Configuração do Google Apps**, clique em **Configurar o Google Apps** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3e79b-182">Copie a **URL de Saída, a URL do Serviço de Logon Único SAML e a URL de Alteração de Senha** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3e79b-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="3e79b-184">Abra uma nova guia no navegador e entre no [Console de Admin do Google Apps](http://admin.google.com/) usando sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="3e79b-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="3e79b-185">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-185">Click **Security**.</span></span> <span data-ttu-id="3e79b-186">Se você não enxergar o link, ele pode estar oculto sob o menu **Mais Controles** , na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="3e79b-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Clique em Segurança.][10]

9. <span data-ttu-id="3e79b-188">Na página **Segurança**, clique em **Configurar logon único (SSO).**</span><span class="sxs-lookup"><span data-stu-id="3e79b-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Clique em SSO.][11]

10. <span data-ttu-id="3e79b-190">Realize as seguintes alterações de configuração:</span><span class="sxs-lookup"><span data-stu-id="3e79b-190">Perform the following configuration changes:</span></span>
   
    ![Configure o SSO][12]
   
    <span data-ttu-id="3e79b-192">a.</span><span class="sxs-lookup"><span data-stu-id="3e79b-192">a.</span></span> <span data-ttu-id="3e79b-193">Selecione **Configurar SSO com um provedor de identidade de terceiros**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="3e79b-194">b.</span><span class="sxs-lookup"><span data-stu-id="3e79b-194">b.</span></span> <span data-ttu-id="3e79b-195">No campo **URL da página de entrada** do Google Apps, cole o valor da **URL do Serviço de Logon Único** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e79b-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3e79b-196">c.</span><span class="sxs-lookup"><span data-stu-id="3e79b-196">c.</span></span> <span data-ttu-id="3e79b-197">No campo **URL da página de saída** do Google Apps, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e79b-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3e79b-198">d.</span><span class="sxs-lookup"><span data-stu-id="3e79b-198">d.</span></span> <span data-ttu-id="3e79b-199">No campo **URL de Alteração de Senha** do Google Apps, cole o valor da **URL de alteração de senha** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e79b-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3e79b-200">e.</span><span class="sxs-lookup"><span data-stu-id="3e79b-200">e.</span></span> <span data-ttu-id="3e79b-201">No Google Apps, para o **Certificado de verificação**, carregue o certificado baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e79b-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3e79b-202">f.</span><span class="sxs-lookup"><span data-stu-id="3e79b-202">f.</span></span> <span data-ttu-id="3e79b-203">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3e79b-204">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3e79b-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3e79b-205">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3e79b-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3e79b-206">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e79b-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e79b-207">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e79b-208">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3e79b-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3e79b-210">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3e79b-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3e79b-211">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e79b-213">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3e79b-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e79b-215">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e79b-217">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3e79b-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e79b-219">a.</span><span class="sxs-lookup"><span data-stu-id="3e79b-219">a.</span></span> <span data-ttu-id="3e79b-220">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e79b-221">b.</span><span class="sxs-lookup"><span data-stu-id="3e79b-221">b.</span></span> <span data-ttu-id="3e79b-222">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3e79b-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e79b-223">c.</span><span class="sxs-lookup"><span data-stu-id="3e79b-223">c.</span></span> <span data-ttu-id="3e79b-224">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3e79b-225">d.</span><span class="sxs-lookup"><span data-stu-id="3e79b-225">d.</span></span> <span data-ttu-id="3e79b-226">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="3e79b-227">Criando um usuário de teste do Google Apps</span><span class="sxs-lookup"><span data-stu-id="3e79b-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="3e79b-228">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="3e79b-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="3e79b-229">O Google Apps dá suporte ao provisionamento automático, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3e79b-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="3e79b-230">Não há nenhuma ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3e79b-230">There is no action for you in this section.</span></span> <span data-ttu-id="3e79b-231">Se um usuário ainda não existir no Google Apps Software, um novo será criado quando você tentar acessar o Google Apps Software.</span><span class="sxs-lookup"><span data-stu-id="3e79b-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="3e79b-232">Se você precisar criar um usuário manualmente, contate a [equipe de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="3e79b-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3e79b-233">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3e79b-234">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Google Apps.</span><span class="sxs-lookup"><span data-stu-id="3e79b-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3e79b-236">**Para atribuir Brenda Fernandes ao Google Apps, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3e79b-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="3e79b-237">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3e79b-239">Na lista de aplicativos, selecione **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-239">In the applications list, select **Google Apps**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="3e79b-241">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3e79b-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3e79b-243">Click **Add** button.</span></span> <span data-ttu-id="3e79b-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3e79b-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3e79b-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3e79b-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e79b-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e79b-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e79b-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3e79b-249">Testing single sign-on</span></span>

<span data-ttu-id="3e79b-250">Nesta seção, para testar as configurações de logon único, abra o Painel de Acesso em [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md) e, depois, entre na conta de teste e clique no bloco **Google Apps** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3e79b-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e79b-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3e79b-251">Additional resources</span></span>

* [<span data-ttu-id="3e79b-252">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3e79b-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e79b-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e79b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3e79b-254">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="3e79b-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png