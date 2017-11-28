---
title: "Tutorial: integração do Azure Active Directory ao Gigya | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="8cbe0-103">Tutorial: integração do Active Directory do Azure ao Gigya</span><span class="sxs-lookup"><span data-stu-id="8cbe0-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="8cbe0-104">Neste tutorial, você aprenderá como toointegrate Gigya com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="8cbe0-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cbe0-105">Integrando o Gigya com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8cbe0-106">Você pode controlar no AD do Azure que tenha acesso tooGigya</span><span class="sxs-lookup"><span data-stu-id="8cbe0-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="8cbe0-107">Você pode habilitar seu usuários tooautomatically get conectado tooGigya (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8cbe0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8cbe0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cbe0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cbe0-110">Prerequisites</span></span>

<span data-ttu-id="8cbe0-111">tooconfigure integração do AD do Azure com o Gigya, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="8cbe0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8cbe0-113">Uma assinatura habilitada para logon único do Gigya</span><span class="sxs-lookup"><span data-stu-id="8cbe0-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cbe0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cbe0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cbe0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cbe0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cbe0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cbe0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8cbe0-118">Scenario description</span></span>
<span data-ttu-id="8cbe0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cbe0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cbe0-121">Adicionando Gigya da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8cbe0-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="8cbe0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="8cbe0-123">Adicionando Gigya da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="8cbe0-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="8cbe0-124">integração de saudação tooconfigure do Gigya no AD do Azure, você precisa tooadd Gigya da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8cbe0-125">**tooadd Gigya da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8cbe0-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cbe0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8cbe0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8cbe0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8cbe0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8cbe0-133">Na caixa de pesquisa hello, digite **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-133">In hello search box, type **Gigya**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="8cbe0-135">No painel de resultados de saudação, selecione **Gigya**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8cbe0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8cbe0-138">Nesta seção, você configura e testa o logon único do Azure AD com o Gigya com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8cbe0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Gigya é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="8cbe0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Gigya precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="8cbe0-141">No Gigya, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8cbe0-142">tooconfigure e teste de logon único do AD do Azure com o Gigya, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8cbe0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8cbe0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cbe0-145">**[Criar um usuário de teste do Gigya](#creating-a-gigya-test-user)**  -toohave um equivalente do Britta Simon no Gigya é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cbe0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cbe0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8cbe0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cbe0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8cbe0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Gigya.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="8cbe0-150">**tooconfigure AD do Azure-logon único com o Gigya, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8cbe0-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cbe0-151">Em Olá portal do Azure, Olá **Gigya** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8cbe0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="8cbe0-155">Em Olá **Gigya domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="8cbe0-157">a.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-157">a.</span></span> <span data-ttu-id="8cbe0-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="8cbe0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="8cbe0-159">b.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-159">b.</span></span> <span data-ttu-id="8cbe0-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8cbe0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8cbe0-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-161">These values are not real.</span></span> <span data-ttu-id="8cbe0-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8cbe0-163">Entre em contato com [equipe de suporte do cliente do Gigya](https://www.gigya.com/support-policy/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8cbe0-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="8cbe0-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8cbe0-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8cbe0-168">Em Olá **Gigya configuração** seção, clique em **configurar Gigya** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8cbe0-169">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="8cbe0-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="8cbe0-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do Gigya como administrador.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="8cbe0-172">Vá muito**configurações \> logon SAML**e, em seguida, clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="8cbe0-173">![Logon SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "logon SAML")</span><span class="sxs-lookup"><span data-stu-id="8cbe0-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="8cbe0-174">Em Olá **logon SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8cbe0-175">![Configuração SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="8cbe0-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="8cbe0-176">a.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-176">a.</span></span> <span data-ttu-id="8cbe0-177">Em Olá **nome** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="8cbe0-178">b.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-178">b.</span></span> <span data-ttu-id="8cbe0-179">Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="8cbe0-180">c.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-180">c.</span></span> <span data-ttu-id="8cbe0-181">Em **o URL de serviço de logon único** caixa de texto valor Olá colar **o URL de serviço de logon único** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="8cbe0-182">d.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-182">d.</span></span> <span data-ttu-id="8cbe0-183">Em **formato de ID de nome** caixa de texto valor Olá colar **formato de nome de identificador** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="8cbe0-184">e.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-184">e.</span></span> <span data-ttu-id="8cbe0-185">Abra seu certificado codificado em base 64 no bloco de notas que baixou do portal do Azure, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="8cbe0-186">f.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-186">f.</span></span> <span data-ttu-id="8cbe0-187">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="8cbe0-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="8cbe0-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8cbe0-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8cbe0-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8cbe0-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8cbe0-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="8cbe0-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8cbe0-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8cbe0-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cbe0-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8cbe0-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8cbe0-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8cbe0-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8cbe0-203">a.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-203">a.</span></span> <span data-ttu-id="8cbe0-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cbe0-205">b.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-205">b.</span></span> <span data-ttu-id="8cbe0-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8cbe0-207">c.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-207">c.</span></span> <span data-ttu-id="8cbe0-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8cbe0-209">d.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-209">d.</span></span> <span data-ttu-id="8cbe0-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="8cbe0-211">Como criar um usuário de teste do Gigya</span><span class="sxs-lookup"><span data-stu-id="8cbe0-211">Creating a Gigya test user</span></span>

<span data-ttu-id="8cbe0-212">Em ordem tooenable AD do Azure usuários toolog no Gigya, eles devem ser provisionados no Gigya.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="8cbe0-213">No caso de saudação do Gigya, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="8cbe0-214">tooprovision contas de usuário, executar Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="8cbe0-215">Faça logon no tooyour **Gigya** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="8cbe0-216">Vá muito**Admin \> gerenciar usuários**e, em seguida, clique em **convidar usuários**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="8cbe0-217">![Gerenciar Usuários](./media/active-directory-saas-gigya-tutorial/ic789535.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="8cbe0-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="8cbe0-218">Na caixa de diálogo Olá convidar usuários, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cbe0-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="8cbe0-219">![Convidar Usuários](./media/active-directory-saas-gigya-tutorial/ic789536.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="8cbe0-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="8cbe0-220">a.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-220">a.</span></span> <span data-ttu-id="8cbe0-221">Em Olá **Email** texto, o alias de email de saudação do tipo de uma conta válida do Active Directory do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="8cbe0-222">b.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-222">b.</span></span> <span data-ttu-id="8cbe0-223">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="8cbe0-224">proprietário de conta do Active Directory do Azure Olá receberá um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8cbe0-225">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8cbe0-226">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooGigya.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8cbe0-228">**tooassign Britta Simon tooGigya, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="8cbe0-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="8cbe0-229">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8cbe0-231">Na lista de aplicativos hello, selecione **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-231">In hello applications list, select **Gigya**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="8cbe0-233">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8cbe0-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-235">Click **Add** button.</span></span> <span data-ttu-id="8cbe0-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8cbe0-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8cbe0-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cbe0-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8cbe0-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8cbe0-241">Testing single sign-on</span></span>

<span data-ttu-id="8cbe0-242">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="8cbe0-243">Quando você clica em bloco Gigya Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Gigya aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cbe0-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8cbe0-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8cbe0-244">Additional resources</span></span>

* [<span data-ttu-id="8cbe0-245">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8cbe0-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cbe0-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8cbe0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

