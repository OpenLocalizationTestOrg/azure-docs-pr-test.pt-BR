---
title: "Tutorial: Integração do Azure Active Directory ao Datahug | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="b2f21-103">Tutorial: integração do Azure Active Directory ao Datahug</span><span class="sxs-lookup"><span data-stu-id="b2f21-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="b2f21-104">Neste tutorial, você aprenderá como toointegrate Datahug com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b2f21-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2f21-105">Integrando Datahug com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f21-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b2f21-106">Você pode controlar no AD do Azure que tenha acesso tooDatahug</span><span class="sxs-lookup"><span data-stu-id="b2f21-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="b2f21-107">Você pode habilitar seu usuários tooautomatically get conectado tooDatahug (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2f21-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b2f21-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="b2f21-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="b2f21-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2f21-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2f21-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2f21-111">Prerequisites</span></span>

<span data-ttu-id="b2f21-112">tooconfigure integração do AD do Azure com Datahug, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f21-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="b2f21-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-113">An Azure AD subscription</span></span>
- <span data-ttu-id="b2f21-114">Uma assinatura do Datahug com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="b2f21-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b2f21-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b2f21-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b2f21-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b2f21-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2f21-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b2f21-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b2f21-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2f21-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b2f21-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b2f21-119">Scenario description</span></span>
<span data-ttu-id="b2f21-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b2f21-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2f21-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b2f21-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2f21-122">Adicionando Datahug da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b2f21-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="b2f21-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="b2f21-124">Adicionando Datahug da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b2f21-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="b2f21-125">integração de saudação tooconfigure de Datahug no AD do Azure, você precisa tooadd Datahug da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b2f21-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b2f21-126">**tooadd Datahug da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b2f21-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2f21-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b2f21-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b2f21-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b2f21-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b2f21-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2f21-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b2f21-134">Na caixa de pesquisa hello, digite **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-134">In hello search box, type **Datahug**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="b2f21-136">No painel de resultados de saudação, selecione **Datahug**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b2f21-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2f21-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2f21-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Datahug, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="b2f21-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b2f21-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Datahug é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2f21-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="b2f21-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Datahug precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b2f21-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="b2f21-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Datahug.</span><span class="sxs-lookup"><span data-stu-id="b2f21-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="b2f21-143">tooconfigure e teste de logon único do AD do Azure com Datahug, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f21-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b2f21-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b2f21-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b2f21-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b2f21-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b2f21-146">**[Criar um usuário de teste Datahug](#creating-a-datahug-test-user)**  -toohave um equivalente do Britta Simon em Datahug é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2f21-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b2f21-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b2f21-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2f21-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b2f21-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2f21-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2f21-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2f21-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Datahug.</span><span class="sxs-lookup"><span data-stu-id="b2f21-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="b2f21-151">**tooconfigure AD do Azure-logon único com Datahug, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b2f21-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2f21-152">Em Olá portal do Azure, Olá **Datahug** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b2f21-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b2f21-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="b2f21-156">Em Olá **Datahug domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="b2f21-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="b2f21-158">a.</span><span class="sxs-lookup"><span data-stu-id="b2f21-158">a.</span></span> <span data-ttu-id="b2f21-159">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="b2f21-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="b2f21-160">b.</span><span class="sxs-lookup"><span data-stu-id="b2f21-160">b.</span></span> <span data-ttu-id="b2f21-161">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="b2f21-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="b2f21-162">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="b2f21-163">Se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="b2f21-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="b2f21-165">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="b2f21-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b2f21-166">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="b2f21-166">These values are not hello real.</span></span> <span data-ttu-id="b2f21-167">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f21-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b2f21-168">Aqui, sugerimos você toouse Olá valor exclusivo de cadeia de caracteres em Olá identificador e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="b2f21-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="b2f21-169">Entre em contato com [equipe de suporte do cliente Datahug](http://datahug.com/about/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b2f21-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="b2f21-170">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b2f21-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="b2f21-172">Verificar **"Mostrar configurações de assinatura de certificado avançadas"** e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f21-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="b2f21-174">a.</span><span class="sxs-lookup"><span data-stu-id="b2f21-174">a.</span></span> <span data-ttu-id="b2f21-175">Em **Opção de Assinatura**, selecione **Assinar declaração SAML**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="b2f21-176">b.</span><span class="sxs-lookup"><span data-stu-id="b2f21-176">b.</span></span> <span data-ttu-id="b2f21-177">Em **Algoritmo de assinatura**, selecione **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="b2f21-178">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b2f21-178">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="b2f21-180">Em Olá **Datahug configuração** seção, clique em **configurar Datahug** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b2f21-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b2f21-181">Saudação de cópia **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b2f21-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="b2f21-183">tooconfigure logon único no **Datahug** lado, você precisa toosend Olá baixado **Metadata XML**, **ID da entidade SAML** e **serviço de logon único SAML URL** muito[Datahug suporte](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="b2f21-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="b2f21-184">Eles definidos neste aplicativo backup toohave Olá conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="b2f21-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b2f21-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b2f21-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b2f21-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f21-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b2f21-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b2f21-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2f21-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2f21-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2f21-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b2f21-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b2f21-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2f21-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b2f21-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2f21-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2f21-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f21-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2f21-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2f21-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2f21-200">a.</span><span class="sxs-lookup"><span data-stu-id="b2f21-200">a.</span></span> <span data-ttu-id="b2f21-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2f21-202">b.</span><span class="sxs-lookup"><span data-stu-id="b2f21-202">b.</span></span> <span data-ttu-id="b2f21-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b2f21-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2f21-204">c.</span><span class="sxs-lookup"><span data-stu-id="b2f21-204">c.</span></span> <span data-ttu-id="b2f21-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b2f21-206">d.</span><span class="sxs-lookup"><span data-stu-id="b2f21-206">d.</span></span> <span data-ttu-id="b2f21-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="b2f21-208">Criar um usuário de teste Datahug</span><span class="sxs-lookup"><span data-stu-id="b2f21-208">Creating a Datahug test user</span></span>

