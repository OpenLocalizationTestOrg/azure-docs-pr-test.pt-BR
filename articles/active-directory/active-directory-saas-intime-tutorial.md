---
title: "Tutorial: Integração do Azure Active Directory ao InTime | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="08390-103">Tutorial: Integração do Azure Active Directory ao InTime</span><span class="sxs-lookup"><span data-stu-id="08390-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="08390-104">Neste tutorial, você aprenderá como toointegrate InTime com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="08390-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08390-105">Integrando InTime com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="08390-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08390-106">Você pode controlar no AD do Azure que tenha acesso tooInTime.</span><span class="sxs-lookup"><span data-stu-id="08390-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="08390-107">Você pode habilitar seu usuários tooautomatically get conectado tooInTime (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08390-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="08390-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08390-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="08390-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08390-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08390-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08390-110">Prerequisites</span></span>

<span data-ttu-id="08390-111">tooconfigure integração do AD do Azure com InTime, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="08390-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="08390-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08390-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08390-113">Uma assinatura habilitada para logon único do InTime</span><span class="sxs-lookup"><span data-stu-id="08390-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08390-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="08390-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08390-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="08390-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08390-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="08390-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08390-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08390-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08390-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="08390-118">Scenario description</span></span>
<span data-ttu-id="08390-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="08390-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08390-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="08390-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08390-121">Adicionando InTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08390-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="08390-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08390-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="08390-123">Adicionando InTime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08390-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="08390-124">integração de saudação tooconfigure de InTime no AD do Azure, você precisa tooadd InTime da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="08390-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08390-125">**tooadd InTime da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08390-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08390-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="08390-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="08390-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="08390-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08390-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08390-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="08390-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08390-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="08390-133">Na caixa de pesquisa hello, digite **InTime**, selecione **InTime** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="08390-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![InTime na lista de resultados de saudação](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="08390-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08390-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="08390-136">Nesta seção, você configura e testa o logon único do Azure AD com o InTime, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="08390-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08390-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em InTime é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08390-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="08390-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em InTime precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="08390-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="08390-139">InTime, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="08390-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08390-140">tooconfigure e teste de logon único do AD do Azure com InTime, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="08390-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08390-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="08390-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08390-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08390-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08390-143">**[Criar um usuário de teste InTime](#create-a-intime-test-user)**  -toohave um equivalente do Britta Simon em InTime é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="08390-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08390-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="08390-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08390-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="08390-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="08390-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08390-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="08390-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="08390-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="08390-148">**tooconfigure AD do Azure-logon único com InTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08390-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="08390-149">Em Olá portal do Azure, Olá **InTime** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="08390-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="08390-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="08390-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="08390-153">Em Olá **InTime de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08390-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="08390-155">a.</span><span class="sxs-lookup"><span data-stu-id="08390-155">a.</span></span> <span data-ttu-id="08390-156">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="08390-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="08390-157">b.</span><span class="sxs-lookup"><span data-stu-id="08390-157">b.</span></span> <span data-ttu-id="08390-158">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="08390-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="08390-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="08390-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="08390-161">Seu aplicativo InTime espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="08390-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="08390-162">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="08390-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="08390-163">Olá valor padrão de **identificador de usuário** é **User** mas InTime espera este toobe mapeada com o endereço de email do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="08390-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="08390-164">Para que você pode usar **user.mail** de atributo na lista de saudação ou usar o valor do atributo apropriado Olá com base na configuração de sua organização</span><span class="sxs-lookup"><span data-stu-id="08390-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Configurar Atributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="08390-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="08390-166">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="08390-168">Em Olá **configuração InTime** seção, clique em **configurar InTime** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="08390-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="08390-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="08390-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="08390-171">tooconfigure logon único no **InTime** lado, você precisa toosend Olá baixado **Metadata XML**, **URL de logout e Single Sign-On URL do serviço SAML** muito[a equipe de suporte inTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="08390-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="08390-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="08390-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="08390-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="08390-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08390-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="08390-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08390-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08390-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="08390-176">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08390-176">Create an Azure AD test user</span></span>

<span data-ttu-id="08390-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08390-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="08390-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08390-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08390-180">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="08390-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="08390-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="08390-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="08390-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08390-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="08390-186">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08390-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="08390-188">a.</span><span class="sxs-lookup"><span data-stu-id="08390-188">a.</span></span> <span data-ttu-id="08390-189">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08390-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08390-190">b.</span><span class="sxs-lookup"><span data-stu-id="08390-190">b.</span></span> <span data-ttu-id="08390-191">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08390-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="08390-192">c.</span><span class="sxs-lookup"><span data-stu-id="08390-192">c.</span></span> <span data-ttu-id="08390-193">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="08390-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="08390-194">d.</span><span class="sxs-lookup"><span data-stu-id="08390-194">d.</span></span> <span data-ttu-id="08390-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08390-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="08390-196">Criar um usuário de teste do InTime</span><span class="sxs-lookup"><span data-stu-id="08390-196">Create a InTime test user</span></span>

<span data-ttu-id="08390-197">Nesta seção, você cria um usuário chamado Brenda Fernandes no InTime.</span><span class="sxs-lookup"><span data-stu-id="08390-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="08390-198">Trabalhar com [a equipe de suporte InTime](mailto:hdollard@intimesoft.com) tooadd usuários de saudação na plataforma InTime hello.</span><span class="sxs-lookup"><span data-stu-id="08390-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="08390-199">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="08390-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="08390-200">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08390-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="08390-201">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooInTime.</span><span class="sxs-lookup"><span data-stu-id="08390-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="08390-203">**tooassign Britta Simon tooInTime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08390-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="08390-204">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08390-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="08390-206">Na lista de aplicativos hello, selecione **InTime**.</span><span class="sxs-lookup"><span data-stu-id="08390-206">In hello applications list, select **InTime**.</span></span>

    ![Olá InTime link na lista de aplicativos Olá](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="08390-208">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="08390-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="08390-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08390-210">Click **Add** button.</span></span> <span data-ttu-id="08390-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08390-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="08390-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="08390-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08390-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08390-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08390-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08390-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="08390-216">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="08390-216">Test single sign-on</span></span>

<span data-ttu-id="08390-217">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="08390-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="08390-218">Quando você clica em bloco InTime Olá em Olá painel de acesso, você deve obter a página de logon de saudação do seu aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="08390-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="08390-219">Clique em Olá **Login** botão, uma série de IdPs será exibido em uma lista de botões.</span><span class="sxs-lookup"><span data-stu-id="08390-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="08390-220">Clique em **nome IDP** determinado por [a equipe de suporte InTime](mailto:hdollard@intimesoft.com) toologin em seu aplicativo InTime.</span><span class="sxs-lookup"><span data-stu-id="08390-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="08390-221">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08390-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="08390-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08390-222">Additional resources</span></span>

* [<span data-ttu-id="08390-223">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="08390-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08390-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08390-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

