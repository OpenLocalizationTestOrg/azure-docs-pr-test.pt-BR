---
title: "Tutorial: Integração do Azure Active Directory ao myPolicies | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="9ec83-103">Tutorial: Integração do Azure Active Directory ao myPolicies</span><span class="sxs-lookup"><span data-stu-id="9ec83-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="9ec83-104">Neste tutorial, você aprenderá como myPolicies toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9ec83-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ec83-105">Integrando myPolicies com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ec83-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ec83-106">Você pode controlar no AD do Azure que tenha acesso toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="9ec83-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="9ec83-107">Você pode habilitar seus usuários tooautomatically get conectado toomyPolicies (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ec83-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9ec83-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ec83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ec83-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ec83-110">Prerequisites</span></span>

<span data-ttu-id="9ec83-111">tooconfigure integração do AD do Azure com myPolicies, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ec83-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="9ec83-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ec83-113">Uma assinatura habilitada para logon único do myPolicies</span><span class="sxs-lookup"><span data-stu-id="9ec83-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ec83-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9ec83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ec83-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9ec83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ec83-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9ec83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ec83-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ec83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ec83-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9ec83-118">Scenario description</span></span>
<span data-ttu-id="9ec83-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9ec83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ec83-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9ec83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ec83-121">Adicionando myPolicies da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9ec83-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="9ec83-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="9ec83-123">Adicionando myPolicies da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9ec83-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="9ec83-124">integração de saudação tooconfigure de myPolicies no AD do Azure, você precisa myPolicies tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9ec83-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ec83-125">**myPolicies tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ec83-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ec83-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9ec83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ec83-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9ec83-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9ec83-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9ec83-133">Na caixa de pesquisa hello, digite **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-133">In hello search box, type **myPolicies**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="9ec83-135">No painel de resultados de saudação, selecione **myPolicies**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9ec83-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ec83-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ec83-138">Nesta seção, você configura e testa o logon único do Azure AD com o myPolicies, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9ec83-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ec83-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em myPolicies é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec83-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="9ec83-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em myPolicies precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9ec83-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="9ec83-141">MyPolicies, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9ec83-142">tooconfigure e teste de logon único do AD do Azure com myPolicies, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ec83-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ec83-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9ec83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ec83-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ec83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ec83-145">**[Criar um usuário de teste myPolicies](#creating-a-mypolicies-test-user)**  -toohave um equivalente do Britta Simon em myPolicies é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9ec83-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ec83-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9ec83-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ec83-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9ec83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ec83-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ec83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ec83-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo myPolicies.</span><span class="sxs-lookup"><span data-stu-id="9ec83-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="9ec83-150">**tooconfigure AD do Azure-logon único com myPolicies, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ec83-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ec83-151">Em Olá portal do Azure, Olá **myPolicies** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9ec83-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9ec83-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="9ec83-155">Em Olá **myPolicies domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ec83-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="9ec83-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ec83-157">a.</span></span> <span data-ttu-id="9ec83-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="9ec83-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="9ec83-159">b.</span><span class="sxs-lookup"><span data-stu-id="9ec83-159">b.</span></span> <span data-ttu-id="9ec83-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="9ec83-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ec83-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9ec83-161">These values are not real.</span></span> <span data-ttu-id="9ec83-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9ec83-163">Entre em contato com [myPolicies equipe de suporte](mailto:support@mypolicies.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="9ec83-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="9ec83-164">aplicativo de myPolicies Hello espera asserções SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="9ec83-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="9ec83-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ec83-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="9ec83-166">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="9ec83-167">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="9ec83-169">Clique em **exibir e editar todos os outros atributos de usuário** caixa de seleção no hello **atributos de usuário** seção tooexpand atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="9ec83-170">Executar Olá seguindo as etapas em cada um dos atributos de saudação exibida-</span><span class="sxs-lookup"><span data-stu-id="9ec83-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="9ec83-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9ec83-171">Attribute Name</span></span> | <span data-ttu-id="9ec83-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9ec83-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="9ec83-173">givenname</span><span class="sxs-lookup"><span data-stu-id="9ec83-173">givenname</span></span> | <span data-ttu-id="9ec83-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9ec83-174">user.givenname</span></span> |
    | <span data-ttu-id="9ec83-175">sobrenome</span><span class="sxs-lookup"><span data-stu-id="9ec83-175">surname</span></span> | <span data-ttu-id="9ec83-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="9ec83-176">user.surname</span></span> |
    | <span data-ttu-id="9ec83-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="9ec83-177">emailaddress</span></span> | <span data-ttu-id="9ec83-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="9ec83-178">user.mail</span></span> |
    | <span data-ttu-id="9ec83-179">name</span><span class="sxs-lookup"><span data-stu-id="9ec83-179">name</span></span> | <span data-ttu-id="9ec83-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9ec83-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="9ec83-181">a.</span><span class="sxs-lookup"><span data-stu-id="9ec83-181">a.</span></span> <span data-ttu-id="9ec83-182">Clique em saudação do hello atributo tooopen **Editar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="9ec83-184">b.</span><span class="sxs-lookup"><span data-stu-id="9ec83-184">b.</span></span> <span data-ttu-id="9ec83-185">Excluir o valor da URL de saudação da saudação **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="9ec83-186">c.</span><span class="sxs-lookup"><span data-stu-id="9ec83-186">c.</span></span> <span data-ttu-id="9ec83-187">Clique em **Okey** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="9ec83-188">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9ec83-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="9ec83-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9ec83-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9ec83-192">Em Olá **myPolicies configuração** seção, clique em **configurar myPolicies** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9ec83-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9ec83-193">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9ec83-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="9ec83-195">tooconfigure logon único no **myPolicies** lado, você precisa toosend Olá baixado **Certificate(Base64)** e **Single Sign-On URL do serviço SAML** muito[equipe de suporte do myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="9ec83-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="9ec83-196">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9ec83-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ec83-197">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ec83-198">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ec83-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ec83-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ec83-200">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec83-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9ec83-202">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ec83-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ec83-203">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9ec83-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ec83-205">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ec83-207">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ec83-209">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ec83-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ec83-211">a.</span><span class="sxs-lookup"><span data-stu-id="9ec83-211">a.</span></span> <span data-ttu-id="9ec83-212">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ec83-213">b.</span><span class="sxs-lookup"><span data-stu-id="9ec83-213">b.</span></span> <span data-ttu-id="9ec83-214">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9ec83-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ec83-215">c.</span><span class="sxs-lookup"><span data-stu-id="9ec83-215">c.</span></span> <span data-ttu-id="9ec83-216">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9ec83-217">d.</span><span class="sxs-lookup"><span data-stu-id="9ec83-217">d.</span></span> <span data-ttu-id="9ec83-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="9ec83-219">Criando um usuário de teste do myPolicies</span><span class="sxs-lookup"><span data-stu-id="9ec83-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="9ec83-220">Nesta seção, você cria um usuário chamado Brenda Fernandes no myPolicies.</span><span class="sxs-lookup"><span data-stu-id="9ec83-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="9ec83-221">Trabalhar com [myPolicies equipe de suporte](mailto:support@mypolicies.com) para adicionar usuários de saudação na plataforma de myPolicies hello.</span><span class="sxs-lookup"><span data-stu-id="9ec83-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="9ec83-222">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9ec83-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9ec83-223">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9ec83-224">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="9ec83-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9ec83-226">**tooassign Britta Simon toomyPolicies, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9ec83-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="9ec83-227">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9ec83-229">Na lista de aplicativos hello, selecione **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-229">In hello applications list, select **myPolicies**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="9ec83-231">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9ec83-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9ec83-233">Click **Add** button.</span></span> <span data-ttu-id="9ec83-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9ec83-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9ec83-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ec83-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ec83-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9ec83-239">Testing single sign-on</span></span>

<span data-ttu-id="9ec83-240">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ec83-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9ec83-241">Quando você clica em Olá myPolicies bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour myPolicies aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9ec83-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="9ec83-242">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9ec83-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ec83-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9ec83-243">Additional resources</span></span>

* [<span data-ttu-id="9ec83-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9ec83-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ec83-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ec83-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

