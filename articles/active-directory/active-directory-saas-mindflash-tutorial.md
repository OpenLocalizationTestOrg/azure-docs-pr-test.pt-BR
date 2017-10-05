---
title: "Tutorial: Integração do Azure Active Directory ao Mindflash | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 90de7b6a82d88f9407a35fbfebe8a652928d76cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="e0e80-103">Tutorial: Integração do Active Directory do Azure com o Mindflash</span><span class="sxs-lookup"><span data-stu-id="e0e80-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="e0e80-104">Neste tutorial, você aprenderá a integrar o Mindflash ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e0e80-104">In this tutorial, you learn how to integrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0e80-105">A integração do Mindflash ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e0e80-105">Integrating Mindflash with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0e80-106">No Azure AD, é possível controlar quem tem acesso ao Mindflash</span><span class="sxs-lookup"><span data-stu-id="e0e80-106">You can control in Azure AD who has access to Mindflash</span></span>
- <span data-ttu-id="e0e80-107">Você pode permitir que seus usuários façam logon automaticamente no Mindflash (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0e80-107">You can enable your users to automatically get signed-on to Mindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0e80-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0e80-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0e80-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0e80-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0e80-110">Prerequisites</span></span>

<span data-ttu-id="e0e80-111">Para configurar a integração do Azure AD com o Mindflash, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e0e80-111">To configure Azure AD integration with Mindflash, you need the following items:</span></span>

- <span data-ttu-id="e0e80-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0e80-113">Uma assinatura habilitada para logon único do Mindflash</span><span class="sxs-lookup"><span data-stu-id="e0e80-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0e80-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e0e80-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0e80-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e0e80-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0e80-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e0e80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0e80-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0e80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0e80-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e0e80-118">Scenario description</span></span>
<span data-ttu-id="e0e80-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e0e80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0e80-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e0e80-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0e80-121">Adicionando Mindflash por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e0e80-121">Adding Mindflash from the gallery</span></span>
2. <span data-ttu-id="e0e80-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-the-gallery"></a><span data-ttu-id="e0e80-123">Adicionando Mindflash por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="e0e80-123">Adding Mindflash from the gallery</span></span>
<span data-ttu-id="e0e80-124">Para configurar a integração do Mindflash ao Azure AD, você precisará adicionar o Mindflash da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e0e80-124">To configure the integration of Mindflash into Azure AD, you need to add Mindflash from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0e80-125">**Para adicionar o Mindflash por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0e80-125">**To add Mindflash from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0e80-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0e80-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0e80-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e0e80-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e0e80-133">Na caixa de pesquisa, digite **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-133">In the search box, type **Mindflash**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="e0e80-135">No painel de resultados, selecione **Mindflash** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-135">In the results panel, select **Mindflash**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0e80-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0e80-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Mindflash, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e0e80-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0e80-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Mindflash é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0e80-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mindflash is to a user in Azure AD.</span></span> <span data-ttu-id="e0e80-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Mindflash.</span><span class="sxs-lookup"><span data-stu-id="e0e80-140">In other words, a link relationship between an Azure AD user and the related user in Mindflash needs to be established.</span></span>

<span data-ttu-id="e0e80-141">No Mindflash, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-141">In Mindflash, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0e80-142">Para configurar e testar o logon único do Azure AD com o Mindflash, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e0e80-142">To configure and test Azure AD single sign-on with Mindflash, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0e80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e0e80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0e80-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0e80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0e80-145">**[Criação de um usuário de teste do Mindflash](#creating-a-mindflash-test-user)**: para ter um equivalente de Brenda Fernandes no Mindflash que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0e80-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - to have a counterpart of Britta Simon in Mindflash that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0e80-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e80-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0e80-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e0e80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0e80-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0e80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0e80-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Mindflash.</span><span class="sxs-lookup"><span data-stu-id="e0e80-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="e0e80-150">**Para configurar o logon único do Azure AD com o Mindflash, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0e80-150">**To configure Azure AD single sign-on with Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="e0e80-151">No Portal do Azure, na página de integração de aplicativos do **Mindflash**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-151">In the Azure portal, on the **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e0e80-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e0e80-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="e0e80-155">Na seção **Domínio e URLs do Mindflash**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0e80-155">On the **Mindflash Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="e0e80-157">a.</span><span class="sxs-lookup"><span data-stu-id="e0e80-157">a.</span></span> <span data-ttu-id="e0e80-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="e0e80-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="e0e80-159">b.</span><span class="sxs-lookup"><span data-stu-id="e0e80-159">b.</span></span> <span data-ttu-id="e0e80-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="e0e80-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e0e80-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e0e80-161">These values are not real.</span></span> <span data-ttu-id="e0e80-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="e0e80-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e0e80-163">Contate a [equipe de suporte do Cliente Mindflash](https://www.mindflash.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e0e80-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="e0e80-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e0e80-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="e0e80-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e0e80-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0e80-168">Para configurar o logon único no lado do **Mindflash**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e0e80-168">To configure single sign-on on **Mindflash** side, you need to send the downloaded **Metadata XML** to [Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="e0e80-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e0e80-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0e80-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e0e80-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0e80-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e0e80-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0e80-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0e80-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0e80-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e0e80-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0e80-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0e80-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0e80-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e0e80-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0e80-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0e80-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0e80-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0e80-184">a.</span><span class="sxs-lookup"><span data-stu-id="e0e80-184">a.</span></span> <span data-ttu-id="e0e80-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0e80-186">b.</span><span class="sxs-lookup"><span data-stu-id="e0e80-186">b.</span></span> <span data-ttu-id="e0e80-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0e80-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0e80-188">c.</span><span class="sxs-lookup"><span data-stu-id="e0e80-188">c.</span></span> <span data-ttu-id="e0e80-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0e80-190">d.</span><span class="sxs-lookup"><span data-stu-id="e0e80-190">d.</span></span> <span data-ttu-id="e0e80-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="e0e80-192">Criação de um usuário de teste do Mindflash</span><span class="sxs-lookup"><span data-stu-id="e0e80-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="e0e80-193">Para permitir que os usuários do AD do Azure façam logon no Mindflash, eles devem ser provisionados no Mindflash.</span><span class="sxs-lookup"><span data-stu-id="e0e80-193">In order to enable Azure AD users to log into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="e0e80-194">No caso do Mindflash, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="e0e80-194">In the case of Mindflash, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="e0e80-195">Para provisionar contas de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0e80-195">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="e0e80-196">Faça logon em seu site de empresa do **Mindflash** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e0e80-196">Log in to your **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="e0e80-197">Vá para **Gerenciar Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-197">Go to **Manage Users**.</span></span>
   
    <span data-ttu-id="e0e80-198">![Gerenciar Usuários](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="e0e80-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="e0e80-199">Clique em **Adicionar Usuários** e, em seguida, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-199">Click the **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="e0e80-200">Na seção **Adicionar Novos Usuários**, execute as seguintes etapas de uma conta do Azure AD válida que deseja provisionar:</span><span class="sxs-lookup"><span data-stu-id="e0e80-200">In the **Add New Users** section, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="e0e80-201">![Adicionar Novos Usuários](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Adicionar Novos Usuários")</span><span class="sxs-lookup"><span data-stu-id="e0e80-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="e0e80-202">a.</span><span class="sxs-lookup"><span data-stu-id="e0e80-202">a.</span></span> <span data-ttu-id="e0e80-203">Na caixa de texto **Nome**, digite o **Nome** do usuário como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-203">In the **First name** textbox, type **First name** of the user as **Britta**.</span></span>

    <span data-ttu-id="e0e80-204">b.</span><span class="sxs-lookup"><span data-stu-id="e0e80-204">b.</span></span> <span data-ttu-id="e0e80-205">Na caixa de texto **Sobrenome**, digite o **Sobrenome** do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-205">In the **Last name** textbox, type **Last name** of the user as **Simon**.</span></span>
    
    <span data-ttu-id="e0e80-206">c.</span><span class="sxs-lookup"><span data-stu-id="e0e80-206">c.</span></span> <span data-ttu-id="e0e80-207">Na caixa de texto **Email**, digite o **Endereço de Email** do usuário como **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-207">In the **Email** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="e0e80-208">b.</span><span class="sxs-lookup"><span data-stu-id="e0e80-208">b.</span></span> <span data-ttu-id="e0e80-209">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="e0e80-210">É possível usar qualquer outra ferramenta de criação da conta de usuário do Mindflash ou as APIs fornecidas pelo Mindflash para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="e0e80-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0e80-211">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0e80-212">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao garantir acesso ao Fuse.</span><span class="sxs-lookup"><span data-stu-id="e0e80-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mindflash.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e0e80-214">**Para atribuir Brenda Fernandes ao Mindflash, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0e80-214">**To assign Britta Simon to Mindflash, perform the following steps:**</span></span>

1. <span data-ttu-id="e0e80-215">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e0e80-217">Na lista de aplicativos, selecione **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-217">In the applications list, select **Mindflash**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="e0e80-219">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e0e80-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e0e80-221">Click **Add** button.</span></span> <span data-ttu-id="e0e80-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e0e80-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e0e80-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0e80-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0e80-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0e80-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0e80-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e0e80-227">Testing single sign-on</span></span>

<span data-ttu-id="e0e80-228">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e0e80-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0e80-229">Ao clicar no bloco Mindflash no Painel de Acesso, você deverá acessar a página de logon do aplicativo Mindflash.</span><span class="sxs-lookup"><span data-stu-id="e0e80-229">When you click the Mindflash tile in the Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="e0e80-230">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e0e80-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0e80-231">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e0e80-231">Additional resources</span></span>

* [<span data-ttu-id="e0e80-232">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e0e80-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0e80-233">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0e80-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

