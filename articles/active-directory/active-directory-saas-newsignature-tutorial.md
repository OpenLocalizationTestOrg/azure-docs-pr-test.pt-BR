---
title: "Tutorial: Integração do Azure Active Directory com o Cloud Management Portal for Microsoft Azure | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Portal de gerenciamento de nuvem do Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="f2988-103">Tutorial: Integração do Azure Active Directory com o Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="f2988-104">Neste tutorial, você aprenderá como toointegrate Portal de gerenciamento de nuvem do Microsoft Azure com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="f2988-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2988-105">Integração do Portal de gerenciamento de nuvem do Microsoft Azure com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2988-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f2988-106">Você pode controlar no AD do Azure que tenha acesso tooCloud Portal de gerenciamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="f2988-107">Você pode habilitar seu usuários tooautomatically get conectado tooCloud Portal de gerenciamento do Microsoft Azure (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2988-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f2988-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2988-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2988-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f2988-110">Prerequisites</span></span>

<span data-ttu-id="f2988-111">tooconfigure integração do AD do Azure com o Portal de gerenciamento de nuvem do Microsoft Azure, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2988-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="f2988-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2988-113">Uma assinatura habilitada para logon único do Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2988-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f2988-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2988-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f2988-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2988-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f2988-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2988-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2988-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2988-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f2988-118">Scenario description</span></span>
<span data-ttu-id="f2988-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f2988-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2988-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="f2988-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2988-121">Adicionando o Portal de gerenciamento de nuvem do Microsoft Azure da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f2988-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="f2988-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="f2988-123">Adicionando o Portal de gerenciamento de nuvem do Microsoft Azure da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="f2988-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="f2988-124">integração de saudação tooconfigure do Portal de gerenciamento de nuvem do Microsoft Azure no AD do Azure, você precisa tooadd Portal de gerenciamento de nuvem do Microsoft Azure na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f2988-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2988-125">**tooadd Portal de gerenciamento de nuvem do Microsoft Azure da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2988-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2988-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f2988-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f2988-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f2988-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f2988-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f2988-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f2988-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2988-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f2988-133">Na caixa de pesquisa hello, digite **Portal de gerenciamento de nuvem do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2988-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="f2988-135">No painel de resultados de saudação, selecione **Portal de gerenciamento de nuvem do Microsoft Azure**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f2988-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2988-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2988-138">O objetivo desta seção é mostrar como configurar e testar o logon único do Azure AD com o Cloud Management Portal for Microsoft Azure, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f2988-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2988-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Portal de gerenciamento de nuvem do Microsoft Azure é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="f2988-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Portal de gerenciamento de nuvem do Microsoft Azure precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f2988-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="f2988-141">No Portal de gerenciamento de nuvem do Microsoft Azure, atribua o valor de saudação da saudação **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2988-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f2988-142">tooconfigure e teste de logon único do AD do Azure com o Portal de gerenciamento de nuvem do Microsoft Azure, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2988-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2988-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f2988-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2988-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f2988-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2988-145">**[Criando um Portal de gerenciamento de nuvem para o usuário de teste do Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)**  -toohave um equivalente do Britta Simon no Portal de gerenciamento de nuvem do Microsoft Azure é a representação toohello vinculado AD do Azure do usuário.</span><span class="sxs-lookup"><span data-stu-id="f2988-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2988-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="f2988-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2988-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="f2988-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2988-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2988-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2988-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu Portal de gerenciamento de nuvem para aplicativos do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="f2988-150">**tooconfigure logon único do AD do Azure com o Portal de gerenciamento de nuvem do Microsoft Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2988-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2988-151">Em Olá portal do Azure, Olá **Portal de gerenciamento de nuvem do Microsoft Azure** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="f2988-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f2988-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="f2988-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="f2988-155">Em Olá **Portal de gerenciamento de nuvem para o domínio do Microsoft Azure e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2988-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="f2988-157">a.</span><span class="sxs-lookup"><span data-stu-id="f2988-157">a.</span></span> <span data-ttu-id="f2988-158">Em Olá **URL de logon** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="f2988-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="f2988-159">b.</span><span class="sxs-lookup"><span data-stu-id="f2988-159">b.</span></span> <span data-ttu-id="f2988-160">Em Olá **identificador** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="f2988-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="f2988-161">c.</span><span class="sxs-lookup"><span data-stu-id="f2988-161">c.</span></span> <span data-ttu-id="f2988-162">Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="f2988-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="f2988-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f2988-163">These values are not real.</span></span> <span data-ttu-id="f2988-164">Atualize esses valores com a URL real Olá URL de logon, o identificador e a resposta.</span><span class="sxs-lookup"><span data-stu-id="f2988-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="f2988-165">Entre em contato com [Portal de gerenciamento de nuvem para a equipe de suporte do cliente do Microsoft Azure](mailto:jczernuszka@newsignature.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="f2988-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="f2988-166">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f2988-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="f2988-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f2988-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2988-170">Em Olá **Portal de gerenciamento de nuvem para a configuração do Microsoft Azure** seção, clique em **configurar o Portal de gerenciamento de nuvem do Microsoft Azure** tooopen **configurar o logon**janela.</span><span class="sxs-lookup"><span data-stu-id="f2988-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f2988-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f2988-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="f2988-173">tooconfigure logon único no **Portal de gerenciamento de nuvem do Microsoft Azure** lado, você precisa toosend Olá baixado **certificado**, **URL de logout**, **Single Sign-On URL do serviço SAML** e **ID da entidade SAML** muito[Portal de gerenciamento de nuvem para a equipe de suporte do Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="f2988-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="f2988-174">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f2988-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f2988-175">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="f2988-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f2988-176">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f2988-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f2988-177">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2988-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2988-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2988-179">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f2988-181">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2988-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2988-182">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="f2988-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2988-184">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="f2988-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2988-186">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2988-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2988-188">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2988-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2988-190">a.</span><span class="sxs-lookup"><span data-stu-id="f2988-190">a.</span></span> <span data-ttu-id="f2988-191">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2988-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2988-192">b.</span><span class="sxs-lookup"><span data-stu-id="f2988-192">b.</span></span> <span data-ttu-id="f2988-193">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f2988-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f2988-194">c.</span><span class="sxs-lookup"><span data-stu-id="f2988-194">c.</span></span> <span data-ttu-id="f2988-195">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="f2988-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f2988-196">d.</span><span class="sxs-lookup"><span data-stu-id="f2988-196">d.</span></span> <span data-ttu-id="f2988-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f2988-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="f2988-198">Criação de um usuário de teste do Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="f2988-199">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no Portal de gerenciamento de nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="f2988-200">Trabalhe com [Portal de gerenciamento de nuvem para a equipe de suporte do Microsoft Azure](mailto:jczernuszka@newsignature.com) tooadd usuários Olá Olá Portal de gerenciamento de nuvem para a conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2988-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f2988-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCloud Portal de gerenciamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f2988-204">**tooassign Britta Simon tooCloud Portal de gerenciamento do Microsoft Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2988-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2988-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f2988-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f2988-207">Na lista de aplicativos hello, selecione **Portal de gerenciamento de nuvem do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2988-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="f2988-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f2988-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f2988-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f2988-211">Click **Add** button.</span></span> <span data-ttu-id="f2988-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2988-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f2988-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2988-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f2988-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2988-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2988-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f2988-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2988-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f2988-217">Testing single sign-on</span></span>

<span data-ttu-id="f2988-218">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f2988-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="f2988-219">Quando você clica em hello Portal de gerenciamento de nuvem para o bloco do Microsoft Azure no hello painel de acesso, você deve obter tooyour automaticamente conectado no Portal de gerenciamento de nuvem para o aplicativo do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2988-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="f2988-220">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f2988-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2988-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f2988-221">Additional resources</span></span>

* [<span data-ttu-id="f2988-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f2988-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2988-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2988-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

