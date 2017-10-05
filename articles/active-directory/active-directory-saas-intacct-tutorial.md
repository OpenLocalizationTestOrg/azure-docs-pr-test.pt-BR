---
title: "Tutorial: Integração do Azure Active Directory com o Intacct | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="bcf98-103">Tutorial: Integração do Active Directory do Azure com o Intacct</span><span class="sxs-lookup"><span data-stu-id="bcf98-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="bcf98-104">Neste tutorial, você aprenderá como integrar o Intacct ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="bcf98-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bcf98-105">A integração do Intacct ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="bcf98-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bcf98-106">Você pode controlar no Azure AD quem terá acesso ao Intacct</span><span class="sxs-lookup"><span data-stu-id="bcf98-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="bcf98-107">Você pode permitir que seus usuários entrem automaticamente no Intacct (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcf98-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bcf98-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bcf98-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bcf98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcf98-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bcf98-110">Prerequisites</span></span>

<span data-ttu-id="bcf98-111">Para configurar a integração do Azure AD ao Intacct, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="bcf98-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="bcf98-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bcf98-113">Uma assinatura habilitada para logon único do Intacct</span><span class="sxs-lookup"><span data-stu-id="bcf98-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bcf98-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bcf98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bcf98-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bcf98-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bcf98-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="bcf98-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bcf98-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcf98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bcf98-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bcf98-118">Scenario description</span></span>
<span data-ttu-id="bcf98-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bcf98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bcf98-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="bcf98-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bcf98-121">Como adicionar o Intacct da galeria</span><span class="sxs-lookup"><span data-stu-id="bcf98-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="bcf98-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="bcf98-123">Como adicionar o Intacct da galeria</span><span class="sxs-lookup"><span data-stu-id="bcf98-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="bcf98-124">Para configurar a integração do Intacct ao Azure AD, você precisa adicionar o Intacct por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="bcf98-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bcf98-125">**Para adicionar o Intacct por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bcf98-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bcf98-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bcf98-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bcf98-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="bcf98-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="bcf98-133">Na caixa de pesquisa, digite **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-133">In the search box, type **Intacct**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="bcf98-135">No painel de resultados, selecione **Intacct** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bcf98-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bcf98-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Intacct, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="bcf98-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bcf98-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Intacct é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcf98-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="bcf98-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="bcf98-141">No Intacct, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bcf98-142">Para configurar e testar o logon único do Azure AD com o Intacct, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="bcf98-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bcf98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bcf98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bcf98-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bcf98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bcf98-145">**[Criação de um usuário de teste do Intacct](#creating-an-intacct-test-user)**: para ter um equivalente de Brenda Fernandes no Intacct, que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcf98-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bcf98-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf98-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bcf98-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="bcf98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bcf98-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bcf98-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bcf98-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="bcf98-150">**Para configurar o logon único do Azure AD com o Intacct, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bcf98-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="bcf98-151">No Portal do Azure, na página de integração de aplicativos do **Intacct**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="bcf98-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="bcf98-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="bcf98-155">Na seção **URLs e Domínio do Intacct**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bcf98-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="bcf98-157">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="bcf98-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="bcf98-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="bcf98-158">This value is not real.</span></span> <span data-ttu-id="bcf98-159">Atualize esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="bcf98-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="bcf98-160">Entre em contato com a [equipe de suporte do Intacct](https://us.intacct.com/support) para obter este valor.</span><span class="sxs-lookup"><span data-stu-id="bcf98-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="bcf98-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="bcf98-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="bcf98-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="bcf98-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bcf98-165">Na seção **Configuração do Intacct**, clique em **Configurar o Intacct** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bcf98-166">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="bcf98-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="bcf98-168">Em outra janela do navegador da Web, entre em seu site de empresa do Intacct como administrador.</span><span class="sxs-lookup"><span data-stu-id="bcf98-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="bcf98-169">Clique na guia **Empresa** e em **Informações da Empresa**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="bcf98-170">![Empresa](./media/active-directory-saas-intacct-tutorial/ic790037.png "Empresa")</span><span class="sxs-lookup"><span data-stu-id="bcf98-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="bcf98-171">Clique na guia **Segurança** e em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="bcf98-172">![Segurança](./media/active-directory-saas-intacct-tutorial/ic790038.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="bcf98-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="bcf98-173">Na seção **SSO (logon único)** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bcf98-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="bcf98-174">![Logon único](./media/active-directory-saas-intacct-tutorial/ic790039.png "logon único")</span><span class="sxs-lookup"><span data-stu-id="bcf98-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="bcf98-175">a.</span><span class="sxs-lookup"><span data-stu-id="bcf98-175">a.</span></span> <span data-ttu-id="bcf98-176">Selecione **Habilitar logon único**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="bcf98-177">b.</span><span class="sxs-lookup"><span data-stu-id="bcf98-177">b.</span></span> <span data-ttu-id="bcf98-178">Para **Tipo de provedor de identidade**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="bcf98-179">c.</span><span class="sxs-lookup"><span data-stu-id="bcf98-179">c.</span></span> <span data-ttu-id="bcf98-180">Na caixa de texto **URL do Emissor**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf98-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="bcf98-181">d.</span><span class="sxs-lookup"><span data-stu-id="bcf98-181">d.</span></span> <span data-ttu-id="bcf98-182">Na caixa de texto **URL de Logon**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcf98-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bcf98-183">e.</span><span class="sxs-lookup"><span data-stu-id="bcf98-183">e.</span></span> <span data-ttu-id="bcf98-184">Abra seu certificado codificado em **Base 64** no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="bcf98-185">f.</span><span class="sxs-lookup"><span data-stu-id="bcf98-185">f.</span></span> <span data-ttu-id="bcf98-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bcf98-187">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="bcf98-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bcf98-188">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="bcf98-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bcf98-189">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bcf98-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bcf98-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="bcf98-191">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bcf98-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="bcf98-193">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bcf98-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bcf98-194">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bcf98-196">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="bcf98-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bcf98-198">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bcf98-200">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bcf98-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bcf98-202">a.</span><span class="sxs-lookup"><span data-stu-id="bcf98-202">a.</span></span> <span data-ttu-id="bcf98-203">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bcf98-204">b.</span><span class="sxs-lookup"><span data-stu-id="bcf98-204">b.</span></span> <span data-ttu-id="bcf98-205">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="bcf98-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bcf98-206">c.</span><span class="sxs-lookup"><span data-stu-id="bcf98-206">c.</span></span> <span data-ttu-id="bcf98-207">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bcf98-208">d.</span><span class="sxs-lookup"><span data-stu-id="bcf98-208">d.</span></span> <span data-ttu-id="bcf98-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="bcf98-210">Criação de um usuário de teste do Intacct</span><span class="sxs-lookup"><span data-stu-id="bcf98-210">Creating an Intacct test user</span></span>

