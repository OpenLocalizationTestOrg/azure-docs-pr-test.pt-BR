---
title: "Tutorial: integração do Azure Active Directory ao Lesson.ly | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="3e7aa-103">Tutorial: integração do Active Directory do Azure com o Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="3e7aa-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="3e7aa-104">Neste tutorial, você aprenderá como toointegrate Lesson.ly com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3e7aa-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e7aa-105">Integrando Lesson.ly com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e7aa-106">Você pode controlar no AD do Azure que tenha acesso tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="3e7aa-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="3e7aa-107">Você pode habilitar seus usuários tooautomatically get conectado tooLesson.ly (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3e7aa-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3e7aa-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e7aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e7aa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3e7aa-110">Prerequisites</span></span>

<span data-ttu-id="3e7aa-111">tooconfigure integração do AD do Azure com Lesson.ly, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="3e7aa-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e7aa-113">Uma assinatura habilitada para logon único do Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="3e7aa-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e7aa-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e7aa-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e7aa-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e7aa-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e7aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e7aa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3e7aa-118">Scenario description</span></span>
<span data-ttu-id="3e7aa-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e7aa-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e7aa-121">Adicionando Lesson.ly da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3e7aa-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="3e7aa-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="3e7aa-123">Adicionando Lesson.ly da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3e7aa-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="3e7aa-124">integração de saudação tooconfigure de Lesson.ly no AD do Azure, você precisa tooadd Lesson.ly da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e7aa-125">**tooadd Lesson.ly da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3e7aa-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7aa-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3e7aa-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e7aa-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3e7aa-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3e7aa-133">Na caixa de pesquisa hello, digite **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="3e7aa-135">No painel de resultados de saudação, selecione **Lesson.ly**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3e7aa-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3e7aa-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lesson.ly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e7aa-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Lesson.ly é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="3e7aa-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Lesson.ly precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="3e7aa-141">Lesson.ly, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e7aa-142">tooconfigure e teste de logon único do AD do Azure com Lesson.ly, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e7aa-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e7aa-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e7aa-145">**[Criar um usuário de teste Lesson.ly](#creating-a-lessonly-test-user)**  -toohave um equivalente do Britta Simon em Lesson.ly é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e7aa-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e7aa-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3e7aa-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e7aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3e7aa-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="3e7aa-150">**tooconfigure AD do Azure-logon único com Lesson.ly, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3e7aa-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7aa-151">Em Olá portal do Azure, Olá **Lesson.ly** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3e7aa-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="3e7aa-155">Em Olá **Lesson.ly domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="3e7aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-157">a.</span></span> <span data-ttu-id="3e7aa-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="3e7aa-159">Ao nome de referência um genérico que **companyname** precisa toobe substituído por um nome real.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="3e7aa-160">b.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-160">b.</span></span> <span data-ttu-id="3e7aa-161">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="3e7aa-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-162">These values are not real.</span></span> <span data-ttu-id="3e7aa-163">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3e7aa-164">Entre em contato com [equipe de suporte do cliente Lesson.ly](mailto:dev@lessonly.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="3e7aa-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="3e7aa-167">Olá Lesson.ly aplicativo espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens SAML** configuration.hello captura de tela a seguir mostra um exemplo de Essa opção.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="3e7aa-169">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, como mostrado no hello anterior a imagem e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="3e7aa-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="3e7aa-170">Attribute Name</span></span>   | <span data-ttu-id="3e7aa-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="3e7aa-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="3e7aa-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="3e7aa-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="3e7aa-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3e7aa-173">user.givenname</span></span> |
    | <span data-ttu-id="3e7aa-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="3e7aa-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="3e7aa-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="3e7aa-175">user.surname</span></span> |
    | <span data-ttu-id="3e7aa-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="3e7aa-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="3e7aa-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="3e7aa-177">user.mail</span></span> |

    <span data-ttu-id="3e7aa-178">a.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-178">a.</span></span> <span data-ttu-id="3e7aa-179">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3e7aa-182">b.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-182">b.</span></span> <span data-ttu-id="3e7aa-183">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="3e7aa-184">c.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-184">c.</span></span> <span data-ttu-id="3e7aa-185">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3e7aa-186">d.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-186">d.</span></span> <span data-ttu-id="3e7aa-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="3e7aa-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3e7aa-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3e7aa-190">Em Olá **Lesson.ly configuração** seção, clique em **configurar Lesson.ly** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e7aa-191">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3e7aa-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="3e7aa-193">tooconfigure logon único no **Lesson.ly** lado, você precisa toosend Olá baixado **Certificate(Base64)** e **URL de logout, ID de entidade de SAML e SAML Single Sign-On URL do serviço** muito[a equipe de suporte Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="3e7aa-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="3e7aa-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3e7aa-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e7aa-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e7aa-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e7aa-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3e7aa-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3e7aa-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3e7aa-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3e7aa-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7aa-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3e7aa-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3e7aa-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3e7aa-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e7aa-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3e7aa-209">a.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-209">a.</span></span> <span data-ttu-id="3e7aa-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e7aa-211">b.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-211">b.</span></span> <span data-ttu-id="3e7aa-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3e7aa-213">c.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-213">c.</span></span> <span data-ttu-id="3e7aa-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3e7aa-215">d.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-215">d.</span></span> <span data-ttu-id="3e7aa-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="3e7aa-217">Criar um usuário de teste Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="3e7aa-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="3e7aa-218">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="3e7aa-219">O Lesson.ly dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="3e7aa-220">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-220">There is no action item for you in this section.</span></span> <span data-ttu-id="3e7aa-221">Será criado um novo usuário durante uma tentativa tooaccess Lesson.ly se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="3e7aa-222">Se você precisar toocreate um usuário manualmente, você precisa Olá toocontact [a equipe de suporte Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="3e7aa-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3e7aa-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3e7aa-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLesson.ly.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3e7aa-226">**tooassign Britta Simon tooLesson.ly, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3e7aa-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e7aa-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3e7aa-229">Na lista de aplicativos hello, selecione **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="3e7aa-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3e7aa-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-233">Click **Add** button.</span></span> <span data-ttu-id="3e7aa-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3e7aa-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e7aa-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e7aa-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3e7aa-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3e7aa-239">Testing single sign-on</span></span>

<span data-ttu-id="3e7aa-240">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e7aa-241">Quando você clica em bloco Lesson.ly Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Lesson.ly aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e7aa-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e7aa-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3e7aa-242">Additional resources</span></span>

* [<span data-ttu-id="3e7aa-243">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3e7aa-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e7aa-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3e7aa-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

