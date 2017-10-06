---
title: "Tutorial: integração do Azure Active Directory ao FreshGrade | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="0af57-103">Tutorial: Integração do Active Directory do Azure ao FreshGrade</span><span class="sxs-lookup"><span data-stu-id="0af57-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="0af57-104">Neste tutorial, você aprenderá como toointegrate FreshGrade com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0af57-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0af57-105">Integrando FreshGrade com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0af57-106">Você pode controlar no AD do Azure que tenha acesso tooFreshGrade</span><span class="sxs-lookup"><span data-stu-id="0af57-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="0af57-107">Você pode habilitar seu usuários tooautomatically get conectado tooFreshGrade (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0af57-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0af57-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0af57-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0af57-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0af57-110">Prerequisites</span></span>

<span data-ttu-id="0af57-111">tooconfigure integração do AD do Azure com FreshGrade, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="0af57-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0af57-113">Uma assinatura habilitada para logon único do FreshGrade</span><span class="sxs-lookup"><span data-stu-id="0af57-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0af57-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0af57-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0af57-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0af57-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0af57-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0af57-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0af57-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0af57-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0af57-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0af57-118">Scenario description</span></span>
<span data-ttu-id="0af57-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0af57-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0af57-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0af57-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0af57-121">Adicionando FreshGrade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0af57-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="0af57-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="0af57-123">Adicionando FreshGrade da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0af57-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="0af57-124">integração de saudação tooconfigure de FreshGrade no AD do Azure, você precisa tooadd FreshGrade da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0af57-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0af57-125">**tooadd FreshGrade da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0af57-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0af57-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0af57-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0af57-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0af57-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0af57-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0af57-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0af57-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0af57-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0af57-133">Na caixa de pesquisa hello, digite **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="0af57-133">In hello search box, type **FreshGrade**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="0af57-135">No painel de resultados de saudação, selecione **FreshGrade**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0af57-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0af57-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0af57-138">Nesta seção, você configurará e testará o logon único do AD do Azure com o FreshGrade, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0af57-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0af57-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FreshGrade é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af57-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="0af57-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FreshGrade precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0af57-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="0af57-141">FreshGrade, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af57-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0af57-142">tooconfigure e teste de logon único do AD do Azure com FreshGrade, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0af57-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0af57-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0af57-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0af57-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0af57-145">**[Criar um usuário de teste FreshGrade](#creating-a-freshgrade-test-user)**  -toohave um equivalente do Britta Simon em FreshGrade é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="0af57-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0af57-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0af57-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0af57-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0af57-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0af57-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0af57-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0af57-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="0af57-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="0af57-150">**tooconfigure AD do Azure-logon único com FreshGrade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0af57-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="0af57-151">Em Olá portal do Azure, Olá **FreshGrade** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0af57-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0af57-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0af57-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="0af57-155">Em Olá **FreshGrade domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="0af57-157">a.</span><span class="sxs-lookup"><span data-stu-id="0af57-157">a.</span></span> <span data-ttu-id="0af57-158">Em Olá **URL de logon** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="0af57-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="0af57-159">b.</span><span class="sxs-lookup"><span data-stu-id="0af57-159">b.</span></span> <span data-ttu-id="0af57-160">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="0af57-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="0af57-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0af57-161">These values are not real.</span></span> <span data-ttu-id="0af57-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0af57-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0af57-163">Entre em contato com [equipe de suporte do cliente FreshGrade](mailTo:support@freshgrade.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0af57-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="0af57-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0af57-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="0af57-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0af57-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0af57-168">Em Olá **FreshGrade configuração** seção, clique em **configurar FreshGrade** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="0af57-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0af57-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0af57-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="0af57-171">Olá toogenerate **metadados** url, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="0af57-172">a.</span><span class="sxs-lookup"><span data-stu-id="0af57-172">a.</span></span> <span data-ttu-id="0af57-173">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0af57-173">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="0af57-175">b.</span><span class="sxs-lookup"><span data-stu-id="0af57-175">b.</span></span> <span data-ttu-id="0af57-176">Clique em **pontos de extremidade** tooopen **pontos de extremidade** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0af57-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="0af57-178">c.</span><span class="sxs-lookup"><span data-stu-id="0af57-178">c.</span></span> <span data-ttu-id="0af57-179">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="0af57-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="0af57-181">d.</span><span class="sxs-lookup"><span data-stu-id="0af57-181">d.</span></span> <span data-ttu-id="0af57-182">Agora vá toohello a página de propriedades de **FreshGrade** e cópia hello **Id do aplicativo** usando **cópia** botão e cole-o no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="0af57-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="0af57-184">e.</span><span class="sxs-lookup"><span data-stu-id="0af57-184">e.</span></span> <span data-ttu-id="0af57-185">Gerar Olá **URL de metadados** usando saudação padrão a seguir:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="0af57-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="0af57-186">tooconfigure logon único no **FreshGrade** lado, você precisa Olá toosend **URL de metadados** e **Single Sign-On URL do serviço SAML** muito[FreshGrade equipe de suporte](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="0af57-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="0af57-187">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="0af57-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0af57-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0af57-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0af57-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0af57-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0af57-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0af57-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0af57-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="0af57-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af57-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0af57-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0af57-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0af57-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0af57-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0af57-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0af57-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0af57-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af57-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0af57-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af57-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0af57-203">a.</span><span class="sxs-lookup"><span data-stu-id="0af57-203">a.</span></span> <span data-ttu-id="0af57-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0af57-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0af57-205">b.</span><span class="sxs-lookup"><span data-stu-id="0af57-205">b.</span></span> <span data-ttu-id="0af57-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0af57-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0af57-207">c.</span><span class="sxs-lookup"><span data-stu-id="0af57-207">c.</span></span> <span data-ttu-id="0af57-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0af57-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0af57-209">d.</span><span class="sxs-lookup"><span data-stu-id="0af57-209">d.</span></span> <span data-ttu-id="0af57-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0af57-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="0af57-211">Criação de um usuário de teste FreshGrade</span><span class="sxs-lookup"><span data-stu-id="0af57-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="0af57-212">Nesta seção, você criará uma usuária chamado Brenda Fernandes no FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="0af57-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="0af57-213">Trabalhe com [FreshGrade a equipe de suporte](mailTo:support@freshgrade.com) tooadd usuários de saudação na plataforma de FreshGrade hello.</span><span class="sxs-lookup"><span data-stu-id="0af57-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0af57-214">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0af57-215">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFreshGrade.</span><span class="sxs-lookup"><span data-stu-id="0af57-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0af57-217">**tooassign Britta Simon tooFreshGrade, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0af57-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="0af57-218">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0af57-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0af57-220">Na lista de aplicativos hello, selecione **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="0af57-220">In hello applications list, select **FreshGrade**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="0af57-222">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0af57-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0af57-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0af57-224">Click **Add** button.</span></span> <span data-ttu-id="0af57-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0af57-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0af57-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af57-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0af57-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0af57-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0af57-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0af57-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0af57-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0af57-230">Testing single sign-on</span></span>

<span data-ttu-id="0af57-231">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af57-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0af57-232">Quando você clica em bloco FreshGrade Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FreshGrade aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0af57-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="0af57-233">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0af57-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0af57-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0af57-234">Additional resources</span></span>

* [<span data-ttu-id="0af57-235">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0af57-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0af57-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0af57-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

