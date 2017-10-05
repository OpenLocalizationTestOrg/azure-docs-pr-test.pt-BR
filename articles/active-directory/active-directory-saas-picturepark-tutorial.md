---
title: "Tutorial: Integração do Azure Active Directory ao Picturepark | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="d10f3-103">Tutorial: Integração do Azure Active Directory ao Picturepark</span><span class="sxs-lookup"><span data-stu-id="d10f3-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="d10f3-104">Neste tutorial, você aprende a integrar o Picturepark ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d10f3-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d10f3-105">A integração do Picturepark ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d10f3-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d10f3-106">No Azure AD, é possível controlar quem tem acesso ao Picturepark</span><span class="sxs-lookup"><span data-stu-id="d10f3-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="d10f3-107">É possível permitir que os usuários se conectem automaticamente ao Picturepark (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d10f3-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d10f3-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d10f3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d10f3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d10f3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d10f3-110">Prerequisites</span></span>

<span data-ttu-id="d10f3-111">Para configurar a integração do Azure AD ao Picturepark, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d10f3-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="d10f3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d10f3-113">Uma assinatura habilitada para logon único do Picturepark</span><span class="sxs-lookup"><span data-stu-id="d10f3-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d10f3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d10f3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d10f3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d10f3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d10f3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d10f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d10f3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d10f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d10f3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d10f3-118">Scenario description</span></span>
<span data-ttu-id="d10f3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d10f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d10f3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d10f3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d10f3-121">Adicionando o Picturepark por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="d10f3-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="d10f3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="d10f3-123">Adicionando o Picturepark por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="d10f3-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="d10f3-124">Para configurar a integração do Picturepark ao Azure AD, é necessário adicionar o Picturepark à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="d10f3-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d10f3-125">**Para adicionar o Picturepark por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d10f3-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d10f3-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d10f3-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d10f3-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d10f3-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d10f3-133">Na caixa de pesquisa, digite **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-133">In the search box, type **Picturepark**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="d10f3-135">No painel de resultados, selecione **Picturepark** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d10f3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d10f3-138">Nesta seção, você configura e testa o logon único do Azure AD com o Picturepark, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d10f3-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d10f3-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Picturepark é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d10f3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="d10f3-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Picturepark.</span><span class="sxs-lookup"><span data-stu-id="d10f3-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="d10f3-141">No Picturepark, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d10f3-142">Para configurar e testar o logon único do Azure AD com o Picturepark, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d10f3-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d10f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d10f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d10f3-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d10f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d10f3-145">**[Criando um usuário de teste do Picturepark](#creating-a-picturepark-test-user)** – para ter um equivalente de Brenda Fernandes no Picturepark que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d10f3-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d10f3-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d10f3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d10f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d10f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d10f3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d10f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d10f3-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Picturepark.</span><span class="sxs-lookup"><span data-stu-id="d10f3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="d10f3-150">**Para configurar o logon único do Azure AD com o Picturepark, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d10f3-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="d10f3-151">No portal do Azure, na página de integração do aplicativo **Picturepark**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d10f3-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d10f3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="d10f3-155">Na seção **Domínio e URLs do Picturepark**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d10f3-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="d10f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="d10f3-157">a.</span></span> <span data-ttu-id="d10f3-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="d10f3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="d10f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="d10f3-159">b.</span></span> <span data-ttu-id="d10f3-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="d10f3-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="d10f3-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="d10f3-161">These values are not real.</span></span> <span data-ttu-id="d10f3-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="d10f3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d10f3-163">Contate a [equipe de suporte ao Cliente do Picturepark](https://picturepark.com/about/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="d10f3-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="d10f3-164">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="d10f3-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="d10f3-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d10f3-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d10f3-168">Na seção **Configuração do Picturepark**, clique em **Configurar o Picturepark** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d10f3-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="d10f3-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="d10f3-171">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do Picturepark como administrador.</span><span class="sxs-lookup"><span data-stu-id="d10f3-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="d10f3-172">Na barra de ferramentas na parte superior, clique em **Ferramentas administrativas** e em **Console de Gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="d10f3-173">![Console de Gerenciamento](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de Gerenciamento")</span><span class="sxs-lookup"><span data-stu-id="d10f3-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="d10f3-174">Clique em **Autenticação** e em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="d10f3-175">![Autenticação](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="d10f3-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="d10f3-176">Na seção **Configuração do provedor de identidade** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d10f3-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d10f3-177">![Configuração do Provedor de Identidade](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuração do Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="d10f3-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="d10f3-178">a.</span><span class="sxs-lookup"><span data-stu-id="d10f3-178">a.</span></span> <span data-ttu-id="d10f3-179">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-179">Click **Add**.</span></span>
  
    <span data-ttu-id="d10f3-180">b.</span><span class="sxs-lookup"><span data-stu-id="d10f3-180">b.</span></span> <span data-ttu-id="d10f3-181">Digite um nome para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="d10f3-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="d10f3-182">c.</span><span class="sxs-lookup"><span data-stu-id="d10f3-182">c.</span></span> <span data-ttu-id="d10f3-183">Selecione **Definir como padrão**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="d10f3-184">d.</span><span class="sxs-lookup"><span data-stu-id="d10f3-184">d.</span></span> <span data-ttu-id="d10f3-185">Na caixa de texto **URI do Emissor**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d10f3-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d10f3-186">e.</span><span class="sxs-lookup"><span data-stu-id="d10f3-186">e.</span></span> <span data-ttu-id="d10f3-187">Na caixa de texto **Impressão Digital do Emissor Confiável**, cole o valor da **Impressão Digital** copiado da seção **Certificado de Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="d10f3-188">Clique em **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="d10f3-189">Para definir o atributo **Emailaddress** na caixa de texto **Declaração**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="d10f3-190">![Configuração](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="d10f3-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="d10f3-191">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d10f3-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d10f3-192">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d10f3-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d10f3-193">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d10f3-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d10f3-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="d10f3-195">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d10f3-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d10f3-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d10f3-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d10f3-198">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d10f3-200">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d10f3-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d10f3-202">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d10f3-204">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d10f3-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d10f3-206">a.</span><span class="sxs-lookup"><span data-stu-id="d10f3-206">a.</span></span> <span data-ttu-id="d10f3-207">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d10f3-208">b.</span><span class="sxs-lookup"><span data-stu-id="d10f3-208">b.</span></span> <span data-ttu-id="d10f3-209">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d10f3-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d10f3-210">c.</span><span class="sxs-lookup"><span data-stu-id="d10f3-210">c.</span></span> <span data-ttu-id="d10f3-211">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d10f3-212">d.</span><span class="sxs-lookup"><span data-stu-id="d10f3-212">d.</span></span> <span data-ttu-id="d10f3-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="d10f3-214">Criando um usuário de teste do Picturepark</span><span class="sxs-lookup"><span data-stu-id="d10f3-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="d10f3-215">Para permitir que os usuários do AD do Azure façam logon no Picturepark, eles devem ser provisionados no Picturepark.</span><span class="sxs-lookup"><span data-stu-id="d10f3-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="d10f3-216">No caso do Picturepark, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d10f3-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="d10f3-217">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d10f3-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d10f3-218">Faça logon em seu locatário do **Picturepark** .</span><span class="sxs-lookup"><span data-stu-id="d10f3-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="d10f3-219">Na barra de ferramentas na parte superior, clique em **Ferramentas administrativas** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="d10f3-220">![Usuários](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="d10f3-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="d10f3-221">Na guia **Visão geral de usuários**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="d10f3-222">![Gerenciamento de usuário](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gerenciamento de usuário")</span><span class="sxs-lookup"><span data-stu-id="d10f3-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="d10f3-223">Na caixa de diálogo **Criar Usuário**, realize as seguintes etapas de um Usuário válido do Azure Active Directory que você deseja provisionar:</span><span class="sxs-lookup"><span data-stu-id="d10f3-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="d10f3-224">![Criar usuário](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="d10f3-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="d10f3-225">a.</span><span class="sxs-lookup"><span data-stu-id="d10f3-225">a.</span></span> <span data-ttu-id="d10f3-226">Na caixa de texto **Endereço de Email**, digite o **endereço de email** do usuário **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="d10f3-227">b.</span><span class="sxs-lookup"><span data-stu-id="d10f3-227">b.</span></span> <span data-ttu-id="d10f3-228">Nas caixas de texto **Senha** e **Confirmar Senha**, digite a **senha** de BrendaFernandes.</span><span class="sxs-lookup"><span data-stu-id="d10f3-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="d10f3-229">c.</span><span class="sxs-lookup"><span data-stu-id="d10f3-229">c.</span></span> <span data-ttu-id="d10f3-230">Na caixa de texto **Nome**, digite o **Nome** do usuário **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="d10f3-231">d.</span><span class="sxs-lookup"><span data-stu-id="d10f3-231">d.</span></span> <span data-ttu-id="d10f3-232">Na caixa de texto **Sobrenome**, digite o **Sobrenome** do usuário **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="d10f3-233">e.</span><span class="sxs-lookup"><span data-stu-id="d10f3-233">e.</span></span> <span data-ttu-id="d10f3-234">Na caixa de texto **Empresa**, digite o **Nome da empresa** do usuário.</span><span class="sxs-lookup"><span data-stu-id="d10f3-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="d10f3-235">f.</span><span class="sxs-lookup"><span data-stu-id="d10f3-235">f.</span></span> <span data-ttu-id="d10f3-236">Na caixa de texto **País**, selecione o **País** do usuário.</span><span class="sxs-lookup"><span data-stu-id="d10f3-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="d10f3-237">g.</span><span class="sxs-lookup"><span data-stu-id="d10f3-237">g.</span></span> <span data-ttu-id="d10f3-238">Na caixa de texto **CEP**, digite o **CEP** da cidade.</span><span class="sxs-lookup"><span data-stu-id="d10f3-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="d10f3-239">h.</span><span class="sxs-lookup"><span data-stu-id="d10f3-239">h.</span></span> <span data-ttu-id="d10f3-240">Na caixa de texto **Cidade**, digite o **Nome da cidade** do usuário.</span><span class="sxs-lookup"><span data-stu-id="d10f3-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="d10f3-241">i.</span><span class="sxs-lookup"><span data-stu-id="d10f3-241">i.</span></span> <span data-ttu-id="d10f3-242">Selecione um **Idioma**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="d10f3-243">j.</span><span class="sxs-lookup"><span data-stu-id="d10f3-243">j.</span></span> <span data-ttu-id="d10f3-244">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="d10f3-245">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Picturepark ou as APIs fornecidas pelo Picturepark para provisionar contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d10f3-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d10f3-246">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d10f3-247">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Picturepark.</span><span class="sxs-lookup"><span data-stu-id="d10f3-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d10f3-249">**Para atribuir Brenda Fernandes ao Picturepark, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d10f3-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="d10f3-250">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d10f3-252">Na lista de aplicativos, selecione **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-252">In the applications list, select **Picturepark**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="d10f3-254">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d10f3-256">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d10f3-256">Click **Add** button.</span></span> <span data-ttu-id="d10f3-257">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d10f3-259">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d10f3-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d10f3-260">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d10f3-261">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d10f3-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d10f3-262">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d10f3-262">Testing single sign-on</span></span>

<span data-ttu-id="d10f3-263">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d10f3-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d10f3-264">Quando você clicar no bloco do Picturepark no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Picturepark.</span><span class="sxs-lookup"><span data-stu-id="d10f3-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="d10f3-265">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d10f3-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d10f3-266">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d10f3-266">Additional resources</span></span>

* [<span data-ttu-id="d10f3-267">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d10f3-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d10f3-268">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d10f3-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

