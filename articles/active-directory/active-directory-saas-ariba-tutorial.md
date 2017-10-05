---
title: "Tutorial: integração do Azure Active Directory ao Ariba | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="3104d-103">Tutorial: Integração do Active Directory do Azure ao Ariba</span><span class="sxs-lookup"><span data-stu-id="3104d-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="3104d-104">Neste tutorial, você aprende a integrar o Ariba ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3104d-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3104d-105">A integração do Ariba ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3104d-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3104d-106">Você pode controlar no AD do Azure quem terá acesso ao Ariba</span><span class="sxs-lookup"><span data-stu-id="3104d-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="3104d-107">Você pode permitir que seus usuários faça logon automaticamente no Ariba (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3104d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3104d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3104d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3104d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3104d-110">Prerequisites</span></span>

<span data-ttu-id="3104d-111">Para configurar a integração do AD do Azure ao Ariba, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3104d-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="3104d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3104d-113">Uma assinatura habilitada para logon único do Ariba</span><span class="sxs-lookup"><span data-stu-id="3104d-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3104d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3104d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3104d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3104d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3104d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3104d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3104d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3104d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3104d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3104d-118">Scenario description</span></span>
<span data-ttu-id="3104d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3104d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3104d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3104d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3104d-121">Adicionando o Ariba da galeria</span><span class="sxs-lookup"><span data-stu-id="3104d-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="3104d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="3104d-123">Adicionando o Ariba da galeria</span><span class="sxs-lookup"><span data-stu-id="3104d-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="3104d-124">Para configurar a integração do Ariba ao AD do Azure, você precisará adicionar o Ariba da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3104d-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3104d-125">**Para adicionar o Ariba da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3104d-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3104d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3104d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3104d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3104d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3104d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3104d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3104d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3104d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3104d-133">Na caixa de pesquisa, digite **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="3104d-133">In the search box, type **Ariba**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="3104d-135">No painel de resultados, selecione **Ariba** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3104d-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3104d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3104d-138">Nesta seção, você configura e testa o logon único do Azure AD com o Ariba, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3104d-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3104d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Ariba é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3104d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="3104d-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="3104d-141">No Ariba, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3104d-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3104d-142">Para configurar e testar o logon único do AD do Azure com o Ariba, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3104d-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3104d-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3104d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3104d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3104d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3104d-145">**[Criando um usuário de teste do Ariba](#creating-an-ariba-test-user)** – para ter um equivalente de Brenda Fernandes no Ariba que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3104d-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3104d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3104d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3104d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3104d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3104d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3104d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3104d-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="3104d-150">**Para configurar o logon único do AD do Azure com o Ariba, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3104d-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="3104d-151">No portal do Azure, na página de integração do aplicativo do **Ariba**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3104d-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3104d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3104d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="3104d-155">Na seção **Domínio e URLs do Ariba**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3104d-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="3104d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3104d-157">a.</span></span> <span data-ttu-id="3104d-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.sourcing.ariba.com` ou `https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="3104d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="3104d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3104d-159">b.</span></span> <span data-ttu-id="3104d-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="3104d-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3104d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3104d-161">These values are not real.</span></span> <span data-ttu-id="3104d-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="3104d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3104d-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="3104d-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="3104d-164">Contate a equipe de suporte ao Cliente do Ariba pelo telefone **1-866-218-2155** para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="3104d-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="3104d-165">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="3104d-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="3104d-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3104d-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3104d-169">Para obter o SSO configurado para o aplicativo, ligue para a equipe de suporte do Ariba no número **1-866-218-2155** e ela o ajudará com informações sobre como fornecer o arquivo de **Certificado (Base64)** baixado.</span><span class="sxs-lookup"><span data-stu-id="3104d-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="3104d-170">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3104d-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3104d-171">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3104d-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3104d-172">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3104d-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3104d-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3104d-174">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3104d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3104d-176">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3104d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3104d-177">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3104d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3104d-179">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3104d-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3104d-181">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3104d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3104d-183">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3104d-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3104d-185">a.</span><span class="sxs-lookup"><span data-stu-id="3104d-185">a.</span></span> <span data-ttu-id="3104d-186">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3104d-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3104d-187">b.</span><span class="sxs-lookup"><span data-stu-id="3104d-187">b.</span></span> <span data-ttu-id="3104d-188">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3104d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3104d-189">c.</span><span class="sxs-lookup"><span data-stu-id="3104d-189">c.</span></span> <span data-ttu-id="3104d-190">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3104d-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3104d-191">d.</span><span class="sxs-lookup"><span data-stu-id="3104d-191">d.</span></span> <span data-ttu-id="3104d-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3104d-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="3104d-193">Criando um usuário de teste do Ariba</span><span class="sxs-lookup"><span data-stu-id="3104d-193">Creating an Ariba test user</span></span>

<span data-ttu-id="3104d-194">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="3104d-195">Trabalhe com a equipe de suporte do Ariba pelo telefone **1-866-218-2155** para adicionar os usuários ao sistema do Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="3104d-196">Se precisar criar um usuário manualmente, será necessário contatar a equipe de suporte do Ariba pelo telefone **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="3104d-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3104d-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3104d-198">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3104d-200">**Para atribuir Brenda Fernandes ao Ariba, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3104d-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="3104d-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3104d-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3104d-203">Na lista de aplicativos, escolha **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="3104d-203">In the applications list, select **Ariba**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="3104d-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3104d-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3104d-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3104d-207">Click **Add** button.</span></span> <span data-ttu-id="3104d-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3104d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3104d-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3104d-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3104d-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3104d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3104d-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3104d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3104d-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3104d-213">Testing single sign-on</span></span>
<span data-ttu-id="3104d-214">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3104d-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3104d-215">Ao clicar no bloco do Ariba no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Ariba.</span><span class="sxs-lookup"><span data-stu-id="3104d-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3104d-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3104d-216">Additional resources</span></span>

* [<span data-ttu-id="3104d-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3104d-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3104d-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3104d-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

