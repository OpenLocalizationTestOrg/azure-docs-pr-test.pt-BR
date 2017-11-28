---
title: "Tutorial: Integração do Azure Active Directory com o Lynda.com | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="019e3-103">Tutorial: Integração do Active Directory do Azure com o Lynda.com</span><span class="sxs-lookup"><span data-stu-id="019e3-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="019e3-104">Neste tutorial, você aprenderá como toointegrate Lynda.com com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="019e3-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="019e3-105">Integrando o Lynda.com com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="019e3-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="019e3-106">Você pode controlar no AD do Azure que tenha acesso tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="019e3-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="019e3-107">Você pode habilitar seus usuários tooautomatically get conectado tooLynda.com (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="019e3-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="019e3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="019e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="019e3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="019e3-110">Prerequisites</span></span>

<span data-ttu-id="019e3-111">tooconfigure integração do AD do Azure com Lynda.com, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="019e3-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="019e3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="019e3-113">Uma assinatura do Lynda.com com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="019e3-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="019e3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="019e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="019e3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="019e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="019e3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="019e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="019e3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="019e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="019e3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="019e3-118">Scenario description</span></span>
<span data-ttu-id="019e3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="019e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="019e3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="019e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="019e3-121">Adicionando Lynda.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="019e3-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="019e3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="019e3-123">Adicionando Lynda.com da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="019e3-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="019e3-124">integração de saudação tooconfigure do Lynda.com no AD do Azure, você precisa tooadd Lynda.com da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="019e3-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="019e3-125">**tooadd Lynda.com da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="019e3-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="019e3-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="019e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="019e3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="019e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="019e3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="019e3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="019e3-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="019e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="019e3-133">Na caixa de pesquisa hello, digite **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="019e3-133">In hello search box, type **Lynda.com**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="019e3-135">No painel de resultados de saudação, selecione **Lynda.com**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="019e3-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="019e3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="019e3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lynda.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="019e3-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="019e3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Lynda.com é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="019e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="019e3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Lynda.com precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="019e3-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="019e3-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="019e3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="019e3-142">tooconfigure e teste de logon único do AD do Azure com Lynda.com, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="019e3-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="019e3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="019e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="019e3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="019e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="019e3-145">**[Criar um usuário de teste do Lynda.com](#creating-a-lyndacom-test-user)**  -toohave um equivalente do Britta Simon no Lynda.com é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="019e3-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="019e3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="019e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="019e3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="019e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="019e3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="019e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="019e3-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="019e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="019e3-150">**tooconfigure AD do Azure-logon único com o Lynda.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="019e3-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="019e3-151">Em Olá portal do Azure, Olá **Lynda.com** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="019e3-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="019e3-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="019e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="019e3-155">Em Olá **Lynda.com domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="019e3-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="019e3-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="019e3-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="019e3-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="019e3-158">This value is not real.</span></span> <span data-ttu-id="019e3-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="019e3-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="019e3-160">Entre em contato com [equipe de suporte do Lynda.com cliente](https://www.linkedin.com/help/lynda/ask) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="019e3-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="019e3-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="019e3-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="019e3-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="019e3-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="019e3-165">tooconfigure logon único no **Lynda.com** lado, você precisa toosend Olá baixado **Metadata XML** [suporte do Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="019e3-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="019e3-166">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="019e3-167">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="019e3-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="019e3-169">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="019e3-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="019e3-170">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="019e3-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="019e3-172">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="019e3-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="019e3-174">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="019e3-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="019e3-176">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="019e3-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="019e3-178">a.</span><span class="sxs-lookup"><span data-stu-id="019e3-178">a.</span></span> <span data-ttu-id="019e3-179">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="019e3-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="019e3-180">b.</span><span class="sxs-lookup"><span data-stu-id="019e3-180">b.</span></span> <span data-ttu-id="019e3-181">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="019e3-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="019e3-182">c.</span><span class="sxs-lookup"><span data-stu-id="019e3-182">c.</span></span> <span data-ttu-id="019e3-183">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="019e3-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="019e3-184">d.</span><span class="sxs-lookup"><span data-stu-id="019e3-184">d.</span></span> <span data-ttu-id="019e3-185">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="019e3-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="019e3-186">Criar um usuário de teste do Lynda.com</span><span class="sxs-lookup"><span data-stu-id="019e3-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="019e3-187">Não há nenhum item de ação para você tooconfigure provisionamento de usuário tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="019e3-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="019e3-188">Quando um usuário atribuído tenta toolog em tooLynda.com usando o painel de acesso hello, Lynda.com verifica se o usuário Olá existe.</span><span class="sxs-lookup"><span data-stu-id="019e3-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="019e3-189">Se não houver conta de usuário ainda, ela é criada automaticamente pelo Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="019e3-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="019e3-190">Você pode usar qualquer ferramenta de criação outros Lynda.com usuário conta ou APIs fornecidas pelo Lynda.com tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="019e3-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="019e3-191">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="019e3-192">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="019e3-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="019e3-194">**tooassign Britta Simon tooLynda.com, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="019e3-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="019e3-195">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="019e3-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="019e3-197">Na lista de aplicativos hello, selecione **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="019e3-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="019e3-199">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="019e3-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="019e3-201">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="019e3-201">Click **Add** button.</span></span> <span data-ttu-id="019e3-202">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="019e3-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="019e3-204">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="019e3-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="019e3-205">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="019e3-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="019e3-206">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="019e3-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="019e3-207">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="019e3-207">Testing single sign-on</span></span>

<span data-ttu-id="019e3-208">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="019e3-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="019e3-209">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="019e3-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="019e3-210">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="019e3-210">Additional resources</span></span>

* [<span data-ttu-id="019e3-211">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="019e3-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="019e3-212">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="019e3-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

