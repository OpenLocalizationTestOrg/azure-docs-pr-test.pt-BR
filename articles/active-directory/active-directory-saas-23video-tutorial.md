---
title: "Tutorial: integração do Azure Active Directory com o 23 Video | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o 23 Video."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="4afdd-103">Tutorial: integração do Active Directory do Azure com o 23 Video</span><span class="sxs-lookup"><span data-stu-id="4afdd-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="4afdd-104">Neste tutorial, você aprenderá a integrar o 23 Video ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4afdd-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4afdd-105">A integração do 23 Video ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4afdd-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4afdd-106">Você pode controlar no AD do Azure quem tem acesso ao 23 Video</span><span class="sxs-lookup"><span data-stu-id="4afdd-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="4afdd-107">Você pode habilitar seus usuários a fazerem logon automaticamente no 23 Video (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4afdd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4afdd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4afdd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4afdd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4afdd-110">Prerequisites</span></span>

<span data-ttu-id="4afdd-111">Para configurar a integração do AD do Azure com o 23 Video, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4afdd-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="4afdd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4afdd-113">Uma assinatura habilitada para logon único do 23 Video</span><span class="sxs-lookup"><span data-stu-id="4afdd-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4afdd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4afdd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4afdd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4afdd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4afdd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4afdd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4afdd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4afdd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4afdd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4afdd-118">Scenario description</span></span>
<span data-ttu-id="4afdd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4afdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4afdd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4afdd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4afdd-121">Adicionando o 23 Video por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4afdd-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="4afdd-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="4afdd-123">Adicionando o 23 Video por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4afdd-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="4afdd-124">Para configurar a integração do 23 Video ao AD do Azure, você precisa adicionar o 23 Video por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4afdd-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4afdd-125">**Para adicionar o 23 Video por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4afdd-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4afdd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4afdd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4afdd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4afdd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4afdd-133">Na caixa de pesquisa, digite **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-133">In the search box, type **23 Video**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="4afdd-135">No painel de resultados, selecione **23 Video** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4afdd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4afdd-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 23 Video, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4afdd-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4afdd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do 23 Video é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4afdd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="4afdd-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do 23 Video.</span><span class="sxs-lookup"><span data-stu-id="4afdd-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="4afdd-141">No 23 Video, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4afdd-142">Para configurar e testar o logon único do AD do Azure com o 23 Video, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4afdd-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4afdd-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4afdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4afdd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4afdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4afdd-145">**[Criando um usuário de teste do 23 Video](#creating-a-23-video-test-user)** – para ter um equivalente de Brenda Fernandes no 23 Video que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4afdd-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4afdd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4afdd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4afdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4afdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4afdd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4afdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4afdd-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo 23 Video.</span><span class="sxs-lookup"><span data-stu-id="4afdd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="4afdd-150">**Para configurar o logon único do AD do Azure com o 23 Video, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4afdd-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="4afdd-151">No Portal do Azure, na página de integração de aplicativos do **23 Video**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4afdd-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4afdd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="4afdd-155">Na seção **URLs e Domínio do 23 Video**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4afdd-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="4afdd-157">a.</span><span class="sxs-lookup"><span data-stu-id="4afdd-157">a.</span></span> <span data-ttu-id="4afdd-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="4afdd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="4afdd-159">b.</span><span class="sxs-lookup"><span data-stu-id="4afdd-159">b.</span></span> <span data-ttu-id="4afdd-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="4afdd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4afdd-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4afdd-161">These values are not real.</span></span> <span data-ttu-id="4afdd-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="4afdd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4afdd-163">Contate a [equipe de suporte do Cliente 23 Video](mailto:support@23company.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4afdd-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="4afdd-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4afdd-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="4afdd-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4afdd-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4afdd-168">Na seção **Configuração do 23 Video**, clique em **Configurar o 23 Video** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4afdd-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4afdd-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="4afdd-171">Para configurar o logon único no lado do **23 Video**, você precisará enviar o **Certificado (Base64)** baixado e a **ID de Entidade SAML, URL do Serviço de Logon Único SAML e URL de Saída** para a [equipe de suporte do 23 Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="4afdd-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="4afdd-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4afdd-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4afdd-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4afdd-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4afdd-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4afdd-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4afdd-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4afdd-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4afdd-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4afdd-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4afdd-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4afdd-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4afdd-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4afdd-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4afdd-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4afdd-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4afdd-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4afdd-187">a.</span><span class="sxs-lookup"><span data-stu-id="4afdd-187">a.</span></span> <span data-ttu-id="4afdd-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4afdd-189">b.</span><span class="sxs-lookup"><span data-stu-id="4afdd-189">b.</span></span> <span data-ttu-id="4afdd-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4afdd-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4afdd-191">c.</span><span class="sxs-lookup"><span data-stu-id="4afdd-191">c.</span></span> <span data-ttu-id="4afdd-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4afdd-193">d.</span><span class="sxs-lookup"><span data-stu-id="4afdd-193">d.</span></span> <span data-ttu-id="4afdd-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="4afdd-195">Criando um usuário de teste do 23 Video</span><span class="sxs-lookup"><span data-stu-id="4afdd-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="4afdd-196">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no 23 Video.</span><span class="sxs-lookup"><span data-stu-id="4afdd-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="4afdd-197">**Para criar um usuário chamado Brenda Fernandes no 23 Video, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4afdd-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="4afdd-198">Faça logon no site da empresa 23 Video como administrador.</span><span class="sxs-lookup"><span data-stu-id="4afdd-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="4afdd-199">Vá para **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="4afdd-200">Na seção **Usuários**, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-200">In **Users** section, click **Configure**.</span></span>
   
    ![Atribuir usuário][400]

4. <span data-ttu-id="4afdd-202">Clique em **Adicionar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-202">Click **Add a new user**.</span></span> 
   
    ![Atribuir usuário][401]

5. <span data-ttu-id="4afdd-204">Na seção **Convidar alguém para participar deste site** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4afdd-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Atribuir usuário][402]

    <span data-ttu-id="4afdd-206">a.</span><span class="sxs-lookup"><span data-stu-id="4afdd-206">a.</span></span> <span data-ttu-id="4afdd-207">Na caixa de texto **Endereços de email** , digite o endereço de email de Brenda Fernandes no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4afdd-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="4afdd-208">b.</span><span class="sxs-lookup"><span data-stu-id="4afdd-208">b.</span></span> <span data-ttu-id="4afdd-209">Clique em **Adicionar o usuário**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4afdd-210">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4afdd-211">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao 23 Video.</span><span class="sxs-lookup"><span data-stu-id="4afdd-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4afdd-213">**Para atribuir Brenda Fernandes ao 23 Video, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4afdd-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="4afdd-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4afdd-216">Na lista de aplicativos, selecione **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-216">In the applications list, select **23 Video**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="4afdd-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4afdd-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4afdd-220">Click **Add** button.</span></span> <span data-ttu-id="4afdd-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4afdd-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4afdd-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4afdd-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4afdd-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4afdd-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4afdd-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4afdd-226">Testing single sign-on</span></span>

<span data-ttu-id="4afdd-227">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4afdd-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4afdd-228">Quando você clica no bloco 23 Video no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo 23 Video.</span><span class="sxs-lookup"><span data-stu-id="4afdd-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4afdd-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4afdd-229">Additional resources</span></span>

* [<span data-ttu-id="4afdd-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4afdd-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4afdd-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4afdd-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
