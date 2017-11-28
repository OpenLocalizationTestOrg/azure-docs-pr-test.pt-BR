---
title: "Tutorial: integração do Azure Active Directory ao Promapp | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="cbc76-103">Tutorial: integração do Active Directory do Azure com o Promapp</span><span class="sxs-lookup"><span data-stu-id="cbc76-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="cbc76-104">Neste tutorial, você aprenderá como toointegrate Promapp com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cbc76-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbc76-105">Integrando Promapp com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cbc76-106">Você pode controlar no AD do Azure que tenha acesso tooPromapp</span><span class="sxs-lookup"><span data-stu-id="cbc76-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="cbc76-107">Você pode habilitar seu usuários tooautomatically get conectado tooPromapp (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cbc76-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cbc76-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cbc76-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbc76-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cbc76-110">Prerequisites</span></span>

<span data-ttu-id="cbc76-111">tooconfigure integração do AD do Azure com Promapp, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="cbc76-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbc76-113">Uma assinatura habilitada para logon único do Promapp</span><span class="sxs-lookup"><span data-stu-id="cbc76-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbc76-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cbc76-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbc76-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cbc76-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbc76-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cbc76-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cbc76-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cbc76-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbc76-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cbc76-118">Scenario description</span></span>
<span data-ttu-id="cbc76-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cbc76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbc76-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cbc76-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbc76-121">Adicionando Promapp da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cbc76-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="cbc76-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="cbc76-123">Adicionando Promapp da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cbc76-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="cbc76-124">integração de saudação tooconfigure de Promapp no AD do Azure, você precisa tooadd Promapp da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cbc76-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cbc76-125">**tooadd Promapp da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cbc76-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbc76-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cbc76-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cbc76-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cbc76-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cbc76-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cbc76-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cbc76-133">Na caixa de pesquisa hello, digite **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-133">In hello search box, type **Promapp**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="cbc76-135">No painel de resultados de saudação, selecione **Promapp**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cbc76-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cbc76-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cbc76-138">Nesta seção, você configura e testa o logon único do Azure AD com o Promapp, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cbc76-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbc76-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Promapp é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc76-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="cbc76-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Promapp precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cbc76-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="cbc76-141">Promapp, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbc76-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cbc76-142">tooconfigure e teste de logon único do AD do Azure com Promapp, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cbc76-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cbc76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cbc76-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cbc76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cbc76-145">**[Criar um usuário de teste Promapp](#creating-a-promapp-test-user)**  -toohave um equivalente do Britta Simon em Promapp é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cbc76-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cbc76-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cbc76-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cbc76-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cbc76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cbc76-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbc76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cbc76-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Promapp.</span><span class="sxs-lookup"><span data-stu-id="cbc76-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="cbc76-150">**tooconfigure AD do Azure-logon único com Promapp, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cbc76-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbc76-151">Em Olá portal do Azure, Olá **Promapp** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cbc76-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="cbc76-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="cbc76-155">Em Olá **Promapp domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="cbc76-157">a.</span><span class="sxs-lookup"><span data-stu-id="cbc76-157">a.</span></span> <span data-ttu-id="cbc76-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="cbc76-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="cbc76-159">b.</span><span class="sxs-lookup"><span data-stu-id="cbc76-159">b.</span></span> <span data-ttu-id="cbc76-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="cbc76-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cbc76-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="cbc76-161">These values are not real.</span></span> <span data-ttu-id="cbc76-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="cbc76-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cbc76-163">Entre em contato com [equipe de suporte do cliente Promapp](https://www.promapp.com/about-us/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="cbc76-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="cbc76-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cbc76-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="cbc76-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cbc76-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cbc76-168">Em Olá **Promapp configuração** seção, clique em **configurar Promapp** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="cbc76-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cbc76-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="cbc76-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="cbc76-171">Site de empresa de Promapp tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="cbc76-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="cbc76-172">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Logon Único do AD do Azure][12]

9. <span data-ttu-id="cbc76-174">Clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-174">Click **Configure**.</span></span> 
   
    ![Logon Único do AD do Azure][13]

10. <span data-ttu-id="cbc76-176">Em Olá **segurança** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Logon Único do AD do Azure][14]
    
    <span data-ttu-id="cbc76-178">a.</span><span class="sxs-lookup"><span data-stu-id="cbc76-178">a.</span></span> <span data-ttu-id="cbc76-179">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cbc76-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="cbc76-180">b.</span><span class="sxs-lookup"><span data-stu-id="cbc76-180">b.</span></span> <span data-ttu-id="cbc76-181">Para **SSO - Modo Logon Único**, selecione **Opcional** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="cbc76-182">c.</span><span class="sxs-lookup"><span data-stu-id="cbc76-182">c.</span></span> <span data-ttu-id="cbc76-183">Olá abrir baixado certificado no bloco de notas, cópia Olá certificado conteúdo sem a primeira linha do hello (---Iniciar certificado---) e a última linha do hello (---END certificado---), cole-o em Olá **certificado x. 509 SSO** caixa de texto e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="cbc76-184">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="cbc76-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cbc76-185">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="cbc76-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cbc76-186">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cbc76-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cbc76-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="cbc76-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc76-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cbc76-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cbc76-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbc76-191">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cbc76-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cbc76-193">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cbc76-195">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbc76-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cbc76-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbc76-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cbc76-199">a.</span><span class="sxs-lookup"><span data-stu-id="cbc76-199">a.</span></span> <span data-ttu-id="cbc76-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cbc76-201">b.</span><span class="sxs-lookup"><span data-stu-id="cbc76-201">b.</span></span> <span data-ttu-id="cbc76-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cbc76-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cbc76-203">c.</span><span class="sxs-lookup"><span data-stu-id="cbc76-203">c.</span></span> <span data-ttu-id="cbc76-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cbc76-205">d.</span><span class="sxs-lookup"><span data-stu-id="cbc76-205">d.</span></span> <span data-ttu-id="cbc76-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="cbc76-207">Criar um usuário de teste Promapp</span><span class="sxs-lookup"><span data-stu-id="cbc76-207">Creating a Promapp test user</span></span>

<span data-ttu-id="cbc76-208">Olá Promapp aplicativo suporta Just-in-Time de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="cbc76-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="cbc76-209">Isso significa que, uma conta de usuário é criada automaticamente se necessário durante uma tentativa de tooaccess hello, o aplicativo usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbc76-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cbc76-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cbc76-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPromapp.</span><span class="sxs-lookup"><span data-stu-id="cbc76-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cbc76-213">**tooassign Britta Simon tooPromapp, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cbc76-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbc76-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cbc76-216">Na lista de aplicativos hello, selecione **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-216">In hello applications list, select **Promapp**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="cbc76-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cbc76-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cbc76-220">Click **Add** button.</span></span> <span data-ttu-id="cbc76-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cbc76-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cbc76-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbc76-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cbc76-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cbc76-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cbc76-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cbc76-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cbc76-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cbc76-226">Testing single sign-on</span></span>

<span data-ttu-id="cbc76-227">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="cbc76-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cbc76-228">Quando você clica em bloco Promapp Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Promapp aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cbc76-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbc76-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cbc76-229">Additional resources</span></span>

* [<span data-ttu-id="cbc76-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cbc76-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbc76-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cbc76-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

