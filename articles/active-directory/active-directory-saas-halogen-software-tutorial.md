---
title: "Tutorial: Integração do Azure Active Directory ao Halogen Software | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Halogen Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="32cc6-103">Tutorial: Integração do Active Directory do Azure com o Halogen Software</span><span class="sxs-lookup"><span data-stu-id="32cc6-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="32cc6-104">Neste tutorial, você aprenderá a integrar o Halogen Software ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="32cc6-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32cc6-105">A integração do Halogen Software ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="32cc6-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32cc6-106">Você pode controlar, no Azure AD, quem tem acesso ao Halogen Software</span><span class="sxs-lookup"><span data-stu-id="32cc6-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="32cc6-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Halogen Software (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32cc6-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32cc6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32cc6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32cc6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32cc6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32cc6-110">Prerequisites</span></span>

<span data-ttu-id="32cc6-111">Para configurar a integração do Azure AD com o Halogen Software, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="32cc6-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="32cc6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32cc6-113">Uma assinatura do Halogen Software com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="32cc6-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32cc6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="32cc6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32cc6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="32cc6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32cc6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="32cc6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32cc6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32cc6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32cc6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="32cc6-118">Scenario description</span></span>

<span data-ttu-id="32cc6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="32cc6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32cc6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="32cc6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32cc6-121">Adicionar o Halogen Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="32cc6-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="32cc6-122">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32cc6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="32cc6-123">Adicionar o Halogen Software por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="32cc6-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="32cc6-124">Para configurar a integração do Halogen Software com o Azure AD, você precisa adicionar o Halogen Software, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="32cc6-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32cc6-125">**Para adicionar o Halogen Software por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="32cc6-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32cc6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32cc6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32cc6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="32cc6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="32cc6-133">Na caixa de pesquisa, digite **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-133">In the search box, type **Halogen Software**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="32cc6-135">No painel de resultados, selecione **Halogen Software** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32cc6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32cc6-138">Nesta seção, você configura e testa o logon único do Azure AD com o Halogen Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="32cc6-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32cc6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Halogen Software é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32cc6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="32cc6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="32cc6-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="32cc6-141">No Halogen Software, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32cc6-142">Para configurar e testar o logon único do Azure AD com o Halogen Software, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="32cc6-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32cc6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="32cc6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32cc6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="32cc6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32cc6-145">**[Como criar de um usuário de teste do Halogen Software](#creating-a-halogen-software-test-user)** – para ter um equivalente de Brenda Fernandes no Halogen Software que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32cc6-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32cc6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="32cc6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32cc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="32cc6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32cc6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32cc6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32cc6-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo do Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="32cc6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="32cc6-150">**Para configurar o logon único do Azure AD com o Halogen Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="32cc6-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32cc6-151">No portal do Azure, na página de integração de aplicativos do **Halogen Software**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="32cc6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="32cc6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="32cc6-155">Na seção **URLs e Domínio do Halogen Software**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="32cc6-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="32cc6-157">a.</span><span class="sxs-lookup"><span data-stu-id="32cc6-157">a.</span></span> <span data-ttu-id="32cc6-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="32cc6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="32cc6-159">b.</span><span class="sxs-lookup"><span data-stu-id="32cc6-159">b.</span></span> <span data-ttu-id="32cc6-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:`https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="32cc6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32cc6-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="32cc6-161">These values are not real.</span></span> <span data-ttu-id="32cc6-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="32cc6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32cc6-163">Entre em contato com a [equipe de suporte ao Cliente do Halogen Software](https://support.halogensoftware.com/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="32cc6-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="32cc6-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="32cc6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="32cc6-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="32cc6-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32cc6-168">Em uma janela diferente do navegador, faça logon no aplicativo **Halogen Software** como administrador.</span><span class="sxs-lookup"><span data-stu-id="32cc6-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="32cc6-169">Clique na guia **Opções** .</span><span class="sxs-lookup"><span data-stu-id="32cc6-169">Click the **Options** tab.</span></span> 
   
    ![O que é o Azure AD Connect][12]

8. <span data-ttu-id="32cc6-171">No painel de navegação esquerdo, clique em **Configuração do SAML**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![O que é o Azure AD Connect][13]

9. <span data-ttu-id="32cc6-173">Na página **Configuração do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="32cc6-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![O que é o Azure AD Connect][14]

     <span data-ttu-id="32cc6-175">a.</span><span class="sxs-lookup"><span data-stu-id="32cc6-175">a.</span></span> <span data-ttu-id="32cc6-176">Como **Identificador exclusivo**, selecione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="32cc6-177">b.</span><span class="sxs-lookup"><span data-stu-id="32cc6-177">b.</span></span> <span data-ttu-id="32cc6-178">Em **Identificador exclusivo mapeia para**, selecione **Nome de usuário**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="32cc6-179">c.</span><span class="sxs-lookup"><span data-stu-id="32cc6-179">c.</span></span> <span data-ttu-id="32cc6-180">Para carregar o arquivo de metadados baixado, clique em **Procurar** para selecionar o arquivo e clique em **Carregar arquivo**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="32cc6-181">d.</span><span class="sxs-lookup"><span data-stu-id="32cc6-181">d.</span></span> <span data-ttu-id="32cc6-182">Para testar a configuração, clique em **Executar Teste**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="32cc6-183">Você precisa esperar pela mensagem "*O teste de SAML foi concluído. Feche esta janela*".</span><span class="sxs-lookup"><span data-stu-id="32cc6-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="32cc6-184">Feche a janela do navegador aberta.</span><span class="sxs-lookup"><span data-stu-id="32cc6-184">Then, close the opened browser window.</span></span> <span data-ttu-id="32cc6-185">A caixa de seleção **Habilitar SAML** só será habilitada se o teste for concluído.</span><span class="sxs-lookup"><span data-stu-id="32cc6-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="32cc6-186">e.</span><span class="sxs-lookup"><span data-stu-id="32cc6-186">e.</span></span> <span data-ttu-id="32cc6-187">Selecione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="32cc6-188">f.</span><span class="sxs-lookup"><span data-stu-id="32cc6-188">f.</span></span> <span data-ttu-id="32cc6-189">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="32cc6-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="32cc6-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32cc6-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="32cc6-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32cc6-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32cc6-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32cc6-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="32cc6-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="32cc6-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="32cc6-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="32cc6-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32cc6-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32cc6-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="32cc6-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32cc6-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32cc6-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="32cc6-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32cc6-205">a.</span><span class="sxs-lookup"><span data-stu-id="32cc6-205">a.</span></span> <span data-ttu-id="32cc6-206">Na caixa de texto **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="32cc6-207">b.</span><span class="sxs-lookup"><span data-stu-id="32cc6-207">b.</span></span> <span data-ttu-id="32cc6-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="32cc6-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32cc6-209">c.</span><span class="sxs-lookup"><span data-stu-id="32cc6-209">c.</span></span> <span data-ttu-id="32cc6-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32cc6-211">d.</span><span class="sxs-lookup"><span data-stu-id="32cc6-211">d.</span></span> <span data-ttu-id="32cc6-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="32cc6-213">Criação de um usuário de teste do Halogen Software</span><span class="sxs-lookup"><span data-stu-id="32cc6-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="32cc6-214">O objetivo desta seção é criar um usuário chamado Britta Simon no Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="32cc6-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="32cc6-215">**Para criar um usuário chamado Britta Simon no Halogen Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="32cc6-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32cc6-216">Faça logon no aplicativo **Halogen Software** como administrador.</span><span class="sxs-lookup"><span data-stu-id="32cc6-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="32cc6-217">Clique na guia **Central do Usuário** e clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![O que é o Azure AD Connect][300]  

3. <span data-ttu-id="32cc6-219">Na página do diálogo **Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="32cc6-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![O que é o Azure AD Connect][301]

    <span data-ttu-id="32cc6-221">a.</span><span class="sxs-lookup"><span data-stu-id="32cc6-221">a.</span></span> <span data-ttu-id="32cc6-222">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="32cc6-223">b.</span><span class="sxs-lookup"><span data-stu-id="32cc6-223">b.</span></span> <span data-ttu-id="32cc6-224">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="32cc6-225">c.</span><span class="sxs-lookup"><span data-stu-id="32cc6-225">c.</span></span> <span data-ttu-id="32cc6-226">Na caixa de texto **Nome de Usuário**, digite **Brenda Fernandes**, o nome de usuário como no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32cc6-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="32cc6-227">d.</span><span class="sxs-lookup"><span data-stu-id="32cc6-227">d.</span></span> <span data-ttu-id="32cc6-228">Na caixa de texto **Senha** , digite uma senha para Britta.</span><span class="sxs-lookup"><span data-stu-id="32cc6-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="32cc6-229">e.</span><span class="sxs-lookup"><span data-stu-id="32cc6-229">e.</span></span> <span data-ttu-id="32cc6-230">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32cc6-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32cc6-232">Nesta seção, você habilita Brenda Fernandes a usar o logon único do Azure concedendo acesso ao Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="32cc6-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="32cc6-234">**Para atribuir Britta Simon ao Halogen Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="32cc6-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32cc6-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="32cc6-237">Na lista de aplicativos, selecione **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-237">In the applications list, select **Halogen Software**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="32cc6-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="32cc6-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="32cc6-241">Click **Add** button.</span></span> <span data-ttu-id="32cc6-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="32cc6-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="32cc6-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32cc6-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32cc6-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32cc6-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32cc6-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="32cc6-247">Testing single sign-on</span></span>

<span data-ttu-id="32cc6-248">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="32cc6-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="32cc6-249">Quando clica no bloco Halogen Software no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="32cc6-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32cc6-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="32cc6-250">Additional resources</span></span>

* [<span data-ttu-id="32cc6-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="32cc6-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32cc6-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32cc6-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
