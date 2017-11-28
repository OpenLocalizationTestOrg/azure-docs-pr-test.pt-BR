---
title: "Tutorial: integração do Azure Active Directory com o Workfront | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="ce518-103">Tutorial: integração do Azure Active Directory com o Workfront</span><span class="sxs-lookup"><span data-stu-id="ce518-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="ce518-104">Neste tutorial, você aprenderá a integrar o Workfront ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ce518-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce518-105">A integração do Workfront ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ce518-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce518-106">No Azure AD, é possível controlar quem tem acesso ao Workfront</span><span class="sxs-lookup"><span data-stu-id="ce518-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="ce518-107">Você pode permitir que seus usuários façam logon automaticamente no Workfront (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="ce518-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce518-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ce518-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce518-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce518-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ce518-110">Prerequisites</span></span>

<span data-ttu-id="ce518-111">Para configurar a integração do Azure AD com o Workfront, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ce518-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="ce518-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce518-113">Uma assinatura do Workfront com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="ce518-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce518-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ce518-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce518-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ce518-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce518-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ce518-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce518-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce518-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce518-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ce518-118">Scenario description</span></span>
<span data-ttu-id="ce518-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ce518-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce518-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ce518-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce518-121">Adicionar o Workfront a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="ce518-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="ce518-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="ce518-123">Adicionar o Workfront a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="ce518-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="ce518-124">Para configurar a integração do Workfront ao Azure AD, você precisará adicionar o Workfront da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ce518-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce518-125">**Para adicionar o Workfront por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce518-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce518-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce518-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce518-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ce518-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce518-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce518-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ce518-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce518-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ce518-133">Na caixa de pesquisa, digite **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="ce518-133">In the search box, type **Workfront**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="ce518-135">No painel de resultados, selecione **Workfront** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce518-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce518-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce518-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Workfront com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="ce518-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce518-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Workfront é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce518-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="ce518-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Workfront.</span><span class="sxs-lookup"><span data-stu-id="ce518-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="ce518-141">No Workfront, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ce518-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ce518-142">Para configurar e testar o logon único do Azure AD com o Workfront, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ce518-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce518-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ce518-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce518-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce518-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce518-145">**[Criação de um usuário de teste do Workfront](#creating-a-workfront-test-user)** – para ter um equivalente de Brenda Fernandes no Workfront que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce518-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce518-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce518-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce518-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ce518-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce518-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce518-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce518-149">Nesta seção, você vai habilitar o logon único do Azure AD no Portal do Azure e configurar o logon único em seu aplicativo Workfront.</span><span class="sxs-lookup"><span data-stu-id="ce518-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="ce518-150">**Para configurar o logon único do Azure AD com o Workfront, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce518-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ce518-151">No Portal do Azure, na página de integração de aplicativos do **Workfront**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ce518-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ce518-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ce518-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="ce518-155">Na seção **URLs e Domínio do Workfront**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ce518-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="ce518-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce518-157">a.</span></span> <span data-ttu-id="ce518-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="ce518-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="ce518-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce518-159">b.</span></span> <span data-ttu-id="ce518-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="ce518-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce518-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ce518-161">These values are not real.</span></span> <span data-ttu-id="ce518-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="ce518-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ce518-163">Contate a [equipe de suporte do Cliente Workfront](https://www.workfront.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="ce518-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="ce518-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ce518-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="ce518-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ce518-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce518-168">Na seção **Configuração do Workfront**, clique em **Configurar Workfront** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ce518-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ce518-169">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ce518-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="ce518-171">Faça logon no site da empresa Workfront como administrador.</span><span class="sxs-lookup"><span data-stu-id="ce518-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="ce518-172">Vá para **Configuração de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ce518-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="ce518-173">Na caixa de diálogo **Logon Único** , realize as seguintes etapas</span><span class="sxs-lookup"><span data-stu-id="ce518-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="ce518-175">a.</span><span class="sxs-lookup"><span data-stu-id="ce518-175">a.</span></span> <span data-ttu-id="ce518-176">Como **Tipo**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ce518-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="ce518-177">b.</span><span class="sxs-lookup"><span data-stu-id="ce518-177">b.</span></span> <span data-ttu-id="ce518-178">Selecione **ID do Provedor de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="ce518-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="ce518-179">c.</span><span class="sxs-lookup"><span data-stu-id="ce518-179">c.</span></span> <span data-ttu-id="ce518-180">Cole a **URL do Serviço de Logon Único SAML** na caixa de texto **URL do Portal de Logon**.</span><span class="sxs-lookup"><span data-stu-id="ce518-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="ce518-181">d.</span><span class="sxs-lookup"><span data-stu-id="ce518-181">d.</span></span> <span data-ttu-id="ce518-182">Cole a **URL do Serviço de Logoff Único** na caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="ce518-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="ce518-183">e.</span><span class="sxs-lookup"><span data-stu-id="ce518-183">e.</span></span> <span data-ttu-id="ce518-184">Cole a **URL de Alteração de Senha** na caixa de texto **URL de Alteração de Senha**.</span><span class="sxs-lookup"><span data-stu-id="ce518-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="ce518-185">f.</span><span class="sxs-lookup"><span data-stu-id="ce518-185">f.</span></span> <span data-ttu-id="ce518-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ce518-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ce518-187">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ce518-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ce518-188">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ce518-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ce518-189">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce518-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce518-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce518-191">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce518-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ce518-193">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce518-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce518-194">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce518-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce518-196">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ce518-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce518-198">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce518-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce518-200">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ce518-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce518-202">a.</span><span class="sxs-lookup"><span data-stu-id="ce518-202">a.</span></span> <span data-ttu-id="ce518-203">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ce518-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce518-204">b.</span><span class="sxs-lookup"><span data-stu-id="ce518-204">b.</span></span> <span data-ttu-id="ce518-205">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce518-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce518-206">c.</span><span class="sxs-lookup"><span data-stu-id="ce518-206">c.</span></span> <span data-ttu-id="ce518-207">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ce518-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ce518-208">d.</span><span class="sxs-lookup"><span data-stu-id="ce518-208">d.</span></span> <span data-ttu-id="ce518-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ce518-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="ce518-210">Criar um usuário de teste do Workfront</span><span class="sxs-lookup"><span data-stu-id="ce518-210">Creating a Workfront test user</span></span>

<span data-ttu-id="ce518-211">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Workfront.</span><span class="sxs-lookup"><span data-stu-id="ce518-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="ce518-212">**Para criar um usuário chamado Brenda Fernandes no Workfront, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce518-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ce518-213">Faça logon no site da empresa Workfront como administrador.</span><span class="sxs-lookup"><span data-stu-id="ce518-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="ce518-214">No menu na parte superior, clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="ce518-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="ce518-215">Clique em **Nova Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="ce518-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="ce518-216">Na caixa de diálogo Nova Pessoa, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ce518-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Criar um usuário de teste do Workfront][21] 
   
    <span data-ttu-id="ce518-218">a.</span><span class="sxs-lookup"><span data-stu-id="ce518-218">a.</span></span> <span data-ttu-id="ce518-219">Na caixa de texto **Nome**, digite "Brenda".</span><span class="sxs-lookup"><span data-stu-id="ce518-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="ce518-220">b.</span><span class="sxs-lookup"><span data-stu-id="ce518-220">b.</span></span> <span data-ttu-id="ce518-221">Na caixa de texto **Sobrenome**, digite "Fernandes".</span><span class="sxs-lookup"><span data-stu-id="ce518-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="ce518-222">c.</span><span class="sxs-lookup"><span data-stu-id="ce518-222">c.</span></span> <span data-ttu-id="ce518-223">Na caixa de texto **Endereço de Email** , digite o endereço de email de Brenda Fernandes no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce518-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="ce518-224">d.</span><span class="sxs-lookup"><span data-stu-id="ce518-224">d.</span></span> <span data-ttu-id="ce518-225">Clique em **Adicionar Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="ce518-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ce518-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ce518-227">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Workfront.</span><span class="sxs-lookup"><span data-stu-id="ce518-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ce518-229">**Para atribuir Brenda Fernandes ao Workfront, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce518-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ce518-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce518-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ce518-232">Na lista de aplicativos, escolha **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="ce518-232">In the applications list, select **Workfront**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="ce518-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce518-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ce518-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ce518-236">Click **Add** button.</span></span> <span data-ttu-id="ce518-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce518-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ce518-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ce518-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce518-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce518-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce518-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce518-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce518-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ce518-242">Testing single sign-on</span></span>

<span data-ttu-id="ce518-243">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ce518-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce518-244">Ao clicar no bloco Workfront no Painel de Acesso, você deverá acessar a página de logon do aplicativo Workfront.</span><span class="sxs-lookup"><span data-stu-id="ce518-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="ce518-245">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce518-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ce518-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ce518-246">Additional resources</span></span>

* [<span data-ttu-id="ce518-247">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ce518-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce518-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce518-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

