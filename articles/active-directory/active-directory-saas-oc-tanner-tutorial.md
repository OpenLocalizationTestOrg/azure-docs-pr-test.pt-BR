---
title: "Tutorial: Integração do Azure Active Directory ao O.C. Tanner - AppreciateHub | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o O.C. Tanner - AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="7c24e-105">Tutorial: Integração do Azure Active Directory ao O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="7c24e-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="7c24e-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="7c24e-107">Neste tutorial, você aprenderá a integrar o O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="7c24e-108">Tanner - AppreciateHub ao Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="7c24e-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7c24e-109">Integração do O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-109">Integrating O.C.</span></span> <span data-ttu-id="7c24e-110">O Tanner - AppreciateHub ao AD do Azure oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7c24e-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7c24e-111">Você pode controlar no AD do Azure quem terá acesso ao O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="7c24e-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="7c24e-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="7c24e-113">Você pode permitir que seus usuários façam logon automaticamente no O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="7c24e-114">Tanner - AppreciateHub (Logon Único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7c24e-115">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7c24e-116">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c24e-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c24e-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c24e-117">Prerequisites</span></span>

<span data-ttu-id="7c24e-118">Para configurar a integração do AD do Azure ao O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="7c24e-119">Tanner - AppreciateHub, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7c24e-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="7c24e-120">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-120">An Azure AD subscription</span></span>
- <span data-ttu-id="7c24e-121">Um</span><span class="sxs-lookup"><span data-stu-id="7c24e-121">A O.C.</span></span> <span data-ttu-id="7c24e-122">Assinatura habilitada para logon único do Tanner – AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="7c24e-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c24e-123">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7c24e-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7c24e-124">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7c24e-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7c24e-125">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7c24e-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7c24e-126">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c24e-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7c24e-127">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7c24e-127">Scenario description</span></span>
<span data-ttu-id="7c24e-128">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7c24e-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7c24e-129">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7c24e-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7c24e-130">Adicionar o O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-130">Adding O.C.</span></span> <span data-ttu-id="7c24e-131">Tanner - AppreciateHub a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="7c24e-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="7c24e-132">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="7c24e-133">Adicionar o O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-133">Adding O.C.</span></span> <span data-ttu-id="7c24e-134">Tanner - AppreciateHub a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="7c24e-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="7c24e-135">Para configurar a integração do O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-135">To configure the integration of O.C.</span></span> <span data-ttu-id="7c24e-136">Tanner - AppreciateHub no AD do Azure, você precisa adicionar O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="7c24e-137">Tanner - AppreciateHub a partir da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7c24e-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c24e-138">**Para adicionar o O.C. Tanner - AppreciateHub da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c24e-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c24e-139">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7c24e-141">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7c24e-142">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-142">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7c24e-144">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7c24e-146">Na caixa de pesquisa, digite **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="7c24e-148">No painel de resultados, selecione **O.C. Tanner – AppreciateHub** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c24e-150">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c24e-151">Nesta seção, configura e testa o logon único do Azure AD com o O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="7c24e-152">Tanner - AppreciateHub com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="7c24e-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c24e-153">Para que o logon único funcione, o AD do Azure precisa saber qual o usuário do O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="7c24e-154">Tanner – AppreciateHub é para um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c24e-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="7c24e-155">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado no O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="7c24e-156">Tanner - o AppreciateHub precisa ser estabelecido.</span><span class="sxs-lookup"><span data-stu-id="7c24e-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="7c24e-157">No O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-157">In O.C.</span></span> <span data-ttu-id="7c24e-158">Tanner – AppreciateHub, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7c24e-159">Para configurar e testar o logon único do AD do Azure com O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="7c24e-160">Tanner - AppreciateHub, é necessário concluir os seguintes blocos de criação:</span><span class="sxs-lookup"><span data-stu-id="7c24e-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c24e-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7c24e-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c24e-162">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar logon único do Azure AD com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7c24e-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c24e-163">**[Criar um usuário teste do O.C. Tanner - AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)** - ter um equivalente de Brenda Fernandes no O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="7c24e-164">Tanner – AppreciateHub que é vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c24e-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7c24e-165">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c24e-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c24e-166">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7c24e-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c24e-167">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c24e-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7c24e-168">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no seu aplicativo O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="7c24e-169">Aplicativo Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="7c24e-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="7c24e-170">**Para configurar o logon único do AD do Azure com O.C. Tanner - AppreciateHub, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c24e-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7c24e-171">No Portal do Azure, na página de integração de aplicativos do **O.C. Tanner – AppreciateHub**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7c24e-173">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7c24e-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="7c24e-175">Na seção **URLs e Domínio do O.C. Tanner – AppreciateHub**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c24e-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="7c24e-177">a.</span><span class="sxs-lookup"><span data-stu-id="7c24e-177">a.</span></span> <span data-ttu-id="7c24e-178">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="7c24e-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7c24e-179">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7c24e-179">This value is not real.</span></span> <span data-ttu-id="7c24e-180">Atualize esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="7c24e-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="7c24e-181">Contate a [Equipe de suporte do O.C. Tanner – AppreciateHub](mailto:sso@octanner.com) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="7c24e-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="7c24e-182">b.</span><span class="sxs-lookup"><span data-stu-id="7c24e-182">b.</span></span> <span data-ttu-id="7c24e-183">Abra o arquivo de metadados usando o seguinte link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="7c24e-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="7c24e-184">c.</span><span class="sxs-lookup"><span data-stu-id="7c24e-184">c.</span></span> <span data-ttu-id="7c24e-185">Localize o nó **md:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="7c24e-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="7c24e-186">d.</span><span class="sxs-lookup"><span data-stu-id="7c24e-186">d.</span></span> <span data-ttu-id="7c24e-187">Copie o valor do atributo **Local** .</span><span class="sxs-lookup"><span data-stu-id="7c24e-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Definir configurações de aplicativo][12]
   
    <span data-ttu-id="7c24e-189">e.</span><span class="sxs-lookup"><span data-stu-id="7c24e-189">e.</span></span> <span data-ttu-id="7c24e-190">Na caixa de texto **URL do Logon** , antes do valor que você obteve na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="7c24e-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="7c24e-191">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7c24e-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="7c24e-193">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7c24e-193">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7c24e-195">Para configurar o logon único no lado do aplicativo do **O.C. Tanner – AppreciateHub**, você precisa enviar o **XML de Metadados** baixado para a [equipe de suporte do O.C. Tanner – AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="7c24e-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="7c24e-196">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7c24e-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7c24e-197">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7c24e-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7c24e-198">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7c24e-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c24e-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c24e-200">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c24e-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7c24e-202">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c24e-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c24e-203">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7c24e-205">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c24e-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7c24e-207">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7c24e-209">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7c24e-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7c24e-211">a.</span><span class="sxs-lookup"><span data-stu-id="7c24e-211">a.</span></span> <span data-ttu-id="7c24e-212">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7c24e-213">b.</span><span class="sxs-lookup"><span data-stu-id="7c24e-213">b.</span></span> <span data-ttu-id="7c24e-214">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7c24e-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7c24e-215">c.</span><span class="sxs-lookup"><span data-stu-id="7c24e-215">c.</span></span> <span data-ttu-id="7c24e-216">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7c24e-217">d.</span><span class="sxs-lookup"><span data-stu-id="7c24e-217">d.</span></span> <span data-ttu-id="7c24e-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="7c24e-219">Criar um usuário teste do O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-219">Creating a O.C.</span></span> <span data-ttu-id="7c24e-220">Usuário de teste do Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="7c24e-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="7c24e-221">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="7c24e-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="7c24e-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="7c24e-223">**Para criar um usuário chamado Brenda Fernandes no O.C. Tanner - AppreciateHub, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c24e-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="7c24e-224">Peça à sua [equipe de suporte do O.C. Tanner – AppreciateHub](mailto:sso@octanner.com) para criar um usuário que tenha o atributo nameID com o mesmo valor que o nome de usuário Brenda Fernandes no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c24e-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c24e-225">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7c24e-226">Nesta seção, você concederá a Brenda Fernandes acesso ao O.C. para que ela fique habilitada a usar o logon único do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c24e-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="7c24e-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="7c24e-227">Tanner - AppreciateHub.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7c24e-229">**Para atribuir Brenda Fernandes ao O.C. Tanner - AppreciateHub, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7c24e-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7c24e-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7c24e-232">Na lista de aplicativos, selecione **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="7c24e-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7c24e-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7c24e-236">Click **Add** button.</span></span> <span data-ttu-id="7c24e-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7c24e-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7c24e-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7c24e-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7c24e-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7c24e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7c24e-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7c24e-242">Testing single sign-on</span></span>

<span data-ttu-id="7c24e-243">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7c24e-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7c24e-244">Quando você clica no bloco O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-244">When you click the O.C.</span></span> <span data-ttu-id="7c24e-245">Tanner - AppreciateHub no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo O.C.</span><span class="sxs-lookup"><span data-stu-id="7c24e-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="7c24e-246">Aplicativo Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="7c24e-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c24e-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7c24e-247">Additional resources</span></span>

* [<span data-ttu-id="7c24e-248">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7c24e-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c24e-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c24e-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

