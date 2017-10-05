---
title: "Tutorial: Integração do Azure Active Directory com o Asset Bank | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Asset Bank."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="97ce8-103">Tutorial: Integração do Azure Active Directory ao Asset Bank</span><span class="sxs-lookup"><span data-stu-id="97ce8-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="97ce8-104">Neste tutorial, você aprende a integrar o Asset Bank ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="97ce8-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97ce8-105">A integração do Asset Bank ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="97ce8-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97ce8-106">É possível controlar no Azure AD quem terá acesso ao Asset Bank</span><span class="sxs-lookup"><span data-stu-id="97ce8-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="97ce8-107">Você pode permitir que os usuários façam logon automaticamente no Asset Bank (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="97ce8-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97ce8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="97ce8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97ce8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97ce8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97ce8-110">Prerequisites</span></span>

<span data-ttu-id="97ce8-111">Para configurar a integração do Azure AD com o Asset Bank, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="97ce8-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="97ce8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97ce8-113">Uma assinatura habilitada para logon único do Asset Bank</span><span class="sxs-lookup"><span data-stu-id="97ce8-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97ce8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="97ce8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97ce8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="97ce8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97ce8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="97ce8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97ce8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97ce8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97ce8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="97ce8-118">Scenario description</span></span>
<span data-ttu-id="97ce8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="97ce8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97ce8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="97ce8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97ce8-121">Adicionando o Asset Bank por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="97ce8-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="97ce8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="97ce8-123">Adicionando o Asset Bank por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="97ce8-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="97ce8-124">Para configurar a integração do Asset Bank ao Azure AD, você precisa adicionar o Asset Bank por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="97ce8-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97ce8-125">**Para adicionar o Asset Bank por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="97ce8-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97ce8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97ce8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97ce8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="97ce8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="97ce8-133">Na caixa de pesquisa, digite **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-133">In the search box, type **Asset Bank**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="97ce8-135">No painel de resultados, selecione **Asset Bank** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97ce8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97ce8-138">Nesta seção, você configura e testa o logon único do Azure AD com o Asset Bank, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="97ce8-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97ce8-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Asset Bank é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97ce8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="97ce8-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="97ce8-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="97ce8-141">No Asset Bank, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="97ce8-142">Para configurar e testar o logon único do Azure AD com o Asset Bank, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="97ce8-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97ce8-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="97ce8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97ce8-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="97ce8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97ce8-145">**[Criando um usuário de teste do Asset Bank](#creating-an-asset-bank-test-user)** – para ter um equivalente de Brenda Fernandes no Asset Bank que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97ce8-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="97ce8-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="97ce8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97ce8-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="97ce8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97ce8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="97ce8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97ce8-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="97ce8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="97ce8-150">**Para configurar o logon único do Azure AD com o Asset Bank, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="97ce8-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="97ce8-151">No portal do Azure, na página de integração do aplicativo do **Asset Bank**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="97ce8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="97ce8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="97ce8-155">Na seção **Domínio e URLs do Asset Bank**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="97ce8-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="97ce8-157">a.</span><span class="sxs-lookup"><span data-stu-id="97ce8-157">a.</span></span> <span data-ttu-id="97ce8-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="97ce8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="97ce8-159">b.</span><span class="sxs-lookup"><span data-stu-id="97ce8-159">b.</span></span> <span data-ttu-id="97ce8-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="97ce8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97ce8-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="97ce8-161">These values are not real.</span></span> <span data-ttu-id="97ce8-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="97ce8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="97ce8-163">Contate a [equipe de suporte ao Cliente do Asset Bank](mailto:support@assetbank.co.uk) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="97ce8-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="97ce8-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="97ce8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="97ce8-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="97ce8-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97ce8-168">Para configurar o logon único no lado do **Asset Bank**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="97ce8-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="97ce8-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="97ce8-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="97ce8-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="97ce8-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="97ce8-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97ce8-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97ce8-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="97ce8-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="97ce8-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="97ce8-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="97ce8-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97ce8-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97ce8-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="97ce8-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97ce8-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97ce8-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="97ce8-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97ce8-184">a.</span><span class="sxs-lookup"><span data-stu-id="97ce8-184">a.</span></span> <span data-ttu-id="97ce8-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97ce8-186">b.</span><span class="sxs-lookup"><span data-stu-id="97ce8-186">b.</span></span> <span data-ttu-id="97ce8-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="97ce8-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97ce8-188">c.</span><span class="sxs-lookup"><span data-stu-id="97ce8-188">c.</span></span> <span data-ttu-id="97ce8-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97ce8-190">d.</span><span class="sxs-lookup"><span data-stu-id="97ce8-190">d.</span></span> <span data-ttu-id="97ce8-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="97ce8-192">Criando um usuário de teste do Asset Bank</span><span class="sxs-lookup"><span data-stu-id="97ce8-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="97ce8-193">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="97ce8-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="97ce8-194">O Asset Bank dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="97ce8-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="97ce8-195">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="97ce8-195">There is no action item for you in this section.</span></span> <span data-ttu-id="97ce8-196">Um novo usuário será criado durante uma tentativa de acessar o Asset Bank, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="97ce8-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="97ce8-197">Se precisar criar um usuário manualmente, será necessário contatar a [equipe de suporte do Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="97ce8-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97ce8-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97ce8-199">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="97ce8-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="97ce8-201">**Para atribuir Brenda Fernandes ao Asset Bank, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="97ce8-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="97ce8-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="97ce8-204">Na lista de aplicativos, selecione **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-204">In the applications list, select **Asset Bank**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="97ce8-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="97ce8-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97ce8-208">Click **Add** button.</span></span> <span data-ttu-id="97ce8-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="97ce8-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="97ce8-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97ce8-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97ce8-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97ce8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97ce8-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="97ce8-214">Testing single sign-on</span></span>

<span data-ttu-id="97ce8-215">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="97ce8-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="97ce8-216">Ao clicar no bloco Asset Bank no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo do Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="97ce8-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="97ce8-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="97ce8-217">Additional resources</span></span>

* [<span data-ttu-id="97ce8-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="97ce8-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97ce8-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97ce8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

