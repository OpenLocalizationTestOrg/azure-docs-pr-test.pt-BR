---
title: "Tutorial: Integração do Azure Active Directory com o Veracode | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="74eb3-103">Tutorial: Integração do Active Directory do Azure com o Veracode</span><span class="sxs-lookup"><span data-stu-id="74eb3-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="74eb3-104">Neste tutorial, você aprenderá como toointegrate Veracode com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="74eb3-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74eb3-105">Integrando o Veracode com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="74eb3-106">Você pode controlar no AD do Azure que tenha acesso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="74eb3-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="74eb3-107">Você pode habilitar seu usuários tooautomatically get conectado tooVeracode (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="74eb3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="74eb3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74eb3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74eb3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74eb3-110">Prerequisites</span></span>

<span data-ttu-id="74eb3-111">tooconfigure integração do AD do Azure com o Veracode, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="74eb3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74eb3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74eb3-113">Uma assinatura do Veracode habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="74eb3-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74eb3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="74eb3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74eb3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="74eb3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74eb3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="74eb3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74eb3-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74eb3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74eb3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="74eb3-118">Scenario description</span></span>
<span data-ttu-id="74eb3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="74eb3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74eb3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="74eb3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74eb3-121">Adicionar Veracode da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="74eb3-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="74eb3-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74eb3-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="74eb3-123">Adicionar Veracode da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="74eb3-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="74eb3-124">integração de saudação tooconfigure de Veracode no AD do Azure, você precisa tooadd Veracode da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="74eb3-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="74eb3-125">**tooadd Veracode da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74eb3-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="74eb3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="74eb3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="74eb3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="74eb3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="74eb3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="74eb3-133">Na caixa de pesquisa hello, digite **Veracode**, selecione **Veracode** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="74eb3-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode na lista de resultados de saudação](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="74eb3-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74eb3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="74eb3-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Veracode, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="74eb3-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="74eb3-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Veracode é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="74eb3-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Veracode precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="74eb3-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="74eb3-139">Veracode, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="74eb3-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="74eb3-140">tooconfigure e teste de logon único do AD do Azure com o Veracode, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="74eb3-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="74eb3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="74eb3-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74eb3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74eb3-143">**[Criar um usuário de teste Veracode](#create-a-veracode-test-user)**  -toohave um equivalente do Britta Simon em Veracode é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="74eb3-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="74eb3-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="74eb3-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74eb3-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="74eb3-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="74eb3-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74eb3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="74eb3-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Veracode.</span><span class="sxs-lookup"><span data-stu-id="74eb3-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="74eb3-148">**tooconfigure AD do Azure-logon único com o Veracode, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74eb3-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="74eb3-149">Em Olá portal do Azure, Olá **Veracode** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="74eb3-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="74eb3-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="74eb3-153">Em Olá **Veracode domínio e URLs** seção, o usuário não tem tooperform todas as etapas de como o aplicativo hello previamente já está integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="74eb3-155">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="74eb3-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="74eb3-157">Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooVeracode com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.</span><span class="sxs-lookup"><span data-stu-id="74eb3-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="74eb3-158">Seu aplicativo de Veracode espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens saml** configuração.</span><span class="sxs-lookup"><span data-stu-id="74eb3-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="74eb3-159">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="74eb3-160">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="74eb3-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="74eb3-161">mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="74eb3-162">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="74eb3-162">Attribute Name</span></span> | <span data-ttu-id="74eb3-163">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="74eb3-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="74eb3-164">nome</span><span class="sxs-lookup"><span data-stu-id="74eb3-164">firstname</span></span> |<span data-ttu-id="74eb3-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="74eb3-165">User.givenname</span></span> |
    | <span data-ttu-id="74eb3-166">sobrenome</span><span class="sxs-lookup"><span data-stu-id="74eb3-166">lastname</span></span> |<span data-ttu-id="74eb3-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="74eb3-167">User.surname</span></span> |
    | <span data-ttu-id="74eb3-168">email</span><span class="sxs-lookup"><span data-stu-id="74eb3-168">email</span></span> |<span data-ttu-id="74eb3-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="74eb3-169">User.mail</span></span> |
    
    <span data-ttu-id="74eb3-170">a.</span><span class="sxs-lookup"><span data-stu-id="74eb3-170">a.</span></span> <span data-ttu-id="74eb3-171">Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="74eb3-172">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="74eb3-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="74eb3-173">![Atributos](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="74eb3-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="74eb3-174">b.</span><span class="sxs-lookup"><span data-stu-id="74eb3-174">b.</span></span> <span data-ttu-id="74eb3-175">Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="74eb3-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="74eb3-176">c.</span><span class="sxs-lookup"><span data-stu-id="74eb3-176">c.</span></span> <span data-ttu-id="74eb3-177">Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="74eb3-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="74eb3-178">d.</span><span class="sxs-lookup"><span data-stu-id="74eb3-178">d.</span></span> <span data-ttu-id="74eb3-179">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-179">Click **Ok**.</span></span>

7. <span data-ttu-id="74eb3-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="74eb3-180">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="74eb3-182">Em Olá **Veracode configuração** seção, clique em **configurar Veracode** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="74eb3-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="74eb3-183">Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="74eb3-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuração do Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="74eb3-185">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Veracode como administrador.</span><span class="sxs-lookup"><span data-stu-id="74eb3-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="74eb3-186">No menu de saudação na parte superior de saudação, clique em **configurações**e, em seguida, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="74eb3-187">![Administração](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="74eb3-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="74eb3-188">Clique em Olá **SAML** guia.</span><span class="sxs-lookup"><span data-stu-id="74eb3-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="74eb3-189">Em Olá **configurações do SAML organização** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="74eb3-190">![Administração](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="74eb3-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="74eb3-191">a.</span><span class="sxs-lookup"><span data-stu-id="74eb3-191">a.</span></span>  <span data-ttu-id="74eb3-192">Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="74eb3-193">b.</span><span class="sxs-lookup"><span data-stu-id="74eb3-193">b.</span></span> <span data-ttu-id="74eb3-194">tooupload seu certificado baixado do portal do Azure, clique **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="74eb3-195">c.</span><span class="sxs-lookup"><span data-stu-id="74eb3-195">c.</span></span> <span data-ttu-id="74eb3-196">Selecione **Habilitar Autorregistro**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="74eb3-197">Em Olá **configurações do registro de autoatendimento** seção, executar Olá etapas a seguir e, em seguida, clique em **salvar**:</span><span class="sxs-lookup"><span data-stu-id="74eb3-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="74eb3-198">![Administração](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="74eb3-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="74eb3-199">a.</span><span class="sxs-lookup"><span data-stu-id="74eb3-199">a.</span></span> <span data-ttu-id="74eb3-200">Para **Ativação de Novo Usuário**, selecione **Sem Ativação Necessária**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="74eb3-201">b.</span><span class="sxs-lookup"><span data-stu-id="74eb3-201">b.</span></span> <span data-ttu-id="74eb3-202">Para **Atualizações de Dados do Usuário**, selecione **Dados do Usuário de Preferência do Veracode**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="74eb3-203">c.</span><span class="sxs-lookup"><span data-stu-id="74eb3-203">c.</span></span> <span data-ttu-id="74eb3-204">Para **detalhes de atributos de SAML**, selecione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="74eb3-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="74eb3-205">**Funções de usuário**</span><span class="sxs-lookup"><span data-stu-id="74eb3-205">**User Roles**</span></span>
      * <span data-ttu-id="74eb3-206">**Administrador de políticas**</span><span class="sxs-lookup"><span data-stu-id="74eb3-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="74eb3-207">**Revisor**</span><span class="sxs-lookup"><span data-stu-id="74eb3-207">**Reviewer**</span></span>
      * <span data-ttu-id="74eb3-208">**Orientações de Segurança**</span><span class="sxs-lookup"><span data-stu-id="74eb3-208">**Security Lead**</span></span>
      * <span data-ttu-id="74eb3-209">**Executivo**</span><span class="sxs-lookup"><span data-stu-id="74eb3-209">**Executive**</span></span>
      * <span data-ttu-id="74eb3-210">**Emissor**</span><span class="sxs-lookup"><span data-stu-id="74eb3-210">**Submitter**</span></span>
      * <span data-ttu-id="74eb3-211">**Criador**</span><span class="sxs-lookup"><span data-stu-id="74eb3-211">**Creator**</span></span>
      * <span data-ttu-id="74eb3-212">**Todos os Tipos de Verificação**</span><span class="sxs-lookup"><span data-stu-id="74eb3-212">**All Scan Types**</span></span>
      * <span data-ttu-id="74eb3-213">**Associações de Equipe**</span><span class="sxs-lookup"><span data-stu-id="74eb3-213">**Team Memberships**</span></span>
      * <span data-ttu-id="74eb3-214">**Equipe Padrão**</span><span class="sxs-lookup"><span data-stu-id="74eb3-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="74eb3-215">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="74eb3-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="74eb3-216">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="74eb3-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="74eb3-217">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74eb3-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="74eb3-218">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="74eb3-218">Create an Azure AD test user</span></span>

<span data-ttu-id="74eb3-219">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="74eb3-221">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74eb3-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="74eb3-222">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="74eb3-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="74eb3-224">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="74eb3-226">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="74eb3-228">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="74eb3-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="74eb3-230">a.</span><span class="sxs-lookup"><span data-stu-id="74eb3-230">a.</span></span> <span data-ttu-id="74eb3-231">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74eb3-232">b.</span><span class="sxs-lookup"><span data-stu-id="74eb3-232">b.</span></span> <span data-ttu-id="74eb3-233">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74eb3-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="74eb3-234">c.</span><span class="sxs-lookup"><span data-stu-id="74eb3-234">c.</span></span> <span data-ttu-id="74eb3-235">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="74eb3-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="74eb3-236">d.</span><span class="sxs-lookup"><span data-stu-id="74eb3-236">d.</span></span> <span data-ttu-id="74eb3-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="74eb3-238">Criar um usuário de teste do Veracode</span><span class="sxs-lookup"><span data-stu-id="74eb3-238">Create a Veracode test user</span></span>
<span data-ttu-id="74eb3-239">Em ordem tooenable AD do Azure usuários toolog em Veracode, eles devem ser provisionados no Veracode.</span><span class="sxs-lookup"><span data-stu-id="74eb3-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="74eb3-240">No caso de saudação de Veracode, o provisionamento é uma tarefa automatizada.</span><span class="sxs-lookup"><span data-stu-id="74eb3-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="74eb3-241">Não há nenhum item de ação para você.</span><span class="sxs-lookup"><span data-stu-id="74eb3-241">There is no action item for you.</span></span> <span data-ttu-id="74eb3-242">Os usuários são criados automaticamente se necessário durante a saudação primeiro único tentativa de logon.</span><span class="sxs-lookup"><span data-stu-id="74eb3-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="74eb3-243">Você pode usar qualquer ferramenta de criação outros Veracode usuário conta ou APIs fornecidas pelo Veracode tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb3-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="74eb3-244">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="74eb3-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="74eb3-245">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="74eb3-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="74eb3-247">**tooassign Britta Simon tooVeracode, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="74eb3-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="74eb3-248">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="74eb3-250">Na lista de aplicativos hello, selecione **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-250">In hello applications list, select **Veracode**.</span></span>

    ![link de Veracode Olá na lista de aplicativos Olá](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="74eb3-252">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="74eb3-254">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="74eb3-254">Click **Add** button.</span></span> <span data-ttu-id="74eb3-255">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="74eb3-257">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="74eb3-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="74eb3-258">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74eb3-259">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="74eb3-260">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="74eb3-260">Test single sign-on</span></span>

<span data-ttu-id="74eb3-261">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="74eb3-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="74eb3-262">Quando você clica em bloco Veracode Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Veracode aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74eb3-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="74eb3-263">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="74eb3-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="74eb3-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="74eb3-264">Additional resources</span></span>

* [<span data-ttu-id="74eb3-265">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="74eb3-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74eb3-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74eb3-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

