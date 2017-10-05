---
title: "Tutorial: Integração do Azure Active Directory com o Convercent | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="4d1d5-103">Tutorial: Integração do Azure Active Directory ao Convercent</span><span class="sxs-lookup"><span data-stu-id="4d1d5-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="4d1d5-104">Neste tutorial, você aprenderá a integrar o Convercent ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4d1d5-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4d1d5-105">A integração do Convercent ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4d1d5-106">No Azure AD, é possível controlar quem tem acesso ao Convercent</span><span class="sxs-lookup"><span data-stu-id="4d1d5-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="4d1d5-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Convercent (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d5-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4d1d5-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4d1d5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d1d5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4d1d5-110">Prerequisites</span></span>

<span data-ttu-id="4d1d5-111">Para configurar a integração do Azure AD ao Convercent, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="4d1d5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4d1d5-113">Uma assinatura habilitada para logon único do Convercent</span><span class="sxs-lookup"><span data-stu-id="4d1d5-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4d1d5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4d1d5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4d1d5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4d1d5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4d1d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4d1d5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4d1d5-118">Scenario description</span></span>
<span data-ttu-id="4d1d5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4d1d5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4d1d5-121">Adicionando Convercent da galeria</span><span class="sxs-lookup"><span data-stu-id="4d1d5-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="4d1d5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="4d1d5-123">Adicionando Convercent da galeria</span><span class="sxs-lookup"><span data-stu-id="4d1d5-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="4d1d5-124">Para configurar a integração do Convercent ao Azure AD, você precisará adicionar o Convercent à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4d1d5-125">**Para adicionar o Condeco da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4d1d5-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4d1d5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4d1d5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4d1d5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4d1d5-133">Na caixa de pesquisa, digite **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-133">In the search box, type **Convercent**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="4d1d5-135">No painel de resultados, selecione **Convercent** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4d1d5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4d1d5-138">Nesta seção, você configura e testa o logon único do Azure AD com o Convercent com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4d1d5-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4d1d5-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Convercent é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="4d1d5-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="4d1d5-141">Essa relação de vinculação é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="4d1d5-142">Para configurar e testar o logon único do Azure AD com o Convercent, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4d1d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4d1d5-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4d1d5-145">**[Como criar um usuário de teste do Convercent](#creating-a-convercent-test-user)** – para ter um equivalente de Brenda Fernandes no Convercent que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4d1d5-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4d1d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4d1d5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d1d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4d1d5-149">Nesta seção, você habilita o logon único do Azure AD no novo portal do Azure e configura o logon único em seu aplicativo Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="4d1d5-150">**Para configurar o logon único do Azure AD com o Convercent, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4d1d5-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d5-151">No portal do Azure, na página de integração de aplicativos do **Convercent**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4d1d5-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="4d1d5-155">Na seção **Domínio e URLs do Convercent**, se você quiser configurar o aplicativo em **Modo iniciado pelo IDP**, execute a seguinte etapa:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="4d1d5-157">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4d1d5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="4d1d5-158">Se você quiser configurar o aplicativo em **Modo iniciado pelo SP**, na seção **Domínio e URLs do Convercent**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="4d1d5-160">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-160">a.</span></span> <span data-ttu-id="4d1d5-161">Clique em **"Mostrar configurações de URL avançadas"**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="4d1d5-162">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-162">b.</span></span> <span data-ttu-id="4d1d5-163">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4d1d5-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="4d1d5-164">c.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-164">c.</span></span> <span data-ttu-id="4d1d5-165">Na caixa de texto **Estado de Retransmissão**, digite um valor usando o seguinte padrão: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4d1d5-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d1d5-166">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-166">These values are not the real values.</span></span> <span data-ttu-id="4d1d5-167">Atualize esses valores com o Identificador, a URL de Logon e o Estado de Retransmissão reais.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="4d1d5-168">Contate a [equipe de suporte ao Cliente do Convercent](http://support.convercent.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="4d1d5-169">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="4d1d5-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4d1d5-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4d1d5-173">Para que o SSO seja configurado para seu aplicativo, entre em contato com a [equipe de suporte do Convercent](mailto:support@convercent.com) e forneça o **XML de metadados** baixado.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="4d1d5-174">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4d1d5-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4d1d5-175">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4d1d5-176">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4d1d5-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4d1d5-177">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="4d1d5-178">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4d1d5-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4d1d5-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d5-181">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4d1d5-183">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4d1d5-185">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4d1d5-187">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4d1d5-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4d1d5-189">a.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-189">a.</span></span> <span data-ttu-id="4d1d5-190">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4d1d5-191">b.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-191">b.</span></span> <span data-ttu-id="4d1d5-192">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4d1d5-193">c.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-193">c.</span></span> <span data-ttu-id="4d1d5-194">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4d1d5-195">d.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-195">d.</span></span> <span data-ttu-id="4d1d5-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="4d1d5-197">Criando um usuário de teste do Convercent</span><span class="sxs-lookup"><span data-stu-id="4d1d5-197">Creating a Convercent test user</span></span>

<span data-ttu-id="4d1d5-198">Trabalhe com a [equipe de suporte do Convercent](mailto:support@convercent.com) para adicionar usuários na plataforma do Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4d1d5-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4d1d5-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4d1d5-202">**Para atribuir Brenda Fernandes ao Convercent, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4d1d5-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="4d1d5-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4d1d5-205">Na lista de aplicativos, selecione **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-205">In the applications list, select **Convercent**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="4d1d5-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4d1d5-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-209">Click **Add** button.</span></span> <span data-ttu-id="4d1d5-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4d1d5-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4d1d5-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4d1d5-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4d1d5-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4d1d5-215">Testing single sign-on</span></span>

<span data-ttu-id="4d1d5-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4d1d5-217">Quando você clica no bloco Convercent no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do Convercent.</span><span class="sxs-lookup"><span data-stu-id="4d1d5-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="4d1d5-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4d1d5-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4d1d5-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4d1d5-219">Additional resources</span></span>

* [<span data-ttu-id="4d1d5-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4d1d5-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4d1d5-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d1d5-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

