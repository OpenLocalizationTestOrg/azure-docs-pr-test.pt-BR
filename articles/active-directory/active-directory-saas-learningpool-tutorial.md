---
title: "Tutorial: integração do Azure Active Directory com o Learningpool Act | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="3ed00-103">Tutorial: integração do Azure Active Directory com o Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="3ed00-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="3ed00-104">Neste tutorial, você aprenderá a integrar o Learningpool Act ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3ed00-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ed00-105">A integração do Learningpool Act com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3ed00-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ed00-106">Você pode controlar no Azure AD quem tem acesso ao Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="3ed00-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="3ed00-107">Você pode habilitar que usuários façam logon automaticamente no Learningpool Act (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ed00-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ed00-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ed00-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ed00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ed00-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ed00-110">Prerequisites</span></span>

<span data-ttu-id="3ed00-111">Para configurar a integração do Azure AD ao Learningpool Act, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3ed00-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="3ed00-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ed00-113">Uma assinatura com logon único habilitado do Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="3ed00-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ed00-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3ed00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ed00-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3ed00-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ed00-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3ed00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ed00-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ed00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ed00-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3ed00-118">Scenario description</span></span>
<span data-ttu-id="3ed00-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3ed00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ed00-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3ed00-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ed00-121">Como adicionar o Learningpool Act por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="3ed00-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="3ed00-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="3ed00-123">Como adicionar o Learningpool Act por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="3ed00-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="3ed00-124">Para configurar a integração do Learningpool Act ao Azure AD, você precisará adicionar o Learningpool Act por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3ed00-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ed00-125">**Para adicionar o Learningpool Act por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3ed00-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed00-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ed00-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ed00-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3ed00-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3ed00-133">Na caixa de pesquisa, digite **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-133">In the search box, type **Learningpool Act**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="3ed00-135">No painel de resultados, selecione **Learningpool Act** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ed00-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ed00-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Learningpool Act, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="3ed00-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ed00-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Learningpool Act é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ed00-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="3ed00-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="3ed00-141">No Learningpool Act, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ed00-142">Para configurar e testar o logon único do Azure AD com o Learningpool Act, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3ed00-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ed00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3ed00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ed00-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3ed00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ed00-145">**[Criação de um usuário de teste do Learningpool Act](#creating-a-learningpool-act-test-user)**: para ter um equivalente de Brenda Fernandes no Learningpool Act que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ed00-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ed00-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ed00-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ed00-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3ed00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ed00-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ed00-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ed00-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="3ed00-150">**Para configurar o logon único do Azure AD com o Learningpool Act, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3ed00-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed00-151">No Portal do Azure, na página de integração de aplicativos do **Learningpool Act**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3ed00-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3ed00-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="3ed00-155">Na seção **Domínio e URLs do Learningpool Act**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3ed00-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="3ed00-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ed00-157">a.</span></span> <span data-ttu-id="3ed00-158">Na caixa de texto **URL de Logon**, digite a URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="3ed00-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="3ed00-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ed00-159">b.</span></span> <span data-ttu-id="3ed00-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="3ed00-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="3ed00-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3ed00-161">These values are not real.</span></span> <span data-ttu-id="3ed00-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="3ed00-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3ed00-163">Contate a [equipe de suporte do Cliente Learningpool Act](https://www.Learningpool.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="3ed00-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="3ed00-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3ed00-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="3ed00-166">O aplicativo Learningpool Act espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="3ed00-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3ed00-167">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="3ed00-168">Você pode gerenciar o valor dos atributos na guia **"Atributo"** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="3ed00-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="3ed00-169">The following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="3ed00-171">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ed00-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="3ed00-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="3ed00-172">Attribute Name</span></span> | <span data-ttu-id="3ed00-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="3ed00-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="3ed00-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="3ed00-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="3ed00-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="3ed00-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="3ed00-176">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="3ed00-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="3ed00-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="3ed00-177">user.givenname</span></span> |
    | <span data-ttu-id="3ed00-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="3ed00-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="3ed00-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="3ed00-179">user.mail</span></span> |    
    | <span data-ttu-id="3ed00-180">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="3ed00-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="3ed00-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="3ed00-181">user.surname</span></span> |
    
    <span data-ttu-id="3ed00-182">a.</span><span class="sxs-lookup"><span data-stu-id="3ed00-182">a.</span></span> <span data-ttu-id="3ed00-183">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="3ed00-186">b.</span><span class="sxs-lookup"><span data-stu-id="3ed00-186">b.</span></span> <span data-ttu-id="3ed00-187">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3ed00-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="3ed00-188">c.</span><span class="sxs-lookup"><span data-stu-id="3ed00-188">c.</span></span> <span data-ttu-id="3ed00-189">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3ed00-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="3ed00-190">d.</span><span class="sxs-lookup"><span data-stu-id="3ed00-190">d.</span></span> <span data-ttu-id="3ed00-191">Deixe o **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="3ed00-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="3ed00-192">e.</span><span class="sxs-lookup"><span data-stu-id="3ed00-192">e.</span></span> <span data-ttu-id="3ed00-193">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-193">Click **Ok**.</span></span>

7. <span data-ttu-id="3ed00-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3ed00-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3ed00-196">Para configurar o logon único no lado do **Learningpool Act**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="3ed00-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="3ed00-197">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="3ed00-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3ed00-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3ed00-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ed00-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3ed00-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ed00-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ed00-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ed00-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ed00-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3ed00-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3ed00-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3ed00-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed00-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ed00-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3ed00-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ed00-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ed00-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3ed00-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ed00-213">a.</span><span class="sxs-lookup"><span data-stu-id="3ed00-213">a.</span></span> <span data-ttu-id="3ed00-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ed00-215">b.</span><span class="sxs-lookup"><span data-stu-id="3ed00-215">b.</span></span> <span data-ttu-id="3ed00-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3ed00-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ed00-217">c.</span><span class="sxs-lookup"><span data-stu-id="3ed00-217">c.</span></span> <span data-ttu-id="3ed00-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ed00-219">d.</span><span class="sxs-lookup"><span data-stu-id="3ed00-219">d.</span></span> <span data-ttu-id="3ed00-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="3ed00-221">Criação de um usuário de teste do Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="3ed00-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="3ed00-222">Para permitir que os usuários do Azure AD façam logon no Learningpool Act, eles devem ser provisionados no Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="3ed00-223">Não há nenhum item de ação para a configuração de provisionamento de usuário para o Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="3ed00-224">Os usuários precisam ser criados por sua [equipe de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="3ed00-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="3ed00-225">É possível usar qualquer outra ferramenta de criação de conta de usuário do Learningpool Act ou APIs fornecidas pelo Learningpool Act para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="3ed00-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ed00-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ed00-227">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3ed00-229">**Para atribuir Brenda Fernandes ao Learningpool Act, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3ed00-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed00-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3ed00-232">Na lista de aplicativos, selecione **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="3ed00-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3ed00-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3ed00-236">Click **Add** button.</span></span> <span data-ttu-id="3ed00-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3ed00-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3ed00-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ed00-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ed00-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ed00-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ed00-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3ed00-242">Testing single sign-on</span></span>

<span data-ttu-id="3ed00-243">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3ed00-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ed00-244">Quando você clicar no bloco Learningpool Act no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="3ed00-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ed00-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3ed00-245">Additional resources</span></span>

* [<span data-ttu-id="3ed00-246">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3ed00-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ed00-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ed00-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

