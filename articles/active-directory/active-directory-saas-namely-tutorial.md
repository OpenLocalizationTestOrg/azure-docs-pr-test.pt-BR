---
title: "Tutorial: integração do Azure Active Directory ao Namely | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Namely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="4067d-103">Tutorial: Integração do Active Directory do Azure com o Namely</span><span class="sxs-lookup"><span data-stu-id="4067d-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="4067d-104">Neste tutorial, você aprenderá a integrar o Namely ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4067d-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4067d-105">A integração do Namely ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4067d-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4067d-106">No AD do Azure, você pode controlar quem tem acesso ao Namely</span><span class="sxs-lookup"><span data-stu-id="4067d-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="4067d-107">Você pode permitir que seus usuários façam logon automaticamente no Namely (Logon único) com as contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4067d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4067d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4067d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4067d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4067d-110">Prerequisites</span></span>

<span data-ttu-id="4067d-111">Para configurar a integração do AD do Azure ao Namely, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4067d-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="4067d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4067d-113">Uma assinatura habilitada para logon único do Namely</span><span class="sxs-lookup"><span data-stu-id="4067d-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4067d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4067d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4067d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4067d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4067d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4067d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4067d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4067d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4067d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4067d-118">Scenario description</span></span>
<span data-ttu-id="4067d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4067d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4067d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4067d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4067d-121">Adicionando o Namely da galeria</span><span class="sxs-lookup"><span data-stu-id="4067d-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="4067d-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="4067d-123">Adicionando o Namely da galeria</span><span class="sxs-lookup"><span data-stu-id="4067d-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="4067d-124">Para configurar a integração do Namely ao AD do Azure, você precisa adicionar o do Namely da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4067d-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4067d-125">**Para adicionar o do Namely da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4067d-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4067d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4067d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4067d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4067d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4067d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4067d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4067d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4067d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4067d-133">Na caixa de pesquisa, digite **Namely**.</span><span class="sxs-lookup"><span data-stu-id="4067d-133">In the search box, type **Namely**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="4067d-135">No painel de resultados, selecione **Namely** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4067d-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4067d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4067d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Namely, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4067d-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4067d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Namely é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4067d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="4067d-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado do Namely.</span><span class="sxs-lookup"><span data-stu-id="4067d-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="4067d-141">No Namely, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4067d-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4067d-142">Para configurar e testar o logon único do AD do Azure com o Namely, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4067d-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4067d-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4067d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4067d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4067d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4067d-145">**[Criando um usuário de teste do Namely](#creating-a-namely-test-user)** – para ter um equivalente de Brenda Fernandes no Namely que esteja vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4067d-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4067d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4067d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4067d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4067d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4067d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4067d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4067d-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no seu aplicativo Namely.</span><span class="sxs-lookup"><span data-stu-id="4067d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="4067d-150">**Para configurar o logon único do AD do Azure com o Namely, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4067d-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4067d-151">No Portal do Azure, na página de integração de aplicativos do **Namely**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4067d-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4067d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4067d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="4067d-155">Na seção **URLs e Domínio do Namely**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4067d-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="4067d-157">a.</span><span class="sxs-lookup"><span data-stu-id="4067d-157">a.</span></span> <span data-ttu-id="4067d-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="4067d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="4067d-159">b.</span><span class="sxs-lookup"><span data-stu-id="4067d-159">b.</span></span> <span data-ttu-id="4067d-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4067d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4067d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4067d-161">These values are not real.</span></span> <span data-ttu-id="4067d-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="4067d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4067d-163">Contate a [equipe de suporte do Cliente Namely](https://www.namely.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4067d-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="4067d-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4067d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="4067d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4067d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4067d-168">Na seção **Configuração do Namely**, clique em **Configurar o Namely** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4067d-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4067d-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4067d-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="4067d-171">Em outra janela do navegador, entre em seu site de empresa do Namely como administrador.</span><span class="sxs-lookup"><span data-stu-id="4067d-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="4067d-172">Na barra de ferramentas na parte superior, clique em **Empresa**.</span><span class="sxs-lookup"><span data-stu-id="4067d-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="4067d-174">Clique na guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="4067d-174">Click the **Settings** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="4067d-176">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4067d-176">Click **SAML**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="4067d-178">Na página **Configurações de SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4067d-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="4067d-180">a.</span><span class="sxs-lookup"><span data-stu-id="4067d-180">a.</span></span> <span data-ttu-id="4067d-181">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="4067d-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="4067d-182">b.</span><span class="sxs-lookup"><span data-stu-id="4067d-182">b.</span></span> <span data-ttu-id="4067d-183">Na caixa de texto **URL do SSO do provedor de identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4067d-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4067d-184">c.</span><span class="sxs-lookup"><span data-stu-id="4067d-184">c.</span></span> <span data-ttu-id="4067d-185">Abra o certificado baixado no Bloco de Notas, copie o conteúdo e cole-o na caixa de texto **Certificado do provedor de identidade** .</span><span class="sxs-lookup"><span data-stu-id="4067d-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="4067d-186">d.</span><span class="sxs-lookup"><span data-stu-id="4067d-186">d.</span></span> <span data-ttu-id="4067d-187">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4067d-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4067d-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4067d-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4067d-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4067d-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4067d-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4067d-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4067d-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4067d-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4067d-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4067d-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4067d-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4067d-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4067d-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4067d-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4067d-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4067d-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4067d-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4067d-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4067d-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4067d-203">a.</span><span class="sxs-lookup"><span data-stu-id="4067d-203">a.</span></span> <span data-ttu-id="4067d-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4067d-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4067d-205">b.</span><span class="sxs-lookup"><span data-stu-id="4067d-205">b.</span></span> <span data-ttu-id="4067d-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4067d-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4067d-207">c.</span><span class="sxs-lookup"><span data-stu-id="4067d-207">c.</span></span> <span data-ttu-id="4067d-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4067d-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4067d-209">d.</span><span class="sxs-lookup"><span data-stu-id="4067d-209">d.</span></span> <span data-ttu-id="4067d-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4067d-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="4067d-211">Criando um usuário de teste do Namely</span><span class="sxs-lookup"><span data-stu-id="4067d-211">Creating a Namely test user</span></span>

<span data-ttu-id="4067d-212">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Namely.</span><span class="sxs-lookup"><span data-stu-id="4067d-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="4067d-213">**Para criar um usuário chamado Brenda Fernandes no Namely, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4067d-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4067d-214">Faça logon em seu site de empresa do Namely como administrador.</span><span class="sxs-lookup"><span data-stu-id="4067d-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="4067d-215">Na barra de ferramentas na parte superior, clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="4067d-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="4067d-217">Clique na guia **Diretório** .</span><span class="sxs-lookup"><span data-stu-id="4067d-217">Click the **Directory** tab.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="4067d-219">Clique em **Adicionar Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="4067d-219">Click **Add New Person**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="4067d-221">Na caixa de diálogo **Adicionar Nova Pessoa** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4067d-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="4067d-222">a.</span><span class="sxs-lookup"><span data-stu-id="4067d-222">a.</span></span> <span data-ttu-id="4067d-223">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="4067d-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="4067d-224">b.</span><span class="sxs-lookup"><span data-stu-id="4067d-224">b.</span></span> <span data-ttu-id="4067d-225">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4067d-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="4067d-226">c.</span><span class="sxs-lookup"><span data-stu-id="4067d-226">c.</span></span> <span data-ttu-id="4067d-227">Na caixa de texto **Email**, digite o endereço de **email do usuário** de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4067d-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4067d-228">d.</span><span class="sxs-lookup"><span data-stu-id="4067d-228">d.</span></span> <span data-ttu-id="4067d-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4067d-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4067d-230">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4067d-231">Nesta seção, você concederá a Brenda Fernandes acesso ao Namely para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="4067d-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4067d-233">**Para atribuir Brenda Fernandes ao Namely, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4067d-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4067d-234">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4067d-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4067d-236">Na lista de aplicativos, selecione **Namely**.</span><span class="sxs-lookup"><span data-stu-id="4067d-236">In the applications list, select **Namely**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="4067d-238">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4067d-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4067d-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4067d-240">Click **Add** button.</span></span> <span data-ttu-id="4067d-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4067d-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4067d-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4067d-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4067d-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4067d-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4067d-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4067d-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4067d-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4067d-246">Testing single sign-on</span></span>

<span data-ttu-id="4067d-247">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4067d-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4067d-248">Quando você clicar no bloco Namely no Painel de Acesso, você deverá ser automaticamente conectado ao seu aplicativo Namely</span><span class="sxs-lookup"><span data-stu-id="4067d-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4067d-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4067d-249">Additional resources</span></span>

* [<span data-ttu-id="4067d-250">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4067d-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4067d-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4067d-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

