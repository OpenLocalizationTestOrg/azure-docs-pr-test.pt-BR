---
title: "Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service) | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Symantec Web segurança Service (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="ab211-103">Tutorial: Integração do Azure Active Directory ao Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ab211-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="ab211-104">Neste tutorial, você aprenderá como toointegrate o Symantec Web segurança Service (WSS) a conta com sua conta do Azure Active Directory (AD do Azure) para que o WSS possa autenticar um usuário final provisionado no hello AD do Azure usando a autenticação do SAML e impor o usuário ou regras de política no nível do grupo.</span><span class="sxs-lookup"><span data-stu-id="ab211-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="ab211-105">Integrando o Symantec Web segurança Service (WSS) com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab211-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab211-106">Gerencie todos os usuários finais de saudação e os grupos usados por sua conta do WSS do seu portal do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="ab211-107">Permitir tooauthenticate de usuários finais Olá si no WSS usando suas credenciais do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="ab211-108">Habilitar a imposição de saudação do usuário e grupo de regras de política no nível definidas em sua conta do WSS.</span><span class="sxs-lookup"><span data-stu-id="ab211-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="ab211-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab211-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab211-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab211-110">Prerequisites</span></span>

<span data-ttu-id="ab211-111">tooconfigure integração do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab211-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="ab211-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab211-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab211-113">Uma conta do Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ab211-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="ab211-114">Olá tootest as etapas neste tutorial, não recomendamos usar uma conta do WSS que está sendo usada para fins de produção.</span><span class="sxs-lookup"><span data-stu-id="ab211-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="ab211-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ab211-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab211-116">Não use sua conta do WSS que esteja sendo usada para fins de produção neste teste, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ab211-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="ab211-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab211-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab211-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ab211-118">Scenario description</span></span>
<span data-ttu-id="ab211-119">Neste tutorial, você irá configurar o AD do Azure tooenable único logon tooWSS usando credenciais do usuário final Olá definidas em sua conta do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="ab211-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ab211-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab211-121">Adicionando o aplicativo de serviço de segurança da Web da Symantec (WSS) hello da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ab211-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="ab211-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab211-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="ab211-123">Adicionando Symantec Web segurança Service (WSS) da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ab211-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="ab211-124">integração de saudação do tooconfigure da Symantec Web segurança Service (WSS) no AD do Azure, você precisa tooadd Symantec Web segurança Service (WSS) na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ab211-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab211-125">**tooadd Symantec Web segurança Service (WSS) da Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab211-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab211-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ab211-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="ab211-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ab211-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab211-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab211-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="ab211-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab211-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="ab211-133">Na caixa de pesquisa hello, digite **Symantec Web segurança Service (WSS)**, selecione **Symantec Web segurança Service (WSS)** no painel de resultados e clique em **adicionar** saudação do botão tooadd aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab211-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec Web segurança Service (WSS) na lista de resultados de saudação](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ab211-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab211-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ab211-136">Nesta seção, você configura e testa o logon único do Azure AD com o Symantec WSS (Web Security Service), com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ab211-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab211-137">Para toowork de logon único, o AD do Azure precisa tooknow que o usuário de contraparte Olá no Symantec Web segurança Service (WSS) é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="ab211-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Symantec Web segurança Service (WSS) precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ab211-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="ab211-139">No Web segurança Service (WSS) de Symantec, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab211-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab211-140">tooconfigure e teste de logon único do AD do Azure com o Symantec Web segurança Service (WSS), você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab211-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab211-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ab211-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab211-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab211-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab211-143">**[Criar um usuário de teste do serviço de segurança da Web da Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave um equivalente de Britta Simon na segurança de Web da Symantec Service (WSS) que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ab211-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab211-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ab211-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab211-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ab211-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ab211-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab211-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ab211-147">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de serviço de segurança da Web da Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="ab211-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="ab211-148">**tooconfigure logon único do AD do Azure com o Web segurança Service (WSS) de Symantec, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab211-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ab211-149">Em Olá portal do Azure, Olá **Symantec Web segurança Service (WSS)** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ab211-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="ab211-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ab211-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="ab211-153">Em Olá **Symantec Web segurança Service (WSS) domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab211-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="ab211-155">a.</span><span class="sxs-lookup"><span data-stu-id="ab211-155">a.</span></span> <span data-ttu-id="ab211-156">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="ab211-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="ab211-157">b.</span><span class="sxs-lookup"><span data-stu-id="ab211-157">b.</span></span> <span data-ttu-id="ab211-158">Em Olá **URL de resposta** caixa de texto, digite a URL de saudação:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="ab211-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab211-159">Entre em contato com hello [equipe de suporte do cliente do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) se valores Olá Olá **identificador** e **URL de resposta** por algum motivo, não estão funcionando.</span><span class="sxs-lookup"><span data-stu-id="ab211-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="ab211-160">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ab211-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="ab211-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ab211-162">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ab211-164">tooconfigure logon único no hello lado Symantec Web segurança Service (WSS), consulte a documentação online do toohello WSS.</span><span class="sxs-lookup"><span data-stu-id="ab211-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="ab211-165">Olá baixado **Metadata XML** arquivo precisará toobe importada no portal do WSS hello.</span><span class="sxs-lookup"><span data-stu-id="ab211-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="ab211-166">Olá contato [equipe de suporte do serviço de segurança da Web da Symantec (WSS)](https://www.symantec.com/contact-us) se precisar de ajuda com a configuração de saudação no portal do WSS hello.</span><span class="sxs-lookup"><span data-stu-id="ab211-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="ab211-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ab211-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab211-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ab211-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab211-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab211-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab211-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab211-170">Create an Azure AD test user</span></span>

<span data-ttu-id="ab211-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="ab211-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab211-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab211-174">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="ab211-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ab211-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ab211-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ab211-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab211-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ab211-180">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab211-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ab211-182">a.</span><span class="sxs-lookup"><span data-stu-id="ab211-182">a.</span></span> <span data-ttu-id="ab211-183">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab211-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab211-184">b.</span><span class="sxs-lookup"><span data-stu-id="ab211-184">b.</span></span> <span data-ttu-id="ab211-185">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab211-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ab211-186">c.</span><span class="sxs-lookup"><span data-stu-id="ab211-186">c.</span></span> <span data-ttu-id="ab211-187">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="ab211-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ab211-188">d.</span><span class="sxs-lookup"><span data-stu-id="ab211-188">d.</span></span> <span data-ttu-id="ab211-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ab211-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="ab211-190">Criar um usuário de teste do Symantec WSS (Web Security Service)</span><span class="sxs-lookup"><span data-stu-id="ab211-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="ab211-191">Nesta seção, você cria um usuário chamado Brenda Fernandes no Symantec WSS (Web Security Service).</span><span class="sxs-lookup"><span data-stu-id="ab211-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="ab211-192">Olá de nome correspondente de usuário final pode ser criado manualmente no portal do WSS hello, ou pode esperar que os usuários/grupos de saudação provisionados no portal WSS hello Azure AD toobe sincronizado toohello após alguns minutos (aproximadamente 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="ab211-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="ab211-193">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ab211-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="ab211-194">endereço IP público de saudação do computador do usuário final hello, que será usado toobrowse sites também precisará toobe provisionada no portal de serviço de segurança da Web da Symantec (WSS) hello.</span><span class="sxs-lookup"><span data-stu-id="ab211-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ab211-195">Por favor, [clique aqui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget sua máquina do pública IPaddress.</span><span class="sxs-lookup"><span data-stu-id="ab211-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ab211-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab211-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ab211-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSymantec segurança de Web Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="ab211-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="ab211-199">**tooassign Britta Simon tooSymantec Web segurança Service (WSS), execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab211-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="ab211-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab211-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ab211-202">Na lista de aplicativos hello, selecione **Symantec Web segurança Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="ab211-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Olá Symantec Web segurança Service (WSS) link na lista de aplicativos Olá](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="ab211-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ab211-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="ab211-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab211-206">Click **Add** button.</span></span> <span data-ttu-id="ab211-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab211-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="ab211-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab211-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab211-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab211-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab211-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab211-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ab211-212">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="ab211-212">Test single sign-on</span></span>

<span data-ttu-id="ab211-213">Nesta seção, você vai testar a funcionalidade de logon único Olá agora que você configurou seu toouse de conta do WSS AD do Azure para autenticação SAML.</span><span class="sxs-lookup"><span data-stu-id="ab211-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="ab211-214">Depois de ter configurado o tráfego de tooproxy do navegador da web tooWSS, quando você abre o navegador da web e tente toobrowse tooa site e em seguida, você será redirecionado página toohello logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab211-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="ab211-215">Insira as credenciais de saudação do usuário final do hello teste que foi configurado no hello (ou seja, BrittaSimon) do AD do Azure e associados a senha.</span><span class="sxs-lookup"><span data-stu-id="ab211-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="ab211-216">Uma vez autenticados, você será capaz de toobrowse toohello site que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="ab211-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="ab211-217">Você deve criar uma regra de política em Olá WSS lado tooblock BrittaSimon de navegação tooa determinado site, em seguida, você deve ver Olá WSS bloco página quando você tenta toobrowse toothat site como usuário BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ab211-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab211-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ab211-218">Additional resources</span></span>

* [<span data-ttu-id="ab211-219">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab211-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab211-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab211-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

