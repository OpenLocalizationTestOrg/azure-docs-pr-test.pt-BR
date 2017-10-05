---
title: "Tutorial: integração do Azure Active Directory ao eDigitalResearch | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="e3824-103">Tutorial: integração do Azure Active Directory ao eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="e3824-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="e3824-104">Neste tutorial, você aprenderá a integrar o eDigitalResearch ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e3824-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3824-105">A integração do eDigitalResearch ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e3824-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e3824-106">No Azure AD, é possível controlar quem tem acesso ao eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="e3824-107">Você pode permitir que os usuários façam logon automaticamente no eDigitalResearch (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3824-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e3824-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3824-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e3824-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3824-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3824-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3824-110">Prerequisites</span></span>

<span data-ttu-id="e3824-111">Para configurar a integração do Azure AD com o eDigitalResearch, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e3824-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="e3824-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3824-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3824-113">Uma assinatura do eDigitalResearch habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="e3824-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3824-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e3824-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3824-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e3824-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3824-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e3824-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3824-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3824-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3824-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e3824-118">Scenario description</span></span>
<span data-ttu-id="e3824-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e3824-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3824-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e3824-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3824-121">Adicionando o eDigitalResearch da galeria</span><span class="sxs-lookup"><span data-stu-id="e3824-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="e3824-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e3824-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="e3824-123">Adicionando o eDigitalResearch da galeria</span><span class="sxs-lookup"><span data-stu-id="e3824-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="e3824-124">Para configurar a integração do eDigitalResearch ao Azure AD, você precisará adicionar o eDigitalResearch da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e3824-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3824-125">**Para adicionar o eDigitalResearch da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e3824-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3824-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3824-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="e3824-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e3824-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e3824-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e3824-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="e3824-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3824-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="e3824-133">Na caixa de pesquisa, digite **eDigitalResearch**, selecione **eDigitalResearch** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3824-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch na lista de resultados](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3824-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3824-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e3824-136">Nesta seção, você configurará e testará o logon único do Azure AD com o eDigitalResearch, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e3824-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3824-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do eDigitalResearch é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3824-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="e3824-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="e3824-139">No eDigitalResearch, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e3824-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e3824-140">Para configurar e testar o logon único do Azure AD com o eDigitalResearch, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e3824-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3824-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e3824-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3824-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e3824-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3824-143">**[Criar um usuário de teste eDigitalResearch](#create-a-edigitalresearch-test-user)** – para ter um equivalente de Brenda Fernandes no eDigitalResearch vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3824-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3824-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3824-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3824-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e3824-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3824-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3824-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e3824-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="e3824-148">**Para configurar o logon único do Azure AD com o eDigitalResearch, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e3824-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="e3824-149">No Portal do Azure, na página de integração de aplicativos do **eDigitalResearch**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e3824-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="e3824-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e3824-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="e3824-153">Na seção **Domínio e URLs do eDigitalResearch**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e3824-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="e3824-155">a.</span><span class="sxs-lookup"><span data-stu-id="e3824-155">a.</span></span> <span data-ttu-id="e3824-156">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="e3824-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="e3824-157">b.</span><span class="sxs-lookup"><span data-stu-id="e3824-157">b.</span></span> <span data-ttu-id="e3824-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="e3824-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3824-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e3824-159">These values are not real.</span></span> <span data-ttu-id="e3824-160">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="e3824-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e3824-161">Contate a [equipe de suporte do eDigitalResearch](http://www.maruedr.com/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="e3824-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="e3824-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado Base(64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e3824-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="e3824-163">!</span><span class="sxs-lookup"><span data-stu-id="e3824-163">!</span></span>![O link de download do Certificado](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="e3824-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e3824-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3824-167">Na seção **Configuração do eDigitalResearch**, clique em **Configurar o eDigitalResearch** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e3824-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e3824-168">Copie a **URL de Saída e a ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e3824-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuração do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="e3824-170">Para configurar o logon único no lado do **eDigitalResearch**, é necessário enviar o **Arquivo de Certificado (Base64)** baixado, a **ID da Entidade SAML** e a **URL de Saída** para a [equipe de suporte do eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="e3824-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="e3824-171">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="e3824-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e3824-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e3824-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e3824-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e3824-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e3824-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3824-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3824-175">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3824-175">Create an Azure AD test user</span></span>

<span data-ttu-id="e3824-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e3824-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="e3824-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e3824-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3824-179">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3824-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e3824-181">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e3824-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e3824-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="e3824-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e3824-185">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e3824-185">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e3824-187">a.</span><span class="sxs-lookup"><span data-stu-id="e3824-187">a.</span></span> <span data-ttu-id="e3824-188">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="e3824-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3824-189">b.</span><span class="sxs-lookup"><span data-stu-id="e3824-189">b.</span></span> <span data-ttu-id="e3824-190">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e3824-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e3824-191">c.</span><span class="sxs-lookup"><span data-stu-id="e3824-191">c.</span></span> <span data-ttu-id="e3824-192">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="e3824-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e3824-193">d.</span><span class="sxs-lookup"><span data-stu-id="e3824-193">d.</span></span> <span data-ttu-id="e3824-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3824-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="e3824-195">Criar um usuário de teste eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="e3824-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="e3824-196">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="e3824-197">Trabalhe com a [equipe de suporte do eDigitalResearch](http://www.maruedr.com/contact) para criar os usuários.</span><span class="sxs-lookup"><span data-stu-id="e3824-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="e3824-198">O titular da conta do Azure Active Directory recebe um email e segue um link para confirmar sua conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="e3824-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e3824-199">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3824-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="e3824-200">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="e3824-202">**Para atribuir Brenda Fernandes ao eDigitalResearch, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e3824-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="e3824-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e3824-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e3824-205">Na lista de aplicativos, selecione **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="e3824-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![O link eDigitalResearch na lista de Aplicativos](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="e3824-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e3824-207">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="e3824-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e3824-209">Click **Add** button.</span></span> <span data-ttu-id="e3824-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3824-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="e3824-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e3824-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e3824-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3824-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3824-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e3824-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e3824-215">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="e3824-215">Test single sign-on</span></span>

<span data-ttu-id="e3824-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e3824-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e3824-217">Quando você clica no bloco eDigitalResearch no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="e3824-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="e3824-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3824-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e3824-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e3824-219">Additional resources</span></span>

* [<span data-ttu-id="e3824-220">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e3824-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3824-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e3824-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

