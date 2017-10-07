---
title: "Tutorial: integração do Azure Active Directory com Druva | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="7c63c-103">Tutorial: integração do Azure Active Directory com o Druva</span><span class="sxs-lookup"><span data-stu-id="7c63c-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="7c63c-104">Neste tutorial, você aprenderá como toointegrate Druva com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7c63c-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c63c-105">Integrando o Druva com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7c63c-106">Você pode controlar no AD do Azure que tenha acesso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="7c63c-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="7c63c-107">Você pode habilitar seu usuários tooautomatically get conectado tooDruva (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c63c-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7c63c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c63c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7c63c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c63c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c63c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c63c-110">Prerequisites</span></span>

<span data-ttu-id="7c63c-111">tooconfigure integração do AD do Azure com o Druva, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="7c63c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c63c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c63c-113">Uma assinatura habilitada para logon único do Druva</span><span class="sxs-lookup"><span data-stu-id="7c63c-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c63c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7c63c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c63c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c63c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c63c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c63c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c63c-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c63c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c63c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c63c-118">Scenario description</span></span>
<span data-ttu-id="7c63c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c63c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c63c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7c63c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c63c-121">Adicionando Druva da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7c63c-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="7c63c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c63c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="7c63c-123">Adicionando Druva da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7c63c-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="7c63c-124">integração de saudação tooconfigure do Druva no AD do Azure, você precisa tooadd Druva da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7c63c-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7c63c-125">**tooadd Druva da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c63c-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c63c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7c63c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="7c63c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7c63c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="7c63c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="7c63c-133">Na caixa de pesquisa hello, digite **Druva**, selecione **Druva** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7c63c-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva na lista de resultados de saudação](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7c63c-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c63c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7c63c-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Druva, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7c63c-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c63c-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Druva é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c63c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="7c63c-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Druva precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7c63c-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="7c63c-139">No Druva, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c63c-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7c63c-140">tooconfigure e teste de logon único do AD do Azure com o Druva, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7c63c-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7c63c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7c63c-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c63c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c63c-143">**[Criar um usuário de teste do Druva](#create-a-druva-test-user)**  -toohave um equivalente do Britta Simon no Druva é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7c63c-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c63c-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7c63c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c63c-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7c63c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7c63c-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c63c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7c63c-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu aplicativo Druva.</span><span class="sxs-lookup"><span data-stu-id="7c63c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="7c63c-148">**tooconfigure AD do Azure-logon único com o Druva, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c63c-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c63c-149">Em Olá portal do Azure, Olá **Druva** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="7c63c-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7c63c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="7c63c-153">Em Olá **Druva domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="7c63c-155">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="7c63c-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="7c63c-156">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c63c-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="7c63c-158">Seu aplicativo Druva espera as asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuração.</span><span class="sxs-lookup"><span data-stu-id="7c63c-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="7c63c-160">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, como mostrado no hello anterior a imagem e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="7c63c-161">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="7c63c-161">Attribute Name</span></span>      | <span data-ttu-id="7c63c-162">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="7c63c-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7c63c-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="7c63c-163">insync\_auth\_token</span></span> |<span data-ttu-id="7c63c-164">Insira o valor gerado do token Olá</span><span class="sxs-lookup"><span data-stu-id="7c63c-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="7c63c-165">a.</span><span class="sxs-lookup"><span data-stu-id="7c63c-165">a.</span></span> <span data-ttu-id="7c63c-166">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="7c63c-169">b.</span><span class="sxs-lookup"><span data-stu-id="7c63c-169">b.</span></span> <span data-ttu-id="7c63c-170">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="7c63c-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="7c63c-171">c.</span><span class="sxs-lookup"><span data-stu-id="7c63c-171">c.</span></span> <span data-ttu-id="7c63c-172">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="7c63c-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="7c63c-173">Olá valor do token gerado é explicado posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="7c63c-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="7c63c-174">d.</span><span class="sxs-lookup"><span data-stu-id="7c63c-174">d.</span></span> <span data-ttu-id="7c63c-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="7c63c-176">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7c63c-176">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7c63c-178">Em Olá **Druva configuração** seção, clique em **configurar Druva** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="7c63c-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7c63c-179">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7c63c-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="7c63c-181">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Druva como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7c63c-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="7c63c-182">Vá muito**gerenciar \> configurações**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="7c63c-183">![Configurações](./media/active-directory-saas-druva-tutorial/ic795091.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="7c63c-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="7c63c-184">Na caixa de diálogo de configurações de logon único hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="7c63c-185">![Configurações de Logon Único](./media/active-directory-saas-druva-tutorial/ic795092.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="7c63c-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="7c63c-186">a.</span><span class="sxs-lookup"><span data-stu-id="7c63c-186">a.</span></span> <span data-ttu-id="7c63c-187">Colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7c63c-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="7c63c-188">b.</span><span class="sxs-lookup"><span data-stu-id="7c63c-188">b.</span></span> <span data-ttu-id="7c63c-189">Colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7c63c-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="7c63c-190">c.</span><span class="sxs-lookup"><span data-stu-id="7c63c-190">c.</span></span> <span data-ttu-id="7c63c-191">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado do provedor de ID** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="7c63c-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="7c63c-192">d.</span><span class="sxs-lookup"><span data-stu-id="7c63c-192">d.</span></span> <span data-ttu-id="7c63c-193">Olá tooopen **configurações** , clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="7c63c-194">Em Olá **configurações** , clique em **gerar Token do SSO**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="7c63c-195">![Configurações](./media/active-directory-saas-druva-tutorial/ic795093.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="7c63c-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="7c63c-196">Em Olá **único logon no Token de autenticação** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="7c63c-197">![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")</span><span class="sxs-lookup"><span data-stu-id="7c63c-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="7c63c-198">a.</span><span class="sxs-lookup"><span data-stu-id="7c63c-198">a.</span></span> <span data-ttu-id="7c63c-199">Clique em **cópia**, colar copiados valor em Olá **valor** textbox em Olá **Adicionar atributo** seção.</span><span class="sxs-lookup"><span data-stu-id="7c63c-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="7c63c-200">b.</span><span class="sxs-lookup"><span data-stu-id="7c63c-200">b.</span></span> <span data-ttu-id="7c63c-201">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="7c63c-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="7c63c-202">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7c63c-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7c63c-203">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7c63c-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7c63c-204">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c63c-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7c63c-205">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c63c-205">Create an Azure AD test user</span></span>

<span data-ttu-id="7c63c-206">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c63c-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7c63c-208">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c63c-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c63c-209">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="7c63c-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7c63c-211">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7c63c-213">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7c63c-215">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7c63c-217">a.</span><span class="sxs-lookup"><span data-stu-id="7c63c-217">a.</span></span> <span data-ttu-id="7c63c-218">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c63c-219">b.</span><span class="sxs-lookup"><span data-stu-id="7c63c-219">b.</span></span> <span data-ttu-id="7c63c-220">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c63c-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7c63c-221">c.</span><span class="sxs-lookup"><span data-stu-id="7c63c-221">c.</span></span> <span data-ttu-id="7c63c-222">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="7c63c-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7c63c-223">d.</span><span class="sxs-lookup"><span data-stu-id="7c63c-223">d.</span></span> <span data-ttu-id="7c63c-224">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="7c63c-225">Criar um usuário de teste do Druva</span><span class="sxs-lookup"><span data-stu-id="7c63c-225">Create a Druva test user</span></span>

<span data-ttu-id="7c63c-226">Ordem tooenable AD do Azure usuários toolog em tooDruva, eles devem ser provisionados no Druva.</span><span class="sxs-lookup"><span data-stu-id="7c63c-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="7c63c-227">No caso de saudação do Druva, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7c63c-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="7c63c-228">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c63c-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c63c-229">Faça logon no tooyour **Druva** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="7c63c-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="7c63c-230">Vá muito**gerenciar \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="7c63c-231">![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795097.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="7c63c-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="7c63c-232">Clique em **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="7c63c-233">![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795098.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="7c63c-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="7c63c-234">Na caixa de diálogo de criar novo usuário hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c63c-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="7c63c-235">![Criar Novo Usuário](./media/active-directory-saas-druva-tutorial/ic795099.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="7c63c-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="7c63c-236">a.</span><span class="sxs-lookup"><span data-stu-id="7c63c-236">a.</span></span> <span data-ttu-id="7c63c-237">Em Olá **endereço de Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7c63c-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="7c63c-238">b.</span><span class="sxs-lookup"><span data-stu-id="7c63c-238">b.</span></span> <span data-ttu-id="7c63c-239">Em Olá **nome** caixa de texto, insira o nome de saudação do usuário, como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="7c63c-240">c.</span><span class="sxs-lookup"><span data-stu-id="7c63c-240">c.</span></span> <span data-ttu-id="7c63c-241">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="7c63c-242">Você pode usar qualquer ferramenta de criação outros Druva usuário conta ou APIs fornecidas pelo Druva tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c63c-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7c63c-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c63c-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7c63c-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDruva.</span><span class="sxs-lookup"><span data-stu-id="7c63c-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="7c63c-246">**tooassign Britta Simon tooDruva, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7c63c-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7c63c-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7c63c-249">Na lista de aplicativos hello, selecione **Druva**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-249">In hello applications list, select **Druva**.</span></span>

    ![link do Druva Olá na lista de aplicativos Olá](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="7c63c-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="7c63c-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7c63c-253">Click **Add** button.</span></span> <span data-ttu-id="7c63c-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="7c63c-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c63c-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7c63c-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c63c-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7c63c-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7c63c-259">Test single sign-on</span></span>

<span data-ttu-id="7c63c-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c63c-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7c63c-261">Quando você clica em bloco Druva Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Druva aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c63c-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="7c63c-262">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c63c-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7c63c-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c63c-263">Additional resources</span></span>

* [<span data-ttu-id="7c63c-264">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7c63c-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c63c-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c63c-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

