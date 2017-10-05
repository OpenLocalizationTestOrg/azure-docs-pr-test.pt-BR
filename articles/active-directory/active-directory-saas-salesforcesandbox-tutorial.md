---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="4b1fe-103">Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce</span><span class="sxs-lookup"><span data-stu-id="4b1fe-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="4b1fe-104">Neste tutorial, você aprende a integrar o Salesforce Sandbox ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b1fe-105">A integração do Salesforce Sandbox ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b1fe-106">No Azure AD, é possível controlar quem tem acesso ao Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b1fe-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="4b1fe-107">É possível permitir que os usuários se conectem automaticamente ao Salesforce Sandbox (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b1fe-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b1fe-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b1fe-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b1fe-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b1fe-110">Prerequisites</span></span>

<span data-ttu-id="4b1fe-111">Para configurar a integração do Azure AD ao Salesforce Sandbox, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="4b1fe-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b1fe-113">Uma assinatura habilitada para logon único do Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b1fe-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b1fe-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b1fe-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b1fe-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b1fe-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b1fe-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4b1fe-118">Scenario description</span></span>
<span data-ttu-id="4b1fe-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b1fe-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b1fe-121">Adicionando o Salesforce Sandbox por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4b1fe-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="4b1fe-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="4b1fe-123">Adicionando o Salesforce Sandbox por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4b1fe-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="4b1fe-124">Para configurar a integração do Salesforce Sandbox ao Azure AD, é necessário adicionar o Salesforce Sandbox à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b1fe-125">**Para adicionar o Salesforce Sandbox por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1fe-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b1fe-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b1fe-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4b1fe-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4b1fe-133">Na caixa de pesquisa, digite **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="4b1fe-135">No painel de resultados, selecione **Salesforce Sandbox** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b1fe-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b1fe-138">Nesta seção, você configura e testa o logon único do Azure AD com o Salesforce Sandbox, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b1fe-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Salesforce Sandbox é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="4b1fe-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="4b1fe-141">Essa relação de vínculo é estabelecida com a atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="4b1fe-142">Para configurar e testar o logon único do Azure AD com o Salesforce Sandbox, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b1fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b1fe-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b1fe-145">**[Criando um usuário de teste do Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)** – para ter um equivalente de Brenda Fernandes no Salesforce Sandbox que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b1fe-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b1fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b1fe-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b1fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b1fe-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="4b1fe-150">**Para configurar o logon único do Azure AD com o Salesforce Sandbox, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1fe-151">No portal do Azure, na página de integração do aplicativo **Salesforce Sandbox**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4b1fe-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="4b1fe-155">Na seção **Domínio e URLs do Salesforce Sandbox**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="4b1fe-157">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4b1fe-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b1fe-158">Esse valor não é o real.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-158">This value is not the real.</span></span> <span data-ttu-id="4b1fe-159">Atualize esse valor com a URL de Logon real. Contate a [equipe de suporte ao Cliente do Salesforce Sandbox](https://help.salesforce.com/support) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="4b1fe-160">Se já tiver configurado o logon único para outra instância de Área restrita do Salesforce em seu diretório, você também deve configurar o **Identificador** para ter o mesmo valor que a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="4b1fe-161">O campo **Identificador** pode ser encontrado marcando a caixa de seleção **Mostrar configurações avançadas** na página **Configurar URL do Aplicativo** da caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="4b1fe-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="4b1fe-162">Na seção **Certificado de Autenticação SAML**, clique em **Certificado** e, em seguida, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="4b1fe-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4b1fe-164">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4b1fe-166">Na seção **Configuração do Salesforce Sandbox**, clique em **Configurar o Salesforce Sandbox** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b1fe-167">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="4b1fe-168">![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="4b1fe-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="4b1fe-169">Abra uma nova guia no navegador e faça logon em sua conta Administrador do Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="4b1fe-170">No menu na parte superior, clique em **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-170">In the menu on the top, click **Setup**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="4b1fe-172">No painel de navegação à esquerda, clique em **Controles de Segurança** e clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="4b1fe-174">Na seção Configurações de Logon Único, realize as seguintes etapas: ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="4b1fe-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="4b1fe-175">a.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-175">a.</span></span>  <span data-ttu-id="4b1fe-176">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="4b1fe-177">b.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-177">b.</span></span>  <span data-ttu-id="4b1fe-178">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-178">Click **New**.</span></span>

12. <span data-ttu-id="4b1fe-179">Na seção Configurações de Logon Único de SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="4b1fe-181">a. Na caixa de texto Nome, digite o nome da configuração (por exemplo: *SPSSOWAAD\_Teste*).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="4b1fe-182">b.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-182">b.</span></span> <span data-ttu-id="4b1fe-183">Cole o valor da **ID da Entidade SAML** na caixa de texto **Emissor**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="4b1fe-184">c.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-184">c.</span></span> <span data-ttu-id="4b1fe-185">Na caixa de texto **ID da Entidade**, digite **https://test.salesforce.com** se essa for a primeira instância do Salesforce Sandbox que você está adicionando ao diretório.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="4b1fe-186">Se você já tiver adicionado uma instância da Área restrita do Salesforce, para a **ID da Entidade**, digite a **URL de Logon** que deve estar no seguinte formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4b1fe-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="4b1fe-187">d.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-187">d.</span></span> <span data-ttu-id="4b1fe-188">Clique em **Procurar** para carregar o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="4b1fe-189">e.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-189">e.</span></span> <span data-ttu-id="4b1fe-190">Para o **Tipo de Identidade SAML**, selecione **A declaração contém a ID de Federação do objeto de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="4b1fe-191">f.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-191">f.</span></span> <span data-ttu-id="4b1fe-192">Para **Local de Identidade SAML**, selecione **A identidade está no elemento NameIdentifier da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="4b1fe-193">g.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-193">g.</span></span> <span data-ttu-id="4b1fe-194">Cole a **URL do Serviço de Logon Único** na caixa de texto **URL de Logon do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="4b1fe-195">h.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-195">h.</span></span> <span data-ttu-id="4b1fe-196">O SFDC não dá suporte a logout SAML.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="4b1fe-197">Como alternativa, cole “https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0” na caixa de texto **URL de Logoff do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="4b1fe-198">i.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-198">i.</span></span> <span data-ttu-id="4b1fe-199">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="4b1fe-200">j.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-200">j.</span></span> <span data-ttu-id="4b1fe-201">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="4b1fe-202">Habilitar seu domínio</span><span class="sxs-lookup"><span data-stu-id="4b1fe-202">Enable your domain</span></span>
<span data-ttu-id="4b1fe-203">Esta seção pressupõe que você já tenha criado um domínio.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="4b1fe-204">Para obter mais informações, consulte [Definindo o nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="4b1fe-205">**Para habilitar seu domínio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1fe-206">No painel de navegação esquerdo, clique em **Gerenciamento de Domínio** e clique em **Meu Domínio.**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="4b1fe-208">Verifique se o domínio foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="4b1fe-209">Na seção **Configurações de Página de Logon**, clique em **Editar** e, para o **Serviço de Autenticação**, selecione o nome da Configuração de Logon Único SAML da seção anterior e, por fim, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="4b1fe-211">Assim que você tiver um domínio configurado, seus usuários deverão usar a URL do domínio para fazer logon na área restrita Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="4b1fe-212">Para obter o valor da URL, clique no perfil SSO criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="4b1fe-213">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4b1fe-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b1fe-214">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b1fe-215">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b1fe-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b1fe-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b1fe-217">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4b1fe-219">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1fe-220">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b1fe-222">para exibir a lista de usuários, acesse **Usuários e grupos** e clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b1fe-224">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b1fe-226">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b1fe-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b1fe-228">a.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-228">a.</span></span> <span data-ttu-id="4b1fe-229">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b1fe-230">b.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-230">b.</span></span> <span data-ttu-id="4b1fe-231">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b1fe-232">c.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-232">c.</span></span> <span data-ttu-id="4b1fe-233">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b1fe-234">d.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-234">d.</span></span> <span data-ttu-id="4b1fe-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="4b1fe-236">Criando um usuário de teste do Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="4b1fe-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="4b1fe-237">Nesta seção, um usuário chamado Brenda Fernandes é criado no Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="4b1fe-238">O Salesforce Sandbox dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="4b1fe-239">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-239">There is no action item for you in this section.</span></span> <span data-ttu-id="4b1fe-240">Se um usuário ainda não existir no Salesforce Sandbox, um novo será criado quando você tentar acessar o Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b1fe-241">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b1fe-242">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4b1fe-244">**Para atribuir Brenda Fernandes ao Salesforce Sandbox, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b1fe-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="4b1fe-245">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4b1fe-247">Na lista de aplicativos, selecione **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="4b1fe-249">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4b1fe-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-251">Click **Add** button.</span></span> <span data-ttu-id="4b1fe-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4b1fe-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b1fe-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b1fe-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b1fe-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4b1fe-257">Testing single sign-on</span></span>

<span data-ttu-id="4b1fe-258">Se você quiser testar suas configurações de SSO, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4b1fe-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="4b1fe-259">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b1fe-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b1fe-260">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4b1fe-260">Additional resources</span></span>

* [<span data-ttu-id="4b1fe-261">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b1fe-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b1fe-262">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b1fe-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4b1fe-263">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="4b1fe-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

