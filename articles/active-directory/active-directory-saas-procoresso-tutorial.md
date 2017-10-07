---
title: "Tutorial: Integração do Azure Active Directory com o Procore SSO | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="c061c-103">Tutorial: integração do Azure Active Directory com o Procore SSO</span><span class="sxs-lookup"><span data-stu-id="c061c-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="c061c-104">Neste tutorial, você aprenderá como toointegrate Procore SSO com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c061c-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c061c-105">Integrando Procore SSO com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c061c-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c061c-106">Você pode controlar no AD do Azure que tenha acesso tooProcore SSO</span><span class="sxs-lookup"><span data-stu-id="c061c-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="c061c-107">Você pode habilitar seu usuários tooautomatically get conectado tooProcore SSO (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c061c-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="c061c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c061c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c061c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="c061c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c061c-110">Prerequisites</span></span>

<span data-ttu-id="c061c-111">tooconfigure integração do AD do Azure com Procore SSO, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c061c-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="c061c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c061c-113">Uma assinatura do Procore SSO habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c061c-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c061c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c061c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c061c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c061c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c061c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c061c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c061c-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c061c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c061c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c061c-118">Scenario description</span></span>
<span data-ttu-id="c061c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c061c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c061c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c061c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c061c-121">Adicionando Procore SSO da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c061c-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="c061c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="c061c-123">Adicionando Procore SSO da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c061c-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="c061c-124">integração de saudação tooconfigure do SSO Procore no AD do Azure, você precisa tooadd Procore SSO na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c061c-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c061c-125">**tooadd Procore SSO da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c061c-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c061c-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c061c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c061c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c061c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c061c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c061c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c061c-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c061c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c061c-133">Na caixa de pesquisa hello, digite **SSO Procore**.</span><span class="sxs-lookup"><span data-stu-id="c061c-133">In hello search box, type **Procore SSO**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="c061c-135">No painel de resultados de saudação, selecione **SSO Procore**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c061c-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c061c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c061c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Procore SSO, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c061c-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c061c-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SSO Procore é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c061c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="c061c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em SSO Procore precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c061c-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="c061c-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="c061c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="c061c-142">tooconfigure e teste de logon único do AD do Azure com Procore SSO, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c061c-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c061c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c061c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c061c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c061c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c061c-145">**[Criar um usuário de teste de SSO Procore](#creating-a-procore-sso-test-user)**  -toohave um equivalente do Britta Simon no SSO Procore que é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="c061c-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c061c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c061c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c061c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c061c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c061c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c061c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c061c-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="c061c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="c061c-150">**tooconfigure AD do Azure-logon único com o SSO Procore, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c061c-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="c061c-151">No portal de gerenciamento do Azure do hello, no hello **SSO Procore** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c061c-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c061c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="c061c-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="c061c-155">Em Olá **Procore domínio de SSO e URLs** seção, hello usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="c061c-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="c061c-157">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c061c-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="c061c-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c061c-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c061c-161">Em Olá **Procore configuração de SSO** seção, clique em **configurar SSO Procore** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c061c-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c061c-162">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c061c-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="c061c-164">tooconfigure logon único no **Procore SSO** lado, o site de empresa procore tooyour logon como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c061c-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="c061c-165">Lista de ferramentas Olá para baixo, clique em **Admin** tooopen página de configurações de SSO de saudação.</span><span class="sxs-lookup"><span data-stu-id="c061c-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="c061c-167">Colar Olá valores nas caixas de saudação conforme descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="c061c-167">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="c061c-169">a.</span><span class="sxs-lookup"><span data-stu-id="c061c-169">a.</span></span> <span data-ttu-id="c061c-170">Em Olá **emissor URL de logon único** caixa, cole Olá ID da entidade SAML copiado da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c061c-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="c061c-171">b.</span><span class="sxs-lookup"><span data-stu-id="c061c-171">b.</span></span> <span data-ttu-id="c061c-172">Em Olá **SAML destino URL de logon** caixa, cole Olá Single Sign-On URL do serviço SAML copiado da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c061c-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="c061c-173">c.</span><span class="sxs-lookup"><span data-stu-id="c061c-173">c.</span></span> <span data-ttu-id="c061c-174">Agora, abra Olá **Metadata XML** baixado acima do hello portal do Azure e cópia Olá certificado na marca de saudação chamada **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="c061c-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="c061c-175">Olá colar copiado o valor para Olá **certificado de logon único x509** caixa.</span><span class="sxs-lookup"><span data-stu-id="c061c-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="c061c-176">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="c061c-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="c061c-177">Depois que essas configurações, você precisa Olá toosend **nome de domínio** (por exemplo **contoso.com**) por meio do qual você está fazendo login toohello Procore [a equipe de suporte Procore](https://support.procore.com/) e elas serão Ative o SSO federado para esse domínio.</span><span class="sxs-lookup"><span data-stu-id="c061c-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c061c-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="c061c-179">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c061c-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c061c-181">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c061c-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c061c-182">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c061c-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c061c-184">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="c061c-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c061c-186">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c061c-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c061c-188">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c061c-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c061c-190">a.</span><span class="sxs-lookup"><span data-stu-id="c061c-190">a.</span></span> <span data-ttu-id="c061c-191">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c061c-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c061c-192">b.</span><span class="sxs-lookup"><span data-stu-id="c061c-192">b.</span></span> <span data-ttu-id="c061c-193">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c061c-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c061c-194">c.</span><span class="sxs-lookup"><span data-stu-id="c061c-194">c.</span></span> <span data-ttu-id="c061c-195">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c061c-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c061c-196">d.</span><span class="sxs-lookup"><span data-stu-id="c061c-196">d.</span></span> <span data-ttu-id="c061c-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c061c-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="c061c-198">Criando um usuário de teste do Procore SSO</span><span class="sxs-lookup"><span data-stu-id="c061c-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="c061c-199">Siga Olá abaixo etapas toocreate um usuário de teste Procore em seu lado.</span><span class="sxs-lookup"><span data-stu-id="c061c-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="c061c-200">Site de empresa procore de tooyour de logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="c061c-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="c061c-201">Lista de ferramentas Olá para baixo, clique em **diretório** página de diretório tooopen Olá da empresa.</span><span class="sxs-lookup"><span data-stu-id="c061c-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="c061c-203">Clique em **adicionar uma pessoa** opção formulário de saudação tooopen e digite executar as seguintes opções -</span><span class="sxs-lookup"><span data-stu-id="c061c-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="c061c-205">a.</span><span class="sxs-lookup"><span data-stu-id="c061c-205">a.</span></span> <span data-ttu-id="c061c-206">Em Olá **nome** caixa de texto, nome do usuário do tipo como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c061c-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="c061c-207">b.</span><span class="sxs-lookup"><span data-stu-id="c061c-207">b.</span></span> <span data-ttu-id="c061c-208">Em Olá **Sobrenome** caixa de texto Sobrenome do usuário do tipo como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c061c-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="c061c-209">c.</span><span class="sxs-lookup"><span data-stu-id="c061c-209">c.</span></span> <span data-ttu-id="c061c-210">Em Olá **endereço de Email** caixa de texto, como o endereço de email do usuário do tipo  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c061c-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="c061c-211">d.</span><span class="sxs-lookup"><span data-stu-id="c061c-211">d.</span></span> <span data-ttu-id="c061c-212">Selecione **Modelo de permissão** como **Aplicar o modelo de permissão mais tarde**.</span><span class="sxs-lookup"><span data-stu-id="c061c-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="c061c-213">e.</span><span class="sxs-lookup"><span data-stu-id="c061c-213">e.</span></span> <span data-ttu-id="c061c-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c061c-214">Click **Create**.</span></span>

4. <span data-ttu-id="c061c-215">Verificar e atualizar detalhes Olá Olá recentemente adicionado entre em contato com.</span><span class="sxs-lookup"><span data-stu-id="c061c-215">Check and update hello details for hello newly added contact.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="c061c-217">Clique em **salvar e enviar convite** (se um convite por email é necessário) ou **salvar** (Salvar diretamente) registro de usuário do toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="c061c-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c061c-219">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c061c-220">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooProcore seu acesso SSO.</span><span class="sxs-lookup"><span data-stu-id="c061c-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c061c-222">**tooassign Britta Simon tooProcore SSO, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c061c-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="c061c-223">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c061c-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c061c-225">Na lista de aplicativos hello, selecione **SSO Procore**.</span><span class="sxs-lookup"><span data-stu-id="c061c-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="c061c-227">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c061c-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c061c-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c061c-229">Click **Add** button.</span></span> <span data-ttu-id="c061c-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c061c-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c061c-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c061c-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c061c-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c061c-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c061c-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c061c-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c061c-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c061c-235">Testing single sign-on</span></span>

<span data-ttu-id="c061c-236">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c061c-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c061c-237">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c061c-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c061c-238">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="c061c-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="c061c-239">Quando você clica em um bloco de SSO Procore Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado em aplicativos de SSO Procore.</span><span class="sxs-lookup"><span data-stu-id="c061c-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c061c-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c061c-240">Additional resources</span></span>

* [<span data-ttu-id="c061c-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c061c-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c061c-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c061c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

