---
title: "Tutorial: integração do Azure Active Directory com o Humanity | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e humanidade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="29a8b-103">Tutorial: integração do Azure Active Directory com o Humanity</span><span class="sxs-lookup"><span data-stu-id="29a8b-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="29a8b-104">Neste tutorial, você aprenderá como toointegrate humanidade com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="29a8b-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29a8b-105">Integrando humanidade AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29a8b-106">Você pode controlar no AD do Azure que tenha acesso tooHumanity</span><span class="sxs-lookup"><span data-stu-id="29a8b-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="29a8b-107">Você pode habilitar seu usuários tooautomatically get conectado tooHumanity (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29a8b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="29a8b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29a8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a8b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29a8b-110">Prerequisites</span></span>

<span data-ttu-id="29a8b-111">tooconfigure integração do AD do Azure com humanidade, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="29a8b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29a8b-113">Uma assinatura do Humanity habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="29a8b-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29a8b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="29a8b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29a8b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="29a8b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29a8b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="29a8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29a8b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29a8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29a8b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="29a8b-118">Scenario description</span></span>
<span data-ttu-id="29a8b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="29a8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29a8b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="29a8b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29a8b-121">Adicionando humanidade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="29a8b-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="29a8b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="29a8b-123">Adicionando humanidade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="29a8b-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="29a8b-124">integração de saudação tooconfigure da humanidade no AD do Azure, você precisa tooadd humanidade na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="29a8b-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29a8b-125">**tooadd humanidade da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29a8b-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29a8b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="29a8b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29a8b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29a8b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="29a8b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a8b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="29a8b-133">Na caixa de pesquisa hello, digite **humanidade**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-133">In hello search box, type **Humanity**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="29a8b-135">No painel de resultados de saudação, selecione **humanidade**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29a8b-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29a8b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29a8b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Humanity, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="29a8b-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29a8b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em humanidade é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="29a8b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="29a8b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em humanidade precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="29a8b-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="29a8b-141">Humanidade, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a8b-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="29a8b-142">tooconfigure e teste de logon único do AD do Azure com humanidade, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29a8b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="29a8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29a8b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29a8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29a8b-145">**[Criar um usuário de teste humanidade](#creating-a-humanity-test-user)**  -toohave um equivalente do Britta Simon na humanidade que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="29a8b-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29a8b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="29a8b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29a8b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="29a8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29a8b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29a8b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo humanidade.</span><span class="sxs-lookup"><span data-stu-id="29a8b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="29a8b-150">**tooconfigure AD do Azure-logon único com humanidade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29a8b-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="29a8b-151">Em Olá portal do Azure, Olá **humanidade** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="29a8b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="29a8b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="29a8b-155">Em Olá **humanidade domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="29a8b-157">a.</span><span class="sxs-lookup"><span data-stu-id="29a8b-157">a.</span></span> <span data-ttu-id="29a8b-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="29a8b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="29a8b-159">b.</span><span class="sxs-lookup"><span data-stu-id="29a8b-159">b.</span></span> <span data-ttu-id="29a8b-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="29a8b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29a8b-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="29a8b-161">These values are not real.</span></span> <span data-ttu-id="29a8b-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="29a8b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="29a8b-163">Entre em contato com [equipe de suporte de cliente humanidade](https://www.humanity.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="29a8b-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="29a8b-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="29a8b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="29a8b-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="29a8b-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29a8b-168">Em Olá **humanidade configuração** seção, clique em **configurar humanidade** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="29a8b-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="29a8b-169">Saudação de cópia **SAML Single Sign-On URL do serviço e a URL de logout** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="29a8b-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="29a8b-171">Em uma janela do navegador web diferente, faça logon no tooyour **humanidade** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="29a8b-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="29a8b-172">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="29a8b-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="29a8b-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="29a8b-174">Em **Integração**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="29a8b-175">![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29a8b-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="29a8b-176">Em Olá **Single Sign-On** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="29a8b-177">![Logon Único](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="29a8b-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="29a8b-178">a.</span><span class="sxs-lookup"><span data-stu-id="29a8b-178">a.</span></span> <span data-ttu-id="29a8b-179">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="29a8b-180">b.</span><span class="sxs-lookup"><span data-stu-id="29a8b-180">b.</span></span> <span data-ttu-id="29a8b-181">Selecione **Permitir Logon de Senha**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="29a8b-182">c.</span><span class="sxs-lookup"><span data-stu-id="29a8b-182">c.</span></span> <span data-ttu-id="29a8b-183">Saudação de colar **Single Sign-On URL do serviço SAML** valor em Olá **URL do emissor SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="29a8b-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="29a8b-184">d.</span><span class="sxs-lookup"><span data-stu-id="29a8b-184">d.</span></span> <span data-ttu-id="29a8b-185">Saudação de colar **URL de logout** valor em Olá **URL de Logout remoto** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="29a8b-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="29a8b-186">e.</span><span class="sxs-lookup"><span data-stu-id="29a8b-186">e.</span></span> <span data-ttu-id="29a8b-187">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="29a8b-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="29a8b-188">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="29a8b-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="29a8b-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29a8b-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="29a8b-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29a8b-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29a8b-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29a8b-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="29a8b-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29a8b-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="29a8b-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29a8b-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29a8b-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="29a8b-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29a8b-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29a8b-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a8b-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29a8b-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29a8b-204">a.</span><span class="sxs-lookup"><span data-stu-id="29a8b-204">a.</span></span> <span data-ttu-id="29a8b-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29a8b-206">b.</span><span class="sxs-lookup"><span data-stu-id="29a8b-206">b.</span></span> <span data-ttu-id="29a8b-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29a8b-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29a8b-208">c.</span><span class="sxs-lookup"><span data-stu-id="29a8b-208">c.</span></span> <span data-ttu-id="29a8b-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="29a8b-210">d.</span><span class="sxs-lookup"><span data-stu-id="29a8b-210">d.</span></span> <span data-ttu-id="29a8b-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="29a8b-212">Criar um usuário de teste do Humanity</span><span class="sxs-lookup"><span data-stu-id="29a8b-212">Creating a Humanity test user</span></span>

<span data-ttu-id="29a8b-213">Em ordem tooenable AD do Azure usuários toolog em tooHumanity, eles devem ser provisionados no humanidade.</span><span class="sxs-lookup"><span data-stu-id="29a8b-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="29a8b-214">No caso de saudação de humanidade, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="29a8b-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="29a8b-215">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29a8b-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="29a8b-216">Faça logon no tooyour **humanidade** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="29a8b-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="29a8b-217">Clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="29a8b-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="29a8b-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="29a8b-219">Clique em **Equipe**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="29a8b-220">![Equipe](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Equipe")</span><span class="sxs-lookup"><span data-stu-id="29a8b-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="29a8b-221">Em **Ações**, clique em **Adicionar Funcionários**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="29a8b-222">![Adicionar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Adicionar Funcionários")</span><span class="sxs-lookup"><span data-stu-id="29a8b-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="29a8b-223">Em Olá **adicionar funcionários** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="29a8b-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="29a8b-224">![Salvar Funcionários](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvar Funcionários")</span><span class="sxs-lookup"><span data-stu-id="29a8b-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="29a8b-225">a.</span><span class="sxs-lookup"><span data-stu-id="29a8b-225">a.</span></span> <span data-ttu-id="29a8b-226">Saudação de tipo **nome**, **Sobrenome**, e **Email** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="29a8b-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="29a8b-227">b.</span><span class="sxs-lookup"><span data-stu-id="29a8b-227">b.</span></span> <span data-ttu-id="29a8b-228">Clique em **Salvar Funcionários**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="29a8b-229">Você pode usar qualquer ferramenta de criação outros humanidade usuário conta ou APIs fornecidas pelo humanidade tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="29a8b-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="29a8b-230">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="29a8b-231">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHumanity.</span><span class="sxs-lookup"><span data-stu-id="29a8b-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="29a8b-233">**tooassign Britta Simon tooHumanity, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="29a8b-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="29a8b-234">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="29a8b-236">Na lista de aplicativos hello, selecione **humanidade**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-236">In hello applications list, select **Humanity**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="29a8b-238">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="29a8b-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="29a8b-240">Click **Add** button.</span></span> <span data-ttu-id="29a8b-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a8b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="29a8b-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a8b-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29a8b-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a8b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29a8b-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a8b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29a8b-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="29a8b-246">Testing single sign-on</span></span>

<span data-ttu-id="29a8b-247">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a8b-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="29a8b-248">Quando você clica em bloco humanidade Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de humanidade.</span><span class="sxs-lookup"><span data-stu-id="29a8b-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="29a8b-249">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29a8b-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29a8b-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="29a8b-250">Additional resources</span></span>

* [<span data-ttu-id="29a8b-251">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="29a8b-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29a8b-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29a8b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

