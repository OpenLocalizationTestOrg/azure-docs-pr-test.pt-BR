---
title: "Tutorial: Integração do Azure Active Directory ao Litmos | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="4d091-103">Tutorial: Integração do Active Directory do Azure ao Litmos</span><span class="sxs-lookup"><span data-stu-id="4d091-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="4d091-104">Neste tutorial, você aprenderá como toointegrate Litmos com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4d091-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d091-105">Integrando Litmos com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4d091-106">Você pode controlar no AD do Azure que tenha acesso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="4d091-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="4d091-107">Você pode habilitar seus usuários tooautomatically get conectado tooLitmos (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d091-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4d091-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d091-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4d091-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d091-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d091-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d091-110">Prerequisites</span></span>

<span data-ttu-id="4d091-111">tooconfigure integração do AD do Azure com Litmos, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="4d091-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d091-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d091-113">Uma assinatura habilitada para logon único do Litmos</span><span class="sxs-lookup"><span data-stu-id="4d091-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d091-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4d091-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d091-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4d091-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d091-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4d091-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d091-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d091-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d091-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4d091-118">Scenario description</span></span>
<span data-ttu-id="4d091-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4d091-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d091-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4d091-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d091-121">Adicionando Litmos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4d091-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="4d091-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d091-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="4d091-123">Adicionando Litmos da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4d091-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="4d091-124">integração de saudação tooconfigure de Litmos no AD do Azure, você precisa tooadd Litmos da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4d091-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4d091-125">**tooadd Litmos da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4d091-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d091-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4d091-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="4d091-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4d091-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4d091-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4d091-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="4d091-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="4d091-133">Na caixa de pesquisa hello, digite **Litmos**, selecione **Litmos** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4d091-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos na lista de resultados de saudação](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4d091-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d091-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4d091-136">Nesta seção, você configura e testa o logon único do Azure AD com o Litmos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4d091-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4d091-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Litmos é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d091-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="4d091-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Litmos precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4d091-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="4d091-139">Litmos, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d091-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4d091-140">tooconfigure e teste de logon único do AD do Azure com Litmos, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4d091-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4d091-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4d091-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d091-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d091-143">**[Criar um usuário de teste Litmos](#create-a-litmos-test-user)**  -toohave um equivalente do Britta Simon em Litmos é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4d091-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d091-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4d091-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d091-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4d091-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4d091-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d091-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4d091-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Litmos.</span><span class="sxs-lookup"><span data-stu-id="4d091-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="4d091-148">**tooconfigure AD do Azure-logon único com Litmos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4d091-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d091-149">Em Olá portal do Azure, Olá **Litmos** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4d091-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="4d091-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4d091-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="4d091-153">Em Olá **Litmos domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="4d091-155">a.</span><span class="sxs-lookup"><span data-stu-id="4d091-155">a.</span></span> <span data-ttu-id="4d091-156">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="4d091-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="4d091-157">b.</span><span class="sxs-lookup"><span data-stu-id="4d091-157">b.</span></span> <span data-ttu-id="4d091-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="4d091-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d091-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4d091-159">These values are not real.</span></span> <span data-ttu-id="4d091-160">Atualizar esses valores com hello real identificador URL de resposta e, que é explicado posteriormente no tutorial ou entre em contato com [Litmos equipe de suporte](https://www.litmos.com/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4d091-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="4d091-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4d091-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="4d091-163">Como parte da configuração de saudação, você precisa Olá toocustomize **atributos de tokens SAML** para seu aplicativo Litmos.</span><span class="sxs-lookup"><span data-stu-id="4d091-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Seção Atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="4d091-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="4d091-165">Attribute Name</span></span>   | <span data-ttu-id="4d091-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="4d091-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="4d091-167">Nome</span><span class="sxs-lookup"><span data-stu-id="4d091-167">FirstName</span></span> |<span data-ttu-id="4d091-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4d091-168">user.givenname</span></span> |
    | <span data-ttu-id="4d091-169">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="4d091-169">LastName</span></span>  |<span data-ttu-id="4d091-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="4d091-170">user.surname</span></span> |
    | <span data-ttu-id="4d091-171">Email</span><span class="sxs-lookup"><span data-stu-id="4d091-171">Email</span></span> |<span data-ttu-id="4d091-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="4d091-172">user.mail</span></span> |

    <span data-ttu-id="4d091-173">a.</span><span class="sxs-lookup"><span data-stu-id="4d091-173">a.</span></span> <span data-ttu-id="4d091-174">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Caixa de diálogo Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4d091-177">b.</span><span class="sxs-lookup"><span data-stu-id="4d091-177">b.</span></span> <span data-ttu-id="4d091-178">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="4d091-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4d091-179">c.</span><span class="sxs-lookup"><span data-stu-id="4d091-179">c.</span></span> <span data-ttu-id="4d091-180">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="4d091-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4d091-181">d.</span><span class="sxs-lookup"><span data-stu-id="4d091-181">d.</span></span> <span data-ttu-id="4d091-182">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d091-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="4d091-183">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4d091-183">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4d091-185">Em uma janela de navegador diferente, site da empresa Litmos tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="4d091-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="4d091-186">Na barra de navegação Olá no lado esquerdo do hello, clique em **contas**.</span><span class="sxs-lookup"><span data-stu-id="4d091-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Seção Contas no lado do aplicativo][22] 

9. <span data-ttu-id="4d091-188">Clique em Olá **integrações** guia.</span><span class="sxs-lookup"><span data-stu-id="4d091-188">Click hello **Integrations** tab.</span></span>
   
    ![Guia Integração][23] 

10. <span data-ttu-id="4d091-190">Em Olá **integrações** guia, role para baixo demais**integrações do 3ª parte**e, em seguida, clique em **SAML 2.0** guia.</span><span class="sxs-lookup"><span data-stu-id="4d091-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Seção SAML 2.0][24] 

11. <span data-ttu-id="4d091-192">Copiar valor Olá **Olá ponto de extremidade do SAML para litmos é:** e cole-a saudação **URL de resposta** textbox em Olá **Litmos domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d091-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Ponto de extremidade SAML][26] 

12. <span data-ttu-id="4d091-194">No seu **Litmos** aplicativo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Aplicativo Litmos][25] 
     
     <span data-ttu-id="4d091-196">a.</span><span class="sxs-lookup"><span data-stu-id="4d091-196">a.</span></span> <span data-ttu-id="4d091-197">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="4d091-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="4d091-198">b.</span><span class="sxs-lookup"><span data-stu-id="4d091-198">b.</span></span> <span data-ttu-id="4d091-199">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509 de SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4d091-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="4d091-200">c.</span><span class="sxs-lookup"><span data-stu-id="4d091-200">c.</span></span> <span data-ttu-id="4d091-201">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="4d091-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4d091-202">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4d091-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4d091-203">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4d091-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4d091-204">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d091-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4d091-205">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d091-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4d091-206">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d091-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="4d091-208">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4d091-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d091-209">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="4d091-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4d091-211">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4d091-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4d091-213">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4d091-215">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d091-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4d091-217">a.</span><span class="sxs-lookup"><span data-stu-id="4d091-217">a.</span></span> <span data-ttu-id="4d091-218">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4d091-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d091-219">b.</span><span class="sxs-lookup"><span data-stu-id="4d091-219">b.</span></span> <span data-ttu-id="4d091-220">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4d091-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4d091-221">c.</span><span class="sxs-lookup"><span data-stu-id="4d091-221">c.</span></span> <span data-ttu-id="4d091-222">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="4d091-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4d091-223">d.</span><span class="sxs-lookup"><span data-stu-id="4d091-223">d.</span></span> <span data-ttu-id="4d091-224">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4d091-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="4d091-225">Criar um usuário de teste do Litmos</span><span class="sxs-lookup"><span data-stu-id="4d091-225">Create a Litmos test user</span></span>

