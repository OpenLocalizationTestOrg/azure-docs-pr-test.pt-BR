---
title: "Tutorial: integração do Azure Active Directory com o FilesAnywhere | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="1448b-103">Tutorial: Integração do Azure Active Directory com o FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="1448b-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="1448b-104">Neste tutorial, você aprenderá como toointegrate FilesAnywhere com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1448b-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1448b-105">Integrando FilesAnywhere com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1448b-106">Você pode controlar no AD do Azure que tenha acesso tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="1448b-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="1448b-107">Você pode habilitar seu usuários tooautomatically get conectado tooFilesAnywhere (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1448b-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="1448b-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="1448b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1448b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1448b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1448b-110">Prerequisites</span></span>

<span data-ttu-id="1448b-111">tooconfigure integração do AD do Azure com FilesAnywhere, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="1448b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1448b-113">Uma assinatura do FilesAnywhere habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1448b-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1448b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1448b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1448b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1448b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1448b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1448b-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1448b-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1448b-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1448b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1448b-118">Scenario description</span></span>
<span data-ttu-id="1448b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1448b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1448b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1448b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1448b-121">Adicionando FilesAnywhere da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1448b-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="1448b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="1448b-123">Adicionando FilesAnywhere da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1448b-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="1448b-124">integração de saudação tooconfigure de FilesAnywhere no AD do Azure, você precisa tooadd FilesAnywhere da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1448b-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1448b-125">**tooadd FilesAnywhere da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1448b-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1448b-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1448b-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1448b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1448b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1448b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1448b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1448b-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1448b-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1448b-133">Na caixa de pesquisa hello, digite **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="1448b-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="1448b-135">No painel de resultados de saudação, selecione **FilesAnywhere**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1448b-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1448b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1448b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FilesAnywhere, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1448b-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1448b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em FilesAnywhere é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1448b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="1448b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em FilesAnywhere precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1448b-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="1448b-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="1448b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="1448b-142">tooconfigure e teste de logon único do AD do Azure com FilesAnywhere, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1448b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1448b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1448b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1448b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1448b-145">**[Criar um usuário de teste FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave um equivalente do Britta Simon em FilesAnywhere é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="1448b-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="1448b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1448b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="1448b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1448b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1448b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1448b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1448b-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="1448b-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="1448b-150">**tooconfigure AD do Azure-logon único com FilesAnywhere, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1448b-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="1448b-151">No portal de gerenciamento do Azure do hello, no hello **FilesAnywhere** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1448b-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1448b-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="1448b-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="1448b-155">Em Olá **FilesAnywhere domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**:</span><span class="sxs-lookup"><span data-stu-id="1448b-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="1448b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1448b-157">a.</span></span> <span data-ttu-id="1448b-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="1448b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="1448b-159">Observe que esse valor Olá **215** é um **clientid** e é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="1448b-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="1448b-160">Você precisa tooreplace com o valor do hello clientid real.</span><span class="sxs-lookup"><span data-stu-id="1448b-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="1448b-161">Em Olá **FilesAnywhere domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="1448b-163">a.</span><span class="sxs-lookup"><span data-stu-id="1448b-163">a.</span></span> <span data-ttu-id="1448b-164">Clique em Olá **Mostrar configurações de URL avançadas** opção</span><span class="sxs-lookup"><span data-stu-id="1448b-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="1448b-165">b.</span><span class="sxs-lookup"><span data-stu-id="1448b-165">b.</span></span> <span data-ttu-id="1448b-166">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="1448b-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1448b-167">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="1448b-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="1448b-168">Você tem tooupdate esses valores com a URL real Olá URL de logon e de resposta.</span><span class="sxs-lookup"><span data-stu-id="1448b-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="1448b-169">Entre em contato com [FilesAnywhere a equipe de suporte](mailto:support@FilesAnywhere.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="1448b-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="1448b-170">Aplicativo de FilesAnywhere Software espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="1448b-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1448b-171">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1448b-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="1448b-172">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1448b-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1448b-173">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="1448b-173">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="1448b-175">Olá quando os usuários inscreve-se com FilesAnywhere recebem o valor de saudação do **clientid** de atributo de [FilesAnywhere equipe](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="1448b-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="1448b-176">Você tem o atributo de "Id do cliente" hello tooadd com valor exclusivo de saudação fornecido pela FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="1448b-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="1448b-177">Todos esses atributos mostrados acima são necessários.</span><span class="sxs-lookup"><span data-stu-id="1448b-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="1448b-178">Observe que esse valor Olá **2331** de **clientid** é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="1448b-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="1448b-179">É necessário o valor real do tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="1448b-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="1448b-180">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="1448b-181">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="1448b-181">Attribute Name</span></span> | <span data-ttu-id="1448b-182">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="1448b-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="1448b-183">clientid</span><span class="sxs-lookup"><span data-stu-id="1448b-183">clientid</span></span> | <span data-ttu-id="1448b-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="1448b-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="1448b-185">a.</span><span class="sxs-lookup"><span data-stu-id="1448b-185">a.</span></span> <span data-ttu-id="1448b-186">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1448b-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="1448b-189">b.</span><span class="sxs-lookup"><span data-stu-id="1448b-189">b.</span></span> <span data-ttu-id="1448b-190">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="1448b-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="1448b-191">c.</span><span class="sxs-lookup"><span data-stu-id="1448b-191">c.</span></span> <span data-ttu-id="1448b-192">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="1448b-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1448b-193">d.</span><span class="sxs-lookup"><span data-stu-id="1448b-193">d.</span></span> <span data-ttu-id="1448b-194">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="1448b-194">Click **Ok**</span></span>

7. <span data-ttu-id="1448b-195">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1448b-195">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1448b-197">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1448b-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="1448b-199">Em Olá **FilesAnywhere configuração** seção, clique em **configurar FilesAnywhere** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="1448b-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="1448b-202">configuração de SSO de tooget concluída para o seu aplicativo FilesAnywhere final, entre em contato com [FilesAnywhere a equipe de suporte](mailto:support@FilesAnywhere.com) e fornecê-los a URL de logon único (SSO) e de certificado de assinatura de token SAML Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="1448b-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1448b-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="1448b-204">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1448b-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1448b-206">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1448b-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1448b-207">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1448b-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1448b-209">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="1448b-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1448b-211">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1448b-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1448b-213">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1448b-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1448b-215">a.</span><span class="sxs-lookup"><span data-stu-id="1448b-215">a.</span></span> <span data-ttu-id="1448b-216">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1448b-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1448b-217">b.</span><span class="sxs-lookup"><span data-stu-id="1448b-217">b.</span></span> <span data-ttu-id="1448b-218">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1448b-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1448b-219">c.</span><span class="sxs-lookup"><span data-stu-id="1448b-219">c.</span></span> <span data-ttu-id="1448b-220">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1448b-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1448b-221">d.</span><span class="sxs-lookup"><span data-stu-id="1448b-221">d.</span></span> <span data-ttu-id="1448b-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1448b-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="1448b-223">Criando um usuário de teste do FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="1448b-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="1448b-224">Aplicativo dá suporte apenas durante o provisionamento do usuário e depois que os usuários de autenticação serão criados no aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1448b-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1448b-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1448b-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooFilesAnywhere seu acesso.</span><span class="sxs-lookup"><span data-stu-id="1448b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1448b-228">**tooassign Britta Simon tooFilesAnywhere, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1448b-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="1448b-229">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1448b-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1448b-231">Na lista de aplicativos hello, selecione **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="1448b-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="1448b-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1448b-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1448b-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1448b-235">Click **Add** button.</span></span> <span data-ttu-id="1448b-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1448b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1448b-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1448b-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1448b-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1448b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1448b-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1448b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="1448b-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1448b-241">Testing single sign-on</span></span>

<span data-ttu-id="1448b-242">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1448b-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1448b-243">Quando você clica em bloco FilesAnywhere Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour FilesAnywhere aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1448b-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1448b-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1448b-244">Additional resources</span></span>

* [<span data-ttu-id="1448b-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1448b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1448b-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1448b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
