---
title: "Tutorial: Integração do Azure Active Directory com o YouEarnedIt | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="38851-103">Tutorial: Integração do Azure Active Directory com o YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="38851-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="38851-104">Neste tutorial, você aprenderá a integrar o YouEarnedIt ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="38851-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38851-105">A integração do YouEarnedIt ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="38851-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38851-106">No Azure AD, você poderá controlar quem tem acesso ao YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="38851-107">Você pode permitir que os usuários conectem automaticamente no YouEarnedIt (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38851-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="38851-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="38851-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="38851-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38851-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38851-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38851-110">Prerequisites</span></span>

<span data-ttu-id="38851-111">Para configurar a integração do Azure AD com o YouEarnedIt, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="38851-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="38851-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38851-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38851-113">Uma assinatura habilitada para logon único do YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="38851-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38851-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="38851-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38851-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="38851-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38851-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="38851-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38851-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38851-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38851-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="38851-118">Scenario description</span></span>
<span data-ttu-id="38851-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="38851-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38851-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="38851-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38851-121">Adicionando o YouEarnedIt da galeria</span><span class="sxs-lookup"><span data-stu-id="38851-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="38851-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="38851-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="38851-123">Adicionando o YouEarnedIt da galeria</span><span class="sxs-lookup"><span data-stu-id="38851-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="38851-124">Para configurar a integração do YouEarnedIt ao Azure AD, você precisará adicionar o YouEarnedIt da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="38851-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38851-125">**Para adicionar o YouEarnedIt por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38851-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38851-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38851-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="38851-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="38851-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38851-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="38851-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="38851-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38851-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="38851-133">Na caixa de pesquisa, digite **YouEarnedt**, selecione  **YouEarnedt**  do painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="38851-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt na lista de resultados](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="38851-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38851-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="38851-136">Nesta seção, você configurará e testará o logon único do Azure AD com o YouEarnedIt, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="38851-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38851-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do YouEarnedIt é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38851-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="38851-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="38851-139">No YouEarnedIt, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="38851-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38851-140">Para configurar e testar o logon único do AD do Azure com o YouEarnedIt, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="38851-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38851-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="38851-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38851-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38851-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38851-143">**[Criar um usuário de teste do YouEarnedIt](#create-a-youearnedit-test-user)**: para ter um equivalente de Brenda Fernandes no YouEarnedIt que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38851-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38851-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38851-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38851-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="38851-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="38851-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38851-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="38851-147">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo do YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="38851-148">**Para configurar o logon único do Azure AD com o YouEarnedIt, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38851-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="38851-149">No portal do Azure, na página de integração de aplicativos do **YouEarnedIt**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="38851-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="38851-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="38851-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="38851-153">Na seção **Domínio e URLs do YouEarnedIt**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="38851-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="38851-155">a.</span><span class="sxs-lookup"><span data-stu-id="38851-155">a.</span></span> <span data-ttu-id="38851-156">Na caixa de texto **URL de Logon**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="38851-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="38851-157">Ambiente</span><span class="sxs-lookup"><span data-stu-id="38851-157">Environment</span></span>  | <span data-ttu-id="38851-158">Padrão</span><span class="sxs-lookup"><span data-stu-id="38851-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="38851-159">Produção</span><span class="sxs-lookup"><span data-stu-id="38851-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="38851-160">Área restrita</span><span class="sxs-lookup"><span data-stu-id="38851-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="38851-161">b.</span><span class="sxs-lookup"><span data-stu-id="38851-161">b.</span></span> <span data-ttu-id="38851-162">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="38851-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="38851-163">Ambiente</span><span class="sxs-lookup"><span data-stu-id="38851-163">Environment</span></span>  | <span data-ttu-id="38851-164">Padrão</span><span class="sxs-lookup"><span data-stu-id="38851-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="38851-165">Produção</span><span class="sxs-lookup"><span data-stu-id="38851-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="38851-166">Área restrita</span><span class="sxs-lookup"><span data-stu-id="38851-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="38851-167">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="38851-167">These values are not real.</span></span> <span data-ttu-id="38851-168">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="38851-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="38851-169">Contate a [equipe de suporte ao cliente do YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="38851-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="38851-170">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="38851-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="38851-172">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="38851-172">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38851-174">Na seção **Configuração do YouEarnedIt**, clique em **Configurar o YouEarnedIt** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="38851-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="38851-175">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="38851-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="38851-177">Para configurar o logon único no lado do **YouEarnedIt**, é necessário enviar o **Certificado (Base64)** baixado e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="38851-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="38851-178">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="38851-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="38851-179">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="38851-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38851-180">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="38851-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38851-181">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38851-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="38851-182">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38851-182">Create an Azure AD test user</span></span>

<span data-ttu-id="38851-183">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38851-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="38851-185">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38851-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38851-186">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38851-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="38851-188">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="38851-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="38851-190">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="38851-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="38851-192">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="38851-192">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="38851-194">a.</span><span class="sxs-lookup"><span data-stu-id="38851-194">a.</span></span> <span data-ttu-id="38851-195">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="38851-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38851-196">b.</span><span class="sxs-lookup"><span data-stu-id="38851-196">b.</span></span> <span data-ttu-id="38851-197">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="38851-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="38851-198">c.</span><span class="sxs-lookup"><span data-stu-id="38851-198">c.</span></span> <span data-ttu-id="38851-199">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="38851-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="38851-200">d.</span><span class="sxs-lookup"><span data-stu-id="38851-200">d.</span></span> <span data-ttu-id="38851-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="38851-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="38851-202">Criar um usuário de teste do YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="38851-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="38851-203">Nesta seção, você criará um usuário chamado Brenda Fernandes no YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="38851-204">Trabalhe com a equipe de suporte do YouEarnedIt para adicionar os usuários na plataforma do YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="38851-205">O YouEarnedIt espera que o Provedor de Identidade forneça um EmailAddress ou um UserName no atributo NameID.</span><span class="sxs-lookup"><span data-stu-id="38851-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="38851-206">A autenticação falhará se um UserName ou um EmailAddress correspondente não for encontrado no banco de dados ou se não for uma correspondência exata.</span><span class="sxs-lookup"><span data-stu-id="38851-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="38851-207">Isso exigirá que as contas sejam importadas para o sistema do YouEarnedIt antes da integração de SSO (normalmente por meio da importação de API ou CSV).</span><span class="sxs-lookup"><span data-stu-id="38851-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="38851-208">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="38851-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="38851-209">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo acesso ao YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="38851-211">**Para atribuir Brenda Fernandes ao YouEarnedIt, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="38851-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="38851-212">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="38851-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="38851-214">Na lista de aplicativos, selecione **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="38851-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![O link YouEarnedIt na lista de aplicativos](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="38851-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="38851-216">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="38851-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="38851-218">Click **Add** button.</span></span> <span data-ttu-id="38851-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38851-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="38851-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="38851-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38851-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38851-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38851-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="38851-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="38851-224">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="38851-224">Test single sign-on</span></span>

<span data-ttu-id="38851-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="38851-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38851-226">Quando você clicar no bloco do YouEarnedIt no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="38851-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="38851-227">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38851-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="38851-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="38851-228">Additional resources</span></span>

* [<span data-ttu-id="38851-229">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="38851-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38851-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38851-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

