---
title: "Tutorial: Integração do Azure Active Directory ao BetterWorks | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="a6448-103">Tutorial: integração do Azure Active Directory ao BetterWorks</span><span class="sxs-lookup"><span data-stu-id="a6448-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="a6448-104">Neste tutorial, você aprenderá como toointegrate BetterWorks com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a6448-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6448-105">Integrando BetterWorks com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6448-106">Você pode controlar no AD do Azure que tenha acesso tooBetterWorks</span><span class="sxs-lookup"><span data-stu-id="a6448-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="a6448-107">Você pode habilitar seus usuários tooautomatically get conectado tooBetterWorks (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6448-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a6448-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6448-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6448-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6448-110">Prerequisites</span></span>

<span data-ttu-id="a6448-111">tooconfigure integração do AD do Azure com BetterWorks, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="a6448-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6448-113">Uma assinatura habilitada para logon único do BetterWorks</span><span class="sxs-lookup"><span data-stu-id="a6448-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6448-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a6448-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6448-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a6448-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6448-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a6448-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6448-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6448-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6448-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a6448-118">Scenario description</span></span>
<span data-ttu-id="a6448-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a6448-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6448-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a6448-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6448-121">Adicionando BetterWorks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a6448-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="a6448-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="a6448-123">Adicionando BetterWorks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a6448-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="a6448-124">integração de saudação tooconfigure de BetterWorks no AD do Azure, você precisa tooadd BetterWorks da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a6448-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6448-125">**tooadd BetterWorks da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6448-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6448-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6448-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6448-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a6448-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6448-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a6448-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a6448-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6448-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a6448-133">Na caixa de pesquisa hello, digite **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="a6448-133">In hello search box, type **BetterWorks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="a6448-135">No painel de resultados de saudação, selecione **BetterWorks**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a6448-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6448-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6448-138">Nesta seção, você configura e testa o logon único do Azure AD com o BetterWorks, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a6448-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6448-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em BetterWorks é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6448-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="a6448-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em BetterWorks precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a6448-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="a6448-141">BetterWorks, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6448-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a6448-142">tooconfigure e teste de logon único do AD do Azure com BetterWorks, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6448-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a6448-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6448-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6448-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6448-145">**[Criar um usuário de teste BetterWorks](#creating-a-betterworks-test-user)**  -toohave um equivalente do Britta Simon em BetterWorks é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a6448-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6448-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a6448-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6448-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a6448-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6448-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6448-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6448-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="a6448-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="a6448-150">**tooconfigure AD do Azure-logon único com BetterWorks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6448-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6448-151">Em Olá portal do Azure, Olá **BetterWorks** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a6448-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a6448-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a6448-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="a6448-155">Em Olá **BetterWorks domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado pelo IDP**:</span><span class="sxs-lookup"><span data-stu-id="a6448-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="a6448-157">a.</span><span class="sxs-lookup"><span data-stu-id="a6448-157">a.</span></span> <span data-ttu-id="a6448-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="a6448-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="a6448-159">b.</span><span class="sxs-lookup"><span data-stu-id="a6448-159">b.</span></span> <span data-ttu-id="a6448-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="a6448-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="a6448-161">Em Olá **BetterWorks domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **modo iniciado do SP**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="a6448-163">a.</span><span class="sxs-lookup"><span data-stu-id="a6448-163">a.</span></span> <span data-ttu-id="a6448-164">Clique em Olá **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="a6448-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a6448-165">b.</span><span class="sxs-lookup"><span data-stu-id="a6448-165">b.</span></span> <span data-ttu-id="a6448-166">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="a6448-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6448-167">Esses não são valores reais.</span><span class="sxs-lookup"><span data-stu-id="a6448-167">These are not real values.</span></span> <span data-ttu-id="a6448-168">Atualize esses valores com hello URL de resposta real URL de logon e de identificador.</span><span class="sxs-lookup"><span data-stu-id="a6448-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="a6448-169">Entre em contato com [BetterWorks equipe de suporte](mailto:support@betterworks.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="a6448-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="a6448-170">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a6448-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="a6448-172">Aplicativo de BetterWorks espera asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="a6448-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a6448-173">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="a6448-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="a6448-174">Você pode gerenciar os valores hello desses atributos de hello "**atributo**" Guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a6448-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="a6448-175">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="a6448-175">hello following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="a6448-177">Em Olá **atributos de tokens SAML** caixa de diálogo, para cada linha mostrada na tabela abaixo, a saudação execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="a6448-178">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a6448-178">Attribute Name</span></span> | <span data-ttu-id="a6448-179">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a6448-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="a6448-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="a6448-180">saml_token</span></span>     | <span data-ttu-id="a6448-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="a6448-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="a6448-182">a.</span><span class="sxs-lookup"><span data-stu-id="a6448-182">a.</span></span> <span data-ttu-id="a6448-183">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6448-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="a6448-186">b.</span><span class="sxs-lookup"><span data-stu-id="a6448-186">b.</span></span> <span data-ttu-id="a6448-187">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="a6448-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="a6448-188">c.</span><span class="sxs-lookup"><span data-stu-id="a6448-188">c.</span></span> <span data-ttu-id="a6448-189">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="a6448-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="a6448-190">d.</span><span class="sxs-lookup"><span data-stu-id="a6448-190">d.</span></span> <span data-ttu-id="a6448-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6448-191">Click **Ok**.</span></span>

