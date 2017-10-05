---
title: "Tutorial: integração do Azure Active Directory com o software Cezanne HR | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o software Cezanne HR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="4fe9c-103">Tutorial: integração do Azure Active Directory com o software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="4fe9c-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="4fe9c-104">Neste tutorial, você aprende a integrar o software Cezanne HR ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fe9c-105">A integração do software Cezanne HR ao Azure AD oferece os benefícios a seguir.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="4fe9c-106">Você pode:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-106">You can:</span></span>

- <span data-ttu-id="4fe9c-107">Controle, no Azure AD, quem tem acesso ao software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="4fe9c-108">Habilite seus usuários, com as respectivas contas do Azure AD, a fazer logon automaticamente no software Cezanne HR via SSO (logon único).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4fe9c-109">Gerenciar suas contas em um local central: o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="4fe9c-110">Para saber mais sobre a integração de aplicativos de SaaS (software como serviço) com o Azure AD, consulte [O que é acesso a aplicativos e SSO com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe9c-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4fe9c-111">Prerequisites</span></span>

<span data-ttu-id="4fe9c-112">Para configurar a integração do Azure AD com o software Cezanne HR, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="4fe9c-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4fe9c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="4fe9c-114">Uma assinatura do software Cezanne HR com SSO habilitado</span><span class="sxs-lookup"><span data-stu-id="4fe9c-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fe9c-115">Para testar as etapas deste tutorial, recomendamos que você não use um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="4fe9c-116">Para testar as etapas neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4fe9c-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fe9c-118">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fe9c-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4fe9c-119">Scenario description</span></span>
<span data-ttu-id="4fe9c-120">Neste tutorial, você testa o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="4fe9c-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="4fe9c-122">Adicionando o software Cezanne HR da galeria</span><span class="sxs-lookup"><span data-stu-id="4fe9c-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="4fe9c-123">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe9c-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="4fe9c-124">Adicionar o software Cezanne HR da galeria</span><span class="sxs-lookup"><span data-stu-id="4fe9c-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="4fe9c-125">Para configurar a integração do software Cezanne HR com o Azure AD, adicione o software Cezanne HR, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fe9c-126">Para adicionar o software Cezanne HR da galeria, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="4fe9c-127">No **[portal do Azure](https://portal.azure.com)**, no painel esquerdo, selecione o botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Botão "Azure Active Directory"][1]

2. <span data-ttu-id="4fe9c-129">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![O link "Todos os aplicativos"][2]
    
3. <span data-ttu-id="4fe9c-131">Para adicionar um novo aplicativo, na parte superior da caixa de diálogo **Todos os aplicativos**, selecione **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    ![O botão “Novo aplicativo”][3]

4. <span data-ttu-id="4fe9c-133">Na caixa de pesquisa, digite **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![A caixa de pesquisa](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="4fe9c-135">Na lista de resultados, escolha **software Cezanne HR** e adicione o aplicativo selecionando o botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![A lista de resultados](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4fe9c-137">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe9c-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4fe9c-138">Nesta seção, você configura e testa o SSO do Azure AD com o software Cezanne HR, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fe9c-139">Para o SSO funcionar, o Azure AD precisa saber qual é o equivalente do usuário do Azure AD no software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="4fe9c-140">Em outras palavras, você precisa estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="4fe9c-141">Para estabelecer a relação de vínculo, atribua o valor **nome de usuário** do software Cezanne HR como o valor **Username** do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="4fe9c-142">Para configurar e testar o SSO do Azure AD usando o software Cezanne HR, conclua os blocos de construção a seguir.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="4fe9c-143">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe9c-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="4fe9c-144">Nesta seção, você pode habilitar o SSO do Azure AD no portal do Azure e configura o SSO em seu aplicativo do software Cezanne HR fazendo seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="4fe9c-145">No portal do Azure, na página de integração de aplicativo do **software Cezanne HR**, selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![O comando "Logon único"][4]

2. <span data-ttu-id="4fe9c-147">Para habilitar o SSO, na caixa de diálogo **Logon único**, selecione o **Modo** **Logon baseado em SAML**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![A caixa "Modo"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="4fe9c-149">Em **Domínio e URLs do Software Cezanne HR**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![A seção "URLs e Domínio e URLs do Software Cezanne HR"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="4fe9c-151">a.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-151">a.</span></span> <span data-ttu-id="4fe9c-152">Na caixa **URL de Entrada**, digite uma URL com a seguinte sintaxe: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="4fe9c-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="4fe9c-153">b.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-153">b.</span></span> <span data-ttu-id="4fe9c-154">Na caixa **URL de Resposta**, digite uma URL com a seguinte sintaxe: `https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="4fe9c-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="4fe9c-155">Os valores anteriores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-155">The preceding values are not real.</span></span> <span data-ttu-id="4fe9c-156">Atualize-os com a URL de resposta real e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="4fe9c-157">Para obter os valores, entre em contato com a [equipe de suporte do cliente software Cezanne HR](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="4fe9c-158">Na seção **Certificado de Autenticação do SAML**, selecione **Certificado (Base64)** e salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![A seção “Certificado de Autenticação SAML”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="4fe9c-160">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-160">Select **Save**.</span></span>

    ![Clique no botão “Salvar”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4fe9c-162">Em **Configuração do Software Cezanne HR**, selecione **Configurar o software Cezanne HR** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="4fe9c-163">Copie a **ID da Entidade SAML** e a URL do **Serviço de Logon Único SAML** da seção **Referência Rápida**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![A seção "Configuração do Software Cezanne HR"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="4fe9c-165">Em uma janela diferente do navegador da Web, faça logon em seu locatário do software Cezanne HR como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="4fe9c-166">No painel esquerdo, selecione **Configuração do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="4fe9c-167">Selecione **Configurações de Segurança** > **Configuração de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![O link "Configuração de Logon Único"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="4fe9c-169">No painel **Permitir que os usuários façam logon usando o SSO (Serviço de Logon Único)**, marque a caixa de seleção **SAML 2.0** e selecione a opção **Configuração Avançada**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Opções de logon único em serviços](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="4fe9c-171">Selecione **Adicionar Novo**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-171">Select **Add New**.</span></span>

    ![O botão “Adicionar Novo”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="4fe9c-173">Em **Provedores de Identidade SAML 2.0**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![A seção "Provedores de identidade SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="4fe9c-175">a.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-175">a.</span></span> <span data-ttu-id="4fe9c-176">Na caixa **Nome de Exibição**, insira o nome do seu provedor de Identidade.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="4fe9c-177">b.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-177">b.</span></span> <span data-ttu-id="4fe9c-178">Na caixa **Identificador da Entidade**, cole o **ID da Entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="4fe9c-179">c.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-179">c.</span></span> <span data-ttu-id="4fe9c-180">Na caixa de listagem **Associação SAML**, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="4fe9c-181">d.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-181">d.</span></span> <span data-ttu-id="4fe9c-182">Na caixa **Ponto de Extremidade de Serviço de Token de Segurança**, cole a URL **Serviço de Logon Único SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="4fe9c-183">e.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-183">e.</span></span> <span data-ttu-id="4fe9c-184">Na caixa **Nome do atributo de ID de usuário**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="4fe9c-185">f.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-185">f.</span></span> <span data-ttu-id="4fe9c-186">Para carregar o certificado baixado do Azure AD, selecione o botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="4fe9c-187">g.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-187">g.</span></span> <span data-ttu-id="4fe9c-188">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-188">Select **OK**.</span></span> 

12. <span data-ttu-id="4fe9c-189">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-189">Select **Save**.</span></span>

    ![Clique no botão “Salvar”](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="4fe9c-191">Ao configurar o aplicativo, você pode ler as instruções anteriores em uma versão concisa no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4fe9c-192">Depois de adicionar o aplicativo do **Active Directory**, seção  > **Aplicativos Empresariais**, selecione a guia **Logon único**. Em seguida, acesse a documentação inserida na seção **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="4fe9c-193">Para saber mais sobre o recurso de documentação inserida, consulte [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4fe9c-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fe9c-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe9c-194">Create an Azure AD test user</span></span>
<span data-ttu-id="4fe9c-195">Nesta seção, você cria a usuária de teste Brenda Fernandes no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![A usuária de teste Brenda Fernandes][100]

<span data-ttu-id="4fe9c-197">Para criar um usuário de teste no Azure AD, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="4fe9c-198">No **portal do Azure**, no painel esquerdo, selecione o botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Botão "Azure Active Directory"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fe9c-200">Para exibir a lista de usuários, selecione **Usuários e grupos** > **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![O link “Todos os usuários”](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="4fe9c-202">A caixa de diálogo **Todos os usuários** é aberta.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="4fe9c-203">Para abrir a caixa de diálogo **Usuário**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![O botão “Adicionar”](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fe9c-205">Na caixa de diálogo **Usuário**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-205">In the **User** dialog box, do the following:</span></span>
 
    ![Caixa de diálogo "Usuário"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fe9c-207">a.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-207">a.</span></span> <span data-ttu-id="4fe9c-208">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fe9c-209">b.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-209">b.</span></span> <span data-ttu-id="4fe9c-210">Na caixa **Nome de usuário**, digite o **endereço de email** da usuária Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="4fe9c-211">c.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-211">c.</span></span> <span data-ttu-id="4fe9c-212">Marque a caixa de seleção **Mostrar Senha** e anote o valor gerado na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="4fe9c-213">d.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-213">d.</span></span> <span data-ttu-id="4fe9c-214">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="4fe9c-215">Criar um usuário de teste do software Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="4fe9c-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="4fe9c-216">Para habilitar usuários do Azure AD a entrar no software Cezanne HR, eles deverão ser provisionados no software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="4fe9c-217">No caso do software Cezanne HR, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="4fe9c-218">Provisione uma conta de usuário fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="4fe9c-219">Entre no site da empresa do software Cezanne HR como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="4fe9c-220">No painel esquerdo, selecione **System Setup (Configuração do Sistema)** > **Manage Users (Gerenciar Usuários)** > **Add New User (Adicionar Novo Usuário)**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="4fe9c-221">![O link "Adicionar Novo Usuário"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="4fe9c-222">Em **Person Details (Detalhes Pessoais)**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="4fe9c-223">![A seção "Detalhes Pessoais"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="4fe9c-224">a.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-224">a.</span></span> <span data-ttu-id="4fe9c-225">Defina **Internal User (Usuário Interno)** como **OFF (DESATIVADO)**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="4fe9c-226">b.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-226">b.</span></span> <span data-ttu-id="4fe9c-227">Na caixa **First Name (Nome)**, digite o nome do usuário, por exemplo, **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="4fe9c-228">c.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-228">c.</span></span> <span data-ttu-id="4fe9c-229">Em **Last Name (Sobrenome)**, digite o sobrenome do usuário, por exemplo, **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="4fe9c-230">d.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-230">d.</span></span> <span data-ttu-id="4fe9c-231">Na caixa **Email**, digite o endereço de email do usuário, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="4fe9c-232">Em **Account Information (Informações de Conta)**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fe9c-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="4fe9c-233">![A seção "Informações de conta"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="4fe9c-234">a.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-234">a.</span></span> <span data-ttu-id="4fe9c-235">Na caixa **Username (Nome de Usuário)**, digite o endereço de email do usuário, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="4fe9c-236">b.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-236">b.</span></span> <span data-ttu-id="4fe9c-237">Na caixa **Password (Senha)**, digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="4fe9c-238">c.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-238">c.</span></span> <span data-ttu-id="4fe9c-239">Na caixa **Security Role (Função de Segurança)**, selecione **HR Professional (Profissional de RH)**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="4fe9c-240">d.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-240">d.</span></span> <span data-ttu-id="4fe9c-241">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-241">Select **OK**.</span></span>

5. <span data-ttu-id="4fe9c-242">Na guia **Single sign-on (Logon único)**, na seção **SAML 2.0 Identifiers (Identificadores SAML 2.0)**, selecione **Add New (Adicionar Novo)**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="4fe9c-243">![O botão "Adicionar Novo"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="4fe9c-244">Na caixa de listagem **Identity Provider (Provedor de Identidade)**, selecione seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="4fe9c-245">Na caixa **User Identifier (Identificador de Usuário)**, digite o endereço de email para a conta da usuária de teste Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="4fe9c-246">![As caixas "Provedor de Identidade" e "Identificador de Usuário"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="4fe9c-247">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-247">Select **Save**.</span></span>

    <span data-ttu-id="4fe9c-248">![O botão "Salvar"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="4fe9c-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4fe9c-249">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fe9c-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="4fe9c-250">Nesta seção, você permite que a usuária de teste Brenda Fernandes use o SSO do Azure, concedendo a ela acesso ao software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Testar o acesso do usuário][200] 

1. <span data-ttu-id="4fe9c-252">No Portal do Azure, abra a exibição de aplicativos, vá para a exibição de diretório.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="4fe9c-253">Selecione **Aplicativos empresariais** > **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![O link "Todos os aplicativos"][201] 

2. <span data-ttu-id="4fe9c-255">Na lista de aplicativos, selecione **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![A lista "Aplicativos"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="4fe9c-257">No menu à esquerda, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4fe9c-259">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-259">Select **Add**.</span></span> <span data-ttu-id="4fe9c-260">Em seguida, na caixa de diálogo **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Link “Usuários e Grupos”][203]

5. <span data-ttu-id="4fe9c-262">Na caixa de diálogo **Usuários e grupos**, na lista **Usuários**, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="4fe9c-263">Na caixa de diálogo **Usuários e grupos**, selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="4fe9c-264">Na caixa de diálogo **Adicionar Atribuição**, selecione **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="4fe9c-265">Testar o SSO</span><span class="sxs-lookup"><span data-stu-id="4fe9c-265">Test SSO</span></span>

<span data-ttu-id="4fe9c-266">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="4fe9c-267">Quando selecionar o bloco do software Cezanne HR no Painel de Acesso, você entrará automaticamente no seu aplicativo do software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="4fe9c-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fe9c-268">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fe9c-268">Next steps</span></span>

* [<span data-ttu-id="4fe9c-269">Lista de tutoriais sobre como integrar aplicativos SaaS ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4fe9c-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fe9c-270">O que é acesso a aplicativos e SSO com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fe9c-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

