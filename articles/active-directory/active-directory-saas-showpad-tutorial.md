---
title: "Tutorial: integração do Azure Active Directory com o Showpad | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: c8b39c9215675d8073f896f934339e7cd55334cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="901fd-103">Tutorial: Integração do Azure Active Directory com o Showpad</span><span class="sxs-lookup"><span data-stu-id="901fd-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="901fd-104">Neste tutorial, você aprende a integrar o Showpad ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="901fd-104">In this tutorial, you learn how to integrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="901fd-105">A integração do Showpad ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="901fd-105">Integrating Showpad with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="901fd-106">No Azure AD, é possível controlar quem tem acesso ao Showpad</span><span class="sxs-lookup"><span data-stu-id="901fd-106">You can control in Azure AD who has access to Showpad</span></span>
- <span data-ttu-id="901fd-107">Você pode permitir que os usuários façam logon automaticamente no Showpad (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-107">You can enable your users to automatically get signed-on to Showpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="901fd-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="901fd-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="901fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="901fd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="901fd-110">Prerequisites</span></span>

<span data-ttu-id="901fd-111">Para configurar a integração do Azure AD com o Showpad, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="901fd-111">To configure Azure AD integration with Showpad, you need the following items:</span></span>

- <span data-ttu-id="901fd-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="901fd-113">Uma assinatura habilitada para logon único do Showpad</span><span class="sxs-lookup"><span data-stu-id="901fd-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="901fd-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="901fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="901fd-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="901fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="901fd-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="901fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="901fd-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="901fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="901fd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="901fd-118">Scenario description</span></span>
<span data-ttu-id="901fd-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="901fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="901fd-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="901fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="901fd-121">Adição do Showpad da galeria</span><span class="sxs-lookup"><span data-stu-id="901fd-121">Adding Showpad from the gallery</span></span>
2. <span data-ttu-id="901fd-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-the-gallery"></a><span data-ttu-id="901fd-123">Adição do Showpad da galeria</span><span class="sxs-lookup"><span data-stu-id="901fd-123">Adding Showpad from the gallery</span></span>

<span data-ttu-id="901fd-124">Para configurar a integração do Showpad ao Azure AD, você precisará adicionar o Showpad à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="901fd-124">To configure the integration of Showpad into Azure AD, you need to add Showpad from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="901fd-125">**Para adicionar o Showpad da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="901fd-125">**To add Showpad from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="901fd-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="901fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="901fd-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="901fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="901fd-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="901fd-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="901fd-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="901fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="901fd-133">Na caixa de pesquisa, digite **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="901fd-133">In the search box, type **Showpad**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="901fd-135">No painel de resultados, selecione **Showpad** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="901fd-135">In the results panel, select **Showpad**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="901fd-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="901fd-138">Nesta seção, você configura e testa o logon único do Azure AD com o Showpad, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="901fd-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="901fd-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Showpad é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="901fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Showpad is to a user in Azure AD.</span></span> <span data-ttu-id="901fd-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Showpad.</span><span class="sxs-lookup"><span data-stu-id="901fd-140">In other words, a link relationship between an Azure AD user and the related user in Showpad needs to be established.</span></span>

<span data-ttu-id="901fd-141">No Showpad, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="901fd-141">In Showpad, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="901fd-142">Para configurar e testar o logon único do Azure AD com o Showpad, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="901fd-142">To configure and test Azure AD single sign-on with Showpad, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="901fd-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="901fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="901fd-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="901fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="901fd-145">**[Criando um usuário de teste do Showpad](#creating-a-showpad-test-user)** – para ter um equivalente de Brenda Fernandes no Showpad que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="901fd-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - to have a counterpart of Britta Simon in Showpad that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="901fd-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="901fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="901fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="901fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="901fd-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="901fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="901fd-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Showpad.</span><span class="sxs-lookup"><span data-stu-id="901fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="901fd-150">**Para configurar o logon único do Azure AD com o Showpad, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="901fd-150">**To configure Azure AD single sign-on with Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="901fd-151">No portal do Azure, na página de integração do aplicativo **Showpad**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="901fd-151">In the Azure portal, on the **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="901fd-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="901fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="901fd-155">Na seção **Domínio e URLs do Showpad**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="901fd-155">On the **Showpad Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="901fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="901fd-157">a.</span></span> <span data-ttu-id="901fd-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="901fd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="901fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="901fd-159">b.</span></span> <span data-ttu-id="901fd-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="901fd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="901fd-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="901fd-161">These values are not real.</span></span> <span data-ttu-id="901fd-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="901fd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="901fd-163">Contate a [equipe de suporte do Showpad](https://help.showpad.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="901fd-163">Contact [Showpad support team](https://help.showpad.com) to get these values.</span></span> 
 


4. <span data-ttu-id="901fd-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="901fd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="901fd-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="901fd-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="901fd-168">Faça logon no seu locatário do Showpad como administrador.</span><span class="sxs-lookup"><span data-stu-id="901fd-168">Sign-on to your Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="901fd-169">No menu na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="901fd-169">In the menu on the top, click the **Settings**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="901fd-171">Navegue para “**Logon Único**” e clique em “**Habilitar**”.</span><span class="sxs-lookup"><span data-stu-id="901fd-171">Navigate to "**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="901fd-173">No diálogo **Adicionar um Serviço SAML 2.0** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="901fd-173">On the **Add a SAML 2.0 Service** dialog, perform the following steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="901fd-175">a.</span><span class="sxs-lookup"><span data-stu-id="901fd-175">a.</span></span> <span data-ttu-id="901fd-176">Na caixa de texto **Nome**, digite o nome do Provedor do Identificador (por exemplo: o nome de sua empresa).</span><span class="sxs-lookup"><span data-stu-id="901fd-176">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="901fd-177">b.</span><span class="sxs-lookup"><span data-stu-id="901fd-177">b.</span></span> <span data-ttu-id="901fd-178">Como **Fonte de Metadados**, selecione **XML**.</span><span class="sxs-lookup"><span data-stu-id="901fd-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="901fd-179">c.</span><span class="sxs-lookup"><span data-stu-id="901fd-179">c.</span></span> <span data-ttu-id="901fd-180">Copie o conteúdo do arquivo XML de metadados, baixado no portal do Azure e, em seguida, cole-o na caixa de texto **XML de Metadados**.</span><span class="sxs-lookup"><span data-stu-id="901fd-180">Copy the content of metadata XML file, which you have downloaded from the Azure portal, and then paste it into the **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="901fd-181">d.</span><span class="sxs-lookup"><span data-stu-id="901fd-181">d.</span></span> <span data-ttu-id="901fd-182">Selecione **Provisionar automaticamente contas para novos usuários quando eles fizerem logon**.</span><span class="sxs-lookup"><span data-stu-id="901fd-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="901fd-183">e.</span><span class="sxs-lookup"><span data-stu-id="901fd-183">e.</span></span> <span data-ttu-id="901fd-184">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="901fd-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="901fd-185">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="901fd-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="901fd-186">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="901fd-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="901fd-187">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="901fd-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="901fd-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="901fd-189">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="901fd-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="901fd-191">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="901fd-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="901fd-192">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="901fd-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="901fd-194">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="901fd-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="901fd-196">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="901fd-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="901fd-198">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="901fd-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="901fd-200">a.</span><span class="sxs-lookup"><span data-stu-id="901fd-200">a.</span></span> <span data-ttu-id="901fd-201">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="901fd-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="901fd-202">b.</span><span class="sxs-lookup"><span data-stu-id="901fd-202">b.</span></span> <span data-ttu-id="901fd-203">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="901fd-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="901fd-204">c.</span><span class="sxs-lookup"><span data-stu-id="901fd-204">c.</span></span> <span data-ttu-id="901fd-205">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="901fd-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="901fd-206">d.</span><span class="sxs-lookup"><span data-stu-id="901fd-206">d.</span></span> <span data-ttu-id="901fd-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="901fd-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="901fd-208">Criar um usuário de teste do Showpad</span><span class="sxs-lookup"><span data-stu-id="901fd-208">Creating a Showpad test user</span></span>

<span data-ttu-id="901fd-209">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Showpad.</span><span class="sxs-lookup"><span data-stu-id="901fd-209">The objective of this section is to create a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="901fd-210">O Showpad dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="901fd-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="901fd-211">Você já habilitou o provisionamento em **[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="901fd-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="901fd-212">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="901fd-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="901fd-213">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="901fd-214">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Showpad.</span><span class="sxs-lookup"><span data-stu-id="901fd-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Showpad.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="901fd-216">**Para atribuir Brenda Fernandes ao Showpad, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="901fd-216">**To assign Britta Simon to Showpad, perform the following steps:**</span></span>

1. <span data-ttu-id="901fd-217">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="901fd-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="901fd-219">Na lista de aplicativos, selecione **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="901fd-219">In the applications list, select **Showpad**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="901fd-221">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="901fd-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="901fd-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="901fd-223">Click **Add** button.</span></span> <span data-ttu-id="901fd-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="901fd-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="901fd-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="901fd-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="901fd-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="901fd-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="901fd-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="901fd-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="901fd-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="901fd-229">Testing single sign-on</span></span>

<span data-ttu-id="901fd-230">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="901fd-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="901fd-231">Quando você clicar no bloco do Showpad no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Showpad.</span><span class="sxs-lookup"><span data-stu-id="901fd-231">When you click the Showpad tile in the Access Panel, you should get automatically signed-on to Showpad application.</span></span>
<span data-ttu-id="901fd-232">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="901fd-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="901fd-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="901fd-233">Additional resources</span></span>

* [<span data-ttu-id="901fd-234">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="901fd-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="901fd-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="901fd-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

