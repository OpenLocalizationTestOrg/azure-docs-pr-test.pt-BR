---
title: "Tutorial: Integração do Azure Active Directory com o Printix | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="28ac7-103">Tutorial: integração do Azure Active Directory com o Printix</span><span class="sxs-lookup"><span data-stu-id="28ac7-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="28ac7-104">Neste tutorial, você aprenderá a integrar o Printix ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="28ac7-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28ac7-105">A integração do Printix com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="28ac7-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="28ac7-106">Você pode controlar no Azure AD quem tem acesso ao Printix</span><span class="sxs-lookup"><span data-stu-id="28ac7-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="28ac7-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Printix (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="28ac7-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28ac7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="28ac7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28ac7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28ac7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28ac7-110">Prerequisites</span></span>

<span data-ttu-id="28ac7-111">Para configurar a integração do Azure AD com o Printix, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="28ac7-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="28ac7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28ac7-113">Uma assinatura habilitada para logon único do Printix</span><span class="sxs-lookup"><span data-stu-id="28ac7-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28ac7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="28ac7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28ac7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="28ac7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28ac7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="28ac7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28ac7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28ac7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28ac7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="28ac7-118">Scenario description</span></span>
<span data-ttu-id="28ac7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="28ac7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28ac7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="28ac7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28ac7-121">Adicionando Printix da galeria</span><span class="sxs-lookup"><span data-stu-id="28ac7-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="28ac7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="28ac7-123">Adicionando Printix da galeria</span><span class="sxs-lookup"><span data-stu-id="28ac7-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="28ac7-124">Para configurar a integração do Printix ao Azure AD, você precisa adicionar o Printix por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="28ac7-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="28ac7-125">**Para adicionar o Printix por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="28ac7-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28ac7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="28ac7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="28ac7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="28ac7-133">Na caixa de pesquisa, digite **Printix**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-133">In the search box, type **Printix**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="28ac7-135">No painel de resultados, selecione **Printix** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28ac7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28ac7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Printix, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="28ac7-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="28ac7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Printix é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28ac7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="28ac7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Printix.</span><span class="sxs-lookup"><span data-stu-id="28ac7-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="28ac7-141">No Printix, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="28ac7-142">Para configurar e testar o logon único do Azure AD com o Printix, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="28ac7-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="28ac7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="28ac7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="28ac7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="28ac7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28ac7-145">**[Criação de um usuário de teste do Printix](#creating-a-printix-test-user)** – para ter um equivalente de Brenda Fernandes no Printix que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28ac7-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="28ac7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="28ac7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28ac7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="28ac7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28ac7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="28ac7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28ac7-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo do Printix.</span><span class="sxs-lookup"><span data-stu-id="28ac7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="28ac7-150">**Para configurar o logon único do Azure AD com o Printix, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="28ac7-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac7-151">No Portal do Azure, na página de integração de aplicativos do **Printix**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="28ac7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="28ac7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="28ac7-155">Na seção **URLs e Domínio do Printix**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="28ac7-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="28ac7-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="28ac7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="28ac7-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="28ac7-158">The value is not real.</span></span> <span data-ttu-id="28ac7-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="28ac7-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="28ac7-160">Entre em contato com a [equipe de suporte ao cliente do Printix](mailto:support@printix.net) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="28ac7-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="28ac7-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="28ac7-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="28ac7-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="28ac7-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="28ac7-165">Faça logon no seu locatário do Printix como administrador.</span><span class="sxs-lookup"><span data-stu-id="28ac7-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="28ac7-166">No menu na parte superior, clique no ícone no canto superior direito e selecione "**Autenticação**".</span><span class="sxs-lookup"><span data-stu-id="28ac7-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="28ac7-168">Na guia **Instalação**, selecione **Habilitar autenticação do Azure/Office 365**</span><span class="sxs-lookup"><span data-stu-id="28ac7-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="28ac7-170">Na guia **Azure**, insira a URL de metadados de federação para a caixa de texto de “**Documento de metadados federados**”.</span><span class="sxs-lookup"><span data-stu-id="28ac7-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="28ac7-171">Anexe o arquivo XML de metadados baixado do Azure AD para a [equipe de suporte do Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="28ac7-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="28ac7-172">Em seguida, eles carregam o arquivo XML e fornecem uma URL de metadados de federação.</span><span class="sxs-lookup"><span data-stu-id="28ac7-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="28ac7-174">Clique no botão “**Testar**” e em “**OK**” se o teste foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="28ac7-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="28ac7-175">A página do Azure Active Directory será exibida depois que o botão **Testar** receber um clique.</span><span class="sxs-lookup"><span data-stu-id="28ac7-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="28ac7-176">Aqui, “Teste bem-sucedido” significa que, depois de inserir as credenciais de sua conta de teste do Azure, uma mensagem pop-up “Configurações testadas com êxito” será exibida. Em seguida, clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="28ac7-178">Clique no botão **Salvar** na página “**Autenticação**”.</span><span class="sxs-lookup"><span data-stu-id="28ac7-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="28ac7-179">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="28ac7-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="28ac7-180">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="28ac7-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="28ac7-181">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28ac7-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28ac7-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="28ac7-183">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="28ac7-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="28ac7-185">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="28ac7-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac7-186">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28ac7-188">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="28ac7-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28ac7-190">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28ac7-192">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="28ac7-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28ac7-194">a.</span><span class="sxs-lookup"><span data-stu-id="28ac7-194">a.</span></span> <span data-ttu-id="28ac7-195">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28ac7-196">b.</span><span class="sxs-lookup"><span data-stu-id="28ac7-196">b.</span></span> <span data-ttu-id="28ac7-197">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="28ac7-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28ac7-198">c.</span><span class="sxs-lookup"><span data-stu-id="28ac7-198">c.</span></span> <span data-ttu-id="28ac7-199">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="28ac7-200">d.</span><span class="sxs-lookup"><span data-stu-id="28ac7-200">d.</span></span> <span data-ttu-id="28ac7-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="28ac7-202">Criação de um usuário de teste do Printix</span><span class="sxs-lookup"><span data-stu-id="28ac7-202">Creating a Printix test user</span></span>

<span data-ttu-id="28ac7-203">O objetivo desta seção é criar uma usuária chamada Brenda Fernandes no Printix.</span><span class="sxs-lookup"><span data-stu-id="28ac7-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="28ac7-204">O Printix dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="28ac7-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="28ac7-205">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="28ac7-205">There is no action item for you in this section.</span></span> <span data-ttu-id="28ac7-206">Um novo usuário é criado durante uma tentativa de acessar o Printix, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="28ac7-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="28ac7-207">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="28ac7-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="28ac7-208">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="28ac7-209">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Printix.</span><span class="sxs-lookup"><span data-stu-id="28ac7-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="28ac7-211">**Para atribuir Brenda Fernandes ao Printix, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="28ac7-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="28ac7-212">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="28ac7-214">Na lista de aplicativos, selecione **Printix**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-214">In the applications list, select **Printix**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="28ac7-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="28ac7-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28ac7-218">Click **Add** button.</span></span> <span data-ttu-id="28ac7-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="28ac7-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="28ac7-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="28ac7-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28ac7-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28ac7-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28ac7-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="28ac7-224">Testing single sign-on</span></span>

<span data-ttu-id="28ac7-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="28ac7-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="28ac7-226">Quando você clica no bloco Printix no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo Printix.</span><span class="sxs-lookup"><span data-stu-id="28ac7-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28ac7-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="28ac7-227">Additional resources</span></span>

* [<span data-ttu-id="28ac7-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="28ac7-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28ac7-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28ac7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

