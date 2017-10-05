---
title: "Tutorial: integração do Azure Active Directory ao Atlassian Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Atlassian Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="cba4e-103">Tutorial: Integração do Azure Active Directory com o Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="cba4e-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="cba4e-104">Neste tutorial, você aprenderá a integrar o Atlassian Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cba4e-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cba4e-105">A integração do Atlassian Cloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cba4e-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cba4e-106">No Azure AD, você pode controlar quem tem acesso ao Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="cba4e-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="cba4e-107">Você pode habilitar os usuários a fazer logon automaticamente no Atlassian Cloud (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cba4e-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cba4e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cba4e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cba4e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cba4e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cba4e-110">Prerequisites</span></span>

<span data-ttu-id="cba4e-111">Para configurar a integração do Azure AD com o Atlassian Cloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cba4e-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="cba4e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cba4e-113">Uma assinatura do Atlassian Cloud habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="cba4e-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cba4e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cba4e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cba4e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cba4e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cba4e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cba4e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cba4e-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cba4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cba4e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cba4e-118">Scenario description</span></span>
<span data-ttu-id="cba4e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cba4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cba4e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cba4e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cba4e-121">Adição do Atlassian Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="cba4e-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="cba4e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="cba4e-123">Adição do Atlassian Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="cba4e-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="cba4e-124">Para configurar a integração do Atlassian Cloud ao Azure AD, você precisará adicionar o Atlassian Cloud da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cba4e-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cba4e-125">**Para adicionar o Atlassian Cloud da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cba4e-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cba4e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cba4e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cba4e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cba4e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cba4e-133">Na caixa de pesquisa, digite **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="cba4e-135">No painel de resultados, selecione **Atlassian Cloud** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cba4e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cba4e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Atlassian Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cba4e-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cba4e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Atlassian Cloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cba4e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="cba4e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="cba4e-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD ao valor de **Nome de usuário** no Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="cba4e-142">Para configurar e testar o logon único do Azure AD com o Atlassian Cloud, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cba4e-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cba4e-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cba4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cba4e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cba4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cba4e-145">**[Criação de um usuário de teste do Atlassian Cloud](#creating-an-atlassian-cloud-test-user)** – para ter um equivalente de Brenda Fernandes no Atlassian Cloud que esteja vinculado à sua representação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cba4e-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cba4e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cba4e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cba4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cba4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cba4e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cba4e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cba4e-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="cba4e-150">**Para configurar o logon único do Azure AD com o Atlassian Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cba4e-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="cba4e-151">No portal do Azure, na página de integração de aplicativo do **Atlassian Cloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cba4e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cba4e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="cba4e-155">Na seção **URLs e Domínio do Atlassian Cloud**, se desejar configurar o aplicativo em modo iniciado pelo **IDP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="cba4e-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="cba4e-157">a.</span><span class="sxs-lookup"><span data-stu-id="cba4e-157">a.</span></span> <span data-ttu-id="cba4e-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="cba4e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="cba4e-159">b.</span><span class="sxs-lookup"><span data-stu-id="cba4e-159">b.</span></span> <span data-ttu-id="cba4e-160">Na caixa de texto **URL de Resposta**, digite uma URL como: `https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="cba4e-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="cba4e-161">Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:</span><span class="sxs-lookup"><span data-stu-id="cba4e-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="cba4e-163">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="cba4e-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cba4e-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="cba4e-164">These values are not real.</span></span> <span data-ttu-id="cba4e-165">Atualize esses valores com o Identificador e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="cba4e-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="cba4e-166">Você pode obter os valores exatos na tela Configuração do SAML do Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="cba4e-167">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="cba4e-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="cba4e-169">Na seção **Configuração do Atlassian Cloud**, clique em **Configurar Atlassian Cloud** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cba4e-170">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="cba4e-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="cba4e-172">Para configurar o SSO para seu aplicativo, faça logon no Portal do Atlassian usando os direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="cba4e-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="cba4e-173">Na seção Autenticação do painel de navegação esquerdo, clique em **Domínios**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="cba4e-175">a.</span><span class="sxs-lookup"><span data-stu-id="cba4e-175">a.</span></span> <span data-ttu-id="cba4e-176">Na caia de texto, digite seu nome de domínio e clique em **Adicionar domínio**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="cba4e-178">b.</span><span class="sxs-lookup"><span data-stu-id="cba4e-178">b.</span></span> <span data-ttu-id="cba4e-179">Para verificar o domínio, clique em **Verificar**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-179">To verify the domain, click **Verify**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="cba4e-181">c.</span><span class="sxs-lookup"><span data-stu-id="cba4e-181">c.</span></span> <span data-ttu-id="cba4e-182">Baixe o arquivo html de verificação de domínio, carregue-o na pasta raiz do site do seu domínio e, em seguida, clique em **Verificar domínio**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="cba4e-184">d.</span><span class="sxs-lookup"><span data-stu-id="cba4e-184">d.</span></span> <span data-ttu-id="cba4e-185">Depois que o domínio for verificado, o valor do campo **Status** será **Verificado**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="cba4e-187">Na barra de navegação à esquerda, clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="cba4e-189">Crie uma Configuração de SAML e adicione a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="cba4e-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="cba4e-191">a.</span><span class="sxs-lookup"><span data-stu-id="cba4e-191">a.</span></span> <span data-ttu-id="cba4e-192">Na caixa de texto **ID da Entidade do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cba4e-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cba4e-193">b.</span><span class="sxs-lookup"><span data-stu-id="cba4e-193">b.</span></span> <span data-ttu-id="cba4e-194">Na caixa de texto **URL de SSO do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cba4e-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cba4e-195">c.</span><span class="sxs-lookup"><span data-stu-id="cba4e-195">c.</span></span> <span data-ttu-id="cba4e-196">Abra o certificado baixado do portal do Azure, copie os valores sem as linhas Begin e End e cole-os na caixa **Certificado X509 público**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="cba4e-197">d.</span><span class="sxs-lookup"><span data-stu-id="cba4e-197">d.</span></span> <span data-ttu-id="cba4e-198">Clique em **Salvar Configuração** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="cba4e-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="cba4e-199">Atualize as configurações do Azure AD para garantir que você configurou a URL do Identificador correta.</span><span class="sxs-lookup"><span data-stu-id="cba4e-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="cba4e-200">a.</span><span class="sxs-lookup"><span data-stu-id="cba4e-200">a.</span></span> <span data-ttu-id="cba4e-201">Copie a **ID de Identidade do SP** da tela SAML e cole-a no Azure AD como o valor do **Identificador**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="cba4e-202">b.</span><span class="sxs-lookup"><span data-stu-id="cba4e-202">b.</span></span> <span data-ttu-id="cba4e-203">A URL de Entrada é a URL do locatário do seu Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="cba4e-205">No portal do Azure, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-205">In the Azure portal, Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="cba4e-207">Agora, é possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="cba4e-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cba4e-208">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cba4e-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cba4e-209">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cba4e-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cba4e-210">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="cba4e-211">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cba4e-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cba4e-213">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cba4e-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cba4e-214">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cba4e-216">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cba4e-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cba4e-218">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cba4e-220">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cba4e-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cba4e-222">a.</span><span class="sxs-lookup"><span data-stu-id="cba4e-222">a.</span></span> <span data-ttu-id="cba4e-223">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cba4e-224">b.</span><span class="sxs-lookup"><span data-stu-id="cba4e-224">b.</span></span> <span data-ttu-id="cba4e-225">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cba4e-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cba4e-226">c.</span><span class="sxs-lookup"><span data-stu-id="cba4e-226">c.</span></span> <span data-ttu-id="cba4e-227">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cba4e-228">d.</span><span class="sxs-lookup"><span data-stu-id="cba4e-228">d.</span></span> <span data-ttu-id="cba4e-229">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="cba4e-230">Criação de um usuário de teste do Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="cba4e-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="cba4e-231">Para que os usuários do Azure AD possam fazer logon no Atlassian Cloud, eles devem ser provisionados no Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="cba4e-232">No caso do Atlassian Cloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cba4e-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="cba4e-233">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cba4e-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cba4e-234">Na seção Administração do site, clique no botão **Usuários**</span><span class="sxs-lookup"><span data-stu-id="cba4e-234">In the Site administration section, click the **Users** button</span></span>

    ![Criar usuário do Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="cba4e-236">Clique no botão **Criar Usuário** para criar um usuário no Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="cba4e-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Criar usuário do Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="cba4e-238">Insira o **Endereço de email**, o **Nome de usuário** e o **Nome completo** do usuário e atribua o acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Criar usuário do Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="cba4e-240">Clique no botão **Criar usuário** para enviar o convite por email ao usuário. Quando aceitar o convite, o usuário ficará ativo no sistema.</span><span class="sxs-lookup"><span data-stu-id="cba4e-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="cba4e-241">Você também pode criar os usuários em massa clicando no botão **Criar em Massa** na seção Usuários.</span><span class="sxs-lookup"><span data-stu-id="cba4e-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cba4e-242">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cba4e-243">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cba4e-245">**Para atribuir Brenda Fernandes ao Atlassian Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cba4e-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="cba4e-246">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cba4e-248">Na lista de aplicativos, selecione **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="cba4e-250">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cba4e-252">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cba4e-252">Click **Add** button.</span></span> <span data-ttu-id="cba4e-253">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cba4e-255">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cba4e-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cba4e-256">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cba4e-257">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cba4e-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cba4e-258">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cba4e-258">Testing single sign-on</span></span>

<span data-ttu-id="cba4e-259">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cba4e-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="cba4e-260">Ao clicar no bloco Atlassian Cloud no Painel de Acesso, você deve entrar automaticamente no aplicativo Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="cba4e-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="cba4e-261">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cba4e-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cba4e-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cba4e-262">Additional resources</span></span>

* [<span data-ttu-id="cba4e-263">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cba4e-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cba4e-264">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cba4e-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

