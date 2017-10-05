---
title: "Tutorial: integração do Azure Active Directory ao Tidemark | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Tidemark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 170dc58363b12ec671c2fab8c80c7720d3dbf352
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="434fd-103">Tutorial: integração do Active Directory do Azure com o Tidemark</span><span class="sxs-lookup"><span data-stu-id="434fd-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="434fd-104">Neste tutorial, você aprenderá como integrar o Tidemark ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="434fd-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="434fd-105">A integração do Tidemark ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="434fd-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="434fd-106">Você pode controlar no AD do Azure quem tem acesso ao Tidemark</span><span class="sxs-lookup"><span data-stu-id="434fd-106">You can control in Azure AD who has access to Tidemark</span></span>
- <span data-ttu-id="434fd-107">Você pode permitir que os usuários façam logon automaticamente no Tidemark (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="434fd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="434fd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="434fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="434fd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="434fd-110">Prerequisites</span></span>

<span data-ttu-id="434fd-111">Para configurar a integração do AD do Azure com o Tidemark, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="434fd-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

- <span data-ttu-id="434fd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="434fd-113">Uma assinatura do Tidemark habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="434fd-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="434fd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="434fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="434fd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="434fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="434fd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="434fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="434fd-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="434fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="434fd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="434fd-118">Scenario description</span></span>
<span data-ttu-id="434fd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="434fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="434fd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="434fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="434fd-121">Adicionando o Tidemark por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="434fd-121">Adding Tidemark from the gallery</span></span>
2. <span data-ttu-id="434fd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-the-gallery"></a><span data-ttu-id="434fd-123">Adicionando o Tidemark por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="434fd-123">Adding Tidemark from the gallery</span></span>
<span data-ttu-id="434fd-124">Para configurar a integração do Tidemark com o AD do Azure, você precisa adicionar o Tidemark por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="434fd-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="434fd-125">**Para adicionar o Tidemark por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="434fd-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="434fd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="434fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="434fd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="434fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="434fd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="434fd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="434fd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="434fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="434fd-133">Na caixa de pesquisa, digite **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="434fd-133">In the search box, type **Tidemark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="434fd-135">No painel de resultados, selecione **Tidemark** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="434fd-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="434fd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="434fd-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Tidemark, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="434fd-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="434fd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Tidemark é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span></span> <span data-ttu-id="434fd-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="434fd-141">No Tidemark, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="434fd-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="434fd-142">Para configurar e testar o logon único do AD do Azure com o Tidemark, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="434fd-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="434fd-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="434fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="434fd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="434fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="434fd-145">**[Criação de um usuário de teste do Tidemark](#creating-a-tidemark-test-user)** – para ter um equivalente de Brenda Fernandes no Tidemark que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="434fd-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="434fd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="434fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="434fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="434fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="434fd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="434fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="434fd-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="434fd-150">**Para configurar o logon único do AD do Azure com o Tidemark, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="434fd-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="434fd-151">No Portal do Azure, na página de integração de aplicativos do **Tidemark**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="434fd-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="434fd-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="434fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="434fd-155">Na seção **URLs e Domínio do Tidemark**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="434fd-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="434fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="434fd-157">a.</span></span> <span data-ttu-id="434fd-158">Na caixa de texto **URL de Logon**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="434fd-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="434fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="434fd-159">b.</span></span> <span data-ttu-id="434fd-160">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="434fd-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="434fd-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="434fd-161">These values are not real.</span></span> <span data-ttu-id="434fd-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="434fd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="434fd-163">Contate a [equipe de suporte ao cliente do Tidemark](http://www.tidemark.com/contact-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="434fd-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="434fd-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="434fd-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="434fd-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="434fd-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="434fd-168">Na seção **Configuração do Tidemark**, clique em **Configurar o Tidemark** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="434fd-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="434fd-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="434fd-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="434fd-171">Para configurar o logon único no lado do **Tidemark**, é necessário enviar o **Certificado (Base64), a ID da Entidade SAML, a URL do Serviço de Logon Único de SAML e a URL de Saída** baixados para a [equipe de suporte do Tidemark](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="434fd-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="434fd-172">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="434fd-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="434fd-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="434fd-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="434fd-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="434fd-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="434fd-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="434fd-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="434fd-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="434fd-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="434fd-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="434fd-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="434fd-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="434fd-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="434fd-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="434fd-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="434fd-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="434fd-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="434fd-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="434fd-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="434fd-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="434fd-188">a.</span><span class="sxs-lookup"><span data-stu-id="434fd-188">a.</span></span> <span data-ttu-id="434fd-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="434fd-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="434fd-190">b.</span><span class="sxs-lookup"><span data-stu-id="434fd-190">b.</span></span> <span data-ttu-id="434fd-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="434fd-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="434fd-192">c.</span><span class="sxs-lookup"><span data-stu-id="434fd-192">c.</span></span> <span data-ttu-id="434fd-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="434fd-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="434fd-194">d.</span><span class="sxs-lookup"><span data-stu-id="434fd-194">d.</span></span> <span data-ttu-id="434fd-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="434fd-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="434fd-196">Criar um usuário de teste do Tidemark</span><span class="sxs-lookup"><span data-stu-id="434fd-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="434fd-197">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="434fd-198">Trabalhe com a [equipe de suporte do Tidemark](http://www.tidemark.com/contact-us) para adicionar usuários na conta do Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="434fd-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="434fd-200">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="434fd-202">**Para atribuir Brenda Fernandes ao Tidemark, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="434fd-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="434fd-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="434fd-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="434fd-205">Na lista de aplicativos, selecione **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="434fd-205">In the applications list, select **Tidemark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="434fd-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="434fd-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="434fd-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="434fd-209">Click **Add** button.</span></span> <span data-ttu-id="434fd-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="434fd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="434fd-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="434fd-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="434fd-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="434fd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="434fd-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="434fd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="434fd-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="434fd-215">Testing single sign-on</span></span>

<span data-ttu-id="434fd-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="434fd-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="434fd-217">Quando você clicar no bloco Tidemark no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Tidemark.</span><span class="sxs-lookup"><span data-stu-id="434fd-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>
<span data-ttu-id="434fd-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="434fd-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="434fd-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="434fd-219">Additional resources</span></span>

* [<span data-ttu-id="434fd-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="434fd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="434fd-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="434fd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

