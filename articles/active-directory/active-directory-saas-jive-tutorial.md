---
title: "Tutorial: Integração do Azure Active Directory com o Jive | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="c7858-103">Tutorial: Integração do Active Directory do Azure com o Jive</span><span class="sxs-lookup"><span data-stu-id="c7858-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="c7858-104">Neste tutorial, você aprenderá a integrar o Jive ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c7858-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7858-105">A integração do Jive ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c7858-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7858-106">No Azure AD, é possível controlar quem tem acesso ao Jive</span><span class="sxs-lookup"><span data-stu-id="c7858-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="c7858-107">Você pode permitir que seus usuários faça logon automaticamente no Jive (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7858-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7858-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7858-109">Caso deseje obter mais informações sobre a integração de aplicativos SaaS ao Azure AD, consulte [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7858-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7858-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7858-110">Prerequisites</span></span>

<span data-ttu-id="c7858-111">Para configurar a integração do Azure AD com o Jive, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c7858-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="c7858-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7858-113">Uma assinatura habilitada para logon único do Jive</span><span class="sxs-lookup"><span data-stu-id="c7858-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7858-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7858-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7858-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7858-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7858-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7858-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7858-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7858-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7858-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7858-118">Scenario description</span></span>
<span data-ttu-id="c7858-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7858-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7858-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c7858-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7858-121">Adicionar Fuse da galeria</span><span class="sxs-lookup"><span data-stu-id="c7858-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="c7858-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="c7858-123">Adicionar Fuse da galeria</span><span class="sxs-lookup"><span data-stu-id="c7858-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="c7858-124">Para configurar a integração do Jive com o Azure AD, você precisará adicionar o Jive à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="c7858-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7858-125">**Para adicionar o Jive por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7858-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7858-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7858-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7858-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7858-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7858-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7858-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7858-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7858-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7858-133">Na caixa de pesquisa, digite **Jive**.</span><span class="sxs-lookup"><span data-stu-id="c7858-133">In the search box, type **Jive**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="c7858-135">No painel de resultados, selecione **Jive** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c7858-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7858-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7858-138">Nesta seção, você configura e testa o logon único do Azure AD com o Jive, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7858-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7858-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jive é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7858-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="c7858-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="c7858-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="c7858-142">Para configurar e testar o logon único do Azure AD com o Jive, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c7858-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7858-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7858-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7858-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7858-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7858-145">**[Criação de um usuário de teste do Jive](#creating-a-jive-test-user)** – para ter um equivalente de Brenda Fernandes no Jive que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7858-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7858-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7858-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7858-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c7858-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7858-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7858-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7858-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="c7858-150">**Para configurar o logon único do Azure AD com o Jive, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7858-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="c7858-151">No portal do Azure, na página de integração do aplicativo **Jive**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7858-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7858-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c7858-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="c7858-155">Na seção **Domínio e URLs do Jive**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7858-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="c7858-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7858-157">a.</span></span> <span data-ttu-id="c7858-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="c7858-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="c7858-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7858-159">b.</span></span> <span data-ttu-id="c7858-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="c7858-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7858-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="c7858-161">These values are not the real.</span></span> <span data-ttu-id="c7858-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="c7858-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="c7858-163">Contate a [equipe de suporte ao Cliente do Jive](https://www.jivesoftware.com/services-support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c7858-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="c7858-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7858-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="c7858-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7858-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7858-168">Para configurar o logon único no lado do **Jive**, faça logon em seu locatário do Jive como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7858-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="c7858-169">No menu na parte superior, clique em “**SAML**”.</span><span class="sxs-lookup"><span data-stu-id="c7858-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="c7858-171">a.</span><span class="sxs-lookup"><span data-stu-id="c7858-171">a.</span></span> <span data-ttu-id="c7858-172">Selecione **Habilitado** na guia **Geral**.</span><span class="sxs-lookup"><span data-stu-id="c7858-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="c7858-173">b.</span><span class="sxs-lookup"><span data-stu-id="c7858-173">b.</span></span> <span data-ttu-id="c7858-174">Clique no botão "**Salvar todas as configurações de saml**".</span><span class="sxs-lookup"><span data-stu-id="c7858-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="c7858-175">Navegue até a guia "**Metadados Idp**".</span><span class="sxs-lookup"><span data-stu-id="c7858-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="c7858-177">a.</span><span class="sxs-lookup"><span data-stu-id="c7858-177">a.</span></span> <span data-ttu-id="c7858-178">Copie o conteúdo do arquivo XML de metadados baixado e cole-o na caixa de texto **Metadados do IDP (Provedor de Identidade)** .</span><span class="sxs-lookup"><span data-stu-id="c7858-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="c7858-179">b.</span><span class="sxs-lookup"><span data-stu-id="c7858-179">b.</span></span> <span data-ttu-id="c7858-180">Clique no botão "**Salvar todas as configurações de saml**".</span><span class="sxs-lookup"><span data-stu-id="c7858-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="c7858-181">Vá até a guia "**Mapeamento de Atributo de Usuário**".</span><span class="sxs-lookup"><span data-stu-id="c7858-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="c7858-183">a.</span><span class="sxs-lookup"><span data-stu-id="c7858-183">a.</span></span> <span data-ttu-id="c7858-184">Na caixa de texto **Email**, copie e cole o nome de atributo do valor **email**.</span><span class="sxs-lookup"><span data-stu-id="c7858-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="c7858-185">b.</span><span class="sxs-lookup"><span data-stu-id="c7858-185">b.</span></span> <span data-ttu-id="c7858-186">Na caixa de texto **Nome**, copie e cole o nome do atributo do valor **nome**.</span><span class="sxs-lookup"><span data-stu-id="c7858-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="c7858-187">c.</span><span class="sxs-lookup"><span data-stu-id="c7858-187">c.</span></span> <span data-ttu-id="c7858-188">Na caixa de texto **Sobrenome**, copie e cole o nome do atributo do valor **sobrenome**.</span><span class="sxs-lookup"><span data-stu-id="c7858-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="c7858-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c7858-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7858-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c7858-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7858-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7858-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7858-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7858-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7858-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7858-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7858-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7858-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7858-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7858-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c7858-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7858-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7858-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7858-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c7858-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7858-204">a.</span><span class="sxs-lookup"><span data-stu-id="c7858-204">a.</span></span> <span data-ttu-id="c7858-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c7858-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7858-206">b.</span><span class="sxs-lookup"><span data-stu-id="c7858-206">b.</span></span> <span data-ttu-id="c7858-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c7858-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7858-208">c.</span><span class="sxs-lookup"><span data-stu-id="c7858-208">c.</span></span> <span data-ttu-id="c7858-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7858-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7858-210">d.</span><span class="sxs-lookup"><span data-stu-id="c7858-210">d.</span></span> <span data-ttu-id="c7858-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7858-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="c7858-212">Criar um usuário de teste Jive</span><span class="sxs-lookup"><span data-stu-id="c7858-212">Creating a Jive test user</span></span>

<span data-ttu-id="c7858-213">Trabalhe com a [equipe de suporte ao Cliente do Jive](https://www.jivesoftware.com/services-support/) para adicionar os usuários à plataforma Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7858-214">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7858-215">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7858-217">**Para atribuir Brenda Fernandes ao Jive, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c7858-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="c7858-218">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7858-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7858-220">Na lista de aplicativos, escolha **Jive**.</span><span class="sxs-lookup"><span data-stu-id="c7858-220">In the applications list, select **Jive**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="c7858-222">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7858-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7858-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7858-224">Click **Add** button.</span></span> <span data-ttu-id="c7858-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7858-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7858-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c7858-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7858-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7858-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7858-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7858-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7858-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7858-230">Testing single sign-on</span></span>

<span data-ttu-id="c7858-231">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c7858-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7858-232">Ao clicar no bloco do Jive no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo do Jive.</span><span class="sxs-lookup"><span data-stu-id="c7858-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7858-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7858-233">Additional resources</span></span>

* [<span data-ttu-id="c7858-234">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7858-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7858-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7858-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c7858-236">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="c7858-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

