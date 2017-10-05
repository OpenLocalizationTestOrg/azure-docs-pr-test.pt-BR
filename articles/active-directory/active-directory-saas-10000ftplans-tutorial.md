---
title: "Tutorial: Integração do Azure Active Directory ao 10,000ft Plans | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o 10,000ft Plans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="0b013-103">Tutorial: Integração do Azure Active Directory ao 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="0b013-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="0b013-104">Neste tutorial, você aprenderá a integrar o 10,000ft Plans ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0b013-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b013-105">A integração do 10,000ft Plans ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="0b013-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b013-106">Você pode controlar no Azure AD quem tem acesso ao 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="0b013-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="0b013-107">Você pode permitir que usuários façam logon automaticamente no 10,000ft Plans (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b013-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b013-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b013-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b013-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b013-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0b013-110">Prerequisites</span></span>

<span data-ttu-id="0b013-111">Para configurar a integração do Azure AD com o 10,000ft Plans, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0b013-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="0b013-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b013-113">Uma assinatura do 10,000ft Plans habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="0b013-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b013-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0b013-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b013-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0b013-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b013-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0b013-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b013-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b013-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b013-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0b013-118">Scenario description</span></span>
<span data-ttu-id="0b013-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0b013-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b013-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="0b013-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b013-121">Adicionar 10,000ft Plans pela galeria</span><span class="sxs-lookup"><span data-stu-id="0b013-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="0b013-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="0b013-123">Adicionar 10,000ft Plans pela galeria</span><span class="sxs-lookup"><span data-stu-id="0b013-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="0b013-124">Para configurar a integração do 10,000ft Plans ao Azure AD, você precisará adicionar o 10,000ft Plans d galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0b013-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b013-125">**Para adicionar o 10,000ft Plans da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0b013-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b013-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b013-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b013-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0b013-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b013-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0b013-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="0b013-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b013-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="0b013-133">Na caixa de pesquisa, digite **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="0b013-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="0b013-135">No painel de resultados, selecione **10,000ft Plans** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b013-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b013-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b013-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 10,000ft Plans com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="0b013-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b013-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do 10,000ft Plans é equivalente a um determinado usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b013-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="0b013-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="0b013-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="0b013-141">No 10,000ft Plans, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="0b013-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b013-142">Para configurar e testar o logon único do Azure AD com o 10,000ft Plans, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="0b013-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b013-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="0b013-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b013-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0b013-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b013-145">**[Criação de um usuário de teste do 10,000ft Plans](#creating-a-10000ft-plans-test-user)** – para ter um equivalente de Brenda Fernandes no 10,000ft Plans que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b013-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b013-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b013-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b013-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="0b013-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b013-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b013-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b013-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="0b013-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="0b013-150">**Para configurar o logon único do Azure AD com o 10,000ft Plans, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0b013-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="0b013-151">No Portal do Azure, na página de integração de aplicativo do **10,000ft Plans**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="0b013-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="0b013-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="0b013-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="0b013-155">Na seção **URLs e Domínio do 10,000ft Plans**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0b013-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="0b013-157">a.</span><span class="sxs-lookup"><span data-stu-id="0b013-157">a.</span></span> <span data-ttu-id="0b013-158">Na caixa de texto **URL de Logon**, digite a URL: `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="0b013-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="0b013-159">b.</span><span class="sxs-lookup"><span data-stu-id="0b013-159">b.</span></span> <span data-ttu-id="0b013-160">Na caixa de texto **Identificador**, digite a URL: `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="0b013-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b013-161">O valor de **Identificador** será diferente se você tiver um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="0b013-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="0b013-162">Entre em contato com a [equipe de suporte do 10,000ft Plans](https://www.10000ft.com/plans/support) para obter este valor.</span><span class="sxs-lookup"><span data-stu-id="0b013-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="0b013-163">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="0b013-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="0b013-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="0b013-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b013-167">Na seção **Configuração do 10,000ft Plans**, clique em **Configurar 10,000ft Plans** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="0b013-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b013-168">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="0b013-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="0b013-170">Para configurar o logon único no lado do **10,000ft Plans**, é necessário enviar o **Certificado (Bruto) baixado, a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** para a [equipe de suporte do 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="0b013-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="0b013-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="0b013-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b013-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0b013-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b013-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b013-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b013-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b013-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0b013-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="0b013-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0b013-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b013-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b013-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b013-180">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0b013-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b013-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0b013-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b013-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0b013-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b013-186">a.</span><span class="sxs-lookup"><span data-stu-id="0b013-186">a.</span></span> <span data-ttu-id="0b013-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="0b013-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b013-188">b.</span><span class="sxs-lookup"><span data-stu-id="0b013-188">b.</span></span> <span data-ttu-id="0b013-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="0b013-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b013-190">c.</span><span class="sxs-lookup"><span data-stu-id="0b013-190">c.</span></span> <span data-ttu-id="0b013-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="0b013-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b013-192">d.</span><span class="sxs-lookup"><span data-stu-id="0b013-192">d.</span></span> <span data-ttu-id="0b013-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0b013-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="0b013-194">Criando um usuário de teste do 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="0b013-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="0b013-195">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="0b013-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="0b013-196">O 10,000ft Plans dá suporte ao provisionamento Just-In-Time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="0b013-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="0b013-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="0b013-197">There is no action item for you in this section.</span></span> <span data-ttu-id="0b013-198">Um novo usuário será criado durante a tentativa de acessar o 10,000ft Plans se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="0b013-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b013-199">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="0b013-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b013-200">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b013-201">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="0b013-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="0b013-203">**Para atribuir Brenda Fernandes ao 10,000ft Plans, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="0b013-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="0b013-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="0b013-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="0b013-206">Na lista de aplicativos, selecione **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="0b013-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="0b013-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0b013-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="0b013-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0b013-210">Click **Add** button.</span></span> <span data-ttu-id="0b013-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0b013-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="0b013-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="0b013-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b013-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0b013-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b013-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0b013-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b013-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="0b013-216">Testing single sign-on</span></span>

<span data-ttu-id="0b013-217">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="0b013-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="0b013-218">Ao clicar no bloco 10,000ft Plans no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="0b013-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="0b013-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0b013-219">Additional resources</span></span>

* [<span data-ttu-id="0b013-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0b013-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b013-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b013-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

