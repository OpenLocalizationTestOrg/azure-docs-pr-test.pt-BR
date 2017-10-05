---
title: "Tutorial: Integração do Azure Active Directory ao Birst Agile Business Analytics | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Birst Agile Business Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="48c26-103">Tutorial: Integração do Active Directory do Azure ao Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="48c26-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="48c26-104">Neste tutorial, você aprende a integrar o Birst Agile Business Analytics ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="48c26-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48c26-105">A integração do Birst Agile Business Analytics ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="48c26-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48c26-106">Você pode controlar no AD do Azure quem tem acesso ao Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="48c26-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="48c26-107">Você pode permitir que os usuários façam logon automaticamente no Birst Agile Business Analytics (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48c26-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48c26-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48c26-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48c26-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="48c26-110">Prerequisites</span></span>

<span data-ttu-id="48c26-111">Para configurar a integração do AD do Azure ao Birst Agile Business Analytics, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="48c26-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="48c26-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48c26-113">Uma assinatura do Birst Agile Business Analytics com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="48c26-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48c26-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="48c26-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48c26-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="48c26-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48c26-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="48c26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48c26-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48c26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48c26-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="48c26-118">Scenario description</span></span>
<span data-ttu-id="48c26-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="48c26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48c26-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="48c26-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48c26-121">Adicionando o Birst Agile Business Analytics a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="48c26-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="48c26-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="48c26-123">Adicionando o Birst Agile Business Analytics a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="48c26-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="48c26-124">Para configurar a integração do Birst Agile Business Analytics ao AD do Azure, você precisará adicionar o Birst Agile Business Analytics à sua lista de aplicativos de SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="48c26-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48c26-125">**Para adicionar o Birst Agile Business Analytics da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="48c26-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48c26-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48c26-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48c26-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="48c26-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48c26-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="48c26-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="48c26-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48c26-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="48c26-133">Na caixa de pesquisa, digite **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="48c26-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="48c26-135">No painel de resultados, selecione **Birst Agile Business Analytics** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48c26-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48c26-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48c26-138">Nesta seção, você configura e testa o logon único do Azure AD com o Birst Agile Business Analytics, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="48c26-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48c26-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Birst Agile Business Analytics é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c26-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="48c26-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="48c26-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="48c26-141">No Birst Agile Business Analytics, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="48c26-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48c26-142">Para configurar e testar o logon único do AD do Azure com o Birst Agile Business Analytics, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="48c26-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48c26-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="48c26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48c26-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="48c26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48c26-145">**[Criando um usuário de teste do Birst Agile Business Analytics](#creating-a-birst-agile-business-analytics-test-user)** – para ter um equivalente de Brenda Fernandes no Birst Agile Business Analytics que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48c26-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48c26-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="48c26-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48c26-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="48c26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48c26-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="48c26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48c26-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="48c26-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="48c26-150">**Para configurar o logon único do AD do Azure com o Birst Agile Business Analytics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="48c26-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="48c26-151">No portal do Azure, na página de integração do aplicativo do **Birst Agile Business Analytics**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="48c26-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="48c26-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="48c26-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="48c26-155">Na seção **Domínio e URLs do Birst Agile Business Analytics**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="48c26-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="48c26-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="48c26-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="48c26-158">A URL depende do datacenter em que sua conta do Birst está localizada:</span><span class="sxs-lookup"><span data-stu-id="48c26-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="48c26-159">Para um datacenter nos EUA, use o seguinte padrão: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="48c26-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="48c26-160">Para um datacenter na Europa, use o seguinte padrão: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="48c26-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48c26-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="48c26-161">This value is not real.</span></span> <span data-ttu-id="48c26-162">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="48c26-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="48c26-163">Contate a [equipe de suporte ao Cliente do Birst Agile Business Analytics](mailto:info@birst.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="48c26-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="48c26-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="48c26-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="48c26-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="48c26-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48c26-168">Na seção **Configuração do Birst Agile Business Analytics**, clique em **Configurar o Birst Agile Business Analytics** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="48c26-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48c26-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="48c26-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="48c26-171">Para configurar o logon único no lado do **Birst Agile Business Analytics**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="48c26-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="48c26-172">Mencione para a equipe do Birst que essa integração precisa do Algoritmo SHA256 (o SHA1 não terá suporte), de modo que eles possam definir o SSO no servidor apropriado, como **app2101**, etc.</span><span class="sxs-lookup"><span data-stu-id="48c26-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="48c26-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="48c26-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48c26-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="48c26-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48c26-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48c26-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48c26-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="48c26-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="48c26-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="48c26-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="48c26-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48c26-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48c26-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48c26-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="48c26-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48c26-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48c26-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48c26-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="48c26-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48c26-188">a.</span><span class="sxs-lookup"><span data-stu-id="48c26-188">a.</span></span> <span data-ttu-id="48c26-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="48c26-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48c26-190">b.</span><span class="sxs-lookup"><span data-stu-id="48c26-190">b.</span></span> <span data-ttu-id="48c26-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="48c26-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48c26-192">c.</span><span class="sxs-lookup"><span data-stu-id="48c26-192">c.</span></span> <span data-ttu-id="48c26-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="48c26-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48c26-194">d.</span><span class="sxs-lookup"><span data-stu-id="48c26-194">d.</span></span> <span data-ttu-id="48c26-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="48c26-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="48c26-196">Criando um usuário de teste do Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="48c26-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="48c26-197">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="48c26-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="48c26-198">Trabalhe com a [equipe de suporte do Birst Agile Business Analytics](mailto:info@birst.com) para adicionar os usuários à conta do Birst.</span><span class="sxs-lookup"><span data-stu-id="48c26-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48c26-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48c26-200">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="48c26-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="48c26-202">**Para atribuir Brenda Fernandes ao Birst Agile Business Analytics, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="48c26-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="48c26-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="48c26-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="48c26-205">Na lista de aplicativos, escolha **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="48c26-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="48c26-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="48c26-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="48c26-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="48c26-209">Click **Add** button.</span></span> <span data-ttu-id="48c26-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48c26-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="48c26-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="48c26-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48c26-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48c26-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48c26-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48c26-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48c26-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="48c26-215">Testing single sign-on</span></span>

<span data-ttu-id="48c26-216">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="48c26-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="48c26-217">Ao clicar no bloco do Birst Agile Business Analytics no Painel de Acesso, você deverá fazer logon automaticamente em seu aplicativo Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="48c26-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48c26-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="48c26-218">Additional resources</span></span>

* [<span data-ttu-id="48c26-219">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="48c26-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48c26-220">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48c26-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

