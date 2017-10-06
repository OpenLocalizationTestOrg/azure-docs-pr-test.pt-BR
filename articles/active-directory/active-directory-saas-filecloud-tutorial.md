---
title: "Tutorial: integração do Azure Active Directory ao FileCloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="6f0be-103">Tutorial: integração do Azure Active Directory ao FileCloud</span><span class="sxs-lookup"><span data-stu-id="6f0be-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="6f0be-104">Neste tutorial, você aprenderá como toointegrate FileCloud com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="6f0be-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f0be-105">Integrando FileCloud com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f0be-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f0be-106">Você pode controlar no AD do Azure que tenha acesso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="6f0be-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="6f0be-107">Você pode habilitar seu usuários tooautomatically get conectado tooFileCloud (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0be-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6f0be-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0be-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6f0be-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f0be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f0be-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6f0be-110">Prerequisites</span></span>

<span data-ttu-id="6f0be-111">tooconfigure integração do AD do Azure com FileCloud, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f0be-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="6f0be-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6f0be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f0be-113">Uma assinatura habilitada para logon único do FileCloud</span><span class="sxs-lookup"><span data-stu-id="6f0be-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f0be-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6f0be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f0be-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6f0be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f0be-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6f0be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f0be-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f0be-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f0be-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6f0be-118">Scenario description</span></span>
<span data-ttu-id="6f0be-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6f0be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f0be-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="6f0be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f0be-121">Adicionando FileCloud da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6f0be-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="6f0be-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6f0be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="6f0be-123">Adicionando FileCloud da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="6f0be-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="6f0be-124">integração de saudação tooconfigure de FileCloud no AD do Azure, você precisa tooadd FileCloud da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6f0be-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f0be-125">**tooadd FileCloud da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6f0be-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f0be-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="6f0be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="6f0be-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f0be-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="6f0be-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="6f0be-133">Na caixa de pesquisa hello, digite **FileCloud**, selecione **FileCloud** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f0be-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud na lista de resultados de saudação](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6f0be-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f0be-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6f0be-136">Nesta seção, você configura e testa o logon único do Azure AD com o FileCloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6f0be-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f0be-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FileCloud é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0be-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="6f0be-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FileCloud precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6f0be-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="6f0be-139">FileCloud, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f0be-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f0be-140">tooconfigure e teste de logon único do AD do Azure com FileCloud, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f0be-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f0be-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6f0be-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f0be-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f0be-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f0be-143">**[Criar um usuário de teste FileCloud](#create-a-filecloud-test-user)**  -toohave um equivalente do Britta Simon em FileCloud é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="6f0be-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f0be-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="6f0be-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f0be-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="6f0be-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6f0be-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f0be-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6f0be-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo FileCloud.</span><span class="sxs-lookup"><span data-stu-id="6f0be-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="6f0be-148">**tooconfigure AD do Azure-logon único com FileCloud, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6f0be-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f0be-149">Em Olá portal do Azure, Olá **FileCloud** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="6f0be-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="6f0be-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="6f0be-153">Em Olá **FileCloud domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f0be-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="6f0be-155">a.</span><span class="sxs-lookup"><span data-stu-id="6f0be-155">a.</span></span> <span data-ttu-id="6f0be-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="6f0be-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="6f0be-157">b.</span><span class="sxs-lookup"><span data-stu-id="6f0be-157">b.</span></span> <span data-ttu-id="6f0be-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="6f0be-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f0be-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="6f0be-159">These values are not real.</span></span> <span data-ttu-id="6f0be-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="6f0be-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6f0be-161">Entre em contato com [equipe de suporte do cliente FileCloud](mailto:support@codelathe.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="6f0be-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="6f0be-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="6f0be-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="6f0be-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6f0be-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6f0be-166">Em Olá **FileCloud configuração** seção, clique em **configurar FileCloud** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="6f0be-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f0be-167">Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6f0be-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuração do FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="6f0be-169">Em uma janela de navegador web diferente, logon tooyour FileCloud locatário como um administrador.</span><span class="sxs-lookup"><span data-stu-id="6f0be-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="6f0be-170">No painel de navegação esquerdo hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Seção Configurações no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="6f0be-172">Clique na guia **SSO** na seção Configurações.</span><span class="sxs-lookup"><span data-stu-id="6f0be-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Guia Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="6f0be-174">Selecione **SAML** como **Tipo de SSO Padrão** em **Configurações de SSO (Logon Único)** painel.</span><span class="sxs-lookup"><span data-stu-id="6f0be-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Painel de Configurações de Logon Único no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="6f0be-176">Colar **ID da entidade SAML**, que você copiou do portal do Azure em Olá **URL de ponto de extremidade IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6f0be-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![Caixa de texto URL do Ponto de Extremidade do IDP](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="6f0be-178">Abra o arquivo de metadados baixado no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **metadados IdP** textbox em **configurações SAML** painel.</span><span class="sxs-lookup"><span data-stu-id="6f0be-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Seção Metadados do IDP no lado do aplicativo](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="6f0be-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6f0be-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6f0be-181">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="6f0be-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f0be-182">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6f0be-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f0be-183">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f0be-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f0be-184">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f0be-184">Create an Azure AD test user</span></span>

<span data-ttu-id="6f0be-185">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f0be-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="6f0be-187">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6f0be-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f0be-188">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="6f0be-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6f0be-190">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6f0be-192">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6f0be-194">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f0be-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6f0be-196">a.</span><span class="sxs-lookup"><span data-stu-id="6f0be-196">a.</span></span> <span data-ttu-id="6f0be-197">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f0be-198">b.</span><span class="sxs-lookup"><span data-stu-id="6f0be-198">b.</span></span> <span data-ttu-id="6f0be-199">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f0be-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6f0be-200">c.</span><span class="sxs-lookup"><span data-stu-id="6f0be-200">c.</span></span> <span data-ttu-id="6f0be-201">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="6f0be-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6f0be-202">d.</span><span class="sxs-lookup"><span data-stu-id="6f0be-202">d.</span></span> <span data-ttu-id="6f0be-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="6f0be-204">Criar um usuário de teste do FileCloud</span><span class="sxs-lookup"><span data-stu-id="6f0be-204">Create a FileCloud test user</span></span>

<span data-ttu-id="6f0be-205">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no FileCloud.</span><span class="sxs-lookup"><span data-stu-id="6f0be-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="6f0be-206">O FileCloud dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6f0be-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="6f0be-207">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="6f0be-207">There is no action item for you in this section.</span></span> <span data-ttu-id="6f0be-208">Um novo usuário é criado durante uma tentativa tooaccess FileCloud se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="6f0be-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6f0be-209">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [equipe de suporte do cliente FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="6f0be-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6f0be-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6f0be-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6f0be-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="6f0be-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="6f0be-213">**tooassign Britta Simon tooFileCloud, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6f0be-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f0be-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6f0be-216">Na lista de aplicativos hello, selecione **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-216">In hello applications list, select **FileCloud**.</span></span>

    ![link de FileCloud Olá na lista de aplicativos Olá](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="6f0be-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="6f0be-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6f0be-220">Click **Add** button.</span></span> <span data-ttu-id="6f0be-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="6f0be-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f0be-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f0be-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f0be-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6f0be-226">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="6f0be-226">Test single sign-on</span></span>

<span data-ttu-id="6f0be-227">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6f0be-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f0be-228">Quando você clica em bloco FileCloud Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FileCloud aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6f0be-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f0be-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6f0be-229">Additional resources</span></span>

* [<span data-ttu-id="6f0be-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6f0be-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f0be-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f0be-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

