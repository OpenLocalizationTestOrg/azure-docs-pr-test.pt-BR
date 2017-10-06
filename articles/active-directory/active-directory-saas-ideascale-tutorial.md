---
title: "Tutorial: Integração do Azure Active Directory ao IdeaScale | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="0992e-103">Tutorial: integração do Active Directory do Azure ao IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0992e-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="0992e-104">Neste tutorial, você aprenderá como toointegrate IdeaScale com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="0992e-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0992e-105">Integrando o IdeaScale com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0992e-106">Você pode controlar no AD do Azure que tenha acesso tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="0992e-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="0992e-107">Você pode habilitar seu usuários tooautomatically get conectado tooIdeaScale (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0992e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0992e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0992e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0992e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0992e-110">Prerequisites</span></span>

<span data-ttu-id="0992e-111">tooconfigure integração do AD do Azure com IdeaScale, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="0992e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0992e-113">Uma assinatura habilitada para logon único do IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0992e-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0992e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0992e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0992e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0992e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0992e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0992e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0992e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0992e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0992e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0992e-118">Scenario description</span></span>
<span data-ttu-id="0992e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0992e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0992e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="0992e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0992e-121">Adicionando IdeaScale da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0992e-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="0992e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="0992e-123">Adicionando IdeaScale da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="0992e-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="0992e-124">integração de saudação tooconfigure do IdeaScale no AD do Azure, você precisa tooadd IdeaScale da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0992e-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0992e-125">**tooadd IdeaScale da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0992e-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0992e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0992e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0992e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0992e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0992e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0992e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0992e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0992e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0992e-133">Na caixa de pesquisa hello, digite **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="0992e-133">In hello search box, type **IdeaScale**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="0992e-135">No painel de resultados de saudação, selecione **IdeaScale**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0992e-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0992e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0992e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o IdeaScale com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0992e-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0992e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no IdeaScale é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0992e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="0992e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no IdeaScale precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0992e-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="0992e-141">No IdeaScale, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="0992e-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0992e-142">tooconfigure e teste de logon único do AD do Azure com IdeaScale, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0992e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0992e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0992e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0992e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0992e-145">**[Criar um usuário de teste do IdeaScale](#creating-an-ideascale-test-user)**  -toohave um equivalente do Britta Simon no IdeaScale é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="0992e-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0992e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="0992e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0992e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="0992e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0992e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0992e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0992e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0992e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="0992e-150">**tooconfigure AD do Azure-logon único com IdeaScale, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0992e-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="0992e-151">Em Olá portal do Azure, Olá **IdeaScale** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="0992e-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0992e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="0992e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="0992e-155">Em Olá **IdeaScale domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="0992e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0992e-157">a.</span></span> <span data-ttu-id="0992e-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="0992e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="0992e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0992e-159">b.</span></span> <span data-ttu-id="0992e-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="0992e-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0992e-161">These values are not real.</span></span> <span data-ttu-id="0992e-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0992e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0992e-163">Entre em contato com [equipe de suporte do cliente do IdeaScale](http://support.ideascale.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="0992e-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0992e-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0992e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="0992e-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0992e-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0992e-168">Em Olá **IdeaScale configuração** seção, clique em **configurar IdeaScale** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="0992e-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0992e-169">Saudação de cópia **URL de logout e a ID da entidade SAML** de saudação **seção de referência rápida**.</span><span class="sxs-lookup"><span data-stu-id="0992e-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="0992e-171">Em uma janela de navegador web diferente, faça logon no site da empresa IdeaScale tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="0992e-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="0992e-172">Vá muito**configurações da comunidade**.</span><span class="sxs-lookup"><span data-stu-id="0992e-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="0992e-173">![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")</span><span class="sxs-lookup"><span data-stu-id="0992e-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="0992e-174">Vá muito**segurança \> configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="0992e-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="0992e-175">![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="0992e-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="0992e-176">Para **Tipo de Logon Único**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="0992e-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="0992e-177">![Tipo de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Tipo de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="0992e-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="0992e-178">Em Olá **configurações de logon único** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="0992e-179">![Configurações de Logon Único](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="0992e-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="0992e-180">a.</span><span class="sxs-lookup"><span data-stu-id="0992e-180">a.</span></span> <span data-ttu-id="0992e-181">Em **ID da entidade IdP SAML** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0992e-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0992e-182">b.</span><span class="sxs-lookup"><span data-stu-id="0992e-182">b.</span></span> <span data-ttu-id="0992e-183">Copiar o conteúdo de saudação do seu arquivo de metadados baixado do portal do Azure e cole-o em Olá **metadados IdP SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0992e-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="0992e-184">c.</span><span class="sxs-lookup"><span data-stu-id="0992e-184">c.</span></span> <span data-ttu-id="0992e-185">Em **URL de Logout do sucesso** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0992e-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0992e-186">d.</span><span class="sxs-lookup"><span data-stu-id="0992e-186">d.</span></span> <span data-ttu-id="0992e-187">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="0992e-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0992e-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="0992e-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0992e-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="0992e-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0992e-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0992e-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0992e-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="0992e-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0992e-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0992e-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0992e-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0992e-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="0992e-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0992e-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="0992e-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0992e-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0992e-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0992e-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0992e-203">a.</span><span class="sxs-lookup"><span data-stu-id="0992e-203">a.</span></span> <span data-ttu-id="0992e-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0992e-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0992e-205">b.</span><span class="sxs-lookup"><span data-stu-id="0992e-205">b.</span></span> <span data-ttu-id="0992e-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0992e-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0992e-207">c.</span><span class="sxs-lookup"><span data-stu-id="0992e-207">c.</span></span> <span data-ttu-id="0992e-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="0992e-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0992e-209">d.</span><span class="sxs-lookup"><span data-stu-id="0992e-209">d.</span></span> <span data-ttu-id="0992e-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0992e-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="0992e-211">Como criar um usuário de teste do IdeaScale</span><span class="sxs-lookup"><span data-stu-id="0992e-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="0992e-212">toolog de usuários tooenable AD do Azure no IdeaScale, eles devem ser provisionados no tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0992e-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="0992e-213">No caso de saudação do IdeaScale, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="0992e-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="0992e-214">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0992e-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0992e-215">Faça logon no tooyour **IdeaScale** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0992e-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="0992e-216">Vá muito**configurações da comunidade**.</span><span class="sxs-lookup"><span data-stu-id="0992e-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="0992e-217">![Configurações da Comunidade](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Configurações da Comunidade")</span><span class="sxs-lookup"><span data-stu-id="0992e-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="0992e-218">Vá muito**configurações básicas \> gerenciamento membro**.</span><span class="sxs-lookup"><span data-stu-id="0992e-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="0992e-219">Clique em **Adicionar Membro**.</span><span class="sxs-lookup"><span data-stu-id="0992e-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="0992e-220">![Gerenciamento de Membros](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Gerenciamento de Membros")</span><span class="sxs-lookup"><span data-stu-id="0992e-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="0992e-221">Na seção Adicionar novo membro de hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0992e-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0992e-222">![Adicionar Novo Membro](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Adicionar Novo Membro")</span><span class="sxs-lookup"><span data-stu-id="0992e-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="0992e-223">a.</span><span class="sxs-lookup"><span data-stu-id="0992e-223">a.</span></span> <span data-ttu-id="0992e-224">Em Olá **endereços de Email** caixa de texto, endereço de email de saudação do tipo de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0992e-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="0992e-225">b.</span><span class="sxs-lookup"><span data-stu-id="0992e-225">b.</span></span> <span data-ttu-id="0992e-226">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="0992e-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="0992e-227">proprietário de conta do Active Directory do Azure Olá obtém um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="0992e-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="0992e-228">Você pode usar qualquer ferramenta de criação outros IdeaScale usuário conta ou APIs fornecidas pelo IdeaScale tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="0992e-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0992e-229">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0992e-230">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="0992e-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0992e-232">**tooassign Britta Simon tooIdeaScale, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="0992e-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="0992e-233">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0992e-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0992e-235">Na lista de aplicativos hello, selecione **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="0992e-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="0992e-237">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0992e-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0992e-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0992e-239">Click **Add** button.</span></span> <span data-ttu-id="0992e-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0992e-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0992e-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="0992e-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0992e-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0992e-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0992e-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0992e-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0992e-245">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0992e-245">Testing single sign-on</span></span>


<span data-ttu-id="0992e-246">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0992e-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0992e-247">Quando você clica em bloco IdeaScale Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour IdeaScale aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0992e-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0992e-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0992e-248">Additional resources</span></span>

* [<span data-ttu-id="0992e-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0992e-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0992e-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0992e-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

