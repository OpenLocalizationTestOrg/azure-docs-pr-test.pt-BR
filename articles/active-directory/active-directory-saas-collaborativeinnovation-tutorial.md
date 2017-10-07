---
title: "Tutorial: Integração do Azure Active Directory com Inovação Colaborativa | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e inovação colaborativa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="f7dd9-103">Tutorial: Integração do Azure Active Directory com Inovação Colaborativa</span><span class="sxs-lookup"><span data-stu-id="f7dd9-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="f7dd9-104">Neste tutorial, você aprenderá como toointegrate inovação colaboração com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f7dd9-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7dd9-105">Integração de inovação de colaboração com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f7dd9-106">Você pode controlar no AD do Azure que tenha acesso tooCollaborative inovação</span><span class="sxs-lookup"><span data-stu-id="f7dd9-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="f7dd9-107">Você pode habilitar seu usuários tooautomatically get conectado tooCollaborative inovação (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f7dd9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f7dd9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7dd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7dd9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f7dd9-110">Prerequisites</span></span>

<span data-ttu-id="f7dd9-111">tooconfigure integração do AD do Azure com inovações de colaboração, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="f7dd9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f7dd9-113">Um logon único da Inovação Colaborativa em uma assinatura habilitada</span><span class="sxs-lookup"><span data-stu-id="f7dd9-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7dd9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f7dd9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f7dd9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f7dd9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7dd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7dd9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f7dd9-118">Scenario description</span></span>
<span data-ttu-id="f7dd9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f7dd9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7dd9-121">Adicionando inovação colaborativa da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f7dd9-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="f7dd9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="f7dd9-123">Adicionando inovação colaborativa da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f7dd9-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="f7dd9-124">integração de saudação tooconfigure de inovação de colaboração no AD do Azure, você precisa tooadd inovação colaborativa de lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f7dd9-125">**tooadd inovação colaborativa da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7dd9-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7dd9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f7dd9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f7dd9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f7dd9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f7dd9-133">Na caixa de pesquisa hello, digite **inovação colaborativa**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="f7dd9-135">No painel de resultados de saudação, selecione **inovação colaborativa**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7dd9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7dd9-138">Nesta seção, você configurará e testará o logon único do Azure AD com a Inovação Colaborativa com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f7dd9-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f7dd9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na inovação colaborativa é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="f7dd9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na inovação colaborativa precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="f7dd9-141">Em colaboração inovação, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f7dd9-142">tooconfigure e teste de logon único do AD do Azure com inovações de colaboração, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f7dd9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f7dd9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7dd9-145">**[Criar um usuário de teste inovação colaborativa](#creating-a-collaborative-innovation-test-user)**  -toohave um equivalente do Britta Simon na inovação colaborativa que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f7dd9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7dd9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7dd9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7dd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f7dd9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo inovação colaborativa.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="f7dd9-150">**tooconfigure AD do Azure-logon único com inovações de colaboração, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7dd9-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7dd9-151">Em Olá portal do Azure, Olá **inovação colaborativa** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f7dd9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="f7dd9-155">Em Olá **domínio de inovação de colaboração e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="f7dd9-157">a.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-157">a.</span></span> <span data-ttu-id="f7dd9-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="f7dd9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="f7dd9-159">b.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-159">b.</span></span> <span data-ttu-id="f7dd9-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="f7dd9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f7dd9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-161">These values are not real.</span></span> <span data-ttu-id="f7dd9-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f7dd9-163">Entre em contato com [equipe de suporte do cliente de colaboração inovação](https://www.unilever.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="f7dd9-164">Aplicativo de inovação de colaboração espera as asserções de SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f7dd9-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="f7dd9-166">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f7dd9-167">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="f7dd9-169">Clique em **exibir e editar todos os outros atributos de usuário** caixa de seleção no hello **atributos de usuário** seção tooexpand atributos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="f7dd9-170">Executar Olá seguindo as etapas em cada um dos atributos de saudação exibida-</span><span class="sxs-lookup"><span data-stu-id="f7dd9-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="f7dd9-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="f7dd9-171">Attribute Name</span></span> | <span data-ttu-id="f7dd9-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="f7dd9-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="f7dd9-173">givenname</span><span class="sxs-lookup"><span data-stu-id="f7dd9-173">givenname</span></span> | <span data-ttu-id="f7dd9-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f7dd9-174">user.givenname</span></span> |
    | <span data-ttu-id="f7dd9-175">sobrenome</span><span class="sxs-lookup"><span data-stu-id="f7dd9-175">surname</span></span> | <span data-ttu-id="f7dd9-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="f7dd9-176">user.surname</span></span> |
    | <span data-ttu-id="f7dd9-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="f7dd9-177">emailaddress</span></span> | <span data-ttu-id="f7dd9-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f7dd9-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="f7dd9-179">name</span><span class="sxs-lookup"><span data-stu-id="f7dd9-179">name</span></span> | <span data-ttu-id="f7dd9-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f7dd9-180">user.userprincipalname</span></span> |

    <span data-ttu-id="f7dd9-181">a.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-181">a.</span></span> <span data-ttu-id="f7dd9-182">Clique em Olá Olá de tooopen atributo **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="f7dd9-184">b.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-184">b.</span></span> <span data-ttu-id="f7dd9-185">Excluir o valor da URL de saudação da saudação **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="f7dd9-186">c.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-186">c.</span></span> <span data-ttu-id="f7dd9-187">Clique em **Okey** toosave configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="f7dd9-188">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="f7dd9-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f7dd9-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f7dd9-192">tooconfigure logon único no **inovação colaborativa** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte inovação colaborativa](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f7dd9-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="f7dd9-193">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f7dd9-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f7dd9-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f7dd9-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f7dd9-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f7dd9-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7dd9-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7dd9-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f7dd9-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7dd9-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7dd9-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f7dd9-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f7dd9-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7dd9-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7dd9-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f7dd9-209">a.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-209">a.</span></span> <span data-ttu-id="f7dd9-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f7dd9-211">b.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-211">b.</span></span> <span data-ttu-id="f7dd9-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f7dd9-213">c.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-213">c.</span></span> <span data-ttu-id="f7dd9-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f7dd9-215">d.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-215">d.</span></span> <span data-ttu-id="f7dd9-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="f7dd9-217">Como criar um usuário de teste da Inovação Colaborativa</span><span class="sxs-lookup"><span data-stu-id="f7dd9-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="f7dd9-218">tooenable AD do Azure usuários toolog em tooCollaborative inovação, eles devem ser provisionados no inovação colaborativa.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="f7dd9-219">No caso do aplicativo o provisionamento é automática como aplicativo hello dá suporte apenas durante o provisionamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="f7dd9-220">Portanto, há nenhuma necessidade tooperform todas as etapas aqui.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f7dd9-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f7dd9-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCollaborative inovação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f7dd9-224">**tooassign Britta Simon tooCollaborative inovação, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f7dd9-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="f7dd9-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f7dd9-227">Na lista de aplicativos hello, selecione **inovação colaborativa**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="f7dd9-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f7dd9-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-231">Click **Add** button.</span></span> <span data-ttu-id="f7dd9-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f7dd9-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f7dd9-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f7dd9-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f7dd9-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f7dd9-237">Testing single sign-on</span></span>

<span data-ttu-id="f7dd9-238">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f7dd9-239">Quando você clica em bloco inovação colaborativa Olá Olá painel de acesso, você deve obter a página de logon do aplicativo de inovação de colaboração.</span><span class="sxs-lookup"><span data-stu-id="f7dd9-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="f7dd9-240">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f7dd9-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f7dd9-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f7dd9-241">Additional resources</span></span>

* [<span data-ttu-id="f7dd9-242">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dd9-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7dd9-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7dd9-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