<span data-ttu-id="b2f21-209">tooenable AD do Azure usuários toolog em tooDatahug, eles devem ser provisionados no Datahug.</span><span class="sxs-lookup"><span data-stu-id="b2f21-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="b2f21-210">Quando se usa o Datahug, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b2f21-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="b2f21-211">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b2f21-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2f21-212">Faça logon no tooyour Datahug site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b2f21-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="b2f21-213">Passe o mouse sobre Olá **engrenagem** no canto direito superior de saudação e clique em **configurações**</span><span class="sxs-lookup"><span data-stu-id="b2f21-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="b2f21-215">Escolha **pessoas** e clique em Olá **adicionar usuários** guia</span><span class="sxs-lookup"><span data-stu-id="b2f21-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="b2f21-217">Digite hello email da pessoa Olá você gostaria que toocreate uma conta para e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="b2f21-219">Você pode enviar toouser de email de registro selecionando **enviar email de boas-vinda** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="b2f21-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="b2f21-220">Se você estiver criando uma conta do Salesforce não enviar email de boas-vindas hello.</span><span class="sxs-lookup"><span data-stu-id="b2f21-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b2f21-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b2f21-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="b2f21-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b2f21-224">**tooassign Britta Simon tooDatahug, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b2f21-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2f21-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b2f21-227">Na lista de aplicativos hello, selecione **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-227">In hello applications list, select **Datahug**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="b2f21-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b2f21-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b2f21-231">Click **Add** button.</span></span> <span data-ttu-id="b2f21-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2f21-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b2f21-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f21-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b2f21-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2f21-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2f21-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2f21-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b2f21-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b2f21-237">Testing single sign-on</span></span>

<span data-ttu-id="b2f21-238">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2f21-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="b2f21-239">Quando você clica em bloco Datahug Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Datahug aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b2f21-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="b2f21-240">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b2f21-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b2f21-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b2f21-241">Additional resources</span></span>

* [<span data-ttu-id="b2f21-242">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b2f21-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2f21-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b2f21-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

