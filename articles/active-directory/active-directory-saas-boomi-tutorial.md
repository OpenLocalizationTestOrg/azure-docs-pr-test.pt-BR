---
title: "Tutorial: Integração do Azure Active Directory ao Boomi | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="8b39a-103">Tutorial: Integração do Active Directory do Azure ao Boomi</span><span class="sxs-lookup"><span data-stu-id="8b39a-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="8b39a-104">Neste tutorial, você aprenderá a integrar o Boomi ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8b39a-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b39a-105">A integração do Boomi ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8b39a-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b39a-106">Você pode controlar no Azure AD quem terá acesso ao Boomi</span><span class="sxs-lookup"><span data-stu-id="8b39a-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="8b39a-107">Você pode permitir que seus usuários faça logon automaticamente no Boomi (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b39a-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b39a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b39a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b39a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b39a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8b39a-110">Prerequisites</span></span>

<span data-ttu-id="8b39a-111">Para configurar a integração do Azure AD ao Boomi, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8b39a-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="8b39a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b39a-113">Uma assinatura habilitada para logon único do Boomi</span><span class="sxs-lookup"><span data-stu-id="8b39a-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b39a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8b39a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b39a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8b39a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b39a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8b39a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b39a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b39a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b39a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8b39a-118">Scenario description</span></span>
<span data-ttu-id="8b39a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8b39a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b39a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8b39a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b39a-121">Adicionar Boomi da galeria</span><span class="sxs-lookup"><span data-stu-id="8b39a-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="8b39a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="8b39a-123">Adicionar Boomi da galeria</span><span class="sxs-lookup"><span data-stu-id="8b39a-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="8b39a-124">Para configurar a integração do Boomi ao Azure AD, você precisa adicionar o Boomi por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8b39a-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b39a-125">**Para adicionar o Boomi da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8b39a-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b39a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b39a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b39a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8b39a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8b39a-133">Na caixa de pesquisa, digite **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-133">In the search box, type **Boomi**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="8b39a-135">No painel de resultados, selecione **Boomi** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b39a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b39a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Boomi, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8b39a-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b39a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Boomi é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b39a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="8b39a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Boomi.</span><span class="sxs-lookup"><span data-stu-id="8b39a-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="8b39a-141">No Boomi, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b39a-142">Para configurar e testar o logon único do Azure AD com o Boomi, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8b39a-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b39a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8b39a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b39a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8b39a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b39a-145">**[Criação de um usuário de teste do Boomi](#creating-a-boomi-test-user)**: para ter um equivalente de Brenda Fernandes no Boomi que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b39a-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b39a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b39a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b39a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8b39a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b39a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b39a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b39a-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Boomi.</span><span class="sxs-lookup"><span data-stu-id="8b39a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="8b39a-150">**Para configurar o logon único do Azure AD com o Boomi, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8b39a-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="8b39a-151">No portal do Azure, na página de integração de aplicativos do **Boomi**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8b39a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8b39a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="8b39a-155">Na seção **URLs e Domínio do Boomi**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8b39a-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="8b39a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b39a-157">a.</span></span> <span data-ttu-id="8b39a-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="8b39a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="8b39a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8b39a-159">b.</span></span> <span data-ttu-id="8b39a-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="8b39a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b39a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8b39a-161">These values are not real.</span></span> <span data-ttu-id="8b39a-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="8b39a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8b39a-163">Para obter esses valores, entre em contato com a [equipe de suporte do Boomi](https://boomi.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="8b39a-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="8b39a-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="8b39a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="8b39a-166">O aplicativo Boomi espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="8b39a-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8b39a-167">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="8b39a-168">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="8b39a-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="8b39a-169">The following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="8b39a-171">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, para cada linha mostrada na tabela a seguir, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8b39a-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="8b39a-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="8b39a-172">Attribute Name</span></span> | <span data-ttu-id="8b39a-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="8b39a-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="8b39a-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="8b39a-174">FEDERATION_ID</span></span> | <span data-ttu-id="8b39a-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="8b39a-175">user.mail</span></span> |
    
    <span data-ttu-id="8b39a-176">a.</span><span class="sxs-lookup"><span data-stu-id="8b39a-176">a.</span></span> <span data-ttu-id="8b39a-177">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8b39a-180">b.</span><span class="sxs-lookup"><span data-stu-id="8b39a-180">b.</span></span> <span data-ttu-id="8b39a-181">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8b39a-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8b39a-182">c.</span><span class="sxs-lookup"><span data-stu-id="8b39a-182">c.</span></span> <span data-ttu-id="8b39a-183">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="8b39a-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8b39a-184">d.</span><span class="sxs-lookup"><span data-stu-id="8b39a-184">d.</span></span> <span data-ttu-id="8b39a-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-185">Click **Ok**.</span></span>

6. <span data-ttu-id="8b39a-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8b39a-186">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8b39a-188">Na seção **Configuração do Boomi**, clique em **Configurar o Boomi** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8b39a-189">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="8b39a-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="8b39a-191">Em outra janela do navegador da Web, faça logon em seu site de empresa Boomi como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8b39a-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="8b39a-192">Navegue até **Nome da Empresa** e vá para **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="8b39a-193">Clique na guia **Opções de SSO** e execute etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b39a-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="8b39a-195">a.</span><span class="sxs-lookup"><span data-stu-id="8b39a-195">a.</span></span> <span data-ttu-id="8b39a-196">Marque a caixa de seleção **Habilitar Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="8b39a-197">b.</span><span class="sxs-lookup"><span data-stu-id="8b39a-197">b.</span></span> <span data-ttu-id="8b39a-198">Clique em **Importar** para carregar o certificado baixado do Azure AD no **Certificado do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="8b39a-199">c.</span><span class="sxs-lookup"><span data-stu-id="8b39a-199">c.</span></span> <span data-ttu-id="8b39a-200">Na caixa de texto **URL de Logon do Provedor de Identidade**, insira o valor da **URL de Serviço de Logon Único SAML** da janela de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b39a-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="8b39a-201">d.</span><span class="sxs-lookup"><span data-stu-id="8b39a-201">d.</span></span> <span data-ttu-id="8b39a-202">Para **Local do ID de Federação**, selecione o botão de opção **A Id de Federação está contida no elemento Atributo FEDERATION_ID**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="8b39a-203">e.</span><span class="sxs-lookup"><span data-stu-id="8b39a-203">e.</span></span> <span data-ttu-id="8b39a-204">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8b39a-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="8b39a-205">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8b39a-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b39a-206">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8b39a-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b39a-207">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b39a-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b39a-208">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b39a-209">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8b39a-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8b39a-211">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8b39a-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b39a-212">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b39a-214">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8b39a-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b39a-216">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b39a-218">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8b39a-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b39a-220">a.</span><span class="sxs-lookup"><span data-stu-id="8b39a-220">a.</span></span> <span data-ttu-id="8b39a-221">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b39a-222">b.</span><span class="sxs-lookup"><span data-stu-id="8b39a-222">b.</span></span> <span data-ttu-id="8b39a-223">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8b39a-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b39a-224">c.</span><span class="sxs-lookup"><span data-stu-id="8b39a-224">c.</span></span> <span data-ttu-id="8b39a-225">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b39a-226">d.</span><span class="sxs-lookup"><span data-stu-id="8b39a-226">d.</span></span> <span data-ttu-id="8b39a-227">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="8b39a-228">Criar um usuário de teste do Boomi</span><span class="sxs-lookup"><span data-stu-id="8b39a-228">Creating a Boomi test user</span></span>

<span data-ttu-id="8b39a-229">Para permitir que os usuários do Azure AD façam logon no Boomi, eles deverão ser provisionados no Boomi.</span><span class="sxs-lookup"><span data-stu-id="8b39a-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="8b39a-230">No caso do Boomi, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="8b39a-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="8b39a-231">Para provisionar uma conta de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8b39a-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="8b39a-232">Faça logon em seu site de empresa Boomi como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8b39a-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="8b39a-233">Depois de fazer logon, navegue até **Gerenciamento de Usuário** e vá até **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="8b39a-234">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="8b39a-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="8b39a-235">Clique no ícone **+** e o diálogo **Adicionar/Manter Funções de Usuário** será aberto.</span><span class="sxs-lookup"><span data-stu-id="8b39a-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="8b39a-236">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="8b39a-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="8b39a-237">![Usuários](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="8b39a-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="8b39a-238">a.</span><span class="sxs-lookup"><span data-stu-id="8b39a-238">a.</span></span> <span data-ttu-id="8b39a-239">Na caixa de texto **Endereço de email do usuário**, digite o email do usuário, como BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8b39a-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="8b39a-240">b.</span><span class="sxs-lookup"><span data-stu-id="8b39a-240">b.</span></span> <span data-ttu-id="8b39a-241">Na caixa de texto **Nome**, digite o Nome do usuário como Brenda.</span><span class="sxs-lookup"><span data-stu-id="8b39a-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="8b39a-242">c.</span><span class="sxs-lookup"><span data-stu-id="8b39a-242">c.</span></span> <span data-ttu-id="8b39a-243">Na caixa de texto **Sobrenome**, digite o Sobrenome do usuário como Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8b39a-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="8b39a-244">d.</span><span class="sxs-lookup"><span data-stu-id="8b39a-244">d.</span></span> <span data-ttu-id="8b39a-245">Insira a **ID de Federação** do usuário.</span><span class="sxs-lookup"><span data-stu-id="8b39a-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="8b39a-246">Cada usuário deve ter uma ID de Federação que o identifique exclusivamente na conta.</span><span class="sxs-lookup"><span data-stu-id="8b39a-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="8b39a-247">e.</span><span class="sxs-lookup"><span data-stu-id="8b39a-247">e.</span></span> <span data-ttu-id="8b39a-248">Atribua a função **Usuário Padrão** ao usuário.</span><span class="sxs-lookup"><span data-stu-id="8b39a-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="8b39a-249">Não atribua a função Administrador, pois isso daria acesso normal ao Atmosphere, bem como acesso de logon único.</span><span class="sxs-lookup"><span data-stu-id="8b39a-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="8b39a-250">f.</span><span class="sxs-lookup"><span data-stu-id="8b39a-250">f.</span></span> <span data-ttu-id="8b39a-251">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8b39a-252">O usuário não receberá um email de notificação de boas-vindas contendo uma senha que pode ser usada para fazer logon na conta do AtomSphere, pois sua senha é gerenciada por meio do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="8b39a-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="8b39a-253">É possível usar qualquer outra ferramenta de criação da conta de usuário do Boomi ou as APIs fornecidas pelo Boomi para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="8b39a-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b39a-254">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b39a-255">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Boomi.</span><span class="sxs-lookup"><span data-stu-id="8b39a-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8b39a-257">**Para atribuir Brenda Fernandes ao Boomi, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8b39a-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="8b39a-258">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8b39a-260">Na lista de aplicativos, escolha **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-260">In the applications list, select **Boomi**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="8b39a-262">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8b39a-264">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8b39a-264">Click **Add** button.</span></span> <span data-ttu-id="8b39a-265">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8b39a-267">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8b39a-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b39a-268">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b39a-269">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8b39a-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b39a-270">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8b39a-270">Testing single sign-on</span></span>

<span data-ttu-id="8b39a-271">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8b39a-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b39a-272">Ao clicar no bloco do Boomi no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo Boomi.</span><span class="sxs-lookup"><span data-stu-id="8b39a-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b39a-273">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8b39a-273">Additional resources</span></span>

* [<span data-ttu-id="8b39a-274">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8b39a-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b39a-275">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b39a-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

