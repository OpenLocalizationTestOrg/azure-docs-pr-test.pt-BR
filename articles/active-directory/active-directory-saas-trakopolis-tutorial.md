---
title: "Tutorial: Integração do Azure Active Directory ao Trakopolis | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3887cf8c085c30eb01ac769944da2fcfe3df81f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="0e769-103">Tutorial: Integração do Azure Active Directory ao Trakopolis</span><span class="sxs-lookup"><span data-stu-id="0e769-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="0e769-104">Neste tutorial, você aprenderá como integrar o Trakopolis ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0e769-104">In this tutorial, you learn how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e769-105">A integração do Trakopolis ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0e769-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e769-106">No Azure AD, você pode controlar quem tem acesso ao Trakopolis</span><span class="sxs-lookup"><span data-stu-id="0e769-106">You can control in Azure AD who has access to Trakopolis</span></span>
- <span data-ttu-id="0e769-107">Você pode permitir que os usuários façam logon automaticamente no Trakopolis (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e769-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e769-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0e769-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e769-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e769-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0e769-110">Prerequisites</span></span>

<span data-ttu-id="0e769-111">Para configurar a integração do Azure AD ao Trakopolis, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0e769-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

- <span data-ttu-id="0e769-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e769-113">Uma assinatura do Trakopolis habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0e769-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e769-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0e769-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e769-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0e769-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e769-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0e769-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e769-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e769-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e769-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0e769-118">Scenario description</span></span>
<span data-ttu-id="0e769-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0e769-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e769-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0e769-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e769-121">Adicionando o Trakopolis a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="0e769-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="0e769-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="0e769-123">Adicionando o Trakopolis a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="0e769-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="0e769-124">Para configurar a integração do Trakopolis ao Azure AD, você precisará adicionar o Trakopolis da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0e769-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e769-125">**Para adicionar o Trakopolis da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0e769-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e769-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0e769-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e769-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0e769-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e769-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0e769-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0e769-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0e769-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0e769-133">Na caixa de pesquisa, digite **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="0e769-133">In the search box, type **Trakopolis**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="0e769-135">No painel de resultados, selecione **Trakopolis** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0e769-135">In the results panel, select **Trakopolis**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e769-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e769-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Trakopolis com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="0e769-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e769-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Trakopolis é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e769-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis is to a user in Azure AD.</span></span> <span data-ttu-id="0e769-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-140">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>

<span data-ttu-id="0e769-141">No Trakopolis, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0e769-141">In Trakopolis, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0e769-142">Para configurar e testar o logon único do Azure AD com o Trakopolis, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0e769-142">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e769-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0e769-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e769-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0e769-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e769-145">**[Criação de um usuário de teste do Trakopolis](#creating-a-trakopolis-test-user)** – para ter um equivalente de Brenda Fernandes no Trakopolis que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e769-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e769-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e769-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e769-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0e769-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e769-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e769-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e769-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="0e769-150">**Para configurar o logon único do Azure AD com o Trakopolis, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0e769-150">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="0e769-151">No Portal do Azure, na página de integração de aplicativos do **Trakopolis**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0e769-151">In the Azure portal, on the **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0e769-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0e769-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="0e769-155">Na seção **URLs e Domínio do Trakopolis**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="0e769-155">On the **Trakopolis Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="0e769-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e769-157">a.</span></span> <span data-ttu-id="0e769-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="0e769-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="0e769-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e769-159">b.</span></span> <span data-ttu-id="0e769-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="0e769-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e769-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="0e769-161">These values are not real.</span></span> <span data-ttu-id="0e769-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="0e769-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e769-163">Contate [equipe de suporte ao cliente do Trakopolis](mailto:support@cantelematics.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="0e769-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) to get these values.</span></span> 

4. <span data-ttu-id="0e769-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="0e769-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="0e769-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0e769-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e769-168">Na seção **Configuração do Trakopolis**, clique em **Configurar o Trakopolis** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="0e769-168">On the **Trakopolis Configuration** section, click **Configure Trakopolis** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0e769-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0e769-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="0e769-171">Para configurar o logon único no lado do **Trakopolis**, é necessário enviar o **XML de Metadados, a URL de Saída, a ID da Entidade do SAML e a URL do Serviço de Logon Único SAML** baixados para a [equipe de suporte do Trakopolis](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="0e769-171">To configure single sign-on on **Trakopolis** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="0e769-172">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="0e769-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0e769-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0e769-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0e769-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0e769-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0e769-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e769-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e769-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e769-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0e769-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0e769-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0e769-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e769-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0e769-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e769-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0e769-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e769-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e769-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e769-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0e769-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e769-188">a.</span><span class="sxs-lookup"><span data-stu-id="0e769-188">a.</span></span> <span data-ttu-id="0e769-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0e769-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e769-190">b.</span><span class="sxs-lookup"><span data-stu-id="0e769-190">b.</span></span> <span data-ttu-id="0e769-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0e769-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e769-192">c.</span><span class="sxs-lookup"><span data-stu-id="0e769-192">c.</span></span> <span data-ttu-id="0e769-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0e769-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0e769-194">d.</span><span class="sxs-lookup"><span data-stu-id="0e769-194">d.</span></span> <span data-ttu-id="0e769-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0e769-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="0e769-196">Criação de um usuário de teste do Trakopolis</span><span class="sxs-lookup"><span data-stu-id="0e769-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="0e769-197">Nesta seção, você criará um usuário chamado Brenda Fernandes no Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="0e769-198">Trabalhe com a [equipe de suporte do Trakopolis](mailto:support@cantelematics.com) para adicionar os usuários na plataforma do Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add the users in the Trakopolis platform.</span></span> <span data-ttu-id="0e769-199">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0e769-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0e769-200">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0e769-201">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakopolis.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0e769-203">**Para atribuir Brenda Fernandes ao Trakopolis, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0e769-203">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="0e769-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0e769-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0e769-206">Na lista de aplicativos, selecione **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="0e769-206">In the applications list, select **Trakopolis**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="0e769-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e769-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0e769-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0e769-210">Click **Add** button.</span></span> <span data-ttu-id="0e769-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e769-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0e769-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0e769-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e769-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e769-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e769-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e769-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e769-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0e769-216">Testing single sign-on</span></span>

<span data-ttu-id="0e769-217">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0e769-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="0e769-218">Quando você clicar no bloco Trakopolis no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="0e769-218">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e769-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0e769-219">Additional resources</span></span>

* [<span data-ttu-id="0e769-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0e769-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e769-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e769-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

