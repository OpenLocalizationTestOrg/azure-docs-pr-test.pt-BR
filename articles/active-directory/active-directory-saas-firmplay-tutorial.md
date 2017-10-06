---
title: "Tutorial: Integração do Azure Active Directory com o FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FirmPlay - advocacia funcionário de recrutamento."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="8ab3d-103">Tutorial: Integração do Azure Active Directory com FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="8ab3d-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="8ab3d-104">Neste tutorial, você aprenderá como toointegrate FirmPlay - advocacia funcionário de recrutamento com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8ab3d-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ab3d-105">Integrar FirmPlay - advocacia funcionário de recrutamento com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ab3d-106">Você pode controlar no AD do Azure que tenha acesso tooFirmPlay - advocacia funcionário de recrutamento</span><span class="sxs-lookup"><span data-stu-id="8ab3d-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="8ab3d-107">Você pode habilitar seu usuários tooautomatically get conectado tooFirmPlay - advocacia funcionário de recrutamento (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ab3d-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8ab3d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="8ab3d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ab3d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ab3d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ab3d-110">Prerequisites</span></span>

<span data-ttu-id="8ab3d-111">tooconfigure integração do AD do Azure com FirmPlay - advocacia funcionário de recrutamento, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="8ab3d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ab3d-113">Uma assinatura habilitada com logon único do FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="8ab3d-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="8ab3d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="8ab3d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ab3d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8ab3d-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ab3d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="8ab3d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8ab3d-118">Scenario description</span></span>
<span data-ttu-id="8ab3d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ab3d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ab3d-121">Adicionando FirmPlay - advocacia funcionário de recrutamento da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8ab3d-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="8ab3d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="8ab3d-123">Adicionando FirmPlay - advocacia funcionário de recrutamento da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8ab3d-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="8ab3d-124">integração de saudação do tooconfigure do FirmPlay - advocacia funcionário de recrutamento no AD do Azure, você precisa tooadd FirmPlay - advocacia funcionário de recrutamento da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ab3d-125">**tooadd FirmPlay - advocacia funcionário de recrutamento da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ab3d-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ab3d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ab3d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8ab3d-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8ab3d-133">Na caixa de pesquisa hello, digite **FirmPlay - advocacia funcionário de recrutamento**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="8ab3d-135">No painel de resultados de saudação, selecione **FirmPlay - advocacia funcionário de recrutamento**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ab3d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ab3d-138">Nesta seção, você irá configurar e testar o logon único do Azure AD com o FirmPlay - Employee Advocacy for Recruiting com base em um usuário de teste denominado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="8ab3d-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ab3d-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FirmPlay - advocacia funcionário de recrutamento é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="8ab3d-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FirmPlay - advocacia funcionário de recrutamento precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="8ab3d-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em FirmPlay - advocacia funcionário de recrutamento.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="8ab3d-142">tooconfigure e teste de logon único do AD do Azure com FirmPlay - advocacia funcionário de recrutamento, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ab3d-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ab3d-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ab3d-145">**[Criando um FirmPlay - advocacia do funcionário para o usuário de teste de recrutamento](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave um equivalente do Britta Simon em FirmPlay: advocacia funcionário de recrutamento que é vinculado a representação toohello AD do Azure de seus.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8ab3d-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ab3d-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ab3d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ab3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ab3d-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no seu FirmPlay - funcionário advocacia para aplicativos de recrutamento.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="8ab3d-150">**tooconfigure logon único do AD do Azure com FirmPlay - advocacia funcionário de recrutamento, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ab3d-151">No portal de gerenciamento do Azure do hello, no hello **FirmPlay - advocacia funcionário de recrutamento** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8ab3d-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="8ab3d-155">Em Olá **FirmPlay - advocacia do funcionário para o domínio de recrutamento e URLs** seção Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="8ab3d-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="8ab3d-157">Observe que isso não é um valor real hello.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="8ab3d-158">Você tem tooupdate esse valor com hello real URL de logon.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="8ab3d-159">Entre em contato com [FirmPlay - advocacia do funcionário para a equipe de suporte de recrutamento](mailto:engineering@firmplay.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="8ab3d-160">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="8ab3d-162">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="8ab3d-163">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-163">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="8ab3d-165">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="8ab3d-167">Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8ab3d-169">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="8ab3d-171">Em Olá **FirmPlay - advocacia do funcionário para a configuração de recrutamento** seção, clique em **FirmPlay configurar - advocacia funcionário de recrutamento** tooopen **configurar o logon**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="8ab3d-174">tooget SSO configurado para o seu aplicativo, entre em contato com [FirmPlay - advocacia do funcionário para a equipe de suporte de recrutamento](mailto:engineering@firmplay.com) e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="8ab3d-175">• Olá baixado **arquivo de certificado**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="8ab3d-176">• Olá **Single Sign-On URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="8ab3d-177">• Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="8ab3d-178">• Olá **URL de logout**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ab3d-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ab3d-180">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8ab3d-182">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ab3d-183">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ab3d-185">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ab3d-187">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ab3d-189">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab3d-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ab3d-191">a.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-191">a.</span></span> <span data-ttu-id="8ab3d-192">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ab3d-193">b.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-193">b.</span></span> <span data-ttu-id="8ab3d-194">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ab3d-195">c.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-195">c.</span></span> <span data-ttu-id="8ab3d-196">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ab3d-197">d.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-197">d.</span></span> <span data-ttu-id="8ab3d-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="8ab3d-199">Criando um usuário de teste do FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="8ab3d-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="8ab3d-200">Nesta seção, você irá criar um usuário denominado Brenda Fernandes no FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="8ab3d-201">Trabalhe com [FirmPlay - advocacia do funcionário para a equipe de suporte de recrutamento](mailto:engineering@firmplay.com) tooadd usuários Olá Olá FirmPlay - advocacia do funcionário para a plataforma de recrutamento.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ab3d-202">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ab3d-203">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooFirmPlay seu acesso - advocacia funcionário de recrutamento.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8ab3d-205">**tooassign Britta Simon tooFirmPlay - advocacia funcionário de recrutamento, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8ab3d-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ab3d-206">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8ab3d-208">Na lista de aplicativos hello, selecione **FirmPlay - advocacia funcionário de recrutamento**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="8ab3d-210">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8ab3d-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-212">Click **Add** button.</span></span> <span data-ttu-id="8ab3d-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8ab3d-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ab3d-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ab3d-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="8ab3d-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8ab3d-218">Testing single sign-on</span></span>

<span data-ttu-id="8ab3d-219">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ab3d-220">Quando você clica em Olá FirmPlay - funcionário advocacia bloco de recrutamento em Olá painel de acesso, você deve obter automaticamente assinado em tooyour FirmPlay - funcionário advocacia para aplicativos de recrutamento.</span><span class="sxs-lookup"><span data-stu-id="8ab3d-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8ab3d-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8ab3d-221">Additional resources</span></span>

* [<span data-ttu-id="8ab3d-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab3d-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ab3d-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ab3d-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png