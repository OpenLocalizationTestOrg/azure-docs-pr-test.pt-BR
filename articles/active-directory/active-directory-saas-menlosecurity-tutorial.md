---
title: "Tutorial: Integração do Azure Active Directory com o Menlo Security | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Menlo Security."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="19b8c-103">Tutorial: Integração do Azure Active Directory com o Menlo Security</span><span class="sxs-lookup"><span data-stu-id="19b8c-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="19b8c-104">Neste tutorial, você aprenderá a integrar o Menlo Security ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="19b8c-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19b8c-105">A integração do Menlo Security com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="19b8c-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="19b8c-106">No Azure AD, é possível controlar quem tem acesso ao Menlo Security</span><span class="sxs-lookup"><span data-stu-id="19b8c-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="19b8c-107">Você pode permitir que seus usuários façam logon automaticamente no Menlo Security (Logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="19b8c-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19b8c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="19b8c-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="19b8c-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="19b8c-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19b8c-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19b8c-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19b8c-111">Prerequisites</span></span>

<span data-ttu-id="19b8c-112">Para configurar a integração do Azure AD ao Menlo Security, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="19b8c-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="19b8c-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="19b8c-114">Uma assinatura do Menlo Security habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="19b8c-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19b8c-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="19b8c-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19b8c-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="19b8c-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19b8c-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="19b8c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19b8c-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19b8c-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19b8c-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="19b8c-119">Scenario description</span></span>
<span data-ttu-id="19b8c-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="19b8c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19b8c-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="19b8c-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19b8c-122">Adicionar o Menlo Security a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="19b8c-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="19b8c-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="19b8c-124">Adicionar o Menlo Security a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="19b8c-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="19b8c-125">Para configurar a integração do Menlo Security ao Azure AD, você precisa adicionar o Menlo Security da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="19b8c-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="19b8c-126">**Para adicionar o Menlo Security da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19b8c-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="19b8c-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="19b8c-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="19b8c-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="19b8c-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="19b8c-134">Na caixa de pesquisa, digite **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-134">In the search box, type **Menlo Security**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="19b8c-136">No painel de resultados, selecione **Menlo Security** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19b8c-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19b8c-139">Nesta seção, você configura e testa o logon único do Azure AD com o Menlo Security com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="19b8c-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="19b8c-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Menlo Security é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b8c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="19b8c-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="19b8c-142">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como sendo o valor de **Nome de Usuário** no Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="19b8c-143">Para configurar e testar o logon único do AD do Azure com o Menlo Security, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="19b8c-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="19b8c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="19b8c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="19b8c-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19b8c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19b8c-146">**[Criar um usuário de teste do Menlo Security](#creating-a-menlo-security-test-user)** – para ter um equivalente de Brenda Fernandes no Menlo Security que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b8c-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="19b8c-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="19b8c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19b8c-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="19b8c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19b8c-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="19b8c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19b8c-150">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="19b8c-151">**Para configurar o logon único do Azure AD com o Menlo Security, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19b8c-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="19b8c-152">No Portal do Azure, na página de integração de aplicativos do **Menlo Security**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="19b8c-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="19b8c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="19b8c-156">Na seção **URLs e Domínio do Menlo Security**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="19b8c-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="19b8c-158">a.</span><span class="sxs-lookup"><span data-stu-id="19b8c-158">a.</span></span> <span data-ttu-id="19b8c-159">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="19b8c-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="19b8c-160">b.</span><span class="sxs-lookup"><span data-stu-id="19b8c-160">b.</span></span> <span data-ttu-id="19b8c-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="19b8c-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="19b8c-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="19b8c-162">These values are not the real.</span></span> <span data-ttu-id="19b8c-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="19b8c-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="19b8c-164">Contate a [equipe de suporte do cliente Menlo Security](https://www.menlosecurity.com/menlo-contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="19b8c-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="19b8c-165">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e então salve o arquivo do Certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="19b8c-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="19b8c-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="19b8c-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="19b8c-169">Na seção **Configuração do Menlo Security**, clique em **Configurar o Menlo Security** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="19b8c-170">Copie a **ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="19b8c-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar o logon único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="19b8c-172">Para configurar o logon único no lado do **Menlo Security**, faça logon em no site do **Menlo Security** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="19b8c-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="19b8c-173">Em **Configurações**, acesse **Autenticação** e execute as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="19b8c-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="19b8c-175">a.</span><span class="sxs-lookup"><span data-stu-id="19b8c-175">a.</span></span> <span data-ttu-id="19b8c-176">Marque a caixa de seleção **Habilitar a autenticação de usuário usando o SAML**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="19b8c-177">b.</span><span class="sxs-lookup"><span data-stu-id="19b8c-177">b.</span></span> <span data-ttu-id="19b8c-178">Selecione **Permitir o Acesso Externo** como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="19b8c-179">c.</span><span class="sxs-lookup"><span data-stu-id="19b8c-179">c.</span></span> <span data-ttu-id="19b8c-180">Em **Provedor SAML**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="19b8c-181">d.</span><span class="sxs-lookup"><span data-stu-id="19b8c-181">d.</span></span> <span data-ttu-id="19b8c-182">**Ponto de extremidade SAML 2.0**: cole a **URL de serviço de logon único SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="19b8c-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19b8c-183">e.</span><span class="sxs-lookup"><span data-stu-id="19b8c-183">e.</span></span> <span data-ttu-id="19b8c-184">**Identificador de Serviço (Emissor)**: cole a **ID da entidade SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="19b8c-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="19b8c-185">f.</span><span class="sxs-lookup"><span data-stu-id="19b8c-185">f.</span></span> <span data-ttu-id="19b8c-186">**Certificado X.509**: abra o **Certificado (Base64)** baixado do Portal do Azure no bloco de notas e copie-o nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="19b8c-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="19b8c-187">g.</span><span class="sxs-lookup"><span data-stu-id="19b8c-187">g.</span></span> <span data-ttu-id="19b8c-188">Clique em **Salvar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="19b8c-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="19b8c-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="19b8c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="19b8c-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="19b8c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="19b8c-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19b8c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19b8c-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="19b8c-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19b8c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="19b8c-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19b8c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="19b8c-196">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19b8c-198">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="19b8c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19b8c-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19b8c-202">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="19b8c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19b8c-204">a.</span><span class="sxs-lookup"><span data-stu-id="19b8c-204">a.</span></span> <span data-ttu-id="19b8c-205">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19b8c-206">b.</span><span class="sxs-lookup"><span data-stu-id="19b8c-206">b.</span></span> <span data-ttu-id="19b8c-207">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="19b8c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19b8c-208">c.</span><span class="sxs-lookup"><span data-stu-id="19b8c-208">c.</span></span> <span data-ttu-id="19b8c-209">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="19b8c-210">d.</span><span class="sxs-lookup"><span data-stu-id="19b8c-210">d.</span></span> <span data-ttu-id="19b8c-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="19b8c-212">Criar um usuário de teste do Menlo Security</span><span class="sxs-lookup"><span data-stu-id="19b8c-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="19b8c-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="19b8c-214">Trabalhe com a [Equipe de suporte ao cliente do Menlo Security](https://www.menlosecurity.com/menlo-contact) para adicionar os usuários à plataforma do Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="19b8c-215">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="19b8c-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="19b8c-216">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="19b8c-217">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo acesso ao Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="19b8c-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="19b8c-219">**Para atribuir Brenda Fernandes ao Menlo Security, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="19b8c-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="19b8c-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="19b8c-222">Na lista de aplicativos, selecione **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-222">In the applications list, select **Menlo Security**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="19b8c-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="19b8c-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="19b8c-226">Click **Add** button.</span></span> <span data-ttu-id="19b8c-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="19b8c-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="19b8c-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="19b8c-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19b8c-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="19b8c-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19b8c-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="19b8c-232">Testing single sign-on</span></span>

<span data-ttu-id="19b8c-233">Nesta seção, você testará sua configuração de logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b8c-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="19b8c-234">Abra uma janela de navegador em um modo "InPrivate" ou "Anônimo" para disparar uma nova autenticação.</span><span class="sxs-lookup"><span data-stu-id="19b8c-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="19b8c-235">No Internet Explorer, use Ctrl + Shift + P.</span><span class="sxs-lookup"><span data-stu-id="19b8c-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="19b8c-236">No Chrome, use Ctrl + Shift + N.</span><span class="sxs-lookup"><span data-stu-id="19b8c-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="19b8c-237">Na janela de navegação privada, navegue até um recurso protegido e realize um logon do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b8c-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="19b8c-238">Após o logon bem-sucedido, você será levado para o site solicitado em uma sessão de isolamento.</span><span class="sxs-lookup"><span data-stu-id="19b8c-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19b8c-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="19b8c-239">Additional resources</span></span>

* [<span data-ttu-id="19b8c-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="19b8c-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19b8c-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19b8c-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

