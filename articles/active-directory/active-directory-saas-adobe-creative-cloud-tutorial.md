---
title: "Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e a Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="55ed4-103">Tutorial: integração do Azure Active Directory com a Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="55ed4-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="55ed4-104">Neste tutorial, você aprenderá a integrar a Adobe Creative Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="55ed4-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55ed4-105">A integração da Adobe Creative Cloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="55ed4-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55ed4-106">No Azure AD, você pode controlar quem tem acesso à Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="55ed4-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="55ed4-107">É possível permitir que seus usuários façam logon automaticamente na Adobe Creative Cloud (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55ed4-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55ed4-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="55ed4-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55ed4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55ed4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55ed4-110">Prerequisites</span></span>

<span data-ttu-id="55ed4-111">Para configurar a integração do Azure AD com a Adobe Creative Cloud, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="55ed4-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="55ed4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55ed4-113">Uma assinatura da Creative Cloud habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="55ed4-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55ed4-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="55ed4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55ed4-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="55ed4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55ed4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="55ed4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="55ed4-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55ed4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55ed4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="55ed4-118">Scenario description</span></span>
<span data-ttu-id="55ed4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="55ed4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55ed4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="55ed4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55ed4-121">Adicionando o Adobe Creative Cloud da Galeria</span><span class="sxs-lookup"><span data-stu-id="55ed4-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="55ed4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="55ed4-123">Adicionando o Adobe Creative Cloud da Galeria</span><span class="sxs-lookup"><span data-stu-id="55ed4-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="55ed4-124">Para configurar a integração da Adobe Creative Cloud com o Azure AD, será necessário adicionar a Creative Cloud da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="55ed4-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55ed4-125">**Para adicionar a Adobe Creative Cloud da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="55ed4-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55ed4-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55ed4-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55ed4-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="55ed4-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="55ed4-133">Na caixa de pesquisa, digite **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="55ed4-135">No painel de resultados, selecione **Adobe Creative Cloud** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55ed4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55ed4-138">Nesta seção, você configurará e testará o logon único do Azure AD com a Adobe Creative Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="55ed4-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55ed4-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário da Adobe Creative Cloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55ed4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="55ed4-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado da Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="55ed4-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de Usuário** na Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="55ed4-142">Para configurar e testar o logon único do Azure AD com a Adobe Creative Cloud, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="55ed4-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55ed4-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="55ed4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="55ed4-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="55ed4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55ed4-145">**[Criando um usuário de teste da Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)** – para ter um equivalente de Brenda Fernandes na Adobe Creative Cloud que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55ed4-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="55ed4-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55ed4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="55ed4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55ed4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55ed4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55ed4-149">Nesta seção, você habilita o logon único do Azure AD no portal de Gerenciamento do Azure e configura o logon único em seu aplicativo Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="55ed4-150">**Para configurar o logon único do Azure AD com a Adobe Creative Cloud, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="55ed4-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="55ed4-151">No portal de Gerenciamento do Azure, na página de integração de aplicativos do **Adobe Creative Cloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="55ed4-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="55ed4-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="55ed4-155">Na seção **Domínio e URLs da Adobe Creative Cloud**, se você desejar configurar o aplicativo em modo iniciado pelo **IdP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="55ed4-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="55ed4-157">a.</span><span class="sxs-lookup"><span data-stu-id="55ed4-157">a.</span></span> <span data-ttu-id="55ed4-158">Na caixa de texto **Identificador**, digite o valor como `https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="55ed4-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="55ed4-159">b.</span><span class="sxs-lookup"><span data-stu-id="55ed4-159">b.</span></span> <span data-ttu-id="55ed4-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="55ed4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55ed4-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="55ed4-161">Please note that these are not the real values.</span></span> <span data-ttu-id="55ed4-162">Você precisa atualizar esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="55ed4-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="55ed4-163">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="55ed4-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="55ed4-164">Se precisar criar um usuário manualmente, será necessário contatar a equipe de suporte da Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="55ed4-165">Na seção **Domínio e URLs da Adobe Creative Cloud**, se você desejar configurar o aplicativo em modo iniciado por **SP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="55ed4-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="55ed4-167">a.</span><span class="sxs-lookup"><span data-stu-id="55ed4-167">a.</span></span> <span data-ttu-id="55ed4-168">Clique na opção **Mostrar URL configurações avançadas**</span><span class="sxs-lookup"><span data-stu-id="55ed4-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="55ed4-169">b.</span><span class="sxs-lookup"><span data-stu-id="55ed4-169">b.</span></span> <span data-ttu-id="55ed4-170">Na caixa de texto **URL de Logon**, digite o valor como: `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="55ed4-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="55ed4-171">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="55ed4-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="55ed4-173">Na seção **Configuração do Adobe Creative Cloud**, clique em **Configurar a Adobe Creative Cloud** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55ed4-174">Copie a **ID da entidade SAML** e a **URL de serviço do SAML SSO** da seção Referência rápida.</span><span class="sxs-lookup"><span data-stu-id="55ed4-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="55ed4-176">Em uma janela diferente do navegador da Web, faça logon em seu locatário da Adobe Creative Cloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="55ed4-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="55ed4-177">Vá para **Identidade** no painel de navegação esquerdo e clique em seu domínio.</span><span class="sxs-lookup"><span data-stu-id="55ed4-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="55ed4-178">Em seguida, siga as etapas na seção **Configuração do logon único necessária**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="55ed4-179">![Configurações](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="55ed4-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="55ed4-180">Clique em **Procurar** para carregar o certificado baixado do Azure AD para o **Certificado do IdP**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="55ed4-181">Na caixa de texto **Emissor IdP**, coloque o valor da **ID da entidade SAML** que você copiou da seção **Configurar logon** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed4-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="55ed4-182">Na caixa de texto **URL de logon IdP**, coloque o valor da **URL de serviço do SAML SSO** que você copiou da seção **Configurar logon** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ed4-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="55ed4-183">Selecione **Redirecionamento HTTP** como **Associação IdP**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="55ed4-184">Selecione **Endereço de email** como **Configuração de logon do usuário**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="55ed4-185">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="55ed4-185">Click **Save** button.</span></span>

15. <span data-ttu-id="55ed4-186">Agra o painel apresentará o arquivo XML **"Baixar metadados"**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="55ed4-187">Ele contém a URL EntityDescriptor e a URL AssertionConsumerService da Adobe.</span><span class="sxs-lookup"><span data-stu-id="55ed4-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="55ed4-188">Abra o arquivo e configure-os no aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55ed4-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="55ed4-191">a.</span><span class="sxs-lookup"><span data-stu-id="55ed4-191">a.</span></span> <span data-ttu-id="55ed4-192">Use o valor EntityDescriptor que a Adobe forneceu a você para **Identificador** na caixa de diálogo **Definir configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="55ed4-193">b.</span><span class="sxs-lookup"><span data-stu-id="55ed4-193">b.</span></span> <span data-ttu-id="55ed4-194">Use o valor AssertionConsumerService que a Adobe forneceu a você para **URL de resposta** na caixa de diálogo **Definir configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55ed4-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="55ed4-196">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55ed4-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="55ed4-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="55ed4-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55ed4-199">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55ed4-201">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="55ed4-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55ed4-203">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55ed4-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="55ed4-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55ed4-207">a.</span><span class="sxs-lookup"><span data-stu-id="55ed4-207">a.</span></span> <span data-ttu-id="55ed4-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55ed4-209">b.</span><span class="sxs-lookup"><span data-stu-id="55ed4-209">b.</span></span> <span data-ttu-id="55ed4-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="55ed4-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55ed4-211">c.</span><span class="sxs-lookup"><span data-stu-id="55ed4-211">c.</span></span> <span data-ttu-id="55ed4-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55ed4-213">d.</span><span class="sxs-lookup"><span data-stu-id="55ed4-213">d.</span></span> <span data-ttu-id="55ed4-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="55ed4-215">Criando um usuário de teste da Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="55ed4-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="55ed4-216">Para que os usuários do Azure AD façam logon na Adobe Creative Cloud, eles devem ser provisionados na Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="55ed4-217">No caso da Adobe Creative Cloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="55ed4-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="55ed4-218">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="55ed4-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="55ed4-219">Faça logon em seu site de empresa da Adobe Creative Cloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="55ed4-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="55ed4-220">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-220">Click **People**.</span></span>

    <span data-ttu-id="55ed4-221">![Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="55ed4-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="55ed4-222">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-222">Click **Invite User**.</span></span>

    <span data-ttu-id="55ed4-223">![Convidar Usuários](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="55ed4-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="55ed4-224">Na página **Convidar Pessoas**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="55ed4-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="55ed4-225">![Convidar Pessoas](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="55ed4-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="55ed4-226">a.</span><span class="sxs-lookup"><span data-stu-id="55ed4-226">a.</span></span> <span data-ttu-id="55ed4-227">Na caixa de texto **Email**, digite o endereço de email da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="55ed4-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="55ed4-228">b.</span><span class="sxs-lookup"><span data-stu-id="55ed4-228">b.</span></span> <span data-ttu-id="55ed4-229">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="55ed4-230">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="55ed4-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55ed4-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55ed4-232">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso à Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="55ed4-234">**Para atribuir Brenda Fernandes à Adobe Creative Cloud, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="55ed4-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="55ed4-235">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="55ed4-237">Na lista de aplicativos, selecione **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="55ed4-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="55ed4-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="55ed4-241">Click **Add** button.</span></span> <span data-ttu-id="55ed4-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="55ed4-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="55ed4-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="55ed4-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55ed4-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55ed4-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55ed4-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="55ed4-247">Testing single sign-on</span></span>

<span data-ttu-id="55ed4-248">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="55ed4-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="55ed4-249">Ao clicar no bloco Adobe Creative Cloud no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="55ed4-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="55ed4-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="55ed4-250">Additional resources</span></span>

* [<span data-ttu-id="55ed4-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="55ed4-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55ed4-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55ed4-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png