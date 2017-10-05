---
title: "Tutorial: integração do Azure Active Directory ao RunMyProcess | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="7ef8f-103">Tutorial: Integração do Active Directory do Azure com o RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="7ef8f-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="7ef8f-104">Neste tutorial, você aprende a integrar o RunMyProcess ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7ef8f-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ef8f-105">A integração do RunMyProcess ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ef8f-106">Você pode controlar no Azure AD quem tem acesso ao RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="7ef8f-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="7ef8f-107">Você pode habilitar seus usuários a fazerem logon automaticamente no RunMyProcess (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ef8f-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ef8f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ef8f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ef8f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ef8f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ef8f-110">Prerequisites</span></span>

<span data-ttu-id="7ef8f-111">Para configurar a integração do Azure AD com o RunMyProcess, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="7ef8f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ef8f-113">Uma assinatura habilitada para logon único do RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="7ef8f-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ef8f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ef8f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ef8f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ef8f-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ef8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ef8f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7ef8f-118">Scenario description</span></span>
<span data-ttu-id="7ef8f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ef8f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ef8f-121">Adicionando o RunMyProcess da galeria</span><span class="sxs-lookup"><span data-stu-id="7ef8f-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="7ef8f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="7ef8f-123">Adicionando o RunMyProcess da galeria</span><span class="sxs-lookup"><span data-stu-id="7ef8f-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="7ef8f-124">Para configurar a integração do RunMyProcess ao Azure AD, você precisa adicionar o RunMyProcess por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ef8f-125">**Para adicionar o RunMyProcess por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ef8f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ef8f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ef8f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7ef8f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7ef8f-133">Na caixa de pesquisa, digite **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-133">In the search box, type **RunMyProcess**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="7ef8f-135">No painel de resultados, selecione **RunMyProcess** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ef8f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ef8f-138">Nesta seção, você configura e testa o logon único do Azure AD com o RunMyProcess, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ef8f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do RunMyProcess é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="7ef8f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="7ef8f-141">No RunMyProcess, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ef8f-142">Para configurar e testar o logon único do Azure AD com o RunMyProcess, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ef8f-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ef8f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ef8f-145">**[Criando um usuário de teste do RunMyProcess](#creating-a-runmyprocess-test-user)** – para ter um equivalente de Brenda Fernandes no RunMyProcess que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ef8f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ef8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ef8f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ef8f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ef8f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="7ef8f-150">**Para configurar o logon único do Azure AD com o RunMyProcess, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="7ef8f-151">No portal do Azure, na página de integração do aplicativo **RunMyProcess**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7ef8f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="7ef8f-155">Na seção **Domínio e URLs do RunMyProcess**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="7ef8f-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="7ef8f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ef8f-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-158">The value is not real.</span></span> <span data-ttu-id="7ef8f-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="7ef8f-160">Contate a [equipe de suporte ao Cliente do RunMyProcess](mailto:support@runmyprocess.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="7ef8f-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="7ef8f-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7ef8f-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ef8f-165">Na seção **Configuração do RunMyProcess**, clique em **Configurar o RunMyProcess** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ef8f-166">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="7ef8f-168">Em uma janela diferente do navegador da Web, faça logon em seu locatário do RunMyProcess como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="7ef8f-169">No painel de navegação esquerdo, clique em **Conta** e selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="7ef8f-171">Vá para a seção **Método de autenticação** e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="7ef8f-173">a.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-173">a.</span></span> <span data-ttu-id="7ef8f-174">Em **Método**, selecione **SSO com Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="7ef8f-175">b.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-175">b.</span></span> <span data-ttu-id="7ef8f-176">Na caixa de texto **Redirecionamento de SSO**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ef8f-177">c.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-177">c.</span></span> <span data-ttu-id="7ef8f-178">Na caixa de texto **Redirecionamento de logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ef8f-179">d.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-179">d.</span></span> <span data-ttu-id="7ef8f-180">Na caixa de texto **Formato da ID de Nome**, digite o valor do **Formato do Identificador de Nome** como **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="7ef8f-181">e.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-181">e.</span></span> <span data-ttu-id="7ef8f-182">Copie o conteúdo do arquivo do certificado baixado e cole-o na caixa de texto **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="7ef8f-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="7ef8f-183">f.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-183">f.</span></span> <span data-ttu-id="7ef8f-184">Clique no ícone **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="7ef8f-185">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7ef8f-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ef8f-186">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ef8f-187">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ef8f-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ef8f-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ef8f-189">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7ef8f-191">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ef8f-192">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ef8f-194">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ef8f-196">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ef8f-198">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ef8f-200">a.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-200">a.</span></span> <span data-ttu-id="7ef8f-201">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ef8f-202">b.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-202">b.</span></span> <span data-ttu-id="7ef8f-203">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ef8f-204">c.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-204">c.</span></span> <span data-ttu-id="7ef8f-205">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ef8f-206">d.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-206">d.</span></span> <span data-ttu-id="7ef8f-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="7ef8f-208">Criando um usuário de teste no RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="7ef8f-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="7ef8f-209">Para permitir que os usuários do Azure AD façam logon no RunMyProcess, eles devem ser provisionados no RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="7ef8f-210">No caso do RunMyProcess, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="7ef8f-211">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7ef8f-212">Faça logon em seu site de empresa do RunMyProcess como administrador.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="7ef8f-213">Clique em **Conta** e selecione **Usuários** no painel de navegação esquerdo, clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="7ef8f-214">![Novo Usuário](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="7ef8f-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="7ef8f-215">Na seção **Configurações do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7ef8f-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7ef8f-216">![Perfil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="7ef8f-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="7ef8f-217">a.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-217">a.</span></span> <span data-ttu-id="7ef8f-218">Digite o **Nome** e o **Email** de uma conta válida do Azure AD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="7ef8f-219">b.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-219">b.</span></span> <span data-ttu-id="7ef8f-220">Selecione uma **Linguagem IDE**, um **Idioma** e um **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="7ef8f-221">c.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-221">c.</span></span> <span data-ttu-id="7ef8f-222">Selecione **Enviar email de criação da conta para mim**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="7ef8f-223">d.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-223">d.</span></span> <span data-ttu-id="7ef8f-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="7ef8f-225">Você pode usar qualquer outra ferramenta de criação da conta de usuário do RunMyProcess ou as APIs fornecidas pelo RunMyProcess para provisionar as contas de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ef8f-226">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ef8f-227">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7ef8f-229">**Para atribuir Brenda Fernandes ao RunMyProcess, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7ef8f-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="7ef8f-230">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7ef8f-232">Na lista de aplicativos, escolha **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="7ef8f-234">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7ef8f-236">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-236">Click **Add** button.</span></span> <span data-ttu-id="7ef8f-237">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7ef8f-239">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ef8f-240">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ef8f-241">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ef8f-242">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7ef8f-242">Testing single sign-on</span></span>

<span data-ttu-id="7ef8f-243">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7ef8f-244">Quando você clica no bloco RunMyProcess no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="7ef8f-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ef8f-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7ef8f-245">Additional resources</span></span>

* [<span data-ttu-id="7ef8f-246">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7ef8f-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ef8f-247">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ef8f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

