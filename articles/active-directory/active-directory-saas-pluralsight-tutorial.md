---
title: "Tutorial: integração do Azure Active Directory ao Pluralsight | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="e959a-103">Tutorial: Integração do Azure Active Directory com o Pluralsight</span><span class="sxs-lookup"><span data-stu-id="e959a-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="e959a-104">Neste tutorial, você aprenderá como toointegrate Pluralsight com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e959a-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e959a-105">Integrando Pluralsight AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e959a-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e959a-106">Você pode controlar no AD do Azure que tenha acesso tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="e959a-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="e959a-107">Você pode habilitar seu usuários tooautomatically get conectado tooPluralsight (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e959a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e959a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e959a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e959a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e959a-110">Prerequisites</span></span>

<span data-ttu-id="e959a-111">tooconfigure integração do AD do Azure com Pluralsight, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e959a-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="e959a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e959a-113">Uma assinatura habilitada para logon único do Pluralsight</span><span class="sxs-lookup"><span data-stu-id="e959a-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e959a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e959a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e959a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e959a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e959a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e959a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e959a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e959a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e959a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e959a-118">Scenario description</span></span>
<span data-ttu-id="e959a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e959a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e959a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e959a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e959a-121">Adicionando Pluralsight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e959a-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="e959a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="e959a-123">Adicionando Pluralsight da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e959a-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="e959a-124">integração de saudação tooconfigure do Pluralsight no AD do Azure, você precisa tooadd Pluralsight na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e959a-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e959a-125">**tooadd Pluralsight da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e959a-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e959a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e959a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e959a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e959a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e959a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e959a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e959a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e959a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e959a-133">Na caixa de pesquisa hello, digite **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="e959a-133">In hello search box, type **Pluralsight**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="e959a-135">No painel de resultados de saudação, selecione **Pluralsight**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e959a-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e959a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e959a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Pluralsight, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="e959a-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e959a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na Pluralsight é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e959a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="e959a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Pluralsight precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e959a-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="e959a-141">Pluralsight, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e959a-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e959a-142">tooconfigure e teste de logon único do AD do Azure com Pluralsight, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e959a-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e959a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e959a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e959a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e959a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e959a-145">**[Criar um usuário de teste do Pluralsight](#creating-a-pluralsight-test-user)**  -toohave um equivalente do Britta Simon na Pluralsight é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e959a-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e959a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e959a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e959a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e959a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e959a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e959a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e959a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="e959a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="e959a-150">**tooconfigure AD do Azure-logon único com Pluralsight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e959a-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="e959a-151">Em Olá portal do Azure, Olá **Pluralsight** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e959a-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e959a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e959a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="e959a-155">Em Olá **domínio Pluralsight e URLs** , execute o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e959a-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="e959a-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="e959a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e959a-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="e959a-158">This value is not real.</span></span> <span data-ttu-id="e959a-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="e959a-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e959a-160">Entre em contato com [equipe de suporte do cliente do Pluralsight](mailto:support@pluralsight.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="e959a-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="e959a-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e959a-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="e959a-163">Olá objetivo desta seção é tooenable AD do Azure-logon único no hello portal do Azure e tooconfigure SSO no aplicativo do Pluralsight hello.</span><span class="sxs-lookup"><span data-stu-id="e959a-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="e959a-164">Olá Pluralsight aplicativo espera as asserções de SAML de saudação em um formato específico, o que exige que você tooadd atributo personalizado mapeamentos tooyour atributos de token configuração SAML.</span><span class="sxs-lookup"><span data-stu-id="e959a-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="e959a-165">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="e959a-165">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="e959a-167">Você também pode adicionar Olá **"ID exclusivo"** atributo com hello valor apropriado como EmployeeID ou algo que se adapta à sua organização.</span><span class="sxs-lookup"><span data-stu-id="e959a-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="e959a-168">Também Observe que isso não é atributo obrigatório do hello; No entanto, você pode adicioná-lo muito identificar usuário exclusivo hello.</span><span class="sxs-lookup"><span data-stu-id="e959a-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="e959a-169">Olá tooadd necessário **atributos de tokens SAML**, para cada linha mostrada na tabela de saudação abaixo, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e959a-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="e959a-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="e959a-170">Attribute Name</span></span> | <span data-ttu-id="e959a-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="e959a-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="e959a-172">Nome</span><span class="sxs-lookup"><span data-stu-id="e959a-172">First Name</span></span> |<span data-ttu-id="e959a-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e959a-173">user.givenname</span></span> |
   | <span data-ttu-id="e959a-174">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="e959a-174">Last Name</span></span> |<span data-ttu-id="e959a-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="e959a-175">user.surname</span></span> |
   | <span data-ttu-id="e959a-176">Email</span><span class="sxs-lookup"><span data-stu-id="e959a-176">Email</span></span> |<span data-ttu-id="e959a-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="e959a-177">user.mail</span></span> |
   
   <span data-ttu-id="e959a-178">a.</span><span class="sxs-lookup"><span data-stu-id="e959a-178">a.</span></span> <span data-ttu-id="e959a-179">Clique em **Adicionar atributo de usuário** tooopen Olá **adicionar usuário Attribure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e959a-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="e959a-181">b.</span><span class="sxs-lookup"><span data-stu-id="e959a-181">b.</span></span> <span data-ttu-id="e959a-182">Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="e959a-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="e959a-183">c.</span><span class="sxs-lookup"><span data-stu-id="e959a-183">c.</span></span> <span data-ttu-id="e959a-184">De saudação **o valor do atributo** lista, o valor do atributo select Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="e959a-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="e959a-185">d.</span><span class="sxs-lookup"><span data-stu-id="e959a-185">d.</span></span> <span data-ttu-id="e959a-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e959a-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="e959a-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e959a-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e959a-189">tooget SSO configurado para o seu aplicativo, entre em contato com [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) da equipe e forneça o arquivo de metadados baixado hello.</span><span class="sxs-lookup"><span data-stu-id="e959a-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="e959a-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e959a-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e959a-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e959a-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e959a-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e959a-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e959a-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e959a-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e959a-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e959a-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e959a-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e959a-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e959a-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e959a-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e959a-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e959a-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e959a-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e959a-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e959a-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e959a-205">a.</span><span class="sxs-lookup"><span data-stu-id="e959a-205">a.</span></span> <span data-ttu-id="e959a-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e959a-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e959a-207">b.</span><span class="sxs-lookup"><span data-stu-id="e959a-207">b.</span></span> <span data-ttu-id="e959a-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e959a-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e959a-209">c.</span><span class="sxs-lookup"><span data-stu-id="e959a-209">c.</span></span> <span data-ttu-id="e959a-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e959a-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e959a-211">d.</span><span class="sxs-lookup"><span data-stu-id="e959a-211">d.</span></span> <span data-ttu-id="e959a-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e959a-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="e959a-213">Criar um usuário de teste do Pluralsight</span><span class="sxs-lookup"><span data-stu-id="e959a-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="e959a-214">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="e959a-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="e959a-215">Trabalhe com [equipe de suporte do cliente do Pluralsight](mailto:support@pluralsight.com) tooadd usuários Olá Olá Pluralsight conta.</span><span class="sxs-lookup"><span data-stu-id="e959a-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e959a-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e959a-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooPluralsight.</span><span class="sxs-lookup"><span data-stu-id="e959a-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e959a-219">**tooassign Britta Simon tooPluralsight, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e959a-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="e959a-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e959a-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e959a-222">Na lista de aplicativos hello, selecione **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="e959a-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="e959a-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e959a-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e959a-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e959a-226">Click **Add** button.</span></span> <span data-ttu-id="e959a-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e959a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e959a-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e959a-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e959a-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e959a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e959a-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e959a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e959a-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e959a-232">Testing single sign-on</span></span>

<span data-ttu-id="e959a-233">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e959a-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e959a-234">Quando você clica em bloco Pluralsight Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Pluralsight aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e959a-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="e959a-235">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e959a-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e959a-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e959a-236">Additional resources</span></span>

* [<span data-ttu-id="e959a-237">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e959a-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e959a-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e959a-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

