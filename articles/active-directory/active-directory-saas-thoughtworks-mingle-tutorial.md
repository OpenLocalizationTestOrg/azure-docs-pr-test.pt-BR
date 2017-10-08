---
title: "Tutorial: Integração do Azure Active Directory com o Thoughtworks Mingle | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="7d740-103">Tutorial: Integração do Active Directory do Azure com o Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="7d740-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="7d740-104">Neste tutorial, você aprenderá como toointegrate Thoughtworks Mingle com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7d740-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d740-105">Integrar Thoughtworks Mingle com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d740-106">Você pode controlar no AD do Azure que tenha acesso tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="7d740-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="7d740-107">Você pode habilitar seus usuários tooautomatically get conectado tooThoughtworks Mingle (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d740-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d740-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d740-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d740-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7d740-110">Prerequisites</span></span>

<span data-ttu-id="7d740-111">tooconfigure integração do AD do Azure com Thoughtworks Mingle, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="7d740-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d740-113">Uma assinatura do Thoughtworks Mingle habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7d740-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d740-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7d740-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d740-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7d740-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d740-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7d740-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d740-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d740-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d740-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7d740-118">Scenario description</span></span>
<span data-ttu-id="7d740-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7d740-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d740-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7d740-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d740-121">Adicionando Thoughtworks Mingle da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7d740-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="7d740-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="7d740-123">Adicionando Thoughtworks Mingle da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7d740-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="7d740-124">integração de saudação tooconfigure do Thoughtworks Mingle no AD do Azure, você precisa tooadd Thoughtworks Mingle na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7d740-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d740-125">**tooadd Thoughtworks Mingle da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7d740-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d740-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7d740-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="7d740-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7d740-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d740-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7d740-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="7d740-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d740-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="7d740-133">Na caixa de pesquisa hello, digite **Thoughtworks Mingle**, selecione **Thoughtworks Mingle** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7d740-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ThoughtWorks Mingle na lista de resultados de saudação](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7d740-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d740-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7d740-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Thoughtworks Mingle, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7d740-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d740-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Thoughtworks Mingle é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d740-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="7d740-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Thoughtworks Mingle precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7d740-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="7d740-139">Thoughtworks Mingle, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d740-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7d740-140">tooconfigure e teste de logon único do AD do Azure com Thoughtworks Mingle, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d740-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7d740-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d740-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d740-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d740-143">**[Criar um usuário de teste Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave um equivalente do Britta Simon no Thoughtworks Mingle que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7d740-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d740-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7d740-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d740-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7d740-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7d740-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d740-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7d740-147">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="7d740-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="7d740-148">**tooconfigure AD do Azure-logon único com Thoughtworks Mingle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7d740-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d740-149">Em Olá portal do Azure, Olá **Thoughtworks Mingle** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7d740-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7d740-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7d740-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="7d740-153">Em Olá **Thoughtworks Mingle domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="7d740-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="7d740-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7d740-156">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7d740-156">hello value is not real.</span></span> <span data-ttu-id="7d740-157">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="7d740-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7d740-158">Entre em contato com [a equipe de suporte Thoughtworks Mingle cliente](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d740-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7d740-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7d740-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="7d740-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7d740-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7d740-163">Faça logon no tooyour **Thoughtworks Mingle** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="7d740-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="7d740-164">Clique em Olá **Admin** guia e, em seguida, clique em **Config SSO**.</span><span class="sxs-lookup"><span data-stu-id="7d740-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="7d740-165">![Guia Administrador](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="7d740-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="7d740-166">Em Olá **Config SSO** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7d740-167">![Configuração de SSO](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="7d740-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="7d740-168">a.</span><span class="sxs-lookup"><span data-stu-id="7d740-168">a.</span></span> <span data-ttu-id="7d740-169">arquivo de metadados de saudação tooupload, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="7d740-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="7d740-170">b.</span><span class="sxs-lookup"><span data-stu-id="7d740-170">b.</span></span> <span data-ttu-id="7d740-171">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="7d740-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7d740-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7d740-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d740-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7d740-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d740-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d740-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7d740-175">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d740-175">Create an Azure AD test user</span></span>
<span data-ttu-id="7d740-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d740-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7d740-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7d740-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d740-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7d740-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d740-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7d740-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d740-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d740-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão Adicionar de saudação](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d740-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d740-187">a.</span><span class="sxs-lookup"><span data-stu-id="7d740-187">a.</span></span> <span data-ttu-id="7d740-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d740-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d740-189">b.</span><span class="sxs-lookup"><span data-stu-id="7d740-189">b.</span></span> <span data-ttu-id="7d740-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d740-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d740-191">c.</span><span class="sxs-lookup"><span data-stu-id="7d740-191">c.</span></span> <span data-ttu-id="7d740-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7d740-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d740-193">d.</span><span class="sxs-lookup"><span data-stu-id="7d740-193">d.</span></span> <span data-ttu-id="7d740-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7d740-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="7d740-195">Criar um usuário de teste do Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="7d740-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="7d740-196">Para o AD do Azure usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo Thoughtworks Mingle usando seus nomes de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7d740-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="7d740-197">No caso de saudação do Thoughtworks Mingle, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7d740-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="7d740-198">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7d740-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d740-199">Faça logon no tooyour site da empresa Thoughtworks Mingle como administrador.</span><span class="sxs-lookup"><span data-stu-id="7d740-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="7d740-200">Clique em **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="7d740-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="7d740-201">![Seu primeiro projeto](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Seu primeiro projeto")</span><span class="sxs-lookup"><span data-stu-id="7d740-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="7d740-202">Clique em Olá **Admin** guia e, em seguida, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="7d740-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="7d740-203">![Usuários](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="7d740-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="7d740-204">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7d740-204">Click **New User**.</span></span>
   
    <span data-ttu-id="7d740-205">![Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="7d740-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="7d740-206">Em Olá **novo usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7d740-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="7d740-207">![Caixa de diálogo Novo Usuário](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="7d740-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="7d740-208">a.</span><span class="sxs-lookup"><span data-stu-id="7d740-208">a.</span></span> <span data-ttu-id="7d740-209">Saudação de tipo **nome de usuário**, **nome de exibição**, **escolher senha**, **Confirmar senha** de uma válida do Azure você deseja tooprovision de conta do AD em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="7d740-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="7d740-210">b.</span><span class="sxs-lookup"><span data-stu-id="7d740-210">b.</span></span> <span data-ttu-id="7d740-211">Para **Tipo de usuário**, selecione **Usuário completo**.</span><span class="sxs-lookup"><span data-stu-id="7d740-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="7d740-212">c.</span><span class="sxs-lookup"><span data-stu-id="7d740-212">c.</span></span> <span data-ttu-id="7d740-213">Clique em **Criar este Perfil**.</span><span class="sxs-lookup"><span data-stu-id="7d740-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="7d740-214">Você pode usar outras Thoughtworks Mingle usuário conta ferramentas de criação ou APIs fornecidas pelo Thoughtworks Mingle tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="7d740-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7d740-215">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7d740-216">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="7d740-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="7d740-218">**tooassign tooThoughtworks Britta Simon Mingle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7d740-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d740-219">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7d740-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7d740-221">Na lista de aplicativos hello, selecione **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="7d740-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![link de Thoughtworks Mingle Olá na lista de aplicativos Olá](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="7d740-223">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7d740-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202] 

4. <span data-ttu-id="7d740-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7d740-225">Click **Add** button.</span></span> <span data-ttu-id="7d740-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d740-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="7d740-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d740-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d740-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d740-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d740-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d740-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7d740-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7d740-231">Test single sign-on</span></span>

<span data-ttu-id="7d740-232">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7d740-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d740-233">Quando você clica em Olá Thoughtworks Mingle lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Thoughtworks Mingle aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d740-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d740-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7d740-234">Additional resources</span></span>

* [<span data-ttu-id="7d740-235">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7d740-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d740-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d740-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