<span data-ttu-id="4d091-226">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Litmos.</span><span class="sxs-lookup"><span data-stu-id="4d091-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="4d091-227">Olá Litmos aplicativo suporta Just-in-Time de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="4d091-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="4d091-228">Isso significa que, uma conta de usuário é criada automaticamente se necessário durante uma tentativa de tooaccess hello, o aplicativo usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d091-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="4d091-229">**toocreate um usuário chamado Britta Simon no Litmos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4d091-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d091-230">Em uma janela de navegador diferente, site da empresa Litmos tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="4d091-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="4d091-231">Na barra de navegação Olá no lado esquerdo do hello, clique em **contas**.</span><span class="sxs-lookup"><span data-stu-id="4d091-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Seção Contas no lado do aplicativo][22] 

3. <span data-ttu-id="4d091-233">Clique em Olá **integrações** guia.</span><span class="sxs-lookup"><span data-stu-id="4d091-233">Click hello **Integrations** tab.</span></span>
   
    ![Guia Integrações][23] 

4. <span data-ttu-id="4d091-235">Em Olá **integrações** guia, role para baixo demais**integrações do 3ª parte**e, em seguida, clique em **SAML 2.0** guia.</span><span class="sxs-lookup"><span data-stu-id="4d091-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="4d091-237">Selecione **Gerar Usuários Automaticamente**</span><span class="sxs-lookup"><span data-stu-id="4d091-237">Select **Autogenerate Users**</span></span>
   
    ![Gerar usuários automaticamente][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4d091-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d091-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4d091-240">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="4d091-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="4d091-242">**tooassign Britta Simon tooLitmos, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4d091-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4d091-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4d091-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4d091-245">Na lista de aplicativos hello, selecione **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="4d091-245">In hello applications list, select **Litmos**.</span></span>

    ![link de Litmos Olá na lista de aplicativos Olá](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="4d091-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d091-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="4d091-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4d091-249">Click **Add** button.</span></span> <span data-ttu-id="4d091-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="4d091-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d091-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4d091-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d091-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d091-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4d091-255">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4d091-255">Test single sign-on</span></span>

<span data-ttu-id="4d091-256">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4d091-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4d091-257">Quando você clica em Olá Litmos bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Litmos aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d091-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d091-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4d091-258">Additional resources</span></span>

* [<span data-ttu-id="4d091-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4d091-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d091-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d091-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