<span data-ttu-id="bcf98-211">Para configurar os usuários do Azure AD para que possam entrar no Intacct, eles devem ser provisionados no Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="bcf98-212">Para o Intacct, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="bcf98-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="bcf98-213">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bcf98-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="bcf98-214">Entre em seu locatário do **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="bcf98-215">Clique na guia **Empresa** e em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="bcf98-216">![Usuários](./media/active-directory-saas-intacct-tutorial/ic790041.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="bcf98-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="bcf98-217">Clique na guia **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="bcf98-218">![Adicionar](./media/active-directory-saas-intacct-tutorial/ic790042.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="bcf98-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="bcf98-219">Na seção **Informações do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="bcf98-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="bcf98-220">![Informações do Usuário](./media/active-directory-saas-intacct-tutorial/ic790043.png "informações do Usuário")</span><span class="sxs-lookup"><span data-stu-id="bcf98-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="bcf98-221">a.</span><span class="sxs-lookup"><span data-stu-id="bcf98-221">a.</span></span> <span data-ttu-id="bcf98-222">Insira a **ID de Usuário**, o **Sobrenome**, o **Nome**, o **Endereço de email**, o **Título** e o **Telefone** de uma conta do Azure AD que você deseja provisionar na seção **Informações do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="bcf98-223">b.</span><span class="sxs-lookup"><span data-stu-id="bcf98-223">b.</span></span> <span data-ttu-id="bcf98-224">Selecione os **privilégios de Administrador** de uma conta do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="bcf98-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="bcf98-225">c.</span><span class="sxs-lookup"><span data-stu-id="bcf98-225">c.</span></span> <span data-ttu-id="bcf98-226">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-226">Click **Save**.</span></span> <span data-ttu-id="bcf98-227">O titular da conta do Azure AD receberá um email e um link para confirmar sua conta antes de se tornar ativo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="bcf98-228">Para provisionar as contas de usuário do Azure AD, é possível usar qualquer outra ferramenta de criação da conta de usuário do Intacct ou APIs fornecidas pelo Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bcf98-229">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bcf98-230">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="bcf98-232">**Para atribuir Brenda Fernandes ao Intacct, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="bcf98-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="bcf98-233">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="bcf98-235">Na lista de aplicativos, selecione **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-235">In the applications list, select **Intacct**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="bcf98-237">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="bcf98-239">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bcf98-239">Click **Add** button.</span></span> <span data-ttu-id="bcf98-240">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="bcf98-242">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="bcf98-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bcf98-243">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bcf98-244">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bcf98-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bcf98-245">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="bcf98-245">Testing single sign-on</span></span>

<span data-ttu-id="bcf98-246">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="bcf98-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="bcf98-247">Ao clicar no bloco Intacct no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Intacct.</span><span class="sxs-lookup"><span data-stu-id="bcf98-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bcf98-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bcf98-248">Additional resources</span></span>

* [<span data-ttu-id="bcf98-249">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="bcf98-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bcf98-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bcf98-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

