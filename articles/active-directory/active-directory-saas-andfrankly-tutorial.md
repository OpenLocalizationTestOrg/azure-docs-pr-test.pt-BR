---
title: "Tutorial: integração do Azure Active Directory ao &frankly | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o &frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="1c88c-103">Tutorial: integração do Azure Active Directory ao &frankly</span><span class="sxs-lookup"><span data-stu-id="1c88c-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="1c88c-104">Neste tutorial, você aprende a integrar o &frankly ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1c88c-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c88c-105">A integração do &frankly ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1c88c-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c88c-106">No Azure AD, é possível controlar quem tem acesso ao &frankly</span><span class="sxs-lookup"><span data-stu-id="1c88c-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="1c88c-107">Você pode permitir que seus usuários façam logon automaticamente no &frankly (Logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c88c-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c88c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c88c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c88c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c88c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1c88c-110">Prerequisites</span></span>

<span data-ttu-id="1c88c-111">Para configurar a integração do Azure AD ao &frankly, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1c88c-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="1c88c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c88c-113">Uma assinatura do &frankly habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="1c88c-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c88c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1c88c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c88c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1c88c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c88c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1c88c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c88c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c88c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c88c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1c88c-118">Scenario description</span></span>
<span data-ttu-id="1c88c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1c88c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c88c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1c88c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c88c-121">Adicionando &frankly da galeria</span><span class="sxs-lookup"><span data-stu-id="1c88c-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="1c88c-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="1c88c-123">Adicionando &frankly da galeria</span><span class="sxs-lookup"><span data-stu-id="1c88c-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="1c88c-124">Para configurar a integração do &frankly ao Azure AD, você precisa adicionar o &frankly da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1c88c-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c88c-125">**Para adicionar o &frankly da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1c88c-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c88c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c88c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c88c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1c88c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1c88c-133">Na caixa de pesquisa, digite **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-133">In the search box, type **&frankly**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="1c88c-135">No painel de resultados, selecione **&frankly** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c88c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c88c-138">Nesta seção, você configura e testa o logon único do Azure AD com o &frankly, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1c88c-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c88c-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do &frankly é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c88c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="1c88c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do &frankly.</span><span class="sxs-lookup"><span data-stu-id="1c88c-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="1c88c-141">No &frankly, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1c88c-142">Para configurar e testar o logon único do Azure AD com o &frankly, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1c88c-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c88c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1c88c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c88c-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1c88c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c88c-145">**[Criando um usuário de teste do &frankly](#creating-a-frankly-test-user)** – para ter um equivalente de Brenda Fernandes no &frankly que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c88c-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c88c-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c88c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c88c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1c88c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c88c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c88c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c88c-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo &frankly.</span><span class="sxs-lookup"><span data-stu-id="1c88c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="1c88c-150">**Para configurar o logon único do Azure AD com o Namely, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1c88c-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="1c88c-151">No portal do Azure, na página de integração do aplicativo do **&frankly**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1c88c-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1c88c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="1c88c-155">Na seção **Domínio e URLs do &frankly**, se desejar configurar o aplicativo no modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="1c88c-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="1c88c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c88c-157">a.</span></span> <span data-ttu-id="1c88c-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1c88c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="1c88c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c88c-159">b.</span></span> <span data-ttu-id="1c88c-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1c88c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="1c88c-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1c88c-162">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="1c88c-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="1c88c-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1c88c-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="1c88c-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1c88c-165">These values are not real.</span></span> <span data-ttu-id="1c88c-166">Atualize esses valores com o Identificador, o Logon e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="1c88c-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="1c88c-167">Contate a [equipe de suporte do &frankly](mailto:help@andfrankly.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="1c88c-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="1c88c-168">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1c88c-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="1c88c-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1c88c-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1c88c-172">Para configurar o logon único no lado do **&frankly**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="1c88c-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="1c88c-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1c88c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c88c-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1c88c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c88c-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c88c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c88c-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c88c-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1c88c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1c88c-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1c88c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c88c-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c88c-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1c88c-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c88c-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c88c-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1c88c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c88c-188">a.</span><span class="sxs-lookup"><span data-stu-id="1c88c-188">a.</span></span> <span data-ttu-id="1c88c-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c88c-190">b.</span><span class="sxs-lookup"><span data-stu-id="1c88c-190">b.</span></span> <span data-ttu-id="1c88c-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1c88c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c88c-192">c.</span><span class="sxs-lookup"><span data-stu-id="1c88c-192">c.</span></span> <span data-ttu-id="1c88c-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c88c-194">d.</span><span class="sxs-lookup"><span data-stu-id="1c88c-194">d.</span></span> <span data-ttu-id="1c88c-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="1c88c-196">Criar um usuário de teste do &frankly</span><span class="sxs-lookup"><span data-stu-id="1c88c-196">Creating a &frankly test user</span></span>

<span data-ttu-id="1c88c-197">Nesta seção, você criará uma usuária chamado Brenda Fernandes no &frankly.</span><span class="sxs-lookup"><span data-stu-id="1c88c-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="1c88c-198">Trabalhe com a [equipe de suporte do &frankly](mailto:help@andfrankly.com) para adicionar os usuários à plataforma &frankly.</span><span class="sxs-lookup"><span data-stu-id="1c88c-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c88c-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c88c-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao &frankly.</span><span class="sxs-lookup"><span data-stu-id="1c88c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1c88c-202">**Para atribuir Brenda Fernandes ao &frankly, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1c88c-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="1c88c-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1c88c-205">Na lista de aplicativos, escolha **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-205">In the applications list, select **&frankly**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="1c88c-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1c88c-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-209">Click **Add** button.</span></span> <span data-ttu-id="1c88c-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1c88c-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1c88c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c88c-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c88c-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c88c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c88c-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1c88c-215">Testing single sign-on</span></span>

<span data-ttu-id="1c88c-216">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1c88c-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1c88c-217">Quando você clicar no bloco &frankly no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo &frankly</span><span class="sxs-lookup"><span data-stu-id="1c88c-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c88c-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1c88c-218">Additional resources</span></span>

* [<span data-ttu-id="1c88c-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1c88c-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c88c-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c88c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