7. <span data-ttu-id="a6448-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a6448-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a6448-194">tooconfigure logon único no **BetterWorks** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="a6448-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="a6448-195">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a6448-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6448-196">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a6448-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6448-197">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6448-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6448-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6448-199">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6448-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a6448-201">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6448-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6448-202">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6448-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6448-204">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a6448-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6448-206">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6448-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6448-208">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6448-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6448-210">a.</span><span class="sxs-lookup"><span data-stu-id="a6448-210">a.</span></span> <span data-ttu-id="a6448-211">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6448-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6448-212">b.</span><span class="sxs-lookup"><span data-stu-id="a6448-212">b.</span></span> <span data-ttu-id="a6448-213">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6448-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6448-214">c.</span><span class="sxs-lookup"><span data-stu-id="a6448-214">c.</span></span> <span data-ttu-id="a6448-215">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a6448-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a6448-216">d.</span><span class="sxs-lookup"><span data-stu-id="a6448-216">d.</span></span> <span data-ttu-id="a6448-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a6448-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="a6448-218">Criando um usuário de teste do BetterWorks</span><span class="sxs-lookup"><span data-stu-id="a6448-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="a6448-219">Nesta seção, você criará um usuário chamado Brenda Fernandes no BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="a6448-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="a6448-220">Trabalhar com [BetterWorks equipe de suporte](mailto:support@betterworks.com) tooadd usuários de saudação na plataforma de BetterWorks hello.</span><span class="sxs-lookup"><span data-stu-id="a6448-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a6448-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a6448-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBetterWorks.</span><span class="sxs-lookup"><span data-stu-id="a6448-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a6448-224">**tooassign Britta Simon tooBetterWorks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6448-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6448-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a6448-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a6448-227">Na lista de aplicativos hello, selecione **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="a6448-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="a6448-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6448-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a6448-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a6448-231">Click **Add** button.</span></span> <span data-ttu-id="a6448-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6448-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a6448-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6448-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6448-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6448-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6448-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6448-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6448-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a6448-237">Testing single sign-on</span></span>

<span data-ttu-id="a6448-238">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a6448-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6448-239">Quando você clica em Olá BetterWorks bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour BetterWorks aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6448-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6448-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a6448-240">Additional resources</span></span>

* [<span data-ttu-id="a6448-241">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a6448-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6448-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6448-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

