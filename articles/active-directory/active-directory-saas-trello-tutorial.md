---
title: "Tutorial: integração do Azure Active Directory ao Trello | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="049d1-103">Tutorial: integração do Azure Active Directory ao Trello</span><span class="sxs-lookup"><span data-stu-id="049d1-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="049d1-104">Neste tutorial, você aprenderá como toointegrate Trello com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="049d1-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="049d1-105">Integrando Trello com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="049d1-106">Você pode controlar no AD do Azure que tenha acesso tooTrello</span><span class="sxs-lookup"><span data-stu-id="049d1-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="049d1-107">Você pode habilitar seu usuários tooautomatically get conectado tooTrello (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="049d1-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="049d1-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="049d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="049d1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="049d1-110">Prerequisites</span></span>

<span data-ttu-id="049d1-111">tooconfigure integração do AD do Azure com Trello, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="049d1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="049d1-113">Uma assinatura do Trello habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="049d1-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="049d1-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="049d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="049d1-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="049d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="049d1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="049d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="049d1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="049d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="049d1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="049d1-118">Scenario description</span></span>
<span data-ttu-id="049d1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="049d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="049d1-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="049d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="049d1-121">Adicionando Trello da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="049d1-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="049d1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="049d1-123">Adicionando Trello da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="049d1-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="049d1-124">integração de saudação tooconfigure de Trello no AD do Azure, você precisa tooadd Trello da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="049d1-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="049d1-125">**tooadd Trello da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="049d1-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="049d1-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="049d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="049d1-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="049d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="049d1-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="049d1-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="049d1-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="049d1-133">Na caixa de pesquisa hello, digite **Trello**.</span><span class="sxs-lookup"><span data-stu-id="049d1-133">In hello search box, type **Trello**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="049d1-135">No painel de resultados de saudação, selecione **Trello**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="049d1-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="049d1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="049d1-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Trello, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="049d1-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="049d1-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Trello é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="049d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="049d1-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Trello precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="049d1-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="049d1-141">Trello, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="049d1-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="049d1-142">tooconfigure e teste de logon único do AD do Azure com Trello, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="049d1-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="049d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="049d1-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="049d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="049d1-145">**[Criar um usuário de teste Trello](#creating-a-trello-test-user)**  -toohave um equivalente do Britta Simon em Trello é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="049d1-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="049d1-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="049d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="049d1-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="049d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="049d1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="049d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="049d1-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Trello.</span><span class="sxs-lookup"><span data-stu-id="049d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="049d1-150">**tooconfigure AD do Azure-logon único com Trello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="049d1-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="049d1-151">Em Olá portal do Azure, Olá **Trello** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="049d1-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="049d1-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="049d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="049d1-155">Em Olá **Trello domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="049d1-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="049d1-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="049d1-158">Em Olá **Trello domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="049d1-160">a.</span><span class="sxs-lookup"><span data-stu-id="049d1-160">a.</span></span> <span data-ttu-id="049d1-161">Clique em Olá **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="049d1-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="049d1-162">b.</span><span class="sxs-lookup"><span data-stu-id="049d1-162">b.</span></span> <span data-ttu-id="049d1-163">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="049d1-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="049d1-164">Você deve obter Olá  **\<enterprise\>**  espaçador de Trello.</span><span class="sxs-lookup"><span data-stu-id="049d1-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="049d1-165">Se você não tiver o valor do campo de dados dinâmico Olá, entre em contato com [Trello a equipe de suporte](mailto:support@trello.com) tooget o campo de dados dinâmico Olá para você enterprise.</span><span class="sxs-lookup"><span data-stu-id="049d1-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="049d1-166">Aplicativo de Trello espera atributos específicos de toocontain Olá de asserções SAML.</span><span class="sxs-lookup"><span data-stu-id="049d1-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="049d1-167">Configure Olá seguintes atributos para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="049d1-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="049d1-168">Você pode gerenciar os valores hello desses atributos de saudação **"Atributos do usuário"** do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="049d1-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="049d1-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="049d1-169">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="049d1-171">Em Olá **atributos de tokens SAML** caixa de diálogo, para cada linha mostrada na tabela abaixo, a saudação execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="049d1-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="049d1-172">Attribute Name</span></span> | <span data-ttu-id="049d1-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="049d1-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="049d1-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="049d1-174">User.Email</span></span> | <span data-ttu-id="049d1-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="049d1-175">user.mail</span></span> |
    | <span data-ttu-id="049d1-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="049d1-176">User.FirstName</span></span> | <span data-ttu-id="049d1-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="049d1-177">user.givenname</span></span> |
    | <span data-ttu-id="049d1-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="049d1-178">User.LastName</span></span> | <span data-ttu-id="049d1-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="049d1-179">user.surname</span></span> |

    <span data-ttu-id="049d1-180">a.</span><span class="sxs-lookup"><span data-stu-id="049d1-180">a.</span></span> <span data-ttu-id="049d1-181">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049d1-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="049d1-184">b.</span><span class="sxs-lookup"><span data-stu-id="049d1-184">b.</span></span> <span data-ttu-id="049d1-185">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="049d1-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="049d1-186">c.</span><span class="sxs-lookup"><span data-stu-id="049d1-186">c.</span></span> <span data-ttu-id="049d1-187">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="049d1-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="049d1-188">d.</span><span class="sxs-lookup"><span data-stu-id="049d1-188">d.</span></span> <span data-ttu-id="049d1-189">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="049d1-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="049d1-190">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="049d1-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="049d1-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="049d1-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="049d1-194">Em Olá **Trello configuração** seção, clique em **configurar Trello** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="049d1-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="049d1-195">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="049d1-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="049d1-197">tooget SSO configurado para o seu aplicativo, vá muito[configuração de SSO enterprise Trello](https://trello.com/sso-configuration) página toosend [Trello a equipe de suporte](mailto:support@trello.com) Olá **Single Sign-On URL do serviço SAML** e Anexar Olá **certificado (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="049d1-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="049d1-198">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="049d1-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="049d1-199">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="049d1-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="049d1-200">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="049d1-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="049d1-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="049d1-202">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="049d1-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="049d1-204">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="049d1-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="049d1-205">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="049d1-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="049d1-207">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="049d1-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="049d1-209">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="049d1-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="049d1-211">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="049d1-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="049d1-213">a.</span><span class="sxs-lookup"><span data-stu-id="049d1-213">a.</span></span> <span data-ttu-id="049d1-214">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="049d1-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="049d1-215">b.</span><span class="sxs-lookup"><span data-stu-id="049d1-215">b.</span></span> <span data-ttu-id="049d1-216">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="049d1-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="049d1-217">c.</span><span class="sxs-lookup"><span data-stu-id="049d1-217">c.</span></span> <span data-ttu-id="049d1-218">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="049d1-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="049d1-219">d.</span><span class="sxs-lookup"><span data-stu-id="049d1-219">d.</span></span> <span data-ttu-id="049d1-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="049d1-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="049d1-221">Criando um usuário de teste do Trello</span><span class="sxs-lookup"><span data-stu-id="049d1-221">Creating a Trello test user</span></span>

<span data-ttu-id="049d1-222">Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello.</span><span class="sxs-lookup"><span data-stu-id="049d1-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="049d1-223">Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello.</span><span class="sxs-lookup"><span data-stu-id="049d1-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="049d1-224">Trello dá suporte ao provisionamento just-in-time e uma nova conta é criada primeira vez que entrar de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="049d1-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="049d1-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="049d1-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooTrello.</span><span class="sxs-lookup"><span data-stu-id="049d1-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="049d1-228">**tooassign Britta Simon tooTrello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="049d1-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="049d1-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="049d1-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="049d1-231">Na lista de aplicativos hello, selecione **Trello**.</span><span class="sxs-lookup"><span data-stu-id="049d1-231">In hello applications list, select **Trello**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="049d1-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="049d1-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="049d1-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="049d1-235">Click **Add** button.</span></span> <span data-ttu-id="049d1-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049d1-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="049d1-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="049d1-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="049d1-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049d1-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="049d1-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="049d1-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="049d1-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="049d1-241">Testing single sign-on</span></span>

<span data-ttu-id="049d1-242">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="049d1-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="049d1-243">Quando você clica em bloco Trello Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Trello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="049d1-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="049d1-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="049d1-244">Additional resources</span></span>

* [<span data-ttu-id="049d1-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="049d1-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="049d1-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="049d1-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

