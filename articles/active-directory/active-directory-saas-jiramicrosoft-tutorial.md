---
title: "Tutorial: Integração do Azure Active Directory ao SSO do SAML para o JIRA da Microsoft | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SSO do SAML para o JIRA da Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="9f983-103">Tutorial: Integração do Azure Active Directory ao SSO do SAML para o JIRA da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9f983-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="9f983-104">Neste tutorial, você aprende a integrar o SSO do SAML para o JIRA da Microsoft ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9f983-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f983-105">A integração do SSO do SAML para o JIRA da Microsoft ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9f983-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9f983-106">No Azure AD, é possível controlar quem tem acesso ao SSO do SAML para o JIRA da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9f983-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="9f983-107">É possível permitir que os usuários se conectem automaticamente ao SSO do SAML para o JIRA da Microsoft (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f983-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f983-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9f983-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f983-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f983-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f983-110">Prerequisites</span></span>

<span data-ttu-id="9f983-111">Para configurar a integração do Azure AD ao SSO do SAML para o JIRA da Microsoft, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9f983-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="9f983-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f983-113">Aplicativo para servidores do JIRA instalado em um servidor do Windows de 64 bits (localmente ou na infraestrutura de IaaS na nuvem)</span><span class="sxs-lookup"><span data-stu-id="9f983-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="9f983-114">O servidor do JIRA é habilitado para HTTPS</span><span class="sxs-lookup"><span data-stu-id="9f983-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="9f983-115">Observe que as versões com suporte no Plug-in do JIRA são mencionadas na seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="9f983-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="9f983-116">O servidor do JIRA é acessível pela Internet, especialmente na página de Logon do Azure AD para autenticação e deve conseguir receber o token do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f983-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="9f983-117">As credenciais do administrador são configuradas no JIRA</span><span class="sxs-lookup"><span data-stu-id="9f983-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="9f983-118">O WebSudo está desabilitado no JIRA</span><span class="sxs-lookup"><span data-stu-id="9f983-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="9f983-119">Usuário de teste criado no aplicativo para servidores do JIRA</span><span class="sxs-lookup"><span data-stu-id="9f983-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="9f983-120">Para testar as etapas deste tutorial, não recomendamos o uso de um ambiente de produção do JIRA.</span><span class="sxs-lookup"><span data-stu-id="9f983-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="9f983-121">Teste a integração primeiro no ambiente de desenvolvimento ou de preparo do aplicativo e, em seguida, use o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9f983-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="9f983-122">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9f983-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f983-123">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9f983-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f983-124">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f983-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="9f983-125">Versões com suporte do JIRA</span><span class="sxs-lookup"><span data-stu-id="9f983-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="9f983-126">A partir de agora, há suporte para as seguintes versões do JIRA:</span><span class="sxs-lookup"><span data-stu-id="9f983-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="9f983-127">JIRA Core e Software: 6.0 a 7.2.0</span><span class="sxs-lookup"><span data-stu-id="9f983-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="9f983-128">JIRA Service Desk: 3.0 a 3.2</span><span class="sxs-lookup"><span data-stu-id="9f983-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f983-129">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9f983-129">Scenario description</span></span>
<span data-ttu-id="9f983-130">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9f983-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f983-131">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9f983-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f983-132">Adicionando o SSO do SAML para o JIRA da Microsoft por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="9f983-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="9f983-133">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="9f983-134">Adicionando o SSO do SAML para o JIRA da Microsoft por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="9f983-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="9f983-135">Para configurar a integração do SSO do SAML para o JIRA da Microsoft ao Azure AD, é necessário adicionar o SSO do SAML para o JIRA da Microsoft à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="9f983-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9f983-136">**Para adicionar o SSO do SAML para o JIRA da Microsoft por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f983-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9f983-137">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f983-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f983-139">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9f983-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9f983-140">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f983-140">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9f983-142">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f983-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9f983-144">Na caixa de pesquisa, digite **SSO do SAML para o JIRA da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9f983-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="9f983-146">No painel de resultados, selecione **SSO do SAML para o JIRA da Microsoft** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f983-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f983-148">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f983-149">Nesta seção, você configura e testa o logon único do Azure AD com o SSO do SAML para o JIRA da Microsoft, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9f983-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f983-150">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SSO do SAML para o JIRA da Microsoft é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f983-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="9f983-151">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SSO do SAML para o JIRA da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="9f983-152">No SSO do SAML para o JIRA da Microsoft, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9f983-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9f983-153">Para configurar e testar o logon único do Azure AD com o SSO do SAML para o JIRA da Microsoft, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9f983-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9f983-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9f983-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9f983-155">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f983-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f983-156">**[Criando um usuário de teste do SSO do SAML para o JIRA da Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)** – para ter um equivalente de Brenda Fernandes no SSO do SAML para o JIRA da Microsoft que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f983-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f983-157">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f983-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f983-158">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9f983-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f983-159">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f983-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f983-160">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SSO do SAML para o JIRA da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="9f983-161">**Para configurar o logon único do Azure AD com o SSO do SAML para o JIRA da Microsoft, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f983-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="9f983-162">No portal do Azure, na página de integração do aplicativo **SSO do SAML para o JIRA da Microsoft**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9f983-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9f983-164">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9f983-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="9f983-166">Na seção **Domínio e URLs do SSO do SAML para o JIRA da Microsoft**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f983-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="9f983-168">a.</span><span class="sxs-lookup"><span data-stu-id="9f983-168">a.</span></span> <span data-ttu-id="9f983-169">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="9f983-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="9f983-170">b.</span><span class="sxs-lookup"><span data-stu-id="9f983-170">b.</span></span> <span data-ttu-id="9f983-171">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="9f983-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="9f983-172">c.</span><span class="sxs-lookup"><span data-stu-id="9f983-172">c.</span></span> <span data-ttu-id="9f983-173">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="9f983-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f983-174">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9f983-174">These values are not real.</span></span> <span data-ttu-id="9f983-175">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="9f983-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9f983-176">A porta é opcional, caso seja uma URL nomeada.</span><span class="sxs-lookup"><span data-stu-id="9f983-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="9f983-177">Esses valores são recebidos durante a configuração do plug-in do Jira, que é explicada adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="9f983-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="9f983-178">Para gerar a URL de **Metadados**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f983-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="9f983-179">a.</span><span class="sxs-lookup"><span data-stu-id="9f983-179">a.</span></span> <span data-ttu-id="9f983-180">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9f983-180">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="9f983-182">b.</span><span class="sxs-lookup"><span data-stu-id="9f983-182">b.</span></span> <span data-ttu-id="9f983-183">Clique em **Pontos de extremidade** para abrir a caixa de diálogo **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="9f983-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="9f983-185">c.</span><span class="sxs-lookup"><span data-stu-id="9f983-185">c.</span></span> <span data-ttu-id="9f983-186">Clique no botão copiar para copiar a URL **DOCUMENTO DE METADADOS DE FEDERAÇÃO** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="9f983-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="9f983-188">d.</span><span class="sxs-lookup"><span data-stu-id="9f983-188">d.</span></span> <span data-ttu-id="9f983-189">Agora, acesse a página de propriedades do **SSO do SAML para o JIRA da Microsoft** e copie a **ID do Aplicativo** usando o botão **Copiar** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="9f983-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="9f983-191">e.</span><span class="sxs-lookup"><span data-stu-id="9f983-191">e.</span></span> <span data-ttu-id="9f983-192">Gere a **URL de Metadados** usando o padrão `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copie esse valor no bloco de notas, pois ele será usado posteriormente para a configuração do plug-in.</span><span class="sxs-lookup"><span data-stu-id="9f983-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="9f983-193">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9f983-193">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f983-195">Contate a [Microsoft](mailto:waadpartners@microsoft.com) com as seguintes informações sobre o plug-in do JIRA.</span><span class="sxs-lookup"><span data-stu-id="9f983-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="9f983-196">Nome do cliente:</span><span class="sxs-lookup"><span data-stu-id="9f983-196">Customer Name:</span></span>
    *   <span data-ttu-id="9f983-197">Nome de domínio primário:</span><span class="sxs-lookup"><span data-stu-id="9f983-197">Primary domain name:</span></span>
    *   <span data-ttu-id="9f983-198">Azure AD Premium: sim/não (o plug-in estará disponível para todos os SKUs de clientes Gratuito, Básico e Premium)</span><span class="sxs-lookup"><span data-stu-id="9f983-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="9f983-199">Número de usuários que usarão essa integração:</span><span class="sxs-lookup"><span data-stu-id="9f983-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="9f983-200">Versão do JIRA:</span><span class="sxs-lookup"><span data-stu-id="9f983-200">JIRA Version:</span></span>
    *   <span data-ttu-id="9f983-201">Comentários:</span><span class="sxs-lookup"><span data-stu-id="9f983-201">Comments:</span></span>

7. <span data-ttu-id="9f983-202">Em outra janela do navegador da Web, faça logon na instância do JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f983-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="9f983-203">Passe o cursor do mouse sobre a engrenagem e clique em **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="9f983-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="9f983-205">Na seção da guia Complementos, clique em **Gerenciar complementos**.</span><span class="sxs-lookup"><span data-stu-id="9f983-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="9f983-207">Carregue manualmente o plug-in fornecido pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="9f983-208">Depois que o plug-in for instalado, ele será exibido na seção de complementos **Instalados pelo Usuário** da seção **Gerenciar Complemento**.</span><span class="sxs-lookup"><span data-stu-id="9f983-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="9f983-209">Clique em **Configurar** para configurar o novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="9f983-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="9f983-210">Realize as seguintes etapas na página de configuração:</span><span class="sxs-lookup"><span data-stu-id="9f983-210">Perform following steps on configuration page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="9f983-212">a.</span><span class="sxs-lookup"><span data-stu-id="9f983-212">a.</span></span> <span data-ttu-id="9f983-213">Em **URL de Metadados**, cole a **URL de Metadados** gerada no Azure AD e clique no botão **Resolver**.</span><span class="sxs-lookup"><span data-stu-id="9f983-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="9f983-214">Ele lê a URL de metadados do IdP e popula todas as informações dos campos.</span><span class="sxs-lookup"><span data-stu-id="9f983-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="9f983-215">O local padrão da ID de Usuário SAML é o Identificador de Nome.</span><span class="sxs-lookup"><span data-stu-id="9f983-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="9f983-216">Você pode alterar isso para uma opção de atributo e inserir o nome de atributo apropriado.</span><span class="sxs-lookup"><span data-stu-id="9f983-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="9f983-217">Verifique se há apenas um certificado mapeado no aplicativo, para que não haja nenhum erro na resolução dos metadados.</span><span class="sxs-lookup"><span data-stu-id="9f983-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="9f983-218">Se houver vários certificados, após a resolução dos metadados, o administrador receberá um erro.</span><span class="sxs-lookup"><span data-stu-id="9f983-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="9f983-219">b.</span><span class="sxs-lookup"><span data-stu-id="9f983-219">b.</span></span> <span data-ttu-id="9f983-220">Copie os valores de **Identificador, URL de Resposta e URL de Logon** e cole-os nas caixas de texto **Identificador, URL de Resposta e URL de Logon**, respectivamente, na seção **Domínio e URLs do SSO do SAML para o JIRA da Microsoft** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f983-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="9f983-221">c.</span><span class="sxs-lookup"><span data-stu-id="9f983-221">c.</span></span> <span data-ttu-id="9f983-222">Em **Nome do Botão de Logon**, digite o nome do botão que sua organização deseja que os usuários vejam na tela de logon.</span><span class="sxs-lookup"><span data-stu-id="9f983-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="9f983-223">d.</span><span class="sxs-lookup"><span data-stu-id="9f983-223">d.</span></span> <span data-ttu-id="9f983-224">Em **Locais da ID de Usuário SAML**, selecione **A ID de Usuário está no elemento NameIdentifier da instrução Subject** ou **A ID de Usuário está em um elemento Attribute**.</span><span class="sxs-lookup"><span data-stu-id="9f983-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="9f983-225">Essa ID deve ser a ID de usuário do JIRA.</span><span class="sxs-lookup"><span data-stu-id="9f983-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="9f983-226">Se a ID de usuário não tiver uma correspondência, o sistema não permitirá que os usuários façam logon.</span><span class="sxs-lookup"><span data-stu-id="9f983-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="9f983-227">e.</span><span class="sxs-lookup"><span data-stu-id="9f983-227">e.</span></span> <span data-ttu-id="9f983-228">Se você selecionar a opção **A ID de Usuário está em um elemento Attribute**, na caixa de texto **Nome do atributo**, digite o nome do atributo em que a ID de Usuário é esperada.</span><span class="sxs-lookup"><span data-stu-id="9f983-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="9f983-229">f.</span><span class="sxs-lookup"><span data-stu-id="9f983-229">f.</span></span> <span data-ttu-id="9f983-230">Se estiver usando o domínio federado (como o ADFS, etc.) com o Azure AD, clique na opção **Habilitar Descoberta de Realm Inicial** e configure o **Nome de Domínio**.</span><span class="sxs-lookup"><span data-stu-id="9f983-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="9f983-231">g.</span><span class="sxs-lookup"><span data-stu-id="9f983-231">g.</span></span> <span data-ttu-id="9f983-232">Em **Nome de Domínio**, digite o nome de domínio aqui, no caso do logon baseado no ADFS.</span><span class="sxs-lookup"><span data-stu-id="9f983-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="9f983-233">h.</span><span class="sxs-lookup"><span data-stu-id="9f983-233">h.</span></span> <span data-ttu-id="9f983-234">Marque a opção **Habilitar Logoff Único** se desejar fazer logoff do Azure AD quando um usuário fizer logoff do JIRA.</span><span class="sxs-lookup"><span data-stu-id="9f983-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="9f983-235">i.</span><span class="sxs-lookup"><span data-stu-id="9f983-235">i.</span></span> <span data-ttu-id="9f983-236">Clique no botão **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="9f983-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="9f983-237">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9f983-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9f983-238">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9f983-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9f983-239">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f983-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f983-240">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f983-241">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f983-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9f983-243">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f983-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9f983-244">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f983-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f983-246">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f983-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f983-248">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f983-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f983-250">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f983-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f983-252">a.</span><span class="sxs-lookup"><span data-stu-id="9f983-252">a.</span></span> <span data-ttu-id="9f983-253">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9f983-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f983-254">b.</span><span class="sxs-lookup"><span data-stu-id="9f983-254">b.</span></span> <span data-ttu-id="9f983-255">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f983-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f983-256">c.</span><span class="sxs-lookup"><span data-stu-id="9f983-256">c.</span></span> <span data-ttu-id="9f983-257">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9f983-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9f983-258">d.</span><span class="sxs-lookup"><span data-stu-id="9f983-258">d.</span></span> <span data-ttu-id="9f983-259">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9f983-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="9f983-260">Criando um usuário de teste do SSO do SAML para o JIRA da Microsoft</span><span class="sxs-lookup"><span data-stu-id="9f983-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="9f983-261">Para permitir que os usuários do Azure AD façam logon no servidor local do JIRA, eles devem ser provisionados no SSO do SAML para o JIRA da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="9f983-262">Para o SSO do SAML para o JIRA da Microsoft, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9f983-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="9f983-263">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f983-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="9f983-264">Faça logon no servidor local do JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="9f983-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="9f983-265">Passe o cursor do mouse sobre a engrenagem e clique em **Gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f983-265">Hover on cog and click the **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="9f983-267">Você será redirecionado à página de acesso de administrador para inserir a **Senha** e clicar no botão **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="9f983-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="9f983-269">Na seção da guia **Gerenciamento de usuário**, clique em **criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f983-269">Under **User management** tab section, click **create user**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="9f983-271">Na página da caixa de diálogo **"Criar novo usuário"**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9f983-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="9f983-273">a.</span><span class="sxs-lookup"><span data-stu-id="9f983-273">a.</span></span> <span data-ttu-id="9f983-274">Na caixa de texto **Endereço de email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9f983-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="9f983-275">b.</span><span class="sxs-lookup"><span data-stu-id="9f983-275">b.</span></span> <span data-ttu-id="9f983-276">Na caixa de texto **Nome completo**, digite o nome completo do usuário, como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9f983-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="9f983-277">c.</span><span class="sxs-lookup"><span data-stu-id="9f983-277">c.</span></span> <span data-ttu-id="9f983-278">Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9f983-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="9f983-279">d.</span><span class="sxs-lookup"><span data-stu-id="9f983-279">d.</span></span> <span data-ttu-id="9f983-280">Na caixa de texto **Senha**, digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="9f983-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="9f983-281">e.</span><span class="sxs-lookup"><span data-stu-id="9f983-281">e.</span></span> <span data-ttu-id="9f983-282">Clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="9f983-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9f983-283">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9f983-284">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao SSO do SAML para o JIRA da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9f983-286">**Para atribuir Brenda Fernandes ao SSO do SAML para o JIRA da Microsoft, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9f983-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="9f983-287">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9f983-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9f983-289">Na lista de aplicativos, selecione **SSO do SAML para o JIRA da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9f983-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="9f983-291">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9f983-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9f983-293">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9f983-293">Click **Add** button.</span></span> <span data-ttu-id="9f983-294">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f983-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9f983-296">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9f983-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9f983-297">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f983-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f983-298">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9f983-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f983-299">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9f983-299">Testing single sign-on</span></span>

<span data-ttu-id="9f983-300">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9f983-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9f983-301">Quando você clicar no bloco do SSO do SAML para o JIRA da Microsoft no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo SSO do SAML para o JIRA da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f983-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="9f983-302">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9f983-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f983-303">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f983-303">Additional resources</span></span>

* [<span data-ttu-id="9f983-304">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9f983-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f983-305">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f983-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

