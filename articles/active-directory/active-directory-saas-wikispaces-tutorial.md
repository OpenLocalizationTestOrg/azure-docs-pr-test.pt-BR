---
title: "Tutorial: Integração do Azure Active Directory com o Wikispaces | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d01543955bdf6a274571f67eafdff5f637863d5c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="e27b5-103">Tutorial: Integração do Active Directory do Azure com o Wikispaces</span><span class="sxs-lookup"><span data-stu-id="e27b5-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="e27b5-104">Neste tutorial, você aprenderá como integrar o Wikispaces ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e27b5-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e27b5-105">A integração do Wikispaces ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e27b5-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e27b5-106">No Azure AD, é possível controlar quem tem acesso ao Wikispaces</span><span class="sxs-lookup"><span data-stu-id="e27b5-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="e27b5-107">É possível permitir que os usuários entrem automaticamente no Wikispaces (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b5-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e27b5-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e27b5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e27b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e27b5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e27b5-110">Prerequisites</span></span>

<span data-ttu-id="e27b5-111">Para configurar a integração do Azure AD com o Wikispaces, serão necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e27b5-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="e27b5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e27b5-113">Uma assinatura do Wikispaces habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e27b5-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e27b5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e27b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e27b5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e27b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e27b5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e27b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e27b5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e27b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e27b5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e27b5-118">Scenario description</span></span>
<span data-ttu-id="e27b5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e27b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e27b5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e27b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e27b5-121">Adicionar o Wikispaces da galeria</span><span class="sxs-lookup"><span data-stu-id="e27b5-121">Adding Wikispaces from the gallery</span></span>
2. <span data-ttu-id="e27b5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="e27b5-123">Adicionar o Wikispaces da galeria</span><span class="sxs-lookup"><span data-stu-id="e27b5-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="e27b5-124">Para configurar a integração do Wikispaces com o Azure AD, é necessário adicionar o Wikispaces da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e27b5-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e27b5-125">**Para adicionar o Wikispaces da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="e27b5-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e27b5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e27b5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e27b5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e27b5-133">Na caixa de pesquisa, digite **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-133">In the search box, type **Wikispaces**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="e27b5-135">No painel de resultados, selecione **Wikispaces** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e27b5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e27b5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Wikispaces com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e27b5-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e27b5-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Wikispaces é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="e27b5-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="e27b5-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="e27b5-141">No Wikispaces, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e27b5-142">Para configurar e testar o logon único do Azure AD com o Wikispaces, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e27b5-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e27b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e27b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e27b5-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e27b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e27b5-145">**[Criação de um usuário de teste do Wikispaces](#creating-a-wikispaces-test-user)** – para ter um equivalente de Brenda Fernandes no Wikispaces que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e27b5-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e27b5-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e27b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e27b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e27b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e27b5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e27b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e27b5-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="e27b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="e27b5-150">**Para configurar o logon único do Azure AD com o Wikispaces, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="e27b5-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b5-151">No Portal do Azure, na página de integração de aplicativos **Wikispaces**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e27b5-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e27b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="e27b5-155">Na seção **URLs e Domínio do Wikispaces**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e27b5-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="e27b5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e27b5-157">a.</span></span> <span data-ttu-id="e27b5-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="e27b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="e27b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="e27b5-159">b.</span></span> <span data-ttu-id="e27b5-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="e27b5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e27b5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e27b5-161">These values are not real.</span></span> <span data-ttu-id="e27b5-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e27b5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e27b5-163">Contate a [equipe de suporte ao cliente do Wikispaces](https://www.wikispaces.com/site/help) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e27b5-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

4. <span data-ttu-id="e27b5-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e27b5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="e27b5-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e27b5-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e27b5-168">Para configurar o logon único no lado do **Wikispaces**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="e27b5-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="e27b5-169">Assim que a configuração for concluída, você receberá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="e27b5-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="e27b5-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e27b5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e27b5-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e27b5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e27b5-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e27b5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e27b5-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e27b5-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e27b5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e27b5-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e27b5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b5-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e27b5-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e27b5-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e27b5-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e27b5-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e27b5-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e27b5-185">a.</span><span class="sxs-lookup"><span data-stu-id="e27b5-185">a.</span></span> <span data-ttu-id="e27b5-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e27b5-187">b.</span><span class="sxs-lookup"><span data-stu-id="e27b5-187">b.</span></span> <span data-ttu-id="e27b5-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e27b5-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e27b5-189">c.</span><span class="sxs-lookup"><span data-stu-id="e27b5-189">c.</span></span> <span data-ttu-id="e27b5-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e27b5-191">d.</span><span class="sxs-lookup"><span data-stu-id="e27b5-191">d.</span></span> <span data-ttu-id="e27b5-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="e27b5-193">Criação de um usuário de teste do Wikispaces</span><span class="sxs-lookup"><span data-stu-id="e27b5-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="e27b5-194">Para permitir que os usuários do Azure AD façam logon no Wikispaces, eles devem ser provisionados no Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="e27b5-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="e27b5-195">No caso do Wikispaces, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e27b5-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="e27b5-196">Para provisionar contas de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e27b5-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="e27b5-197">Faça logon no site da sua empresa **Wikispaces** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e27b5-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="e27b5-198">Vá para **Membros**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="e27b5-199">![Membros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Membros")</span><span class="sxs-lookup"><span data-stu-id="e27b5-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="e27b5-200">Clique em **Convidar Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="e27b5-201">![Convidar Pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="e27b5-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="e27b5-202">Na seção **Convidar Pessoas** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e27b5-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e27b5-203">![Convidar Pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="e27b5-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="e27b5-204">a.</span><span class="sxs-lookup"><span data-stu-id="e27b5-204">a.</span></span> <span data-ttu-id="e27b5-205">Digite **Nomes de Usuário ou Endereço de Email** de uma conta válida do AAD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e27b5-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="e27b5-206">b.</span><span class="sxs-lookup"><span data-stu-id="e27b5-206">b.</span></span> <span data-ttu-id="e27b5-207">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="e27b5-208">O titular da conta do Active Directory do Azure recebe um email que inclui um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="e27b5-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="e27b5-209">Você pode usar qualquer outra ferramenta de criação da conta de usuário do Wikispaces ou APIs fornecidas pelo Wikispaces para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="e27b5-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e27b5-210">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e27b5-211">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="e27b5-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e27b5-213">**Para atribuir Brenda Fernandes ao Wikispaces, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="e27b5-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="e27b5-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e27b5-216">Na lista de aplicativos, selecione **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-216">In the applications list, select **Wikispaces**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="e27b5-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e27b5-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e27b5-220">Click **Add** button.</span></span> <span data-ttu-id="e27b5-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e27b5-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e27b5-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e27b5-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e27b5-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e27b5-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e27b5-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e27b5-226">Testing single sign-on</span></span>

<span data-ttu-id="e27b5-227">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e27b5-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e27b5-228">Ao clicar no bloco Wikispaces no Painel de Acesso, você deverá entrar automaticamente no seu aplicativo Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="e27b5-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="e27b5-229">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e27b5-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e27b5-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e27b5-230">Additional resources</span></span>

* [<span data-ttu-id="e27b5-231">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e27b5-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e27b5-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e27b5-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

