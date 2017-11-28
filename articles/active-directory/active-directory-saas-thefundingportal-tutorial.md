---
title: "Tutorial: Olá de integração do Active Directory do Azure com o financiamento Portal | Microsoft Docs"
description: "Saiba como tooconfigure único logon entre o Active Directory do Azure e Olá financiamento Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="f263c-103">Tutorial: Olá de integração do Active Directory do Azure com o financiamento Portal</span><span class="sxs-lookup"><span data-stu-id="f263c-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="f263c-104">Neste tutorial, você aprenderá como toointegrate Olá financiamento Portal com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f263c-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f263c-105">Integrando Olá financiamento Portal com o Azure AD fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f263c-106">Você pode controlar no AD do Azure que tenha acesso toohello capital Portal</span><span class="sxs-lookup"><span data-stu-id="f263c-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="f263c-107">Você pode habilitar seu usuários tooautomatically get conectado toohello Portal de capital (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f263c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f263c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f263c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f263c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f263c-110">Prerequisites</span></span>

<span data-ttu-id="f263c-111">integração de tooconfigure AD do Azure com hello capital Portal, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="f263c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f263c-113">Uma saudação financiamento Portal-logon único habilitado por assinatura</span><span class="sxs-lookup"><span data-stu-id="f263c-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f263c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f263c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f263c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f263c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f263c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f263c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f263c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f263c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f263c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f263c-118">Scenario description</span></span>
<span data-ttu-id="f263c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f263c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f263c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f263c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f263c-121">Adicionando Olá Portal capital da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f263c-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="f263c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="f263c-123">Adicionando Olá Portal capital da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f263c-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="f263c-124">tooconfigure Olá integração da saudação capital Portal do AD do Azure, você precisa tooadd Olá capital Portal na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f263c-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f263c-125">**tooadd Olá Portal financiamento da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f263c-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f263c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f263c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f263c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f263c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f263c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f263c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f263c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f263c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f263c-133">Na caixa de pesquisa hello, digite **Olá financiamento Portal**.</span><span class="sxs-lookup"><span data-stu-id="f263c-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="f263c-135">No painel de resultados de saudação, selecione **Olá financiamento Portal**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f263c-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f263c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f263c-138">Nesta seção, configurar e testar o AD do Azure-logon único com hello que financiamento Portal com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f263c-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f263c-139">Para toowork de logon único, AD do Azure precisa tooknow que o usuário de contraparte Olá em Olá financiamento Portal é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f263c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="f263c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Olá financiamento Portal precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f263c-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="f263c-141">Olá financiamento Portal no, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f263c-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f263c-142">tooconfigure e teste de logon único do AD do Azure com hello capital Portal, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f263c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f263c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f263c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f263c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f263c-145">**[Criar usuário de teste do Portal financiamento Olá](#creating-the-funding-portal-test-user)**  -toohave uma duplicata de Britta Simon em Olá Portal capital toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f263c-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f263c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f263c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f263c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f263c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f263c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f263c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f263c-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu aplicativo de Portal financiamento hello.</span><span class="sxs-lookup"><span data-stu-id="f263c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="f263c-150">**tooconfigure AD do Azure-logon único com hello financiamento Portal, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f263c-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="f263c-151">Em Olá portal do Azure, Olá **Olá financiamento Portal** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f263c-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f263c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f263c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="f263c-155">Em Olá **Olá financiamento Portal domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="f263c-157">a.</span><span class="sxs-lookup"><span data-stu-id="f263c-157">a.</span></span> <span data-ttu-id="f263c-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="f263c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="f263c-159">b.</span><span class="sxs-lookup"><span data-stu-id="f263c-159">b.</span></span> <span data-ttu-id="f263c-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="f263c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f263c-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f263c-161">These values are not real.</span></span> <span data-ttu-id="f263c-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f263c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f263c-163">Entre em contato com [Olá a equipe de suporte do cliente de Portal financiamento](mailto:info@regenteducation.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f263c-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="f263c-164">saudação de aplicativo de Portal financiamento espera Olá SAML asserções toocontain um atributo chamado "externalId1".</span><span class="sxs-lookup"><span data-stu-id="f263c-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="f263c-165">valor Hello "externalId1" deve ser um studentID reconhecido.</span><span class="sxs-lookup"><span data-stu-id="f263c-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="f263c-166">Configure a declaração hello "externalId1" para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f263c-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="f263c-167">Você pode gerenciar os valores hello desses atributos de saudação **atributos de usuário** do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f263c-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="f263c-168">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f263c-168">hello following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="f263c-170">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="f263c-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="f263c-171">Attribute Name</span></span> | <span data-ttu-id="f263c-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="f263c-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="f263c-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="f263c-173">externalId1</span></span> | <span data-ttu-id="f263c-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="f263c-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="f263c-175">a.</span><span class="sxs-lookup"><span data-stu-id="f263c-175">a.</span></span> <span data-ttu-id="f263c-176">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f263c-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f263c-179">b.</span><span class="sxs-lookup"><span data-stu-id="f263c-179">b.</span></span> <span data-ttu-id="f263c-180">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="f263c-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="f263c-181">c.</span><span class="sxs-lookup"><span data-stu-id="f263c-181">c.</span></span> <span data-ttu-id="f263c-182">De saudação **o valor do atributo** lista, o atributo de saudação selecione você deseja toouse para sua implementação.</span><span class="sxs-lookup"><span data-stu-id="f263c-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="f263c-183">Por exemplo, caso você tenha armazenado Olá StudentID valor em Olá ExtensionAttribute1, em seguida, selecione user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="f263c-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="f263c-184">d.</span><span class="sxs-lookup"><span data-stu-id="f263c-184">d.</span></span> <span data-ttu-id="f263c-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f263c-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="f263c-186">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f263c-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="f263c-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f263c-188">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f263c-190">tooconfigure logon único no **Olá financiamento Portal** lado, você precisa toosend Olá baixado **Metadata XML** muito[Olá a equipe de suporte do Portal financiamento](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="f263c-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="f263c-191">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f263c-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f263c-192">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f263c-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f263c-193">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f263c-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f263c-194">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f263c-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f263c-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="f263c-196">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f263c-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f263c-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f263c-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f263c-199">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f263c-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f263c-201">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f263c-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f263c-203">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f263c-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f263c-205">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f263c-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f263c-207">a.</span><span class="sxs-lookup"><span data-stu-id="f263c-207">a.</span></span> <span data-ttu-id="f263c-208">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f263c-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f263c-209">b.</span><span class="sxs-lookup"><span data-stu-id="f263c-209">b.</span></span> <span data-ttu-id="f263c-210">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f263c-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f263c-211">c.</span><span class="sxs-lookup"><span data-stu-id="f263c-211">c.</span></span> <span data-ttu-id="f263c-212">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f263c-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f263c-213">d.</span><span class="sxs-lookup"><span data-stu-id="f263c-213">d.</span></span> <span data-ttu-id="f263c-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f263c-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="f263c-215">Criação de usuário de teste do Portal financiamento Olá</span><span class="sxs-lookup"><span data-stu-id="f263c-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="f263c-216">Nesta seção, você deve criar um usuário chamado Britta Simon no hello capital Portal.</span><span class="sxs-lookup"><span data-stu-id="f263c-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="f263c-217">Trabalhar com [Olá a equipe de suporte do Portal financiamento](mailto:info@regenteducation.com) tooadd Olá usuário de teste e habilitar o SSO.</span><span class="sxs-lookup"><span data-stu-id="f263c-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f263c-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f263c-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso toohello Portal de capital.</span><span class="sxs-lookup"><span data-stu-id="f263c-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f263c-221">**tooassign Britta Simon toohello Portal capital, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f263c-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="f263c-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f263c-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f263c-224">Na lista de aplicativos hello, selecione **Olá financiamento Portal**.</span><span class="sxs-lookup"><span data-stu-id="f263c-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="f263c-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f263c-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f263c-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f263c-228">Click **Add** button.</span></span> <span data-ttu-id="f263c-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f263c-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f263c-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f263c-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f263c-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f263c-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f263c-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f263c-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f263c-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f263c-234">Testing single sign-on</span></span>

<span data-ttu-id="f263c-235">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f263c-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f263c-236">Quando você clica em Olá Olá financiamento Portal lado a lado no painel de acesso de saudação, você deve obter um aplicativo de Portal financiamento hello tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="f263c-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f263c-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f263c-237">Additional resources</span></span>

* [<span data-ttu-id="f263c-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f263c-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f263c-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f263c-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

