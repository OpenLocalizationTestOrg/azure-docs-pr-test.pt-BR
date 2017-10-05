---
title: "Tutorial: integração do Azure Active Directory com o Ceridian Dayforce HCM | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="9e51c-103">Tutorial: integração do Azure Active Directory ao Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="9e51c-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="9e51c-104">Neste tutorial, você aprenderá a integrar o Ceridian Dayforce HCM ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9e51c-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e51c-105">A integração do Ceridian Dayforce HCM ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9e51c-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e51c-106">No Azure AD, é possível controlar quem tem acesso ao Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="9e51c-107">Você pode permitir que seus usuários façam logon automaticamente no Ceridian Dayforce HCM (logon único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e51c-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9e51c-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e51c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9e51c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e51c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e51c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e51c-110">Prerequisites</span></span>

<span data-ttu-id="9e51c-111">Para configurar a integração do Azure AD ao Ceridian Dayforce HCM, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9e51c-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="9e51c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9e51c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e51c-113">Uma assinatura Ceridian Dayforce HCM com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="9e51c-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e51c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9e51c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e51c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9e51c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e51c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9e51c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e51c-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e51c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e51c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9e51c-118">Scenario description</span></span>
<span data-ttu-id="9e51c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9e51c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e51c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9e51c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e51c-121">Adição do Ceridian Dayforce HCM a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="9e51c-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="9e51c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9e51c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="9e51c-123">Adição do Ceridian Dayforce HCM a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="9e51c-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="9e51c-124">Para configurar a integração do Ceridian Dayforce HCM ao Azure AD, você precisa adicionar o Ceridian Dayforce HCM à sua lista de aplicativos SaaS gerenciados desde a galeria.</span><span class="sxs-lookup"><span data-stu-id="9e51c-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e51c-125">**Para adicionar o Ceridian Dayforce HCM a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9e51c-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e51c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="9e51c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e51c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="9e51c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="9e51c-133">Na caixa de pesquisa, digite **Ceridian Dayforce HCM**, selecione **Ceridian Dayforce HCM** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![Ceridian Dayforce HCM na lista de resultados](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9e51c-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e51c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9e51c-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Ceridian Dayforce HCM com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9e51c-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e51c-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Ceridian Dayforce HCM é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e51c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="9e51c-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="9e51c-139">No Ceridian Dayforce HCM, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e51c-140">Para configurar e testar o logon único do Azure AD com o Ceridian Dayforce HCM, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9e51c-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e51c-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9e51c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e51c-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9e51c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e51c-143">**[Criar um usuário de teste do Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)** – para ter um equivalente de Brenda Fernandes no Ceridian Dayforce HCM que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e51c-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e51c-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e51c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e51c-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9e51c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9e51c-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e51c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9e51c-147">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo do Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="9e51c-148">**Para configurar o logon único do Azure AD com o Ceridian Dayforce HCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9e51c-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="9e51c-149">No portal do Azure, na página de integração de aplicativo do **Ceridian Dayforce HCM**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="9e51c-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9e51c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="9e51c-153">Na seção **URLs e Domínio do Ceridian Dayforce HCM**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9e51c-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="9e51c-155">a.</span><span class="sxs-lookup"><span data-stu-id="9e51c-155">a.</span></span> <span data-ttu-id="9e51c-156">Na caixa de texto **URL de Entrada** , digite a URL usada pelos usuários para fazer logon em seu aplicativo do Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="9e51c-157">Ambiente</span><span class="sxs-lookup"><span data-stu-id="9e51c-157">Environment</span></span> | <span data-ttu-id="9e51c-158">URL</span><span class="sxs-lookup"><span data-stu-id="9e51c-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="9e51c-159">Para produção</span><span class="sxs-lookup"><span data-stu-id="9e51c-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="9e51c-160">Para teste</span><span class="sxs-lookup"><span data-stu-id="9e51c-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="9e51c-161">b.</span><span class="sxs-lookup"><span data-stu-id="9e51c-161">b.</span></span> <span data-ttu-id="9e51c-162">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="9e51c-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="9e51c-163">Ambiente</span><span class="sxs-lookup"><span data-stu-id="9e51c-163">Environment</span></span> | <span data-ttu-id="9e51c-164">URL</span><span class="sxs-lookup"><span data-stu-id="9e51c-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="9e51c-165">Para produção</span><span class="sxs-lookup"><span data-stu-id="9e51c-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="9e51c-166">Para teste</span><span class="sxs-lookup"><span data-stu-id="9e51c-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="9e51c-167">c.</span><span class="sxs-lookup"><span data-stu-id="9e51c-167">c.</span></span> <span data-ttu-id="9e51c-168">Na caixa de texto **URL de Resposta** , digite a URL usada pelo Azure AD para postar a resposta.</span><span class="sxs-lookup"><span data-stu-id="9e51c-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="9e51c-169">Ambiente</span><span class="sxs-lookup"><span data-stu-id="9e51c-169">Environment</span></span> | <span data-ttu-id="9e51c-170">URL</span><span class="sxs-lookup"><span data-stu-id="9e51c-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="9e51c-171">Para produção</span><span class="sxs-lookup"><span data-stu-id="9e51c-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="9e51c-172">Para teste</span><span class="sxs-lookup"><span data-stu-id="9e51c-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="9e51c-173">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9e51c-173">These values are not real.</span></span> <span data-ttu-id="9e51c-174">Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="9e51c-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="9e51c-175">Entre em contato com a [equipe de suporte ao cliente do Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9e51c-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="9e51c-176">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9e51c-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="9e51c-178">Seu aplicativo Ceridian Dayforce HCM espera as declarações SAML em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="9e51c-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="9e51c-179">Trabalhe com a [equipe de suporte do Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) primeiro para verificar o identificador de usuário correto.</span><span class="sxs-lookup"><span data-stu-id="9e51c-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="9e51c-180">A Microsoft recomenda usar o atributo **"name"** como identificador de usuário.</span><span class="sxs-lookup"><span data-stu-id="9e51c-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="9e51c-181">Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9e51c-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="9e51c-182">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="9e51c-182">The following screenshot shows an example for this.</span></span>  

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="9e51c-184">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="9e51c-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="9e51c-185">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9e51c-185">Attribute Name</span></span>  | <span data-ttu-id="9e51c-186">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9e51c-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="9e51c-187">name</span><span class="sxs-lookup"><span data-stu-id="9e51c-187">name</span></span>  | <span data-ttu-id="9e51c-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="9e51c-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="9e51c-189">a.</span><span class="sxs-lookup"><span data-stu-id="9e51c-189">a.</span></span> <span data-ttu-id="9e51c-190">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="9e51c-193">b.</span><span class="sxs-lookup"><span data-stu-id="9e51c-193">b.</span></span> <span data-ttu-id="9e51c-194">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="9e51c-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9e51c-195">c.</span><span class="sxs-lookup"><span data-stu-id="9e51c-195">c.</span></span> <span data-ttu-id="9e51c-196">Na lista **Valor**, selecione o atributo de usuário que você deseja usar na implementação.</span><span class="sxs-lookup"><span data-stu-id="9e51c-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="9e51c-197">Por exemplo, se você quiser usar EmployeeID como identificador exclusivo de usuário e tiver armazenado o valor do atributo em ExtensionAttribute2, selecione **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="9e51c-198">d.</span><span class="sxs-lookup"><span data-stu-id="9e51c-198">d.</span></span> <span data-ttu-id="9e51c-199">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-199">Click **Ok**.</span></span>

7. <span data-ttu-id="9e51c-200">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9e51c-200">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="9e51c-202">Na seção **Configuração do Ceridian Dayforce HCM**, clique em **Configurar Ceridian Dayforce HCM** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e51c-203">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="9e51c-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="9e51c-205">Para configurar o logon único no lado do **Ceridian Dayforce HCM**, é necessário enviar o **XML de Metadados** baixado e a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** para a [equipe de suporte do Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="9e51c-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="9e51c-206">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9e51c-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e51c-207">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9e51c-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e51c-208">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e51c-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9e51c-209">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e51c-209">Create an Azure AD test user</span></span>

<span data-ttu-id="9e51c-210">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9e51c-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="9e51c-212">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9e51c-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e51c-213">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9e51c-215">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9e51c-217">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9e51c-219">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9e51c-219">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9e51c-221">a.</span><span class="sxs-lookup"><span data-stu-id="9e51c-221">a.</span></span> <span data-ttu-id="9e51c-222">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e51c-223">b.</span><span class="sxs-lookup"><span data-stu-id="9e51c-223">b.</span></span> <span data-ttu-id="9e51c-224">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9e51c-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9e51c-225">c.</span><span class="sxs-lookup"><span data-stu-id="9e51c-225">c.</span></span> <span data-ttu-id="9e51c-226">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9e51c-227">d.</span><span class="sxs-lookup"><span data-stu-id="9e51c-227">d.</span></span> <span data-ttu-id="9e51c-228">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="9e51c-229">Criar um usuário de teste do Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="9e51c-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="9e51c-230">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="9e51c-231">Trabalhe com a [equipe de suporte do Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) para adicionar os usuários à conta do aplicativo Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e51c-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9e51c-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e51c-233">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9e51c-235">**Para atribuir Brenda Fernandes ao Ceridian Dayforce HCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9e51c-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="9e51c-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9e51c-238">Na lista de aplicativos, escolha **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="9e51c-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9e51c-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-242">Click **Add** button.</span></span> <span data-ttu-id="9e51c-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9e51c-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9e51c-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e51c-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e51c-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9e51c-248">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e51c-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="9e51c-249">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="9e51c-251">**Para atribuir Brenda Fernandes ao Ceridian Dayforce HCM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9e51c-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="9e51c-252">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9e51c-254">Na lista de aplicativos, escolha **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![O link Ceridian Dayforce HCM na lista Aplicativos](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="9e51c-256">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-256">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="9e51c-258">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9e51c-258">Click **Add** button.</span></span> <span data-ttu-id="9e51c-259">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="9e51c-261">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9e51c-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e51c-262">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e51c-263">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9e51c-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9e51c-264">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="9e51c-264">Test single sign-on</span></span>

<span data-ttu-id="9e51c-265">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9e51c-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="9e51c-266">Ao clicar no bloco Ceridian Dayforce HCM no Painel de Acesso, você deve fazer logon automaticamente no aplicativo do Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="9e51c-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e51c-267">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9e51c-267">Additional resources</span></span>

* [<span data-ttu-id="9e51c-268">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9e51c-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e51c-269">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e51c-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

