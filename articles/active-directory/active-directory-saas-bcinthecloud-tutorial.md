---
title: "Tutorial: Integração do Azure Active Directory ao BC in the Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BC in the Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: ebc95d600eca1027331cd92cfe481d0c3ee833a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="4c002-103">Tutorial: Integração do Azure Active Directory ao BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c002-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="4c002-104">Neste tutorial, você aprende a integrar o BC in the Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4c002-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c002-105">A integração do BC in the Cloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4c002-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c002-106">No Azure AD, é possível controlar quem tem acesso ao BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c002-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="4c002-107">É possível permitir que os usuários se conectem automaticamente ao BC in the Cloud (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c002-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c002-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c002-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c002-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c002-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c002-110">Prerequisites</span></span>

<span data-ttu-id="4c002-111">Para configurar a integração do Azure AD ao BC in the Cloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4c002-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="4c002-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c002-113">Uma assinatura habilitada para logon único do BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c002-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c002-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4c002-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c002-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4c002-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c002-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4c002-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c002-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c002-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c002-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4c002-118">Scenario description</span></span>
<span data-ttu-id="4c002-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4c002-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c002-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4c002-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c002-121">Adicionando o BC in the Cloud por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4c002-121">Adding BC in the Cloud from the gallery</span></span>
2. <span data-ttu-id="4c002-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="4c002-123">Adicionando o BC in the Cloud por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4c002-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="4c002-124">Para configurar a integração do BC in the Cloud ao Azure AD, você precisa adicionar o BC in the Cloud à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="4c002-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c002-125">**Para adicionar o BC in the Cloud por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c002-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c002-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c002-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c002-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4c002-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c002-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c002-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4c002-131">Para adicionar o novo aplicativo, clique no botão **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c002-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4c002-133">Na caixa de pesquisa, digite **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c002-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="4c002-135">No painel de resultados, selecione **BC in the Cloud** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4c002-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c002-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c002-138">Nesta seção, você configura e testa o logon único do Azure AD com o BC in the Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4c002-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c002-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BC in the Cloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c002-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="4c002-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="4c002-141">No BC in the Cloud, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4c002-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c002-142">Para configurar e testar o logon único do Azure AD com o BC in the Cloud, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4c002-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c002-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4c002-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c002-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c002-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c002-145">**[Criando um usuário de teste do BC in the Cloud](#creating-a-bc-in-the-cloud-test-user)** – para ter um equivalente de Brenda Fernandes no BC in the Cloud que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c002-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c002-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c002-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c002-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4c002-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c002-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c002-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c002-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="4c002-150">**Para configurar o logon único do Azure AD com o BC in the Cloud, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c002-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c002-151">No portal do Azure, na página de integração do aplicativo do **BC in the Cloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4c002-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4c002-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4c002-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="4c002-155">Na seção **Domínio e URLs do BC in the Cloud**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c002-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="4c002-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c002-157">a.</span></span> <span data-ttu-id="4c002-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="4c002-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="4c002-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c002-159">b.</span></span> <span data-ttu-id="4c002-160">Na caixa de texto **Identificador**, digite uma URL como: `https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="4c002-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c002-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="4c002-161">This value is not real.</span></span> <span data-ttu-id="4c002-162">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="4c002-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4c002-163">Contate a [equipe de suporte ao Cliente do BC in the Cloud](https://www.bcinthecloud.com/supportcenter/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="4c002-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
4. <span data-ttu-id="4c002-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4c002-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="4c002-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4c002-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c002-168">Para configurar o logon único no lado do **BC in the Cloud**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="4c002-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="4c002-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4c002-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c002-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4c002-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c002-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c002-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c002-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c002-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c002-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4c002-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c002-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c002-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c002-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c002-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4c002-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c002-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c002-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c002-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c002-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c002-184">a.</span><span class="sxs-lookup"><span data-stu-id="4c002-184">a.</span></span> <span data-ttu-id="4c002-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c002-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c002-186">b.</span><span class="sxs-lookup"><span data-stu-id="4c002-186">b.</span></span> <span data-ttu-id="4c002-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c002-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c002-188">c.</span><span class="sxs-lookup"><span data-stu-id="4c002-188">c.</span></span> <span data-ttu-id="4c002-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4c002-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c002-190">d.</span><span class="sxs-lookup"><span data-stu-id="4c002-190">d.</span></span> <span data-ttu-id="4c002-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4c002-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="4c002-192">Criando um usuário de teste do BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="4c002-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="4c002-193">Nesta seção, você cria um usuário chamado Brenda Fernandes no BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="4c002-194">Trabalhe com a [equipe de suporte do Cliente BC in the Cloud](https://www.bcinthecloud.com/supportcenter/) para adicionar os usuários ao aplicativo BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="4c002-195">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4c002-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c002-196">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c002-197">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4c002-199">**Para atribuir Brenda Fernandes ao BC in the Cloud, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c002-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c002-200">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c002-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4c002-202">Na lista de aplicativos, selecione **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c002-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="4c002-204">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c002-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4c002-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4c002-206">Click **Add** button.</span></span> <span data-ttu-id="4c002-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c002-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4c002-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4c002-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c002-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c002-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c002-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c002-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c002-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4c002-212">Testing single sign-on</span></span>

<span data-ttu-id="4c002-213">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4c002-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="4c002-214">Quando você clicar no bloco BC in the Cloud no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c002-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="4c002-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c002-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c002-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4c002-216">Additional resources</span></span>

* [<span data-ttu-id="4c002-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4c002-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c002-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c002-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

