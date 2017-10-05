---
title: "Tutorial: integração do Azure Active Directory ao Kiteworks | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="7ff76-103">Tutorial: Integração do Active Directory do Azure com o Kiteworks</span><span class="sxs-lookup"><span data-stu-id="7ff76-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="7ff76-104">Neste tutorial, você aprenderá como integrar o Kiteworks ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7ff76-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ff76-105">A integração do Kiteworks ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7ff76-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ff76-106">Você pode controlar no AD do Azure quem tem acesso ao Kiteworks</span><span class="sxs-lookup"><span data-stu-id="7ff76-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="7ff76-107">Você pode permitir que seus usuários façam logon automaticamente no Kiteworks (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ff76-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ff76-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ff76-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ff76-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ff76-110">Prerequisites</span></span>

<span data-ttu-id="7ff76-111">Para configurar a integração do AD do Azure ao Kiteworks, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7ff76-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="7ff76-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ff76-113">Uma assinatura habilitada para logon único do Kiteworks</span><span class="sxs-lookup"><span data-stu-id="7ff76-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ff76-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7ff76-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ff76-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7ff76-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ff76-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7ff76-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ff76-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ff76-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ff76-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7ff76-118">Scenario description</span></span>
<span data-ttu-id="7ff76-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7ff76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ff76-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7ff76-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ff76-121">Adicionando o Kiteworks da galeria</span><span class="sxs-lookup"><span data-stu-id="7ff76-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="7ff76-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="7ff76-123">Adicionando o Kiteworks da galeria</span><span class="sxs-lookup"><span data-stu-id="7ff76-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="7ff76-124">Para configurar a integração do Kiteworks ao AD do Azure, você precisará adicionar o Kiteworks da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7ff76-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ff76-125">**Para adicionar o Kiteworks da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ff76-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff76-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ff76-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ff76-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7ff76-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7ff76-133">Na caixa de pesquisa, digite **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-133">In the search box, type **Kiteworks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="7ff76-135">No painel de resultados, selecione **Kiteworks** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ff76-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ff76-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kiteworks, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7ff76-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ff76-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Kiteworks é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff76-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="7ff76-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="7ff76-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="7ff76-141">No Kiteworks, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ff76-142">Para configurar e testar o logon único do AD do Azure com o Kiteworks, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7ff76-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ff76-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7ff76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ff76-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ff76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ff76-145">**[Criação de um usuário de teste do Kiteworks](#creating-a-kiteworks-test-user)** – para ter um equivalente de Brenda Fernandes no Kiteworks que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ff76-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ff76-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ff76-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ff76-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7ff76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ff76-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ff76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ff76-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="7ff76-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="7ff76-150">**Para configurar o logon único do AD do Azure com o Kiteworks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ff76-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff76-151">No portal do Azure, na página de integração de aplicativos do **Kiteworks**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7ff76-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7ff76-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="7ff76-155">Na seção **Domínio e URLs do Kiteworks**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ff76-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="7ff76-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ff76-157">a.</span></span> <span data-ttu-id="7ff76-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="7ff76-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="7ff76-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ff76-159">b.</span></span> <span data-ttu-id="7ff76-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="7ff76-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ff76-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="7ff76-161">These values are not real.</span></span> <span data-ttu-id="7ff76-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="7ff76-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7ff76-163">Contate a [equipe de suporte do cliente Kiteworks](http://accellion.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="7ff76-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="7ff76-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7ff76-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="7ff76-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7ff76-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ff76-168">Na seção **Configuração do Kiteworks**, clique em **Configurar Kiteworks** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ff76-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7ff76-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="7ff76-171">Faça logon no site da sua empresa do Kiteworks como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7ff76-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="7ff76-172">Na barra de ferramentas na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="7ff76-174">Na seção **Autenticação e Autorização**, clique em **Configuração do SSO**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="7ff76-176">Na página Instalação do SSO, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ff76-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="7ff76-178">a.</span><span class="sxs-lookup"><span data-stu-id="7ff76-178">a.</span></span> <span data-ttu-id="7ff76-179">Selecione **Autenticar via SSO**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="7ff76-180">b.</span><span class="sxs-lookup"><span data-stu-id="7ff76-180">b.</span></span> <span data-ttu-id="7ff76-181">Selecione **Iniciar AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="7ff76-182">c.</span><span class="sxs-lookup"><span data-stu-id="7ff76-182">c.</span></span> <span data-ttu-id="7ff76-183">Na caixa de texto **ID da Entidade do IDP**, cole o valor da **ID da Entidade do SAML** copiado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ff76-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="7ff76-184">d.</span><span class="sxs-lookup"><span data-stu-id="7ff76-184">d.</span></span> <span data-ttu-id="7ff76-185">Cole o valor da **URL de Serviço de Logon Único do SAML** que você colou do portal do Azure em **URL de Serviço de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ff76-186">e.</span><span class="sxs-lookup"><span data-stu-id="7ff76-186">e.</span></span> <span data-ttu-id="7ff76-187">Cole o valor da **URL de Serviço de Saída Única** que você colou do portal do Azure na caixa de texto **URL de Serviço de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ff76-188">f.</span><span class="sxs-lookup"><span data-stu-id="7ff76-188">f.</span></span> <span data-ttu-id="7ff76-189">Abra seu certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto **Certificado de Chave Pública RSA** .</span><span class="sxs-lookup"><span data-stu-id="7ff76-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="7ff76-190">g.</span><span class="sxs-lookup"><span data-stu-id="7ff76-190">g.</span></span> <span data-ttu-id="7ff76-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7ff76-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7ff76-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ff76-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7ff76-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ff76-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ff76-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ff76-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ff76-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ff76-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7ff76-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ff76-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff76-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ff76-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7ff76-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ff76-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ff76-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ff76-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ff76-207">a.</span><span class="sxs-lookup"><span data-stu-id="7ff76-207">a.</span></span> <span data-ttu-id="7ff76-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ff76-209">b.</span><span class="sxs-lookup"><span data-stu-id="7ff76-209">b.</span></span> <span data-ttu-id="7ff76-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ff76-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ff76-211">c.</span><span class="sxs-lookup"><span data-stu-id="7ff76-211">c.</span></span> <span data-ttu-id="7ff76-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ff76-213">d.</span><span class="sxs-lookup"><span data-stu-id="7ff76-213">d.</span></span> <span data-ttu-id="7ff76-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="7ff76-215">Criar um usuário de teste do Kiteworks</span><span class="sxs-lookup"><span data-stu-id="7ff76-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="7ff76-216">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="7ff76-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="7ff76-217">O Kiteworks oferece suporte ao provisionamento Just-In-Time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="7ff76-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="7ff76-218">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7ff76-218">There is no action item for you in this section.</span></span> <span data-ttu-id="7ff76-219">Um novo usuário será criado durante uma tentativa de acessar o Kiteworks se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="7ff76-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="7ff76-220">Se você precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="7ff76-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ff76-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ff76-222">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="7ff76-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7ff76-224">**Para atribuir Brenda Fernandes ao Kiteworks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ff76-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="7ff76-225">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7ff76-227">Na lista de aplicativos, selecione **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-227">In the applications list, select **Kiteworks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="7ff76-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7ff76-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7ff76-231">Click **Add** button.</span></span> <span data-ttu-id="7ff76-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7ff76-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7ff76-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ff76-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ff76-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ff76-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ff76-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7ff76-237">Testing single sign-on</span></span>

<span data-ttu-id="7ff76-238">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7ff76-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="7ff76-239">Quando você clica no bloco Kiteworks no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="7ff76-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ff76-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7ff76-240">Additional resources</span></span>

* [<span data-ttu-id="7ff76-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7ff76-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ff76-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ff76-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

