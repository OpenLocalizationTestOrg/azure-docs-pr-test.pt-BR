---
title: "Tutorial: integração do Azure Active Directory ao Predictix Price Reporting | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Predictix Price Reporting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 62280b205f2fd691e8c75134585172b995377311
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="9f845-103">Tutorial: integração do Azure Active Directory ao Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="9f845-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="9f845-104">Neste tutorial, você aprenderá como integrar o Predictix Price Reporting ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9f845-104">In this tutorial, you learn how to integrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f845-105">a integração do Predictix Price Reporting com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9f845-105">Integrating Predictix Price Reporting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9f845-106">No Azure AD, é possível controlar quem tem acesso ao Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-106">You can control in Azure AD who has access to Predictix Price Reporting.</span></span>
- <span data-ttu-id="9f845-107">Você pode permitir que seus usuários façam logon automaticamente no Predictix Price Reporting usando logon único com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f845-107">You can enable your users to automatically get signed-on to Predictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9f845-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f845-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9f845-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f845-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f845-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f845-110">Prerequisites</span></span>

<span data-ttu-id="9f845-111">Para configurar a integração do AD do Azure ao Predictix Price Reporting, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9f845-111">To configure Azure AD integration with Predictix Price Reporting, you need the following items:</span></span>

- <span data-ttu-id="9f845-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f845-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f845-113">Uma assinatura do Predictix Price Reporting habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="9f845-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f845-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f845-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f845-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f845-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f845-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f845-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f845-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f845-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f845-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f845-118">Scenario description</span></span>
<span data-ttu-id="9f845-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f845-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f845-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9f845-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f845-121">Adicionando Predictix Price Reporting da galeria</span><span class="sxs-lookup"><span data-stu-id="9f845-121">Adding Predictix Price Reporting from the gallery</span></span>
2. <span data-ttu-id="9f845-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f845-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-the-gallery"></a><span data-ttu-id="9f845-123">Adicionando Predictix Price Reporting da galeria</span><span class="sxs-lookup"><span data-stu-id="9f845-123">Adding Predictix Price Reporting from the gallery</span></span>
<span data-ttu-id="9f845-124">Para configurar a integração do Predictix Price Reporting ao Azure AD, você precisa adicionar o Predictix Price Reporting da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9f845-124">To configure the integration of Predictix Price Reporting into Azure AD, you need to add Predictix Price Reporting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9f845-125">**Para adicionar o Predictix Price Reporting da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f845-125">**To add Predictix Price Reporting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9f845-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f845-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="9f845-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f845-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9f845-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f845-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="9f845-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f845-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="9f845-133">Na caixa de pesquisa, digite **Predictix Price Reporting**, selecione **Predictix Price Reporting** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f845-133">In the search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button to add the application.</span></span>

    ![Price Reporting na lista de resultados](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9f845-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f845-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9f845-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Predictix Price Reporting, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="9f845-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f845-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Predictix Price Reporting é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f845-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Price Reporting is to a user in Azure AD.</span></span> <span data-ttu-id="9f845-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Price Reporting needs to be established.</span></span>

<span data-ttu-id="9f845-139">No Predictix Price Reporting, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9f845-139">In Predictix Price Reporting, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9f845-140">Para configurar e testar o logon único do Azure AD com o Predictix Price Reporting, conclua os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9f845-140">To configure and test Azure AD single sign-on with Predictix Price Reporting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9f845-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f845-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9f845-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f845-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f845-143">**[Criar um usuário de teste do Predictix Price Reporting](#create-a-predictix-price-reporting-test-user)** – para ter um equivalente de Brenda Fernandes no Predictix Price Reporting vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f845-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in Predictix Price Reporting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f845-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f845-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f845-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9f845-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9f845-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f845-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9f845-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="9f845-148">**Para configurar o logon único do Azure AD com o Predictix Price Reporting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f845-148">**To configure Azure AD single sign-on with Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="9f845-149">No Portal do Azure, na página de integração do aplicativo **Predictix Price Reporting**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f845-149">In the Azure portal, on the **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="9f845-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9f845-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="9f845-153">Na seção **Domínio e URLs do Predictix Price Reporting**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f845-153">On the **Predictix Price Reporting Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="9f845-155">a.</span><span class="sxs-lookup"><span data-stu-id="9f845-155">a.</span></span> <span data-ttu-id="9f845-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="9f845-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="9f845-157">b.</span><span class="sxs-lookup"><span data-stu-id="9f845-157">b.</span></span> <span data-ttu-id="9f845-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="9f845-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="9f845-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9f845-159">These values are not real.</span></span> <span data-ttu-id="9f845-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="9f845-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9f845-161">Entre em contato com a [equipe de suporte ao cliente do Predictix Price Reporting](http://www.infor.com/company/customer-center/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9f845-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) to get these values.</span></span> 
 
4. <span data-ttu-id="9f845-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9f845-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="9f845-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f845-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f845-166">Na seção **Configuração do Predictix Price Reporting**, clique em **Configurar Predictix Price Reporting** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="9f845-166">On the **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9f845-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="9f845-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="9f845-169">Para configurar o logon único no lado do **Predictix Price Reporting**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** para a [equipe de suporte do Predictix Price Reporting](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="9f845-169">To configure single sign-on on **Predictix Price Reporting** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="9f845-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="9f845-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9f845-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9f845-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9f845-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9f845-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9f845-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f845-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9f845-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f845-174">Create an Azure AD test user</span></span>

<span data-ttu-id="9f845-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f845-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="9f845-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f845-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9f845-178">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f845-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9f845-180">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f845-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9f845-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="9f845-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9f845-184">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f845-184">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9f845-186">a.</span><span class="sxs-lookup"><span data-stu-id="9f845-186">a.</span></span> <span data-ttu-id="9f845-187">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="9f845-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f845-188">b.</span><span class="sxs-lookup"><span data-stu-id="9f845-188">b.</span></span> <span data-ttu-id="9f845-189">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f845-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9f845-190">c.</span><span class="sxs-lookup"><span data-stu-id="9f845-190">c.</span></span> <span data-ttu-id="9f845-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="9f845-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9f845-192">d.</span><span class="sxs-lookup"><span data-stu-id="9f845-192">d.</span></span> <span data-ttu-id="9f845-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f845-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="9f845-194">Criar um usuário de teste do Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="9f845-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="9f845-195">Nesta seção, você criará um usuário chamado Britta Simon no Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="9f845-196">Trabalhe com a [equipe de suporte do Predictix Price Reporting](http://www.infor.com/company/customer-center/) para adicionar os usuários à plataforma Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) to add the users in the Predictix Price Reporting platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9f845-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f845-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="9f845-198">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Price Reporting.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="9f845-200">**Para atribuir Brenda Fernandes ao Predictix Price Reporting, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f845-200">**To assign Britta Simon to Predictix Price Reporting, perform the following steps:**</span></span>

1. <span data-ttu-id="9f845-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f845-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f845-203">Na lista de aplicativos, selecione **Predictix Price Reporting**.</span><span class="sxs-lookup"><span data-stu-id="9f845-203">In the applications list, select **Predictix Price Reporting**.</span></span>

    ![O link do Predictix Price Reporting na lista de Aplicativos](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="9f845-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f845-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="9f845-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f845-207">Click **Add** button.</span></span> <span data-ttu-id="9f845-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f845-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="9f845-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f845-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9f845-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f845-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f845-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f845-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9f845-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="9f845-213">Test single sign-on</span></span>

<span data-ttu-id="9f845-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9f845-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9f845-215">Quando você clica no bloco Predictix Price Reporting no Painel de Acesso, deve ser conectado automaticamente ao seu aplicativo Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="9f845-215">When you click the Predictix Price Reporting tile in the Access Panel, you should get automatically signed-on to your Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f845-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f845-216">Additional resources</span></span>

* [<span data-ttu-id="9f845-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f845-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f845-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f845-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

