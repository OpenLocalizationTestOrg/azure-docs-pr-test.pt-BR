---
title: "Tutorial: integração do Azure Active Directory com o BeeLine | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="f7caf-103">Tutorial: Integração do Azure Active Directory ao Beeline</span><span class="sxs-lookup"><span data-stu-id="f7caf-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="f7caf-104">Neste tutorial, você aprenderá como toointegrate BeeLine com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f7caf-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7caf-105">Integrando BeeLine com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f7caf-106">Você pode controlar no AD do Azure que tenha acesso tooBeeLine</span><span class="sxs-lookup"><span data-stu-id="f7caf-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="f7caf-107">Você pode habilitar seu usuários tooautomatically get conectado tooBeeLine (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7caf-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f7caf-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7caf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7caf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f7caf-110">Prerequisites</span></span>

<span data-ttu-id="f7caf-111">tooconfigure integração do AD do Azure com BeeLine, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="f7caf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7caf-113">Uma assinatura habilitada para logon único do BeeLine</span><span class="sxs-lookup"><span data-stu-id="f7caf-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7caf-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f7caf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7caf-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f7caf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7caf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f7caf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7caf-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7caf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7caf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f7caf-118">Scenario description</span></span>
<span data-ttu-id="f7caf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f7caf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7caf-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f7caf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7caf-121">Adicionando BeeLine da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f7caf-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="f7caf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="f7caf-123">Adicionando BeeLine da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f7caf-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="f7caf-124">integração de saudação tooconfigure de BeeLine no AD do Azure, você precisa tooadd BeeLine da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f7caf-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f7caf-125">**tooadd BeeLine da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7caf-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7caf-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f7caf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7caf-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f7caf-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f7caf-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7caf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f7caf-133">Na caixa de pesquisa hello, digite **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-133">In hello search box, type **BeeLine**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="f7caf-135">No painel de resultados de saudação, selecione **BeeLine**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f7caf-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7caf-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7caf-138">Nesta seção, você configurará e testará o logon único do Azure AD com o BeeLine, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f7caf-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f7caf-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em BeeLine é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7caf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="f7caf-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em BeeLine precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f7caf-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="f7caf-141">BeeLine, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f7caf-142">tooconfigure e teste de logon único do AD do Azure com BeeLine, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f7caf-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f7caf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f7caf-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7caf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7caf-145">**[Criar um usuário de teste BeeLine](#creating-a-beeline-test-user)**  -toohave um equivalente do Britta Simon em BeeLine é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7caf-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7caf-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f7caf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7caf-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f7caf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7caf-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7caf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7caf-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BeeLine.</span><span class="sxs-lookup"><span data-stu-id="f7caf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="f7caf-150">**tooconfigure AD do Azure-logon único com BeeLine, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7caf-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7caf-151">Em Olá portal do Azure, Olá **BeeLine** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f7caf-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f7caf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="f7caf-155">Em Olá **BeeLine domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="f7caf-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7caf-157">a.</span></span> <span data-ttu-id="f7caf-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="f7caf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="f7caf-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7caf-159">b.</span></span> <span data-ttu-id="f7caf-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="f7caf-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f7caf-161">These values are not real.</span></span> <span data-ttu-id="f7caf-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f7caf-163">Entre em contato com [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f7caf-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="f7caf-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f7caf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="f7caf-166">Seu aplicativo de Beeline espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="f7caf-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f7caf-167">Trabalhe com [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooidentify primeiro Olá identificador de usuário correta que será mapeada para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f7caf-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="f7caf-168">Também siga as diretrizes de saudação do [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) sobre Olá atributo que quiserem toouse para que esse mapeamento.</span><span class="sxs-lookup"><span data-stu-id="f7caf-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="f7caf-169">Você pode gerenciar o valor deste atributo Olá de saudação **atributos de usuário** guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f7caf-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="f7caf-170">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f7caf-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="f7caf-171">Aqui nós mapeou hello **identificador de usuário** declarações com hello **userprincipalname** atributo, que fornece a ID de usuário exclusivo, que será enviada toohello Beeline aplicativo hello cada SAML com êxito Resposta.</span><span class="sxs-lookup"><span data-stu-id="f7caf-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="f7caf-173">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f7caf-173">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f7caf-175">Em Olá **BeeLine configuração** seção, clique em **configurar BeeLine** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="f7caf-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f7caf-176">Saudação de cópia **URL de logout** e **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f7caf-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="f7caf-178">tooconfigure logon único no **BeeLine** lado, você precisa toosend Olá baixado **Metadata XML** e **ID da entidade SAML**, **URL de logout**muito[a equipe de suporte BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="f7caf-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="f7caf-179">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f7caf-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f7caf-180">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f7caf-181">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7caf-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7caf-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7caf-183">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7caf-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f7caf-185">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7caf-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7caf-186">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f7caf-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7caf-188">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7caf-190">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7caf-192">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7caf-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7caf-194">a.</span><span class="sxs-lookup"><span data-stu-id="f7caf-194">a.</span></span> <span data-ttu-id="f7caf-195">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7caf-196">b.</span><span class="sxs-lookup"><span data-stu-id="f7caf-196">b.</span></span> <span data-ttu-id="f7caf-197">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f7caf-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7caf-198">c.</span><span class="sxs-lookup"><span data-stu-id="f7caf-198">c.</span></span> <span data-ttu-id="f7caf-199">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f7caf-200">d.</span><span class="sxs-lookup"><span data-stu-id="f7caf-200">d.</span></span> <span data-ttu-id="f7caf-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="f7caf-202">Criação de um usuário de teste do BeeLine</span><span class="sxs-lookup"><span data-stu-id="f7caf-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="f7caf-203">Nesta seção, você criará um usuário chamado Brenda Fernandes no Beeline.</span><span class="sxs-lookup"><span data-stu-id="f7caf-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="f7caf-204">Aplicativo de beeline precisa de todas as toobe de usuários Olá provisionado no aplicativo hello antes de fazer logon único.</span><span class="sxs-lookup"><span data-stu-id="f7caf-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="f7caf-205">Para trabalhar com hello [a equipe de suporte BeeLine](https://www.beeline.com/contact-us/) tooprovision todos esses usuários para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f7caf-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f7caf-206">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f7caf-207">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBeeLine.</span><span class="sxs-lookup"><span data-stu-id="f7caf-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f7caf-209">**tooassign Britta Simon tooBeeLine, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7caf-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7caf-210">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f7caf-212">Na lista de aplicativos hello, selecione **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-212">In hello applications list, select **BeeLine**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="f7caf-214">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f7caf-216">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7caf-216">Click **Add** button.</span></span> <span data-ttu-id="f7caf-217">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7caf-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f7caf-219">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f7caf-220">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7caf-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7caf-221">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7caf-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7caf-222">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f7caf-222">Testing single sign-on</span></span>

<span data-ttu-id="f7caf-223">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7caf-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="f7caf-224">Quando você clica em bloco Beeline Olá Olá painel de acesso, você deve obter o aplicativo de Beeline tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="f7caf-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7caf-225">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f7caf-225">Additional resources</span></span>

* [<span data-ttu-id="f7caf-226">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f7caf-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7caf-227">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7caf-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

