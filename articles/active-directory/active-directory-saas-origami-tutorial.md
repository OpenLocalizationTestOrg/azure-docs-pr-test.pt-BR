---
title: "Tutorial: integração do Azure Active Directory ao Origami | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="f3420-103">Tutorial: Integração do Azure Active Directory ao Origami</span><span class="sxs-lookup"><span data-stu-id="f3420-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="f3420-104">Neste tutorial, você aprenderá a integrar o Origami ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f3420-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3420-105">A integração do Origami ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f3420-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3420-106">No Azure AD, é possível controlar quem tem acesso ao Origami</span><span class="sxs-lookup"><span data-stu-id="f3420-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="f3420-107">É possível permitir que os usuários façam logon automaticamente no Origami (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3420-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3420-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3420-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3420-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3420-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f3420-110">Prerequisites</span></span>

<span data-ttu-id="f3420-111">Para configurar a integração do Azure AD ao Origami, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f3420-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="f3420-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3420-113">Uma assinatura habilitada para logon único do Origami</span><span class="sxs-lookup"><span data-stu-id="f3420-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3420-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f3420-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3420-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f3420-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3420-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f3420-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3420-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3420-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3420-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f3420-118">Scenario description</span></span>
<span data-ttu-id="f3420-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f3420-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3420-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f3420-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3420-121">Adicionando o Origami por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f3420-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="f3420-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="f3420-123">Adicionando o Origami por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f3420-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="f3420-124">Para configurar a integração do Origami ao Azure AD, você precisará adicionar o Origami por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f3420-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3420-125">**Para adicionar o Origami por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f3420-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3420-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f3420-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f3420-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f3420-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3420-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f3420-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f3420-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3420-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f3420-133">Na caixa de pesquisa, digite **Origami**.</span><span class="sxs-lookup"><span data-stu-id="f3420-133">In the search box, type **Origami**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="f3420-135">No painel de resultados, selecione **Origami** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3420-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3420-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3420-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Origami, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f3420-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3420-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Origami é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3420-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="f3420-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Origami.</span><span class="sxs-lookup"><span data-stu-id="f3420-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="f3420-141">No Origami, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f3420-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3420-142">Para configurar e testar o logon único do Azure AD com o Origami, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f3420-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3420-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f3420-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f3420-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f3420-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3420-145">**[Criação de um usuário de teste do Origami](#creating-an-origami-test-user)** – para ter um equivalente de Brenda Fernandes no Origami que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3420-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3420-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3420-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3420-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f3420-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3420-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3420-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3420-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Origami.</span><span class="sxs-lookup"><span data-stu-id="f3420-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="f3420-150">**Para configurar o logon único do Azure AD com o Origami, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f3420-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="f3420-151">No Portal do Azure, na página de integração de aplicativos do **Origami**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f3420-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f3420-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f3420-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="f3420-155">Na seção **URLs e Domínio do Origami**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3420-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="f3420-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f3420-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3420-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f3420-158">The value is not real.</span></span> <span data-ttu-id="f3420-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="f3420-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="f3420-160">Entre em contato com a [equipe de suporte ao cliente do Origami](https://wordpress.org/support/theme/origami) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="f3420-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="f3420-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f3420-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="f3420-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f3420-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3420-165">Na seção **Configuração do Origami**, clique em **Configurar o Origami** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f3420-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f3420-166">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f3420-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="f3420-168">Faça logon na conta do Origami com direitos de Administrador.</span><span class="sxs-lookup"><span data-stu-id="f3420-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="f3420-169">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="f3420-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="f3420-171">Na página do diálogo Configuração de Logon Único, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3420-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="f3420-173">a.</span><span class="sxs-lookup"><span data-stu-id="f3420-173">a.</span></span> <span data-ttu-id="f3420-174">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f3420-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="f3420-175">b.</span><span class="sxs-lookup"><span data-stu-id="f3420-175">b.</span></span> <span data-ttu-id="f3420-176">Na caixa de texto **URL da Página de Entrada do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3420-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f3420-177">c.</span><span class="sxs-lookup"><span data-stu-id="f3420-177">c.</span></span> <span data-ttu-id="f3420-178">Na caixa de texto **URL da Página de Saída do Provedor de Identidade**, cole o valor da **URL de Saída** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3420-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f3420-179">d.</span><span class="sxs-lookup"><span data-stu-id="f3420-179">d.</span></span> <span data-ttu-id="f3420-180">Clique em **Procurar** para carregar o certificado baixado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3420-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="f3420-181">e.</span><span class="sxs-lookup"><span data-stu-id="f3420-181">e.</span></span> <span data-ttu-id="f3420-182">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="f3420-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f3420-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f3420-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3420-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f3420-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3420-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3420-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3420-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3420-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f3420-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f3420-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f3420-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3420-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f3420-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f3420-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f3420-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f3420-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3420-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f3420-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3420-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3420-198">a.</span><span class="sxs-lookup"><span data-stu-id="f3420-198">a.</span></span> <span data-ttu-id="f3420-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f3420-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3420-200">b.</span><span class="sxs-lookup"><span data-stu-id="f3420-200">b.</span></span> <span data-ttu-id="f3420-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f3420-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3420-202">c.</span><span class="sxs-lookup"><span data-stu-id="f3420-202">c.</span></span> <span data-ttu-id="f3420-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f3420-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3420-204">d.</span><span class="sxs-lookup"><span data-stu-id="f3420-204">d.</span></span> <span data-ttu-id="f3420-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f3420-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="f3420-206">Criando um usuário de teste do Origami</span><span class="sxs-lookup"><span data-stu-id="f3420-206">Creating an Origami test user</span></span>

<span data-ttu-id="f3420-207">Nesta seção, você criará um usuário chamado Brenda Fernandes no Origami.</span><span class="sxs-lookup"><span data-stu-id="f3420-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="f3420-208">Faça logon na conta do Origami com direitos de Administrador.</span><span class="sxs-lookup"><span data-stu-id="f3420-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="f3420-209">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="f3420-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="f3420-211">No diálogo **Usuários e Segurança**, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f3420-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="f3420-213">Clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f3420-213">Click **Add New User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="f3420-215">Na caixa de diálogo Adicionar Novo Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f3420-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="f3420-217">a.</span><span class="sxs-lookup"><span data-stu-id="f3420-217">a.</span></span> <span data-ttu-id="f3420-218">Na caixa de texto **Nome de Usuário**, insira o email do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f3420-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f3420-219">b.</span><span class="sxs-lookup"><span data-stu-id="f3420-219">b.</span></span> <span data-ttu-id="f3420-220">Na caixa de texto **Senha** , digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="f3420-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="f3420-221">c.</span><span class="sxs-lookup"><span data-stu-id="f3420-221">c.</span></span> <span data-ttu-id="f3420-222">Na caixa de texto **Confirmar Senha** , digite a senha novamente.</span><span class="sxs-lookup"><span data-stu-id="f3420-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="f3420-223">d.</span><span class="sxs-lookup"><span data-stu-id="f3420-223">d.</span></span> <span data-ttu-id="f3420-224">Na caixa de texto **Nome**, digite o nome do usuário como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="f3420-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="f3420-225">e.</span><span class="sxs-lookup"><span data-stu-id="f3420-225">e.</span></span> <span data-ttu-id="f3420-226">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f3420-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="f3420-227">f.</span><span class="sxs-lookup"><span data-stu-id="f3420-227">f.</span></span> <span data-ttu-id="f3420-228">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f3420-228">Click **Save**.</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="f3420-230">Atribua **Funções de Usuário** e **Acesso para Cliente** ao usuário.</span><span class="sxs-lookup"><span data-stu-id="f3420-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3420-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3420-233">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Origami.</span><span class="sxs-lookup"><span data-stu-id="f3420-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f3420-235">**Para atribuir Brenda Fernandes ao Origami, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f3420-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="f3420-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f3420-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f3420-238">Na lista de aplicativos, selecione **Origami**.</span><span class="sxs-lookup"><span data-stu-id="f3420-238">In the applications list, select **Origami**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="f3420-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3420-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f3420-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3420-242">Click **Add** button.</span></span> <span data-ttu-id="f3420-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3420-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f3420-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f3420-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f3420-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3420-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3420-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3420-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3420-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f3420-248">Testing single sign-on</span></span>

<span data-ttu-id="f3420-249">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f3420-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3420-250">Ao clicar no bloco do Origami no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do Origami.</span><span class="sxs-lookup"><span data-stu-id="f3420-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3420-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f3420-251">Additional resources</span></span>

* [<span data-ttu-id="f3420-252">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f3420-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3420-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3420-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

