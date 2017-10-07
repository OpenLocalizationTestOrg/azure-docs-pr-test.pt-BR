---
title: "Tutorial: integração do Azure Active Directory com o Onit | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="5a5f5-103">Tutorial: Integração do Active Directory do Azure com o Onit</span><span class="sxs-lookup"><span data-stu-id="5a5f5-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="5a5f5-104">Neste tutorial, você aprenderá como toointegrate Onit com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5a5f5-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a5f5-105">Integrando o Onit com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a5f5-106">Você pode controlar no AD do Azure que tenha acesso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="5a5f5-107">Você pode habilitar seu usuários tooautomatically get conectado tooOnit (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5a5f5-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5a5f5-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a5f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a5f5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5a5f5-110">Prerequisites</span></span>

<span data-ttu-id="5a5f5-111">tooconfigure integração do AD do Azure com o Onit, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="5a5f5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a5f5-113">Uma assinatura habilitada para logon único do Onit</span><span class="sxs-lookup"><span data-stu-id="5a5f5-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a5f5-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a5f5-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a5f5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a5f5-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a5f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a5f5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5a5f5-118">Scenario description</span></span>

<span data-ttu-id="5a5f5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a5f5-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a5f5-121">Adicionando Onit da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5a5f5-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="5a5f5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="5a5f5-123">Adicionando Onit da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5a5f5-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="5a5f5-124">integração de saudação tooconfigure do Onit no AD do Azure, você precisa tooadd Onit da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a5f5-125">**tooadd Onit da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a5f5-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="5a5f5-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a5f5-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="5a5f5-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="5a5f5-133">Na caixa de pesquisa hello, digite **Onit**, selecione **Onit** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Onit na lista de resultados de saudação](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5a5f5-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a5f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5a5f5-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Onit, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a5f5-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Onit é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="5a5f5-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Onit precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="5a5f5-139">No Onit, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a5f5-140">tooconfigure e teste de logon único do AD do Azure com o Onit, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a5f5-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a5f5-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a5f5-143">**[Criar um usuário de teste do Onit](#create-an-onit-test-user)**  -toohave um equivalente do Britta Simon no Onit é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a5f5-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a5f5-145">**[Testar o logon único](#test-single-sign-on)**  tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5a5f5-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a5f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5a5f5-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu aplicativo Onit.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="5a5f5-148">**tooconfigure AD do Azure-logon único com o Onit, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a5f5-149">Em Olá portal do Azure, Olá **Onit** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="5a5f5-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="5a5f5-153">Em Olá **Onit domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="5a5f5-155">a.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-155">a.</span></span> <span data-ttu-id="5a5f5-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="5a5f5-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="5a5f5-157">b.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-157">b.</span></span> <span data-ttu-id="5a5f5-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="5a5f5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a5f5-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-159">These values are not real.</span></span> <span data-ttu-id="5a5f5-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a5f5-161">Entre em contato com [equipe de suporte do cliente do Onit](https://www.onit.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="5a5f5-162">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="5a5f5-164">Aplicativo Onit espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="5a5f5-165">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="5a5f5-166">Você pode gerenciar os valores hello desses atributos de saudação **"Atributo"** guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="5a5f5-167">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="5a5f5-169">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, configurar atributos de token SAML, conforme mostrado na imagem hello e executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="5a5f5-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="5a5f5-170">Attribute Name</span></span> | <span data-ttu-id="5a5f5-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="5a5f5-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="5a5f5-172">email</span><span class="sxs-lookup"><span data-stu-id="5a5f5-172">email</span></span> | <span data-ttu-id="5a5f5-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="5a5f5-173">user.mail</span></span> |
    
    <span data-ttu-id="5a5f5-174">a.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-174">a.</span></span> <span data-ttu-id="5a5f5-175">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5a5f5-178">b.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-178">b.</span></span> <span data-ttu-id="5a5f5-179">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="5a5f5-180">c.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-180">c.</span></span> <span data-ttu-id="5a5f5-181">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="5a5f5-182">d.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-182">d.</span></span> <span data-ttu-id="5a5f5-183">Deixe Olá **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="5a5f5-184">e.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-184">e.</span></span> <span data-ttu-id="5a5f5-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-185">Click **Ok**.</span></span>

7. <span data-ttu-id="5a5f5-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5a5f5-186">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5a5f5-188">Em Olá **Onit configuração** seção, clique em **configurar Onit** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5a5f5-189">Saudação de cópia **URL de logout, Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="5a5f5-191">Em outra janela do navegador da Web, faça logon em seu site de empresa Onit como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="5a5f5-192">No menu de saudação na parte superior de saudação, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="5a5f5-193">![Administração](./media/active-directory-saas-onit-tutorial/IC791174.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="5a5f5-194">Clique em **Editar Empresa**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="5a5f5-195">![Editar Corporação](./media/active-directory-saas-onit-tutorial/IC791175.png "Editar Corporação")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="5a5f5-196">Clique em Olá **segurança** guia.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="5a5f5-197">![Editar Informações da Empresa](./media/active-directory-saas-onit-tutorial/IC791176.png "Editar Informações da Empresa")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="5a5f5-198">Em Olá **segurança** guia, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="5a5f5-199">![Logon Único](./media/active-directory-saas-onit-tutorial/IC791177.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="5a5f5-200">a.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-200">a.</span></span> <span data-ttu-id="5a5f5-201">Como **Estratégia de Autenticação**, selecione **Logn Único e Senha**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="5a5f5-202">b.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-202">b.</span></span> <span data-ttu-id="5a5f5-203">Em **URL de destino de Idp** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a5f5-204">c.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-204">c.</span></span> <span data-ttu-id="5a5f5-205">Em **URL de logout Idp** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5a5f5-206">d.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-206">d.</span></span> <span data-ttu-id="5a5f5-207">Em **impressão digital do certificado Idp (SHA1)** caixa de texto, colar Olá **impressão digital** valor de certificado, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="5a5f5-208">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5a5f5-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a5f5-209">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a5f5-210">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a5f5-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5a5f5-211">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a5f5-211">Create an Azure AD test user</span></span>

<span data-ttu-id="5a5f5-212">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="5a5f5-214">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a5f5-215">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5a5f5-217">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5a5f5-219">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5a5f5-221">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5a5f5-223">a.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-223">a.</span></span> <span data-ttu-id="5a5f5-224">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a5f5-225">b.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-225">b.</span></span> <span data-ttu-id="5a5f5-226">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5a5f5-227">c.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-227">c.</span></span> <span data-ttu-id="5a5f5-228">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5a5f5-229">d.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-229">d.</span></span> <span data-ttu-id="5a5f5-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="5a5f5-231">Criar um usuário de teste do Onit</span><span class="sxs-lookup"><span data-stu-id="5a5f5-231">Create an Onit test user</span></span>

<span data-ttu-id="5a5f5-232">Em ordem tooenable AD do Azure usuários toolog no Onit, eles devem ser provisionados no Onit.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="5a5f5-233">No caso de saudação do Onit, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="5a5f5-234">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a5f5-235">Logon tooyour **Onit** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="5a5f5-236">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="5a5f5-237">![Administração](./media/active-directory-saas-onit-tutorial/IC791180.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="5a5f5-238">Em Olá **adicionar usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a5f5-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="5a5f5-239">![Adicionar Usuário](./media/active-directory-saas-onit-tutorial/IC791181.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="5a5f5-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="5a5f5-240">Saudação de tipo **nome** e hello **endereço de Email** de uma válida do Azure relacionados de conta do AD desejados tooprovision para Olá caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="5a5f5-241">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="5a5f5-242">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5a5f5-243">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5f5-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5a5f5-244">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOnit.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="5a5f5-246">**tooassign Britta Simon tooOnit, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5a5f5-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a5f5-247">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5a5f5-249">Na lista de aplicativos hello, selecione **Onit**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-249">In hello applications list, select **Onit**.</span></span>

    ![link do Onit Olá na lista de aplicativos Olá](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="5a5f5-251">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="5a5f5-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-253">Click **Add** button.</span></span> <span data-ttu-id="5a5f5-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="5a5f5-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a5f5-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a5f5-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5a5f5-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5a5f5-259">Test single sign-on</span></span>

<span data-ttu-id="5a5f5-260">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a5f5-261">Quando você clica em bloco Onit Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Onit aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a5f5-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="5a5f5-262">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5a5f5-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5a5f5-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5a5f5-263">Additional resources</span></span>

* [<span data-ttu-id="5a5f5-264">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5a5f5-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a5f5-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5a5f5-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

