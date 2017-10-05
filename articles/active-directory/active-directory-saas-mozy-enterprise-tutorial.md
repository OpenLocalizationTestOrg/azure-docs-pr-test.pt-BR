---
title: "Tutorial: Integração do Azure Active Directory com o Mozy Enterprise | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="7c62a-103">Tutorial: Integração do Active Directory do Azure com o Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="7c62a-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="7c62a-104">Neste tutorial, você aprende a integrar o Mozy Enterprise ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7c62a-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c62a-105">A integração do Mozy Enterprise ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7c62a-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c62a-106">No Azure AD, é possível controlar quem tem acesso ao Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="7c62a-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="7c62a-107">É possível permitir que os usuários sejam automaticamente conectados ao Mozy Enterprise (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c62a-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c62a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c62a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c62a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c62a-110">Prerequisites</span></span>

<span data-ttu-id="7c62a-111">Para configurar a integração do Azure AD ao Mozy Enterprise, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7c62a-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="7c62a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7c62a-113">Uma assinatura habilitada para logon único do Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="7c62a-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c62a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7c62a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c62a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c62a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c62a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c62a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c62a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c62a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c62a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c62a-118">Scenario description</span></span>
<span data-ttu-id="7c62a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c62a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c62a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7c62a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c62a-121">Adicionando o Mozy Enterprise por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7c62a-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="7c62a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="7c62a-123">Adicionando o Mozy Enterprise por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7c62a-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="7c62a-124">Para configurar a integração do Mozy Enterprise com o Azure AD, você precisará adicionar o Mozy Enterprise à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="7c62a-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c62a-125">**Para adicionar o Mozy Enterprise por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c62a-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c62a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c62a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c62a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7c62a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7c62a-133">Na caixa de pesquisa, digite **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="7c62a-135">No painel de resultados, selecione **Mozy Enterprise** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c62a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c62a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Mozy Enterprise, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="7c62a-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c62a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Mozy Enterprise é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c62a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="7c62a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7c62a-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="7c62a-141">No Mozy Enterprise, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c62a-142">Para configurar e testar o logon único do Azure AD com o Mozy Enterprise, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7c62a-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c62a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7c62a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c62a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c62a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c62a-145">**[Criar um usuário de teste do Mozy Enterprise](#creating-a-mozy-enterprise-test-user)** – para ter um equivalente de Brenda Fernandes no Mozy Enterprise que está vinculado à representação desse usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c62a-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c62a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c62a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c62a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7c62a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c62a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c62a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c62a-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7c62a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="7c62a-150">**Para configurar o logon único do Azure AD com o Mozy Enterprise, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c62a-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="7c62a-151">No Portal do Azure, na página de integração de aplicativos do **Mozy Enterprise**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7c62a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7c62a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="7c62a-155">Na seção **URLs e Domínio do Mozy Enterprise**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c62a-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="7c62a-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="7c62a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c62a-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7c62a-158">This value is not real.</span></span> <span data-ttu-id="7c62a-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7c62a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7c62a-160">Contate a [equipe de suporte ao Cliente do Mozy Enterprise](http://support.mozy.com/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="7c62a-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="7c62a-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="7c62a-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="7c62a-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7c62a-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c62a-165">Na seção **Configuração do Mozy Enterprise**, clique em **Configurar Mozy Enterprise** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7c62a-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7c62a-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="7c62a-168">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Mozy Enterprise como administrador.</span><span class="sxs-lookup"><span data-stu-id="7c62a-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="7c62a-169">Na seção **Configuração**, clique em **Política de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="7c62a-170">![Política de autenticação](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Política de autenticação")</span><span class="sxs-lookup"><span data-stu-id="7c62a-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="7c62a-171">Na seção **Política de Autenticação** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c62a-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="7c62a-172">![Política de autenticação](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Política de autenticação")</span><span class="sxs-lookup"><span data-stu-id="7c62a-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="7c62a-173">a.</span><span class="sxs-lookup"><span data-stu-id="7c62a-173">a.</span></span> <span data-ttu-id="7c62a-174">Selecione **Serviço de Diretório** como **Provedor**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="7c62a-175">b.</span><span class="sxs-lookup"><span data-stu-id="7c62a-175">b.</span></span> <span data-ttu-id="7c62a-176">Selecione **Usar Push do LDAP**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="7c62a-177">c.</span><span class="sxs-lookup"><span data-stu-id="7c62a-177">c.</span></span> <span data-ttu-id="7c62a-178">Clique na guia **Autenticação SAML** .</span><span class="sxs-lookup"><span data-stu-id="7c62a-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="7c62a-179">d.</span><span class="sxs-lookup"><span data-stu-id="7c62a-179">d.</span></span> <span data-ttu-id="7c62a-180">Cole a **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure na caixa de texto **URL de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="7c62a-181">e.</span><span class="sxs-lookup"><span data-stu-id="7c62a-181">e.</span></span> <span data-ttu-id="7c62a-182">Cole a **ID de Entidade do SAML** que você copiou do Portal do Azure na caixa de texto **Ponto de Extremidade do SAML**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="7c62a-183">f.</span><span class="sxs-lookup"><span data-stu-id="7c62a-183">f.</span></span> <span data-ttu-id="7c62a-184">Abra seu certificado codificado em Base 64 baixado no bloco de notas, copie o conteúdo dele na área de transferência e cole todo o Certificado na caixa de texto **Certificado SAML**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="7c62a-185">g.</span><span class="sxs-lookup"><span data-stu-id="7c62a-185">g.</span></span> <span data-ttu-id="7c62a-186">Selecione **Habilitar SSO para que os Administradores façam logon com suas credenciais de rede**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="7c62a-187">h.</span><span class="sxs-lookup"><span data-stu-id="7c62a-187">h.</span></span> <span data-ttu-id="7c62a-188">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7c62a-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7c62a-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c62a-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7c62a-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c62a-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c62a-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c62a-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c62a-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c62a-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7c62a-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c62a-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c62a-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c62a-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c62a-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c62a-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c62a-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c62a-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c62a-204">a.</span><span class="sxs-lookup"><span data-stu-id="7c62a-204">a.</span></span> <span data-ttu-id="7c62a-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c62a-206">b.</span><span class="sxs-lookup"><span data-stu-id="7c62a-206">b.</span></span> <span data-ttu-id="7c62a-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c62a-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c62a-208">c.</span><span class="sxs-lookup"><span data-stu-id="7c62a-208">c.</span></span> <span data-ttu-id="7c62a-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c62a-210">d.</span><span class="sxs-lookup"><span data-stu-id="7c62a-210">d.</span></span> <span data-ttu-id="7c62a-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="7c62a-212">Criando um usuário de teste do Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="7c62a-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="7c62a-213">Para permitir que os usuários do AD do Azure façam logon no Mozy Enterprise, eles devem ser provisionados no Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7c62a-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="7c62a-214">No caso do Mozy Enterprise, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7c62a-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="7c62a-215">É possível usar qualquer outra ferramenta de criação da conta de usuário do Mozy Enterprise ou as APIs fornecidas pelo Mozy Enterprise para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="7c62a-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="7c62a-216">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c62a-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7c62a-217">Faça logon em seu locatário do **Mozy Enterprise** .</span><span class="sxs-lookup"><span data-stu-id="7c62a-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="7c62a-218">Clique em **Usuários** e em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="7c62a-219">![Usuários](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="7c62a-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7c62a-220">A opção **Adicionar Novo Usuário** será exibida apenas se **Mozy** estiver selecionado como o provedor em **Política de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="7c62a-221">Se a autenticação SAML for configurada, os usuários serão adicionados automaticamente em seu primeiro logon por meio do Logon único.</span><span class="sxs-lookup"><span data-stu-id="7c62a-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="7c62a-222">Na caixa de diálogo novo usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c62a-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="7c62a-223">![Adicionar Usuários](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Adicionar Usuários")</span><span class="sxs-lookup"><span data-stu-id="7c62a-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="7c62a-224">a.</span><span class="sxs-lookup"><span data-stu-id="7c62a-224">a.</span></span> <span data-ttu-id="7c62a-225">Na lista **Escolher um Grupo** , selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="7c62a-226">b.</span><span class="sxs-lookup"><span data-stu-id="7c62a-226">b.</span></span> <span data-ttu-id="7c62a-227">Na lista **Wue tipo de usuário** , selecione um tipo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="7c62a-228">c.</span><span class="sxs-lookup"><span data-stu-id="7c62a-228">c.</span></span> <span data-ttu-id="7c62a-229">Na caixa de texto **Nome do Usuário** , digite o nome do usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c62a-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="7c62a-230">d.</span><span class="sxs-lookup"><span data-stu-id="7c62a-230">d.</span></span> <span data-ttu-id="7c62a-231">Na caixa de texto **Email** , digite o endereço de email do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c62a-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="7c62a-232">e.</span><span class="sxs-lookup"><span data-stu-id="7c62a-232">e.</span></span> <span data-ttu-id="7c62a-233">Selecione **Enviar email de instruções ao usuário**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="7c62a-234">f.</span><span class="sxs-lookup"><span data-stu-id="7c62a-234">f.</span></span> <span data-ttu-id="7c62a-235">Clique em **Adicionar Usuário(s)**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="7c62a-236">Após a criação do usuário, um email será enviado ao usuário do AD do Azure com um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="7c62a-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c62a-237">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c62a-238">Nesta seção, você concederá a Brenda Fernandes acesso ao Mozy Enterprise para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c62a-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7c62a-240">**Para atribuir Brenda Fernandes ao Mozy Enterprise, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c62a-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="7c62a-241">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7c62a-243">Na lista de aplicativos, selecione **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="7c62a-245">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7c62a-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-247">Click **Add** button.</span></span> <span data-ttu-id="7c62a-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7c62a-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c62a-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c62a-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c62a-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c62a-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c62a-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7c62a-253">Testing single sign-on</span></span>

<span data-ttu-id="7c62a-254">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7c62a-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7c62a-255">Ao clicar no bloco Mozy Enterprise no Painel de Acesso, você deve acessar a página de logon do aplicativo Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7c62a-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="7c62a-256">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c62a-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c62a-257">Additional resources</span></span>

* [<span data-ttu-id="7c62a-258">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7c62a-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c62a-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c62a-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

