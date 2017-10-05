---
title: "Tutorial: integração do Azure Active Directory com Yonyx Interactive Guides | Microsoft Docs"
description: "Saiba como configurar logon único entre o Azure Active Directory e Yonyx Interactive Guides."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 522f440a0b3746e1101aed845678b3930e030fec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="ce80c-103">Tutorial: Integração do Azure Active Directory com Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="ce80c-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="ce80c-104">Neste tutorial, você aprende a integrar o Yonyx Interactive Guides ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ce80c-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce80c-105">Integrar Yonyx Interactive Guides ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ce80c-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce80c-106">Você pode controlar no Azure AD quem tem acesso a Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="ce80c-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
- <span data-ttu-id="ce80c-107">Você pode habilitar seus usuários a entrar automaticamente em Yonyx Interactive Guides (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce80c-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce80c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce80c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ce80c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce80c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce80c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ce80c-110">Prerequisites</span></span>

<span data-ttu-id="ce80c-111">Para configurar a integração do Azure AD com Yonyx Interactive Guides, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ce80c-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

- <span data-ttu-id="ce80c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce80c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce80c-113">Uma assinatura do Yonyx Interactive Guides habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ce80c-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce80c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ce80c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce80c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ce80c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce80c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ce80c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce80c-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce80c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce80c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ce80c-118">Scenario description</span></span>
<span data-ttu-id="ce80c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ce80c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce80c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ce80c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce80c-121">Adicionando Yonyx Interactive Guides da galeria</span><span class="sxs-lookup"><span data-stu-id="ce80c-121">Adding Yonyx Interactive Guides from the gallery</span></span>
2. <span data-ttu-id="ce80c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce80c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="ce80c-123">Adicionando Yonyx Interactive Guides da galeria</span><span class="sxs-lookup"><span data-stu-id="ce80c-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="ce80c-124">Para configurar a integração de Yonyx Interactive Guides no Azure AD, é preciso adicionar Yonyx Interactive Guides da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ce80c-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce80c-125">**Para adicionar Yonyx Interactive Guides da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce80c-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce80c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="ce80c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce80c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="ce80c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="ce80c-133">Na caixa de pesquisa, digite **Yonyx Interactive Guides**, selecione **Yonyx Interactive Guides** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span></span>

    ![Yonyx Interactive Guides na lista de resultados](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ce80c-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce80c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ce80c-136">Nesta seção, você configura e testa o logon único do Azure AD com o Yonyx Interactive Guides, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ce80c-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce80c-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Yonyx Interactive Guides é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce80c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span></span> <span data-ttu-id="ce80c-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="ce80c-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="ce80c-139">No Yonyx Interactive Guides, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ce80c-140">Para configurar e testar o logon único do Azure AD com Yonyx Interactive Guides, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ce80c-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce80c-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ce80c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce80c-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce80c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce80c-143">**[Criar um usuário de teste do Yonyx Interactive Guides](#create-a-yonyx-interactive-guides-test-user)** – para ter um equivalente de Brenda Fernandes no Yonyx Interactive Guides vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce80c-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce80c-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce80c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce80c-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ce80c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ce80c-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce80c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ce80c-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="ce80c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="ce80c-148">**Para configurar o logon único do Azure AD com Yonyx Interactive Guides, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce80c-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="ce80c-149">No portal do Azure, na página de integração do aplicativo **Yonyx Interactive Guides**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="ce80c-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ce80c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="ce80c-153">Na seção **Domínio e URLs do Yonyx Interactive Guides**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ce80c-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="ce80c-155">a.</span><span class="sxs-lookup"><span data-stu-id="ce80c-155">a.</span></span> <span data-ttu-id="ce80c-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="ce80c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="ce80c-157">b.</span><span class="sxs-lookup"><span data-stu-id="ce80c-157">b.</span></span> <span data-ttu-id="ce80c-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="ce80c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce80c-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ce80c-159">These values are not real.</span></span> <span data-ttu-id="ce80c-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="ce80c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ce80c-161">Contate a [equipe de suporte ao Cliente do Yonyx Interactive Guides](mailto:support@yonyx.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="ce80c-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span></span> 
 
4. <span data-ttu-id="ce80c-162">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="ce80c-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="ce80c-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ce80c-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce80c-166">Na seção **Configuração do Yonyx Interactive Guides**, clique em **Configurar o Yonyx Interactive Guides** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ce80c-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ce80c-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Yonyx Interactive Guides](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="ce80c-169">Para configurar o logon único no lado do **Yonyx Interactive Guides**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída**, a **URL do Serviço de Logon Único SAML** e a **ID da Entidade SAML** para A [equipe de suporte do Yonyx Interactive Guides](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="ce80c-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="ce80c-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="ce80c-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ce80c-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ce80c-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ce80c-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ce80c-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ce80c-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce80c-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ce80c-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce80c-174">Create an Azure AD test user</span></span>

<span data-ttu-id="ce80c-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce80c-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

  ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="ce80c-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce80c-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce80c-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce80c-180">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ce80c-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce80c-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce80c-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ce80c-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce80c-186">a.</span><span class="sxs-lookup"><span data-stu-id="ce80c-186">a.</span></span> <span data-ttu-id="ce80c-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce80c-188">b.</span><span class="sxs-lookup"><span data-stu-id="ce80c-188">b.</span></span> <span data-ttu-id="ce80c-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ce80c-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce80c-190">c.</span><span class="sxs-lookup"><span data-stu-id="ce80c-190">c.</span></span> <span data-ttu-id="ce80c-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ce80c-192">d.</span><span class="sxs-lookup"><span data-stu-id="ce80c-192">d.</span></span> <span data-ttu-id="ce80c-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="ce80c-194">Criar um usuário de teste do Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="ce80c-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="ce80c-195">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="ce80c-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="ce80c-196">O Yonyx Interactive Guides dá suporte a provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="ce80c-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ce80c-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ce80c-197">There is no action item for you in this section.</span></span> <span data-ttu-id="ce80c-198">Um novo usuário será criado durante a tentativa de acessar o Yonyx Interactive Guides, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="ce80c-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ce80c-199">Se precisar criar um usuário manualmente, contate a equipe de suporte do Yonyx Interactive Guides pelo email <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="ce80c-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ce80c-200">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce80c-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="ce80c-201">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="ce80c-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="ce80c-203">**Para atribuir Brenda Fernandes ao Yonyx Interactive Guides, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ce80c-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="ce80c-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ce80c-206">Na lista de aplicativos, selecione **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-206">In the applications list, select **Yonyx Interactive Guides**.</span></span>

    ![O link do Yonyx Interactive Guides na lista de Aplicativos](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="ce80c-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-208">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="ce80c-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ce80c-210">Click **Add** button.</span></span> <span data-ttu-id="ce80c-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="ce80c-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ce80c-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce80c-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce80c-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce80c-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ce80c-216">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="ce80c-216">Test single sign-on</span></span>

<span data-ttu-id="ce80c-217">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ce80c-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce80c-218">Ao clicar no bloco Yonyx Interactive Guides no Painel de Acesso, você deverá entrar automaticamente no aplicativo Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="ce80c-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="ce80c-219">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce80c-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce80c-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ce80c-220">Additional resources</span></span>

* [<span data-ttu-id="ce80c-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ce80c-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce80c-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce80c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

