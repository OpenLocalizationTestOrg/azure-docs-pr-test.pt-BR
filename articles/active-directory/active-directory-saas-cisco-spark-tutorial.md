---
title: "Tutorial: integração do Azure Active Directory com o Cisco Spark | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Spark Cisco."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="c886a-103">Tutorial: Integração do Azure Active Directory ao Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="c886a-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="c886a-104">Neste tutorial, você aprenderá como toointegrate Cisco despertar com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c886a-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c886a-105">Integrando Cisco Spark com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c886a-106">Você pode controlar no AD do Azure que tenha acesso tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="c886a-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="c886a-107">Você pode habilitar seu usuários tooautomatically get conectado tooCisco Spark (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c886a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c886a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c886a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c886a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c886a-110">Prerequisites</span></span>

<span data-ttu-id="c886a-111">tooconfigure integração do AD do Azure com o Cisco Spark, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="c886a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c886a-113">Uma assinatura habilitada para logon único do Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="c886a-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c886a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c886a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c886a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c886a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c886a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c886a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c886a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c886a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c886a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c886a-118">Scenario description</span></span>
<span data-ttu-id="c886a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c886a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c886a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c886a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c886a-121">Adicionando Cisco Spark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c886a-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="c886a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="c886a-123">Adicionando Cisco Spark da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c886a-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="c886a-124">integração de saudação tooconfigure do Cisco Spark no Azure AD, é necessário tooadd Cisco Spark na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c886a-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c886a-125">**tooadd Cisco Spark da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c886a-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c886a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c886a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c886a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c886a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c886a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c886a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c886a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c886a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c886a-133">Na caixa de pesquisa hello, digite **Spark Cisco**.</span><span class="sxs-lookup"><span data-stu-id="c886a-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="c886a-135">No painel de resultados de saudação, selecione **Cisco Spark**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c886a-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c886a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c886a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Cisco Spark com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c886a-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c886a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Spark Cisco é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c886a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="c886a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Spark Cisco precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c886a-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="c886a-141">No Spark Cisco, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c886a-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c886a-142">tooconfigure e teste de logon único do AD do Azure com o Cisco Spark, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c886a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c886a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c886a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c886a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c886a-145">**[Criar um usuário de teste do Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave um equivalente do Britta Simon no Spark Cisco que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c886a-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c886a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c886a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c886a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c886a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c886a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c886a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c886a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="c886a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="c886a-150">**tooconfigure AD do Azure-logon único com o Cisco Spark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c886a-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="c886a-151">Em Olá portal do Azure, Olá **Cisco Spark** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c886a-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c886a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c886a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="c886a-155">Em Olá **Cisco Spark domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="c886a-157">a.</span><span class="sxs-lookup"><span data-stu-id="c886a-157">a.</span></span> <span data-ttu-id="c886a-158">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="c886a-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="c886a-159">b.</span><span class="sxs-lookup"><span data-stu-id="c886a-159">b.</span></span> <span data-ttu-id="c886a-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c886a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c886a-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c886a-161">This value is not real.</span></span> <span data-ttu-id="c886a-162">Atualize esse valor com hello identificador real.</span><span class="sxs-lookup"><span data-stu-id="c886a-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="c886a-163">Entre em contato com [equipe de suporte do Cisco Spark cliente](https://support.ciscospark.com/) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="c886a-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="c886a-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c886a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="c886a-166">Aplicativo do Cisco Spark espera atributos específicos de toocontain Olá de asserções SAML.</span><span class="sxs-lookup"><span data-stu-id="c886a-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="c886a-167">Configure Olá seguintes atributos para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c886a-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="c886a-168">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** seção na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c886a-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="c886a-169">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="c886a-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="c886a-171">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem de saudação acima e execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="c886a-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="c886a-172">Attribute Name</span></span>  | <span data-ttu-id="c886a-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="c886a-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="c886a-174">uid</span><span class="sxs-lookup"><span data-stu-id="c886a-174">uid</span></span>    | <span data-ttu-id="c886a-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c886a-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="c886a-176">a.</span><span class="sxs-lookup"><span data-stu-id="c886a-176">a.</span></span> <span data-ttu-id="c886a-177">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c886a-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c886a-180">b.</span><span class="sxs-lookup"><span data-stu-id="c886a-180">b.</span></span> <span data-ttu-id="c886a-181">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="c886a-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="c886a-182">c.</span><span class="sxs-lookup"><span data-stu-id="c886a-182">c.</span></span> <span data-ttu-id="c886a-183">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="c886a-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c886a-184">d.</span><span class="sxs-lookup"><span data-stu-id="c886a-184">d.</span></span> <span data-ttu-id="c886a-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c886a-185">Click **Ok**.</span></span>

7. <span data-ttu-id="c886a-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c886a-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c886a-188">Entrar muito[Cisco nuvem colaboração gerenciamento](https://admin.ciscospark.com/) com suas credenciais de administrador completo.</span><span class="sxs-lookup"><span data-stu-id="c886a-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="c886a-189">Selecione **configurações** e em Olá **autenticação** seção, clique em **modificar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="c886a-191">Escolha **Integrar um provedor de identidade de terceiros. (Avançado)**  e toohello vá próxima tela.</span><span class="sxs-lookup"><span data-stu-id="c886a-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="c886a-192">Em Olá **importar metadados de Idp** página, ou arraste e solte o arquivo de metadados de saudação do AD do Azure para a página de saudação ou usar toolocate de opção de navegador de arquivo hello e carregar o arquivo de metadados de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c886a-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="c886a-193">Em seguida, escolha **Exigir certificado assinado por uma autoridade de certificação em Metadados (mais seguro)** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="c886a-195">Escolha **Testar Conexão SSO** e, quando uma nova guia do navegador for aberta, autentique-se com o Azure AD conectando-se.</span><span class="sxs-lookup"><span data-stu-id="c886a-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="c886a-196">Retornar toohello **Cisco nuvem colaboração gerenciamento** guia do navegador. Se o teste de saudação foi bem-sucedido, selecione **esse teste foi bem-sucedido. Habilitar Logon Único** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="c886a-197">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c886a-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c886a-198">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c886a-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c886a-199">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c886a-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c886a-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="c886a-201">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c886a-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c886a-203">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c886a-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c886a-204">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c886a-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c886a-206">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c886a-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c886a-208">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c886a-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c886a-210">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c886a-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c886a-212">a.</span><span class="sxs-lookup"><span data-stu-id="c886a-212">a.</span></span> <span data-ttu-id="c886a-213">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c886a-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c886a-214">b.</span><span class="sxs-lookup"><span data-stu-id="c886a-214">b.</span></span> <span data-ttu-id="c886a-215">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c886a-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c886a-216">c.</span><span class="sxs-lookup"><span data-stu-id="c886a-216">c.</span></span> <span data-ttu-id="c886a-217">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c886a-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c886a-218">d.</span><span class="sxs-lookup"><span data-stu-id="c886a-218">d.</span></span> <span data-ttu-id="c886a-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="c886a-220">Criando um usuário de teste do Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="c886a-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="c886a-221">Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="c886a-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="c886a-222">Nesta seção, você criará um usuário chamado Brenda Fernandes no Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="c886a-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="c886a-223">Vá toohello [Cisco nuvem colaboração gerenciamento](https://admin.ciscospark.com/) com suas credenciais de administrador completo.</span><span class="sxs-lookup"><span data-stu-id="c886a-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="c886a-224">Clique em **Usuários** e em **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c886a-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="c886a-226">Em Olá **usuário gerenciar** janela, selecione **adicionar manualmente ou modificar a usuários** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c886a-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="c886a-227">Escolha **Nomes e Endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="c886a-227">Select **Names and Email address**.</span></span> <span data-ttu-id="c886a-228">Em seguida, preencha o texto de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c886a-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="c886a-230">a.</span><span class="sxs-lookup"><span data-stu-id="c886a-230">a.</span></span> <span data-ttu-id="c886a-231">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c886a-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="c886a-232">b.</span><span class="sxs-lookup"><span data-stu-id="c886a-232">b.</span></span> <span data-ttu-id="c886a-233">Em Olá **Sobrenome** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c886a-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="c886a-234">c.</span><span class="sxs-lookup"><span data-stu-id="c886a-234">c.</span></span> <span data-ttu-id="c886a-235">Em Olá **endereço de Email** caixa de texto, tipo  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c886a-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="c886a-236">Clique em hello mais entrar tooadd Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c886a-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="c886a-237">Em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="c886a-238">Em Olá **adicionar serviços para os usuários** janela, clique em **salvar** e **concluir**.</span><span class="sxs-lookup"><span data-stu-id="c886a-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c886a-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c886a-240">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="c886a-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c886a-242">**tooassign Britta Simon tooCisco Spark, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c886a-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="c886a-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c886a-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c886a-245">Na lista de aplicativos hello, selecione **Spark Cisco**.</span><span class="sxs-lookup"><span data-stu-id="c886a-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="c886a-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c886a-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c886a-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c886a-249">Click **Add** button.</span></span> <span data-ttu-id="c886a-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c886a-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c886a-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c886a-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c886a-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c886a-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c886a-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c886a-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c886a-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c886a-255">Testing single sign-on</span></span>

<span data-ttu-id="c886a-256">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c886a-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c886a-257">Quando você clica em bloco Cisco Spark Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="c886a-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c886a-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c886a-258">Additional resources</span></span>

* [<span data-ttu-id="c886a-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c886a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c886a-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c886a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

