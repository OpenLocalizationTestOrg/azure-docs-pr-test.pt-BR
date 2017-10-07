---
title: "Tutorial: integração do Azure Active Directory ao Domo | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Domo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 058626e4-73b3-4dc2-86ca-b060d002d70a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: cc70f8e5013f864d275762bbc1f84bd9677e8c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-domo"></a><span data-ttu-id="ce6b4-103">Tutorial: Integração do Azure Active Directory ao Domo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-103">Tutorial: Azure Active Directory integration with Domo</span></span>

<span data-ttu-id="ce6b4-104">Neste tutorial, você aprenderá como toointegrate Domo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ce6b4-104">In this tutorial, you learn how toointegrate Domo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce6b4-105">Integrando Domo AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-105">Integrating Domo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce6b4-106">Você pode controlar no AD do Azure que tenha acesso tooDomo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-106">You can control in Azure AD who has access tooDomo</span></span>
- <span data-ttu-id="ce6b4-107">Você pode habilitar seu usuários tooautomatically get conectado tooDomo (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-107">You can enable your users tooautomatically get signed-on tooDomo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce6b4-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce6b4-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce6b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce6b4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ce6b4-110">Prerequisites</span></span>

<span data-ttu-id="ce6b4-111">tooconfigure integração do AD do Azure com Domo, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-111">tooconfigure Azure AD integration with Domo, you need hello following items:</span></span>

- <span data-ttu-id="ce6b4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce6b4-113">Uma assinatura habilitada para logon único do Domo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-113">A Domo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce6b4-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce6b4-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce6b4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce6b4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce6b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce6b4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ce6b4-118">Scenario description</span></span>
<span data-ttu-id="ce6b4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce6b4-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce6b4-121">Adicionando Domo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ce6b4-121">Adding Domo from hello gallery</span></span>
2. <span data-ttu-id="ce6b4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-domo-from-hello-gallery"></a><span data-ttu-id="ce6b4-123">Adicionando Domo da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ce6b4-123">Adding Domo from hello gallery</span></span>
<span data-ttu-id="ce6b4-124">integração de saudação tooconfigure do Domo no AD do Azure, você precisa tooadd Domo na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-124">tooconfigure hello integration of Domo into Azure AD, you need tooadd Domo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce6b4-125">**tooadd Domo da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ce6b4-125">**tooadd Domo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce6b4-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce6b4-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce6b4-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ce6b4-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ce6b4-133">Na caixa de pesquisa hello, digite **Domo**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-133">In hello search box, type **Domo**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/tutorial_domo_search.png)

5. <span data-ttu-id="ce6b4-135">No painel de resultados de saudação, selecione **Domo**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-135">In hello results panel, select **Domo**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/tutorial_domo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce6b4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce6b4-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Domo com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-138">In this section, you configure and test Azure AD single sign-on with Domo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce6b4-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Domo é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Domo is tooa user in Azure AD.</span></span> <span data-ttu-id="ce6b4-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Domo precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-140">In other words, a link relationship between an Azure AD user and hello related user in Domo needs toobe established.</span></span>

<span data-ttu-id="ce6b4-141">Domo, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-141">In Domo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce6b4-142">tooconfigure e teste de logon único do AD do Azure com Domo, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-142">tooconfigure and test Azure AD single sign-on with Domo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce6b4-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce6b4-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce6b4-145">**[Criar um usuário de teste Domo](#creating-a-domo-test-user)**  -toohave um equivalente do Britta Simon em Domo é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-145">**[Creating a Domo test user](#creating-a-domo-test-user)** - toohave a counterpart of Britta Simon in Domo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce6b4-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce6b4-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce6b4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce6b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce6b4-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Domo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Domo application.</span></span>

<span data-ttu-id="ce6b4-150">**tooconfigure AD do Azure-logon único com Domo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ce6b4-150">**tooconfigure Azure AD single sign-on with Domo, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce6b4-151">Em Olá portal do Azure, Olá **Domo** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-151">In hello Azure portal, on hello **Domo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ce6b4-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_samlbase.png)

3. <span data-ttu-id="ce6b4-155">Em Olá **Domo domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-155">On hello **Domo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_url.png)

    <span data-ttu-id="ce6b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-157">a.</span></span> <span data-ttu-id="ce6b4-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.domo.com`</span><span class="sxs-lookup"><span data-stu-id="ce6b4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.domo.com`</span></span>

    <span data-ttu-id="ce6b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-159">b.</span></span> <span data-ttu-id="ce6b4-160">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>     

    | |
    |--|    
    | `https://<companyname>.domo.com` |
    | `https://<companyname>.beta.domo.com` |
    | `https://<companyname>.demo.domo.com` |
    | `https://<companyname>.dev.domo.com` | 
    | `https://<companyname>.fastage1.domo.com` |       
    | `https://<companyname>.frdev.domo.com` |       
    | `https://<companyname>.gastage.domo.com` |       
    | `https://<companyname>.load.domo.com` |       
    | `https://<companyname>.local.domo.com` |       
    | `https://<companyname>.qa.domo.com` |
    | `https://<companyname>.stage.domo.com` |
    
    > [!NOTE] 
    > <span data-ttu-id="ce6b4-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-161">These values are not real.</span></span> <span data-ttu-id="ce6b4-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ce6b4-163">Entre em contato com [equipe de suporte de cliente Domo](mailto:support@domo.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-163">Contact [Domo Client support team](mailto:support@domo.com) tooget these values.</span></span>

4. <span data-ttu-id="ce6b4-164">Aplicativo domo espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-164">Domo application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="ce6b4-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ce6b4-166">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ce6b4-167">Olá captura de tela a seguir mostra um exemplo para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-167">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_attributes.png)
    
5. <span data-ttu-id="ce6b4-169">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="ce6b4-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-170">Attribute Name</span></span> | <span data-ttu-id="ce6b4-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ce6b4-172">name</span><span class="sxs-lookup"><span data-stu-id="ce6b4-172">name</span></span> | <span data-ttu-id="ce6b4-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="ce6b4-173">user.displayname</span></span> |
    | <span data-ttu-id="ce6b4-174">email</span><span class="sxs-lookup"><span data-stu-id="ce6b4-174">email</span></span> | <span data-ttu-id="ce6b4-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="ce6b4-175">user.mail</span></span> |
    
    <span data-ttu-id="ce6b4-176">a.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-176">a.</span></span> <span data-ttu-id="ce6b4-177">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ce6b4-180">b.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-180">b.</span></span> <span data-ttu-id="ce6b4-181">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ce6b4-182">c.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-182">c.</span></span> <span data-ttu-id="ce6b4-183">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ce6b4-184">d.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-184">d.</span></span> <span data-ttu-id="ce6b4-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-185">Click **Ok**.</span></span> 
 
6. <span data-ttu-id="ce6b4-186">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-186">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_certificate.png) 

7. <span data-ttu-id="ce6b4-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ce6b4-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_general_400.png)


8. <span data-ttu-id="ce6b4-190">Em Olá **Domo configuração** seção, clique em **configurar Domo** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-190">On hello **Domo Configuration** section, click **Configure Domo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce6b4-191">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ce6b4-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

   ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_configure.png) 

9. <span data-ttu-id="ce6b4-193">tooconfigure logon único no **Domo** lado, você precisa toosend Olá baixado **certificado**, **ID da entidade SAML**, Olá **serviço de logon único SAML URL** e hello **URL de logout** muito[a equipe de suporte Domo](mailto:support@domo.com).</span><span class="sxs-lookup"><span data-stu-id="ce6b4-193">tooconfigure single sign-on on **Domo** side, you need toosend hello downloaded **Certificate**, **SAML Entity ID**, hello **SAML Single Sign-On Service URL** and hello **Sign-Out URL** too[Domo support team](mailto:support@domo.com).</span></span> <span data-ttu-id="ce6b4-194">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-194">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ce6b4-195">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ce6b4-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce6b4-196">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce6b4-197">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce6b4-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce6b4-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce6b4-199">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ce6b4-201">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ce6b4-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce6b4-202">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce6b4-204">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce6b4-206">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce6b4-208">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce6b4-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-domo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce6b4-210">a.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-210">a.</span></span> <span data-ttu-id="ce6b4-211">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce6b4-212">b.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-212">b.</span></span> <span data-ttu-id="ce6b4-213">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce6b4-214">c.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-214">c.</span></span> <span data-ttu-id="ce6b4-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce6b4-216">d.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-216">d.</span></span> <span data-ttu-id="ce6b4-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-217">Click **Create**.</span></span>
 
### <a name="creating-a-domo-test-user"></a><span data-ttu-id="ce6b4-218">Criação de um usuário de teste do Domo</span><span class="sxs-lookup"><span data-stu-id="ce6b4-218">Creating a Domo test user</span></span>

<span data-ttu-id="ce6b4-219">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Domo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-219">hello objective of this section is toocreate a user called Britta Simon in Domo.</span></span> <span data-ttu-id="ce6b4-220">O Domo dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-220">Domo supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ce6b4-221">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-221">There is no action item for you in this section.</span></span> <span data-ttu-id="ce6b4-222">Um novo usuário é criado durante uma tentativa tooaccess Domo se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-222">A new user is created during an attempt tooaccess Domo if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce6b4-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce6b4-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDomo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDomo.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ce6b4-226">**tooassign Britta Simon tooDomo, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ce6b4-226">**tooassign Britta Simon tooDomo, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce6b4-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ce6b4-229">Na lista de aplicativos hello, selecione **Domo**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-229">In hello applications list, select **Domo**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-domo-tutorial/tutorial_domo_app.png) 

3. <span data-ttu-id="ce6b4-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ce6b4-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-233">Click **Add** button.</span></span> <span data-ttu-id="ce6b4-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ce6b4-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce6b4-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce6b4-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce6b4-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ce6b4-239">Testing single sign-on</span></span>

<span data-ttu-id="ce6b4-240">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="ce6b4-241">Quando você clica em bloco Domo Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Domo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce6b4-241">When you click hello Domo tile in hello Access Panel, you should get automatically signed-on tooyour Domo application.</span></span>

<span data-ttu-id="ce6b4-242">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce6b4-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ce6b4-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ce6b4-243">Additional resources</span></span>

* [<span data-ttu-id="ce6b4-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ce6b4-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce6b4-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce6b4-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-domo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-domo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-domo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-domo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-domo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-domo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-domo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-domo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-domo-tutorial/tutorial_general_203.png

