---
title: "Tutorial: integração do Azure Active Directory ao AnswerHub | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="010ac-103">Tutorial: Integração do Active Directory do Azure ao AnswerHub</span><span class="sxs-lookup"><span data-stu-id="010ac-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="010ac-104">Neste tutorial, você aprenderá como toointegrate AnswerHub com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="010ac-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="010ac-105">Integrando o AnswerHub com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="010ac-106">Você pode controlar no AD do Azure que tenha acesso tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="010ac-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="010ac-107">Você pode habilitar seu usuários tooautomatically get conectado tooAnswerHub (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="010ac-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="010ac-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="010ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="010ac-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="010ac-110">Prerequisites</span></span>

<span data-ttu-id="010ac-111">tooconfigure integração do AD do Azure com AnswerHub, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="010ac-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="010ac-113">Uma assinatura habilitada para logon único do AnswerHub</span><span class="sxs-lookup"><span data-stu-id="010ac-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="010ac-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="010ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="010ac-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="010ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="010ac-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="010ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="010ac-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="010ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="010ac-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="010ac-118">Scenario description</span></span>
<span data-ttu-id="010ac-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="010ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="010ac-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="010ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="010ac-121">Adicionando AnswerHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="010ac-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="010ac-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="010ac-123">Adicionando AnswerHub da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="010ac-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="010ac-124">integração de saudação tooconfigure do AnswerHub no AD do Azure, você precisa tooadd AnswerHub da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="010ac-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="010ac-125">**tooadd AnswerHub da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="010ac-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ac-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="010ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="010ac-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="010ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="010ac-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="010ac-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="010ac-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="010ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="010ac-133">Na caixa de pesquisa hello, digite **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="010ac-133">In hello search box, type **AnswerHub**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="010ac-135">No painel de resultados de saudação, selecione **AnswerHub**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="010ac-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="010ac-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="010ac-138">Nesta seção, você configura e testa o logon único do Azure AD com o AnswerHub, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="010ac-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="010ac-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no AnswerHub é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="010ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="010ac-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no AnswerHub precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="010ac-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="010ac-141">No AnswerHub, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="010ac-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="010ac-142">tooconfigure e teste de logon único do AD do Azure com AnswerHub, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="010ac-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="010ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="010ac-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="010ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="010ac-145">**[Criar um usuário de teste do AnswerHub](#creating-an-answerhub-test-user)**  -toohave um equivalente do Britta Simon no AnswerHub é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="010ac-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="010ac-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="010ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="010ac-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="010ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="010ac-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="010ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="010ac-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="010ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="010ac-150">**tooconfigure AD do Azure-logon único com AnswerHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="010ac-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ac-151">Em Olá portal do Azure, Olá **AnswerHub** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="010ac-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="010ac-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="010ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="010ac-155">Em Olá **AnswerHub domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="010ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="010ac-157">a.</span></span> <span data-ttu-id="010ac-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="010ac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="010ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="010ac-159">b.</span></span> <span data-ttu-id="010ac-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="010ac-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="010ac-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="010ac-161">These values are not real.</span></span> <span data-ttu-id="010ac-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="010ac-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="010ac-163">Entre em contato com [equipe de suporte do cliente AnswerHub](mailto:success@answerhub.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="010ac-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="010ac-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="010ac-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="010ac-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="010ac-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="010ac-168">Em Olá **AnswerHub configuração** seção, clique em **configurar AnswerHub** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="010ac-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="010ac-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="010ac-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="010ac-171">Em outra janela do navegador da Web, faça logon em seu site de empresa AnswerHub como um administrador.</span><span class="sxs-lookup"><span data-stu-id="010ac-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="010ac-172">Se você precisar de ajuda para configurar o AnswerHub, entre em contato com a [equipe de suporte do AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="010ac-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="010ac-173">Vá muito**administração**.</span><span class="sxs-lookup"><span data-stu-id="010ac-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="010ac-174">Clique em Olá **usuário e grupo** guia.</span><span class="sxs-lookup"><span data-stu-id="010ac-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="010ac-175">No painel de navegação Olá Olá deixados de lado, no hello **configurações sociais** seção, clique em **instalação do SAML**.</span><span class="sxs-lookup"><span data-stu-id="010ac-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="010ac-176">Clique na guia **Config. de IDP** .</span><span class="sxs-lookup"><span data-stu-id="010ac-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="010ac-177">Em Olá **Config IDP** guia, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="010ac-178">![Instalação do SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="010ac-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="010ac-179">a.</span><span class="sxs-lookup"><span data-stu-id="010ac-179">a.</span></span> <span data-ttu-id="010ac-180">Na caixa de texto **URL de Logon do IDP**, cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="010ac-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="010ac-181">b.</span><span class="sxs-lookup"><span data-stu-id="010ac-181">b.</span></span> <span data-ttu-id="010ac-182">Na caixa de texto **URL de Logoff do IDP**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="010ac-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="010ac-183">c.</span><span class="sxs-lookup"><span data-stu-id="010ac-183">c.</span></span> <span data-ttu-id="010ac-184">Em **formato do identificador de nome IDP** caixa de texto, insira o usuário Olá identificador mesmo valor selecionado no portal do Azure em **atributos de usuário** seção.</span><span class="sxs-lookup"><span data-stu-id="010ac-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="010ac-185">d.</span><span class="sxs-lookup"><span data-stu-id="010ac-185">d.</span></span> <span data-ttu-id="010ac-186">Clique em **Chaves e Certificados**.</span><span class="sxs-lookup"><span data-stu-id="010ac-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="010ac-187">Na guia certificados e chaves hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="010ac-188">![Chaves e Certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Chaves e Certificados")</span><span class="sxs-lookup"><span data-stu-id="010ac-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="010ac-189">a.</span><span class="sxs-lookup"><span data-stu-id="010ac-189">a.</span></span> <span data-ttu-id="010ac-190">Abra seu certificado codificado em base 64, que você baixou do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência, e, em seguida, cole-o toohello **a chave pública IDP (x formato X509)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="010ac-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="010ac-191">b.</span><span class="sxs-lookup"><span data-stu-id="010ac-191">b.</span></span> <span data-ttu-id="010ac-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="010ac-192">Click **Save**.</span></span>

14. <span data-ttu-id="010ac-193">Em Olá **Config IDP** , clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="010ac-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="010ac-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="010ac-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="010ac-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="010ac-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="010ac-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="010ac-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="010ac-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="010ac-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="010ac-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="010ac-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="010ac-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ac-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="010ac-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="010ac-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="010ac-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="010ac-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="010ac-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="010ac-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="010ac-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="010ac-209">a.</span><span class="sxs-lookup"><span data-stu-id="010ac-209">a.</span></span> <span data-ttu-id="010ac-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="010ac-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="010ac-211">b.</span><span class="sxs-lookup"><span data-stu-id="010ac-211">b.</span></span> <span data-ttu-id="010ac-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="010ac-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="010ac-213">c.</span><span class="sxs-lookup"><span data-stu-id="010ac-213">c.</span></span> <span data-ttu-id="010ac-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="010ac-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="010ac-215">d.</span><span class="sxs-lookup"><span data-stu-id="010ac-215">d.</span></span> <span data-ttu-id="010ac-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="010ac-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="010ac-217">Criando um usuário de teste do AnswerHub</span><span class="sxs-lookup"><span data-stu-id="010ac-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="010ac-218">tooenable AD do Azure usuários toolog em tooAnswerHub, eles devem ser provisionados no AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="010ac-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="010ac-219">No caso de saudação do AnswerHub, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="010ac-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="010ac-220">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="010ac-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ac-221">Faça logon no tooyour **AnswerHub** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="010ac-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="010ac-222">Vá muito**administração**.</span><span class="sxs-lookup"><span data-stu-id="010ac-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="010ac-223">Clique em Olá **usuários e grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="010ac-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="010ac-224">No painel de navegação Olá Olá deixados de lado, no hello **gerenciar usuários** seção, clique em **criar ou importar usuários**.</span><span class="sxs-lookup"><span data-stu-id="010ac-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="010ac-225">![Usuários e Grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Usuários e Grupos")</span><span class="sxs-lookup"><span data-stu-id="010ac-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="010ac-226">Saudação de tipo **endereço de Email**, **Username** e **senha** de uma válida do Azure conta do Active Directory que você deseja tooprovision em Olá relacionadas a caixas de texto e clique em  **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="010ac-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="010ac-227">Você pode usar qualquer ferramenta de criação outros AnswerHub usuário conta ou APIs fornecidas pela AnswerHub tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="010ac-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="010ac-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="010ac-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAnswerHub.</span><span class="sxs-lookup"><span data-stu-id="010ac-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="010ac-231">**tooassign Britta Simon tooAnswerHub, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="010ac-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="010ac-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="010ac-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="010ac-234">Na lista de aplicativos hello, selecione **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="010ac-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="010ac-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="010ac-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="010ac-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="010ac-238">Click **Add** button.</span></span> <span data-ttu-id="010ac-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="010ac-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="010ac-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="010ac-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="010ac-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="010ac-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="010ac-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="010ac-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="010ac-244">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="010ac-244">Testing single sign-on</span></span>

<span data-ttu-id="010ac-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="010ac-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="010ac-246">Quando você clica em bloco AnswerHub Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour AnswerHub aplicativo.</span><span class="sxs-lookup"><span data-stu-id="010ac-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="010ac-247">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="010ac-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="010ac-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="010ac-248">Additional resources</span></span>

* [<span data-ttu-id="010ac-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="010ac-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="010ac-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="010ac-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

