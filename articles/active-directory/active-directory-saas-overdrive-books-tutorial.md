---
title: "Tutorial: Integração do Azure Active Directory com o Overdrive | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Overdrive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0aafacdedee25587132fc88ff93829f4367b0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="7af13-103">Tutorial: Integração do Azure Active Directory com o Overdrive</span><span class="sxs-lookup"><span data-stu-id="7af13-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="7af13-104">Neste tutorial, você aprenderá como toointegrate Overdrive com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7af13-104">In this tutorial, you learn how toointegrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7af13-105">Integrando o Overdrive com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="7af13-105">Integrating Overdrive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7af13-106">Você pode controlar no AD do Azure que tenha acesso tooOverdrive</span><span class="sxs-lookup"><span data-stu-id="7af13-106">You can control in Azure AD who has access tooOverdrive</span></span> 
- <span data-ttu-id="7af13-107">Você pode habilitar seu usuários tooautomatically get conectado tooOverdrive (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-107">You can enable your users tooautomatically get signed-on tooOverdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7af13-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7af13-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7af13-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7af13-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7af13-110">Prerequisites</span></span>

<span data-ttu-id="7af13-111">tooconfigure integração do AD do Azure com o Overdrive, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7af13-111">tooconfigure Azure AD integration with Overdrive, you need hello following items:</span></span>

- <span data-ttu-id="7af13-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7af13-113">Uma assinatura habilitada para logon único do Overdrive</span><span class="sxs-lookup"><span data-stu-id="7af13-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7af13-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7af13-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7af13-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7af13-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7af13-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7af13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7af13-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7af13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7af13-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7af13-118">Scenario description</span></span>
<span data-ttu-id="7af13-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7af13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7af13-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="7af13-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7af13-121">Adicionando Overdrive da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7af13-121">Adding Overdrive from hello gallery</span></span>
2. <span data-ttu-id="7af13-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-hello-gallery"></a><span data-ttu-id="7af13-123">Adicionando Overdrive da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="7af13-123">Adding Overdrive from hello gallery</span></span>
<span data-ttu-id="7af13-124">integração de saudação do tooconfigure do Overdrive no AD do Azure, você precisa tooadd Overdrive na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7af13-124">tooconfigure hello integration of Overdrive into Azure AD, you need tooadd Overdrive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7af13-125">**tooadd Overdrive da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7af13-125">**tooadd Overdrive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7af13-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7af13-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7af13-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7af13-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7af13-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7af13-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7af13-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7af13-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7af13-133">Na caixa de pesquisa hello, digite **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="7af13-133">In hello search box, type **Overdrive**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="7af13-135">No painel de resultados de saudação, selecione **Overdrive**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7af13-135">In hello results panel, select **Overdrive**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7af13-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7af13-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Overdrive com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7af13-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7af13-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Overdrive é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7af13-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Overdrive is tooa user in Azure AD.</span></span> <span data-ttu-id="7af13-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Overdrive precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7af13-140">In other words, a link relationship between an Azure AD user and hello related user in Overdrive needs toobe established.</span></span>

<span data-ttu-id="7af13-141">No Overdrive, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="7af13-141">In Overdrive, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7af13-142">tooconfigure e teste de logon único do AD do Azure com o Overdrive, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="7af13-142">tooconfigure and test Azure AD single sign-on with Overdrive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7af13-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7af13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7af13-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7af13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7af13-145">**[Criar um usuário de teste do Overdrive](#creating-an-overdrive-test-user)**  -toohave um equivalente do Britta Simon no Overdrive é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7af13-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - toohave a counterpart of Britta Simon in Overdrive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7af13-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="7af13-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7af13-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="7af13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7af13-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7af13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7af13-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Overdrive.</span><span class="sxs-lookup"><span data-stu-id="7af13-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="7af13-150">**tooconfigure AD do Azure-logon único com o Overdrive, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7af13-150">**tooconfigure Azure AD single sign-on with Overdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="7af13-151">Em Olá portal do Azure, Olá **Overdrive** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="7af13-151">In hello Azure portal, on hello **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7af13-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="7af13-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="7af13-155">Em Olá **Overdrive domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7af13-155">On hello **Overdrive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="7af13-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="7af13-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7af13-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7af13-158">hello value is not real.</span></span> <span data-ttu-id="7af13-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="7af13-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7af13-160">Entre em contato com [equipe de suporte do Overdrive cliente](https://help.overdrive.com/) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="7af13-160">Contact [Overdrive Client support team](https://help.overdrive.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7af13-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7af13-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="7af13-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7af13-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7af13-165">tooconfigure logon único no **Overdrive** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="7af13-165">tooconfigure single sign-on on **Overdrive** side, you need toosend hello downloaded **Metadata XML** too[Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="7af13-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="7af13-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7af13-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="7af13-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7af13-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="7af13-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7af13-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7af13-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7af13-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="7af13-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7af13-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7af13-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7af13-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7af13-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="7af13-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7af13-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7af13-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7af13-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7af13-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7af13-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7af13-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7af13-182">a.</span><span class="sxs-lookup"><span data-stu-id="7af13-182">a.</span></span> <span data-ttu-id="7af13-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7af13-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7af13-184">b.</span><span class="sxs-lookup"><span data-stu-id="7af13-184">b.</span></span> <span data-ttu-id="7af13-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7af13-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7af13-186">c.</span><span class="sxs-lookup"><span data-stu-id="7af13-186">c.</span></span> <span data-ttu-id="7af13-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="7af13-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7af13-188">d.</span><span class="sxs-lookup"><span data-stu-id="7af13-188">d.</span></span> <span data-ttu-id="7af13-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7af13-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="7af13-190">Criação de um usuário de teste do Overdrive</span><span class="sxs-lookup"><span data-stu-id="7af13-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="7af13-191">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooOverDrive.</span><span class="sxs-lookup"><span data-stu-id="7af13-191">There is no action item for you tooconfigure user provisioning tooOverDrive.</span></span>  

<span data-ttu-id="7af13-192">Quando um toolog de tentativas de usuário atribuído em tooOverDrive, uma conta do OverDrive é criada automaticamente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="7af13-192">When an assigned user tries toolog in tooOverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="7af13-193">Você pode usar qualquer ferramenta de criação outros OverDrive usuário conta ou APIs fornecidas pelo OverDrive tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="7af13-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive tooprovision AAD user accounts.</span></span>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7af13-194">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7af13-195">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOverdrive.</span><span class="sxs-lookup"><span data-stu-id="7af13-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOverdrive.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7af13-197">**tooassign Britta Simon tooOverdrive, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="7af13-197">**tooassign Britta Simon tooOverdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="7af13-198">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7af13-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7af13-200">Na lista de aplicativos hello, selecione **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="7af13-200">In hello applications list, select **Overdrive**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="7af13-202">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7af13-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7af13-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7af13-204">Click **Add** button.</span></span> <span data-ttu-id="7af13-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7af13-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7af13-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="7af13-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7af13-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7af13-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7af13-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7af13-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7af13-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7af13-210">Testing single sign-on</span></span>

<span data-ttu-id="7af13-211">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7af13-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7af13-212">Quando você clica em bloco Overdrive Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Overdrive.</span><span class="sxs-lookup"><span data-stu-id="7af13-212">When you click hello Overdrive tile in hello Access Panel, you should get automatically signed-on tooyour Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7af13-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7af13-213">Additional resources</span></span>

* [<span data-ttu-id="7af13-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7af13-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7af13-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7af13-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

