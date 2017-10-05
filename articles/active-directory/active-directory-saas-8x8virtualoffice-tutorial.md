---
title: "Tutorial: Integração do Azure Active Directory com o 8x8 Virtual Office | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o 8x8 Virtual Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="73e3e-103">Tutorial: Integração do Azure Active Directory com o 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="73e3e-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="73e3e-104">Neste tutorial, você aprende a integrar o 8x8 Virtual Office ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="73e3e-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73e3e-105">A integração do 8x8 Virtual Office ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="73e3e-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="73e3e-106">No Azure AD, você poderá controlar quem tem acesso ao 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="73e3e-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="73e3e-107">Você pode permitir que seus usuários façam logon automaticamente no8x8 Virtual Office (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e3e-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73e3e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="73e3e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73e3e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73e3e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="73e3e-110">Prerequisites</span></span>

<span data-ttu-id="73e3e-111">Para configurar a integração do Azure AD com o 8x8 Virtual Office, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="73e3e-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="73e3e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73e3e-113">Uma assinatura habilitada para logon único do 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="73e3e-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73e3e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="73e3e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73e3e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="73e3e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73e3e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="73e3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73e3e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73e3e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73e3e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="73e3e-118">Scenario description</span></span>
<span data-ttu-id="73e3e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="73e3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73e3e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="73e3e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73e3e-121">Adicionando o 8x8 Virtual Office da galeria</span><span class="sxs-lookup"><span data-stu-id="73e3e-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="73e3e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="73e3e-123">Adicionando o 8x8 Virtual Office da galeria</span><span class="sxs-lookup"><span data-stu-id="73e3e-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="73e3e-124">Para configurar a integração do 8x8 Virtual Office ao Azure AD, você precisará adicionar o 8x8 Virtual Office à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="73e3e-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="73e3e-125">**Para adicionar o 8x8 Virtual Office por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73e3e-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="73e3e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73e3e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="73e3e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="73e3e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="73e3e-133">Na caixa de pesquisa, digite **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="73e3e-135">No painel de resultados, selecione **8x8 Virtual Office** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73e3e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73e3e-138">Nesta seção, você configura e testa o logon único do Azure AD com o 8x8 Virtual Office, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="73e3e-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="73e3e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do 8x8 Virtual Office é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73e3e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="73e3e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="73e3e-141">No 8x8 Virtual Office, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="73e3e-142">Para configurar e testar o logon único do Azure AD com o 8x8 Virtual Office, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="73e3e-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="73e3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="73e3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="73e3e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73e3e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="73e3e-145">**[Criando um usuário de teste do 8x8 Virtual Office](#creating-a-8x8-virtual-office-test-user)** – para ter um equivalente de Brenda Fernandes no 8x8 Virtual Office que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73e3e-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="73e3e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e3e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="73e3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="73e3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73e3e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e3e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73e3e-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="73e3e-150">**Para configurar o logon único do Azure AD com o 8x8 Virtual Office, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73e3e-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="73e3e-151">No portal do Azure, na página de integração do aplicativo do **8x8 Virtual Office**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="73e3e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="73e3e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="73e3e-155">Na seção **Domínio e URLs do 8x8 Virtual Office**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73e3e-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="73e3e-157">a.</span><span class="sxs-lookup"><span data-stu-id="73e3e-157">a.</span></span> <span data-ttu-id="73e3e-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="73e3e-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="73e3e-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="73e3e-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="73e3e-160">b.</span><span class="sxs-lookup"><span data-stu-id="73e3e-160">b.</span></span> <span data-ttu-id="73e3e-161">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="73e3e-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="73e3e-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="73e3e-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73e3e-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="73e3e-163">These values are not real.</span></span> <span data-ttu-id="73e3e-164">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="73e3e-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="73e3e-165">Contate a [equipe de suporte do 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="73e3e-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="73e3e-166">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="73e3e-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="73e3e-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="73e3e-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73e3e-170">Na seção **Configuração do 8x8 Virtual Office**, clique em **Configurar o 8x8 Virtual Office** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="73e3e-171">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="73e3e-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="73e3e-173">Faça logon no seu locatário do 8x8 Virtual Office como administrador.</span><span class="sxs-lookup"><span data-stu-id="73e3e-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="73e3e-174">Selecione **Virtual Office Account Mgr** no painel do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="73e3e-176">Selecione a **conta comercial** que deseja gerenciar e clique no botão **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="73e3e-178">Clique na guia **Accounts** na lista de menus.</span><span class="sxs-lookup"><span data-stu-id="73e3e-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="73e3e-180">Clique em **Single Sign On** na lista Accounts.</span><span class="sxs-lookup"><span data-stu-id="73e3e-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="73e3e-182">Selecione **Logon Único** em Método de autenticação e clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="73e3e-184">Copie a **URL de SSO de SAML**, a **URL de Serviço de Logoff Único** e a **URL do Emissor** do Azure AD para **Entrar**, **URL de Logoff** e **URL do Emissor** no 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurar no lado do aplicativo](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="73e3e-186">Clique no botão **Navegador** para carregar o certificado que você baixou do Azure AD e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="73e3e-187">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="73e3e-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="73e3e-188">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="73e3e-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="73e3e-189">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73e3e-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73e3e-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="73e3e-191">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73e3e-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="73e3e-193">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73e3e-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="73e3e-194">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73e3e-196">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73e3e-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73e3e-198">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73e3e-200">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="73e3e-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73e3e-202">a.</span><span class="sxs-lookup"><span data-stu-id="73e3e-202">a.</span></span> <span data-ttu-id="73e3e-203">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73e3e-204">b.</span><span class="sxs-lookup"><span data-stu-id="73e3e-204">b.</span></span> <span data-ttu-id="73e3e-205">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="73e3e-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73e3e-206">c.</span><span class="sxs-lookup"><span data-stu-id="73e3e-206">c.</span></span> <span data-ttu-id="73e3e-207">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="73e3e-208">d.</span><span class="sxs-lookup"><span data-stu-id="73e3e-208">d.</span></span> <span data-ttu-id="73e3e-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="73e3e-210">Criar um usuário de teste no 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="73e3e-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="73e3e-211">O objetivo desta seção é criar uma usuária chamada Brenda Fernandes no 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="73e3e-212">O 8x8 Virtual Office dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="73e3e-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="73e3e-213">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="73e3e-213">There is no action item for you in this section.</span></span> <span data-ttu-id="73e3e-214">Um novo usuário será criado durante uma tentativa de acessar o 8x8 Virtual Office, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="73e3e-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="73e3e-215">Se precisar criar um usuário manualmente, será necessário contatar a [equipe de suporte do 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="73e3e-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="73e3e-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="73e3e-217">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="73e3e-219">**Para atribuir Brenda Fernandes ao 8x8 Virtual Office, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="73e3e-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="73e3e-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="73e3e-222">Na lista de aplicativos, selecione **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="73e3e-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="73e3e-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="73e3e-226">Click **Add** button.</span></span> <span data-ttu-id="73e3e-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="73e3e-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="73e3e-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="73e3e-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73e3e-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="73e3e-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73e3e-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="73e3e-232">Testing single sign-on</span></span>

<span data-ttu-id="73e3e-233">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="73e3e-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="73e3e-234">Ao clicar no bloco do 8x8 Virtual Office no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="73e3e-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="73e3e-235">Para obter mais informações sobre o Painel de Acesso, consulte [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="73e3e-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73e3e-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="73e3e-236">Additional resources</span></span>

* [<span data-ttu-id="73e3e-237">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="73e3e-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73e3e-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73e3e-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

