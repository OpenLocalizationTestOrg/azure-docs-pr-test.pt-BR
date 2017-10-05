---
title: "Tutorial: integração do Azure Active Directory ao CloudPassage | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="6e5f6-103">Tutorial: integração do Active Directory do Azure ao CloudPassage</span><span class="sxs-lookup"><span data-stu-id="6e5f6-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="6e5f6-104">Neste tutorial, você aprende a integrar o CloudPassage ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6e5f6-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e5f6-105">A integração do CloudPassage ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e5f6-106">Você pode controlar, no AD do Azure, quem tem acesso ao CloudPassage</span><span class="sxs-lookup"><span data-stu-id="6e5f6-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="6e5f6-107">Você pode habilitar seus usuários a fazerem logon automaticamente no CloudPassage (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e5f6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e5f6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e5f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e5f6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e5f6-110">Prerequisites</span></span>

<span data-ttu-id="6e5f6-111">Para configurar a integração do AD do Azure com o CloudPassage, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="6e5f6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e5f6-113">Uma assinatura do CloudPassage com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="6e5f6-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e5f6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e5f6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e5f6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e5f6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e5f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e5f6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6e5f6-118">Scenario description</span></span>
<span data-ttu-id="6e5f6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e5f6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e5f6-121">Adicionando CloudPassage da Galeria</span><span class="sxs-lookup"><span data-stu-id="6e5f6-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="6e5f6-122">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e5f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="6e5f6-123">Adicionando CloudPassage da Galeria</span><span class="sxs-lookup"><span data-stu-id="6e5f6-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="6e5f6-124">Para configurar a integração do CloudPassage com o AD do Azure, você precisa adicionar o CloudPassage, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e5f6-125">**Para adicionar o CloudPassage por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e5f6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e5f6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e5f6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6e5f6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6e5f6-133">Na caixa de pesquisa, digite **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-133">In the search box, type **CloudPassage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="6e5f6-135">No painel de resultados, selecione **CloudPassage** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e5f6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e5f6-138">Nesta seção, você configura e testa o logon único do Azure AD com o CloudPassage com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="6e5f6-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e5f6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do CloudPassage é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="6e5f6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="6e5f6-141">No CloudPassage, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e5f6-142">Para configurar e testar o logon único do AD do Azure com o CloudPassage, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e5f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e5f6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e5f6-145">**[Como criar um usuário de teste do CloudPassage](#creating-a-cloudpassage-test-user)** – para ter um equivalente de Brenda Fernandes no CloudPassage que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e5f6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e5f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e5f6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e5f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e5f6-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="6e5f6-150">**Para configurar o logon único do AD do Azure com o CloudPassage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="6e5f6-151">No portal do Azure, na página de integração de aplicativos do **CloudPassage**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6e5f6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="6e5f6-155">Na seção **URLs e Domínio do CloudPassage**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="6e5f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-157">a.</span></span> <span data-ttu-id="6e5f6-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="6e5f6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="6e5f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-159">b.</span></span> <span data-ttu-id="6e5f6-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="6e5f6-161">Você pode obter o valor para este atributo clicando em **documentação de instalação do SSO** na seção **Configurações de Logon Único** do seu portal CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="6e5f6-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-163">These values are not real.</span></span> <span data-ttu-id="6e5f6-164">Atualize esses valores com a URL de Resposta real e a URL de Logon.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6e5f6-165">Entre em contato com a [equipe de suporte ao cliente do CloudPassage](https://www.cloudpassage.com/company/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="6e5f6-166">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="6e5f6-168">Seu aplicativo CloudPassage espera as asserções SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizado à sua configuração de atributos de token SAML.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="6e5f6-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-169">The following screenshot shows an example for this.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="6e5f6-171">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="6e5f6-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="6e5f6-172">Attribute Name</span></span> | <span data-ttu-id="6e5f6-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="6e5f6-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="6e5f6-174">nome</span><span class="sxs-lookup"><span data-stu-id="6e5f6-174">firstname</span></span> |<span data-ttu-id="6e5f6-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="6e5f6-175">user.givenname</span></span> |
    | <span data-ttu-id="6e5f6-176">sobrenome</span><span class="sxs-lookup"><span data-stu-id="6e5f6-176">lastname</span></span> |<span data-ttu-id="6e5f6-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="6e5f6-177">user.surname</span></span> |
    | <span data-ttu-id="6e5f6-178">email</span><span class="sxs-lookup"><span data-stu-id="6e5f6-178">email</span></span> |<span data-ttu-id="6e5f6-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="6e5f6-179">user.mail</span></span> |
    
    <span data-ttu-id="6e5f6-180">a.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-180">a.</span></span> <span data-ttu-id="6e5f6-181">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="6e5f6-184">b.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-184">b.</span></span> <span data-ttu-id="6e5f6-185">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="6e5f6-186">c.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-186">c.</span></span> <span data-ttu-id="6e5f6-187">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6e5f6-188">d.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-188">d.</span></span> <span data-ttu-id="6e5f6-189">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-189">Click **Ok**.</span></span>

7. <span data-ttu-id="6e5f6-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6e5f6-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="6e5f6-192">Na seção **Configuração do CloudPassage**, clique em **Configurar CloudPassage** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e5f6-193">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="6e5f6-195">Em outra janela do navegador, entre em seu site de empresa CloudPassage como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="6e5f6-196">No menu, na parte superior, clique em **Configurações** e clique em **Administração do Site**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configurar o logon único][12]

