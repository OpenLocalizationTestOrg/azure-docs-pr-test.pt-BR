---
title: "Tutorial: Integração do Azure Active Directory ao Predictix Ordering | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Predictix Ordering."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2fe2f976-e97f-4368-9695-3e1624409e8b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8536a741f9b114ac6787c7aefb4c76ec6c4ed83e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-ordering"></a><span data-ttu-id="68b37-103">Tutorial: Integração do Azure Active Directory com o Predictix Ordering</span><span class="sxs-lookup"><span data-stu-id="68b37-103">Tutorial: Azure Active Directory integration with Predictix Ordering</span></span>

<span data-ttu-id="68b37-104">Neste tutorial, você aprenderá como integrar o Predictix Ordering ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="68b37-104">In this tutorial, you learn how to integrate Predictix Ordering with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68b37-105">Integração do Predictix Ordering com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="68b37-105">Integrating Predictix Ordering with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68b37-106">Você pode controlar no Azure AD quem tem acesso ao Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-106">You can control in Azure AD who has access to Predictix Ordering.</span></span>
- <span data-ttu-id="68b37-107">Você pode permitir que seus usuários façam logon automaticamente no Predictix Ordering (logon único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68b37-107">You can enable your users to automatically get signed-on to Predictix Ordering (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="68b37-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68b37-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="68b37-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68b37-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68b37-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68b37-110">Prerequisites</span></span>

<span data-ttu-id="68b37-111">Para configurar a integração do Azure AD ao Predictix Ordering, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="68b37-111">To configure Azure AD integration with Predictix Ordering, you need the following items:</span></span>

- <span data-ttu-id="68b37-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68b37-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68b37-113">Uma assinatura habilitada do Predictix Ordering com logon único</span><span class="sxs-lookup"><span data-stu-id="68b37-113">A Predictix Ordering single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68b37-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="68b37-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68b37-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="68b37-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68b37-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="68b37-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68b37-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68b37-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68b37-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="68b37-118">Scenario description</span></span>
<span data-ttu-id="68b37-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="68b37-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68b37-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="68b37-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68b37-121">Adição do Predictix Ordering da galeria</span><span class="sxs-lookup"><span data-stu-id="68b37-121">Adding Predictix Ordering from the gallery</span></span>
2. <span data-ttu-id="68b37-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="68b37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-ordering-from-the-gallery"></a><span data-ttu-id="68b37-123">Adição do Predictix Ordering da galeria</span><span class="sxs-lookup"><span data-stu-id="68b37-123">Adding Predictix Ordering from the gallery</span></span>
<span data-ttu-id="68b37-124">Para configurar a integração do Predictix Ordering ao Azure AD, você precisa adicionar o Predictix Ordering da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="68b37-124">To configure the integration of Predictix Ordering into Azure AD, you need to add Predictix Ordering from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68b37-125">**Para adicionar o Predictix Ordering da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="68b37-125">**To add Predictix Ordering from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68b37-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68b37-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="68b37-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="68b37-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68b37-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="68b37-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="68b37-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68b37-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="68b37-133">Na caixa de pesquisa, digite **Predictix Ordering**, selecione **Predictix Ordering** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68b37-133">In the search box, type **Predictix Ordering**, select **Predictix Ordering** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix Ordering na lista de resultados](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="68b37-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b37-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="68b37-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Predictix Ordering, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="68b37-136">In this section, you configure and test Azure AD single sign-on with Predictix Ordering based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68b37-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Predictix Ordering é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68b37-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Ordering is to a user in Azure AD.</span></span> <span data-ttu-id="68b37-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Ordering needs to be established.</span></span>

<span data-ttu-id="68b37-139">No Predictix Ordering, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="68b37-139">In Predictix Ordering, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68b37-140">Para configurar e testar o logon único do Azure AD com o Predictix Ordering, conclua os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="68b37-140">To configure and test Azure AD single sign-on with Predictix Ordering, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68b37-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="68b37-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68b37-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="68b37-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68b37-143">**[Criar um usuário de teste Predictix Ordering](#create-a-predictix-ordering-test-user)** – para ter um equivalente de Brenda Fernandes no Predictix Ordering vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68b37-143">**[Create a Predictix Ordering test user](#create-a-predictix-ordering-test-user)** - to have a counterpart of Britta Simon in Predictix Ordering that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68b37-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68b37-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68b37-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="68b37-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="68b37-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b37-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="68b37-147">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Ordering application.</span></span>

<span data-ttu-id="68b37-148">**Para configurar o logon único do Azure AD com o Predictix Ordering, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="68b37-148">**To configure Azure AD single sign-on with Predictix Ordering, perform the following steps:**</span></span>

1. <span data-ttu-id="68b37-149">No portal do Azure, na página de integração de aplicativos do **Predictix Ordering**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="68b37-149">In the Azure portal, on the **Predictix Ordering** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="68b37-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="68b37-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_samlbase.png)

3. <span data-ttu-id="68b37-153">Na seção **URLs e Domínio do Predictix Ordering**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="68b37-153">On the **Predictix Ordering Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do Predictix Ordering](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_url.png)

    <span data-ttu-id="68b37-155">a.</span><span class="sxs-lookup"><span data-stu-id="68b37-155">a.</span></span> <span data-ttu-id="68b37-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname-pricing>.ordering.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="68b37-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname-pricing>.ordering.predictix.com/sso/request`</span></span>

    <span data-ttu-id="68b37-157">b.</span><span class="sxs-lookup"><span data-stu-id="68b37-157">b.</span></span> <span data-ttu-id="68b37-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="68b37-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<companyname-pricing>.dev.ordering.predictix.com` |
    | `https://<companyname-pricing>.ordering.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="68b37-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="68b37-159">These values are not real.</span></span> <span data-ttu-id="68b37-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="68b37-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="68b37-161">Entre em contato com a [equipe de suporte do Cliente do Predictix Ordering](https://www.predix.io/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="68b37-161">Contact [Predictix Ordering Client support team](https://www.predix.io/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="68b37-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="68b37-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_certificate.png) 

5. <span data-ttu-id="68b37-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="68b37-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-predictixordering-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="68b37-166">Na seção **Configuração do Predictix Ordering**, clique em **Configurar Predictix Ordering** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="68b37-166">On the **Predictix Ordering Configuration** section, click **Configure Predictix Ordering** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68b37-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="68b37-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Predictix Ordering](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_configure.png) 

7. <span data-ttu-id="68b37-169">Para configurar o logon único no lado do **Predictix Ordering**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** para a [equipe de suporte do Predictix Ordering](https://www.predix.io/support/).</span><span class="sxs-lookup"><span data-stu-id="68b37-169">To configure single sign-on on **Predictix Ordering** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Predictix Ordering support team](https://www.predix.io/support/).</span></span> <span data-ttu-id="68b37-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="68b37-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="68b37-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="68b37-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68b37-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="68b37-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68b37-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68b37-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="68b37-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b37-174">Create an Azure AD test user</span></span>
<span data-ttu-id="68b37-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="68b37-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="68b37-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="68b37-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68b37-178">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68b37-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="68b37-180">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="68b37-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="68b37-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="68b37-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="68b37-184">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="68b37-184">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-predictixordering-tutorial/create_aaduser_04.png)

   <span data-ttu-id="68b37-186">a.</span><span class="sxs-lookup"><span data-stu-id="68b37-186">a.</span></span> <span data-ttu-id="68b37-187">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="68b37-187">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="68b37-188">b.</span><span class="sxs-lookup"><span data-stu-id="68b37-188">b.</span></span> <span data-ttu-id="68b37-189">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="68b37-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="68b37-190">c.</span><span class="sxs-lookup"><span data-stu-id="68b37-190">c.</span></span> <span data-ttu-id="68b37-191">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="68b37-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="68b37-192">d.</span><span class="sxs-lookup"><span data-stu-id="68b37-192">d.</span></span> <span data-ttu-id="68b37-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="68b37-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-ordering-test-user"></a><span data-ttu-id="68b37-194">Criar um usuário de teste do Predictix Ordering</span><span class="sxs-lookup"><span data-stu-id="68b37-194">Create a Predictix Ordering test user</span></span>

<span data-ttu-id="68b37-195">Nesta seção, você criará um usuário chamado Brenda Fernandes no Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-195">In this section, you create a user called Britta Simon in Predictix Ordering.</span></span> <span data-ttu-id="68b37-196">Trabalhe com a [equipe de suporte do Predictix Ordering](https://www.predix.io/support/) para adicionar os usuários à plataforma Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-196">Work with [Predictix Ordering support team](https://www.predix.io/support/) to add the users in the Predictix Ordering platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="68b37-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68b37-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="68b37-198">Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo acesso ao Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Ordering.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="68b37-200">**Para atribuir Brenda Fernandes ao Predictix Ordering, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="68b37-200">**To assign Britta Simon to Predictix Ordering, perform the following steps:**</span></span>

1. <span data-ttu-id="68b37-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="68b37-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="68b37-203">Na lista de aplicativos, selecione **Predictix Ordering**.</span><span class="sxs-lookup"><span data-stu-id="68b37-203">In the applications list, select **Predictix Ordering**.</span></span>

    ![Link do Predictix Ordering na lista de aplicativos](./media/active-directory-saas-predictixordering-tutorial/tutorial_predictixordering_app.png)  

3. <span data-ttu-id="68b37-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="68b37-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="68b37-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="68b37-207">Click **Add** button.</span></span> <span data-ttu-id="68b37-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68b37-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="68b37-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="68b37-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68b37-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68b37-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68b37-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="68b37-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="68b37-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="68b37-213">Test single sign-on</span></span>

<span data-ttu-id="68b37-214">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="68b37-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="68b37-215">Quando você clica no bloco Predictix Ordering no Painel de Acesso, deve ser conectado automaticamente ao seu aplicativo Predictix Ordering.</span><span class="sxs-lookup"><span data-stu-id="68b37-215">When you click the Predictix Ordering tile in the Access Panel, you should get automatically signed-on to your Predictix Ordering application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="68b37-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="68b37-216">Additional resources</span></span>

* [<span data-ttu-id="68b37-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="68b37-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68b37-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="68b37-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixordering-tutorial/tutorial_general_203.png

