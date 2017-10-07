---
title: "Tutorial: Integração do Azure Active Directory ao Blackboard Learn | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e aprenda-quadro-negro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="b8caa-103">Tutorial: integração do Azure Active Directory ao Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="b8caa-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="b8caa-104">Neste tutorial, você aprenderá como toointegrate-quadro-negro aprender com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b8caa-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8caa-105">Integrando-quadro-negro Saiba AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8caa-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b8caa-106">Você pode controlar no AD do Azure que tenha acesso tooBlackboard Saiba mais</span><span class="sxs-lookup"><span data-stu-id="b8caa-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="b8caa-107">Você pode habilitar seu usuários tooautomatically get conectado tooBlackboard Saiba (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8caa-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b8caa-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8caa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8caa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8caa-110">Prerequisites</span></span>

<span data-ttu-id="b8caa-111">tooconfigure integração do AD do Azure com-quadro-negro saber, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8caa-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="b8caa-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8caa-113">Uma assinatura habilitada para logon único do Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="b8caa-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8caa-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b8caa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8caa-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b8caa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8caa-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b8caa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8caa-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8caa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8caa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b8caa-118">Scenario description</span></span>
<span data-ttu-id="b8caa-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b8caa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8caa-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b8caa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8caa-121">Adicionando-quadro-negro Saiba da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b8caa-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="b8caa-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="b8caa-123">Adicionando-quadro-negro Saiba da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b8caa-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="b8caa-124">integração de saudação tooconfigure do-quadro-negro Saiba no AD do Azure, você precisa tooadd-quadro-negro Saiba mais na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b8caa-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b8caa-125">**tooadd-quadro-negro Saiba da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b8caa-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8caa-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b8caa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8caa-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b8caa-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b8caa-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b8caa-133">Na caixa de pesquisa hello, digite **-quadro-negro Saiba**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="b8caa-135">No painel de resultados de saudação, selecione **-quadro-negro Saiba**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b8caa-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8caa-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8caa-138">Nesta seção, você configura e testa o logon único do Azure AD com o Blackboard Learn, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b8caa-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8caa-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte de saudação em-Quadro-negro Saiba é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8caa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="b8caa-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em aprender-quadro-negro precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b8caa-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="b8caa-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em-Quadro-negro saber.</span><span class="sxs-lookup"><span data-stu-id="b8caa-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="b8caa-142">tooconfigure e teste de logon único do AD do Azure com-quadro-negro saber mais, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8caa-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b8caa-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b8caa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b8caa-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8caa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8caa-145">**[Criar um usuário de teste-quadro-negro Saiba](#creating-a-blackboard-learn-test-user)**  -toohave um equivalente do Britta Simon no-quadro-negro Saiba que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b8caa-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8caa-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b8caa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8caa-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b8caa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8caa-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8caa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8caa-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo-quadro-negro saber.</span><span class="sxs-lookup"><span data-stu-id="b8caa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="b8caa-150">**tooconfigure AD do Azure-logon único com-quadro-negro saber, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b8caa-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8caa-151">Em Olá portal do Azure, Olá **-quadro-negro Saiba** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b8caa-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b8caa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="b8caa-155">Em Olá **-quadro-negro Saiba domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8caa-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="b8caa-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8caa-157">a.</span></span> <span data-ttu-id="b8caa-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="b8caa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="b8caa-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8caa-159">b.</span></span> <span data-ttu-id="b8caa-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="b8caa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b8caa-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b8caa-161">These values are not real.</span></span> <span data-ttu-id="b8caa-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="b8caa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b8caa-163">Entre em contato com [a equipe de suporte-quadro-negro Saiba cliente](https://www.blackboard.com/support/index.aspx) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b8caa-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="b8caa-164">Aplicativo de Saiba-quadro-negro espera as asserções de SAML de Olá em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="b8caa-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b8caa-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8caa-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="b8caa-166">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b8caa-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="b8caa-167">Olá captura de tela a seguir mostra um exemplo sobre ele.</span><span class="sxs-lookup"><span data-stu-id="b8caa-167">hello following screenshot shows an example about it.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="b8caa-169">Em Olá **atributos de usuário** seção **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8caa-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="b8caa-170">Mapeamos Olá Userprincipalname como atributo de usuário exclusivo Olá aqui mas você pode mapear toohello valor apropriado, que distingue exclusivamente o usuário Olá na organização hello e que mapeia o campo de nome de usuário tooBlackboard Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="b8caa-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="b8caa-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="b8caa-171">Attribute Name</span></span> | <span data-ttu-id="b8caa-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="b8caa-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="b8caa-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="b8caa-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="b8caa-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="b8caa-174">user.userprincipalname</span></span> |

    <span data-ttu-id="b8caa-175">a.</span><span class="sxs-lookup"><span data-stu-id="b8caa-175">a.</span></span> <span data-ttu-id="b8caa-176">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b8caa-179">b.</span><span class="sxs-lookup"><span data-stu-id="b8caa-179">b.</span></span> <span data-ttu-id="b8caa-180">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="b8caa-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b8caa-181">c.</span><span class="sxs-lookup"><span data-stu-id="b8caa-181">c.</span></span> <span data-ttu-id="b8caa-182">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="b8caa-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b8caa-183">d.</span><span class="sxs-lookup"><span data-stu-id="b8caa-183">d.</span></span> <span data-ttu-id="b8caa-184">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-184">Click **Ok**.</span></span>

4. <span data-ttu-id="b8caa-185">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b8caa-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="b8caa-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b8caa-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b8caa-189">Em Olá **-quadro-negro Saiba configuração** seção, clique em **configurar-quadro-negro Saiba** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b8caa-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b8caa-190">Saudação de cópia **ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b8caa-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="b8caa-192">tooconfigure logon único no **-quadro-negro Saiba** lado, você precisa toosend Olá baixado **Metadata XML** e **ID da entidade SAML** muito[Saiba-quadro-negro suporte a](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8caa-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="b8caa-193">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b8caa-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b8caa-194">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b8caa-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b8caa-195">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8caa-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8caa-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8caa-197">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8caa-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b8caa-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b8caa-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8caa-200">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b8caa-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8caa-202">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8caa-204">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8caa-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8caa-206">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8caa-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8caa-208">a.</span><span class="sxs-lookup"><span data-stu-id="b8caa-208">a.</span></span> <span data-ttu-id="b8caa-209">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8caa-210">b.</span><span class="sxs-lookup"><span data-stu-id="b8caa-210">b.</span></span> <span data-ttu-id="b8caa-211">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8caa-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b8caa-212">c.</span><span class="sxs-lookup"><span data-stu-id="b8caa-212">c.</span></span> <span data-ttu-id="b8caa-213">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b8caa-214">d.</span><span class="sxs-lookup"><span data-stu-id="b8caa-214">d.</span></span> <span data-ttu-id="b8caa-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="b8caa-216">Criando um usuário de teste do Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="b8caa-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="b8caa-217">Nesta seção, você deve criar um usuário chamado Brenda Fernandes no Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="b8caa-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="b8caa-218">O aplicativo Blackboard Learn dá suporte a provisionamento de usuários imediato.</span><span class="sxs-lookup"><span data-stu-id="b8caa-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="b8caa-219">Certifique-se de que você tenha configurado Olá declarações conforme descrito na seção Olá  **[Configurando o AD do Azure Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="b8caa-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b8caa-220">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b8caa-221">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBlackboard Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="b8caa-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b8caa-223">**tooassign Britta Simon tooBlackboard saiba, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b8caa-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8caa-224">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b8caa-226">Na lista de aplicativos hello, selecione **-quadro-negro Saiba**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="b8caa-228">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b8caa-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b8caa-230">Click **Add** button.</span></span> <span data-ttu-id="b8caa-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b8caa-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8caa-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b8caa-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8caa-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8caa-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b8caa-236">Testing single sign-on</span></span>

<span data-ttu-id="b8caa-237">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8caa-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b8caa-238">Quando você clica em hello-quadro-negro Saiba lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour-quadro-negro Saiba aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8caa-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="b8caa-239">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8caa-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b8caa-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b8caa-240">Additional resources</span></span>

* [<span data-ttu-id="b8caa-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b8caa-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8caa-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8caa-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

