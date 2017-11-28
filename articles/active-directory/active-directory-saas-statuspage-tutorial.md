---
title: "Tutorial: integração do Azure Active Directory ao StatusPage | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="72783-103">Tutorial: Integração do Active Directory do Azure com o StatusPage</span><span class="sxs-lookup"><span data-stu-id="72783-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="72783-104">Neste tutorial, você aprenderá como toointegrate StatusPage com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="72783-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72783-105">Integrando StatusPage com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72783-106">Você pode controlar no AD do Azure que tenha acesso tooStatusPage</span><span class="sxs-lookup"><span data-stu-id="72783-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="72783-107">Você pode habilitar seu usuários tooautomatically get conectado tooStatusPage (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72783-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72783-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72783-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72783-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72783-110">Prerequisites</span></span>

<span data-ttu-id="72783-111">tooconfigure integração do AD do Azure com StatusPage, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="72783-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72783-113">Uma assinatura habilitada para logon único do StatusPage</span><span class="sxs-lookup"><span data-stu-id="72783-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72783-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="72783-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72783-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="72783-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72783-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="72783-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72783-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72783-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72783-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="72783-118">Scenario description</span></span>
<span data-ttu-id="72783-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="72783-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72783-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="72783-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72783-121">Adicionando StatusPage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72783-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="72783-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="72783-123">Adicionando StatusPage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="72783-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="72783-124">integração de saudação tooconfigure de StatusPage no AD do Azure, você precisa tooadd StatusPage da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="72783-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72783-125">**tooadd StatusPage da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72783-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72783-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72783-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="72783-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="72783-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72783-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72783-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="72783-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72783-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="72783-133">Na caixa de pesquisa hello, digite **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="72783-133">In hello search box, type **StatusPage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="72783-135">No painel de resultados de saudação, selecione **StatusPage**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="72783-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72783-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72783-138">Nesta seção, você configura e testa o logon único do Azure AD com o StatusPage, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="72783-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72783-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em StatusPage é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="72783-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="72783-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em StatusPage precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="72783-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="72783-141">StatusPage, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="72783-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72783-142">tooconfigure e teste de logon único do AD do Azure com StatusPage, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72783-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="72783-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72783-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72783-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72783-145">**[Criar um usuário de teste StatusPage](#creating-a-statuspage-test-user)**  -toohave um equivalente do Britta Simon em StatusPage é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="72783-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72783-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="72783-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72783-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="72783-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72783-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="72783-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72783-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo StatusPage.</span><span class="sxs-lookup"><span data-stu-id="72783-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="72783-150">**tooconfigure AD do Azure-logon único com StatusPage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72783-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="72783-151">Em Olá portal do Azure, Olá **StatusPage** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="72783-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="72783-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="72783-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="72783-155">Em Olá **StatusPage domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="72783-157">a.</span><span class="sxs-lookup"><span data-stu-id="72783-157">a.</span></span> <span data-ttu-id="72783-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="72783-159">b.</span><span class="sxs-lookup"><span data-stu-id="72783-159">b.</span></span> <span data-ttu-id="72783-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="72783-161">Entre em contato com a equipe de suporte de StatusPage Olá no [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest metadados necessários tooconfigure logon único.</span><span class="sxs-lookup"><span data-stu-id="72783-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="72783-162">a.</span><span class="sxs-lookup"><span data-stu-id="72783-162">a.</span></span> <span data-ttu-id="72783-163">De metadados hello, copie o valor de emissor hello e, em seguida, cole-o em hello **identificador** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="72783-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="72783-164">b.</span><span class="sxs-lookup"><span data-stu-id="72783-164">b.</span></span> <span data-ttu-id="72783-165">Metadados de saudação do copiar Olá URL de resposta e, em seguida, cole-o em Olá **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="72783-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="72783-166">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="72783-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="72783-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="72783-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72783-170">Em Olá **StatusPage configuração** seção, clique em **configurar StatusPage** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="72783-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="72783-171">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="72783-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="72783-173">Em outra janela do navegador, entre no site da empresa StatusPage tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="72783-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="72783-174">Na barra de ferramentas principal hello, clique em **Gerenciar conta**.</span><span class="sxs-lookup"><span data-stu-id="72783-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="72783-176">Clique em Olá **Single Sign-on** guia.</span><span class="sxs-lookup"><span data-stu-id="72783-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="72783-178">Na página de configuração de SSO de hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="72783-181">a.</span><span class="sxs-lookup"><span data-stu-id="72783-181">a.</span></span> <span data-ttu-id="72783-182">Em hello **URL de destino SSO** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72783-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="72783-183">b.</span><span class="sxs-lookup"><span data-stu-id="72783-183">b.</span></span> <span data-ttu-id="72783-184">Abra seu certificado baixado no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="72783-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="72783-185">c.</span><span class="sxs-lookup"><span data-stu-id="72783-185">c.</span></span> <span data-ttu-id="72783-186">Clique em **SALVAR CONFIGURAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="72783-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="72783-187">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="72783-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72783-188">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="72783-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72783-189">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72783-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72783-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="72783-191">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72783-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="72783-193">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72783-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72783-194">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="72783-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72783-196">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="72783-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72783-198">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="72783-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72783-200">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="72783-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72783-202">a.</span><span class="sxs-lookup"><span data-stu-id="72783-202">a.</span></span> <span data-ttu-id="72783-203">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72783-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72783-204">b.</span><span class="sxs-lookup"><span data-stu-id="72783-204">b.</span></span> <span data-ttu-id="72783-205">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72783-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72783-206">c.</span><span class="sxs-lookup"><span data-stu-id="72783-206">c.</span></span> <span data-ttu-id="72783-207">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="72783-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72783-208">d.</span><span class="sxs-lookup"><span data-stu-id="72783-208">d.</span></span> <span data-ttu-id="72783-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72783-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="72783-210">Criando um usuário de teste de StatusPage</span><span class="sxs-lookup"><span data-stu-id="72783-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="72783-211">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no StatusPage.</span><span class="sxs-lookup"><span data-stu-id="72783-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="72783-212">O StatusPage dá suporte ao provisionamento de usuário just-in-time.</span><span class="sxs-lookup"><span data-stu-id="72783-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="72783-213">Você já habilitou isso em [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="72783-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="72783-214">**toocreate um usuário chamado Britta Simon no StatusPage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72783-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="72783-215">Site de empresa de StatusPage tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="72783-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="72783-216">No menu de saudação na parte superior de saudação, clique em **Gerenciar conta**.</span><span class="sxs-lookup"><span data-stu-id="72783-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="72783-218">Clique em Olá **membros da equipe** guia.</span><span class="sxs-lookup"><span data-stu-id="72783-218">Click hello **Team Members** tab.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="72783-220">Clique em **ADICIONAR MEMBRO DA EQUIPE**.</span><span class="sxs-lookup"><span data-stu-id="72783-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="72783-222">Saudação de tipo **endereço de Email**, **nome**, e **nome Sur** de um usuário válido, você deseja tooprovision em Olá relacionadas a caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="72783-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="72783-224">Como **Função**, escolha **Administrador do Cliente**.</span><span class="sxs-lookup"><span data-stu-id="72783-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="72783-225">Clique em **CRIAR CONTA**.</span><span class="sxs-lookup"><span data-stu-id="72783-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="72783-226">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="72783-227">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooStatusPage.</span><span class="sxs-lookup"><span data-stu-id="72783-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="72783-229">**tooassign Britta Simon tooStatusPage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="72783-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="72783-230">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="72783-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="72783-232">Na lista de aplicativos hello, selecione **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="72783-232">In hello applications list, select **StatusPage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="72783-234">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="72783-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="72783-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72783-236">Click **Add** button.</span></span> <span data-ttu-id="72783-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72783-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="72783-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="72783-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72783-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72783-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72783-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="72783-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72783-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="72783-242">Testing single sign-on</span></span>

<span data-ttu-id="72783-243">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="72783-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72783-244">Quando você clica em bloco StatusPage Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour StatusPage aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72783-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72783-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="72783-245">Additional resources</span></span>

* [<span data-ttu-id="72783-246">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="72783-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72783-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72783-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