11. <span data-ttu-id="6e5f6-198">Clique na guia **Configurações de Autenticação** .</span><span class="sxs-lookup"><span data-stu-id="6e5f6-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configurar Logon Único][13]

12. <span data-ttu-id="6e5f6-200">Na seção **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configurar Logon Único][14]

    <span data-ttu-id="6e5f6-202">a.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-202">a.</span></span> <span data-ttu-id="6e5f6-203">Marque a caixa de seleção **Habilitar SSO (Logon Único) (Documentação de instalação de SSO)**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="6e5f6-204">b.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-204">b.</span></span> <span data-ttu-id="6e5f6-205">Cole **ID da Entidade SAML** na caixa de texto **URL do emissor do SAML**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="6e5f6-206">c.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-206">c.</span></span> <span data-ttu-id="6e5f6-207">Cole **URL de Serviço de Logon Único do SAML** na caixa de texto **URL do ponto de extremidade do SAML**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="6e5f6-208">d.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-208">d.</span></span> <span data-ttu-id="6e5f6-209">Cole **URL de Logoff** na caixa de texto **página de aterrissagem de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="6e5f6-210">e.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-210">e.</span></span> <span data-ttu-id="6e5f6-211">Abra seu certificado baixado no bloco de notas, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado x 509**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="6e5f6-212">f.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-212">f.</span></span> <span data-ttu-id="6e5f6-213">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6e5f6-214">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6e5f6-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e5f6-215">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e5f6-216">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e5f6-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e5f6-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e5f6-218">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6e5f6-220">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e5f6-221">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e5f6-223">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e5f6-225">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e5f6-227">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e5f6-229">a.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-229">a.</span></span> <span data-ttu-id="6e5f6-230">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e5f6-231">b.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-231">b.</span></span> <span data-ttu-id="6e5f6-232">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e5f6-233">c.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-233">c.</span></span> <span data-ttu-id="6e5f6-234">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e5f6-235">d.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-235">d.</span></span> <span data-ttu-id="6e5f6-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="6e5f6-237">Criar um usuário de teste CloudPassage</span><span class="sxs-lookup"><span data-stu-id="6e5f6-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="6e5f6-238">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="6e5f6-239">**Para criar um usuário chamado Brenda Fernandes no CloudPassage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="6e5f6-240">Faça logon em seu site de empresa do **CloudPassage** como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="6e5f6-241">Na barra de ferramentas, na parte superior, clique em **Configurações** e clique em **Administração do Site**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Criar um usuário de teste CloudPassage][22] 

3. <span data-ttu-id="6e5f6-243">Clique na guia **Usuários** e clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Criar um usuário de teste CloudPassage][23]

4. <span data-ttu-id="6e5f6-245">Na seção **Adicionar Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e5f6-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Criar um usuário de teste CloudPassage][24]
    
    <span data-ttu-id="6e5f6-247">a.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-247">a.</span></span> <span data-ttu-id="6e5f6-248">Na caixa de texto **Nome** , digite Brenda.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="6e5f6-249">b.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-249">b.</span></span> <span data-ttu-id="6e5f6-250">Na caixa de texto **Sobrenome** , digite Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="6e5f6-251">c.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-251">c.</span></span> <span data-ttu-id="6e5f6-252">Nas caixas de texto **Nome de usuário**, **E-mail** e **Digite novamente o e-mail**, digite o nome de usuário da Brenda no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="6e5f6-253">d.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-253">d.</span></span> <span data-ttu-id="6e5f6-254">Como **Tipo de acesso**, selecione **Habilitar acesso do Portal de Halo**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="6e5f6-255">e.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-255">e.</span></span> <span data-ttu-id="6e5f6-256">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e5f6-257">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e5f6-258">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6e5f6-260">**Para atribuir Brenda Fernandes ao CloudPassage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e5f6-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="6e5f6-261">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6e5f6-263">Na lista de aplicativos, selecione **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-263">In the applications list, select **CloudPassage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="6e5f6-265">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6e5f6-267">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-267">Click **Add** button.</span></span> <span data-ttu-id="6e5f6-268">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6e5f6-270">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e5f6-271">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e5f6-272">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e5f6-273">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6e5f6-273">Testing single sign-on</span></span>

<span data-ttu-id="6e5f6-274">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6e5f6-275">Quando você clica no bloco CloudPassage no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="6e5f6-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e5f6-276">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6e5f6-276">Additional resources</span></span>

* [<span data-ttu-id="6e5f6-277">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6e5f6-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e5f6-278">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e5f6-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

