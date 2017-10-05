---
title: "Tutorial: Integração do Azure Active Directory ao LiquidFiles | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: b858c6d26b78be4641a46b3453f53d103b512356
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="9dba4-103">Tutorial: Integração do Azure Active Directory ao LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9dba4-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="9dba4-104">Neste tutorial, você aprende a integrar o LiquidFiles ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9dba4-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9dba4-105">A integração do LiquidFiles ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="9dba4-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9dba4-106">No Azure AD, é possível controlar quem tem acesso ao LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9dba4-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="9dba4-107">É possível permitir que os usuários se conectem automaticamente ao LiquidFiles (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dba4-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9dba4-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9dba4-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9dba4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dba4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9dba4-110">Prerequisites</span></span>

<span data-ttu-id="9dba4-111">Para configurar a integração do Azure AD ao LiquidFiles, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9dba4-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="9dba4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9dba4-113">Uma assinatura habilitada para logon único do LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9dba4-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9dba4-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9dba4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9dba4-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9dba4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9dba4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9dba4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9dba4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9dba4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9dba4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9dba4-118">Scenario description</span></span>
<span data-ttu-id="9dba4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9dba4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9dba4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="9dba4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9dba4-121">Adicionando o LiquidFiles por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="9dba4-121">Adding LiquidFiles from the gallery</span></span>
2. <span data-ttu-id="9dba4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="9dba4-123">Adicionando o LiquidFiles por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="9dba4-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="9dba4-124">Para configurar a integração do LiquidFiles ao Azure AD, é necessário adicionar o LiquidFiles à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="9dba4-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9dba4-125">**Para adicionar o LiquidFiles por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9dba4-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9dba4-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9dba4-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9dba4-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9dba4-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9dba4-133">Na caixa de pesquisa, digite **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-133">In the search box, type **LiquidFiles**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="9dba4-135">No painel de resultados, selecione **LiquidFiles** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9dba4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9dba4-138">Nesta seção, você configura e testa o logon único do Azure AD com o LiquidFiles, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9dba4-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9dba4-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LiquidFiles é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dba4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="9dba4-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="9dba4-141">No LiquidFiles, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9dba4-142">Para configurar e testar o logon único do Azure AD com o LiquidFiles, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="9dba4-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9dba4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9dba4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9dba4-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dba4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9dba4-145">**[Criando um usuário de teste do LiquidFiles](#creating-a-liquidfiles-test-user)** – para ter um equivalente de Brenda Fernandes no LiquidFiles que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dba4-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9dba4-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dba4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9dba4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="9dba4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9dba4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9dba4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9dba4-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="9dba4-150">**Para configurar o logon único do Azure AD com o LiquidFiles, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9dba4-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="9dba4-151">No portal do Azure, na página de integração do aplicativo **LiquidFiles**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9dba4-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="9dba4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="9dba4-155">Na seção **Domínio e URLs do LiquidFiles**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9dba4-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="9dba4-157">a.</span><span class="sxs-lookup"><span data-stu-id="9dba4-157">a.</span></span> <span data-ttu-id="9dba4-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="9dba4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="9dba4-159">b.</span><span class="sxs-lookup"><span data-stu-id="9dba4-159">b.</span></span> <span data-ttu-id="9dba4-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="9dba4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="9dba4-161">c.</span><span class="sxs-lookup"><span data-stu-id="9dba4-161">c.</span></span> <span data-ttu-id="9dba4-162">b.</span><span class="sxs-lookup"><span data-stu-id="9dba4-162">b.</span></span> <span data-ttu-id="9dba4-163">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="9dba4-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9dba4-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9dba4-164">These values are not real.</span></span> <span data-ttu-id="9dba4-165">Atualize esses valores com a URL de Logon, o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="9dba4-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="9dba4-166">Contate a [equipe de suporte ao Cliente do LiquidFiles](https://www.liquidfiles.com/support.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="9dba4-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="9dba4-167">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="9dba4-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="9dba4-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9dba4-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9dba4-171">Na seção **Configuração do LiquidFiles**, clique em **Configurar o LiquidFiles** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9dba4-172">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="9dba4-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="9dba4-174">Faça logon em seu site de empresa do LiquidFiles como administrador.</span><span class="sxs-lookup"><span data-stu-id="9dba4-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="9dba4-175">Clique em **Logon Único** em **Administrador > Configuração** no menu.</span><span class="sxs-lookup"><span data-stu-id="9dba4-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

9. <span data-ttu-id="9dba4-176">Na página **Configuração de Logon Único**, realize as seguintes etapas</span><span class="sxs-lookup"><span data-stu-id="9dba4-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="9dba4-178">a.</span><span class="sxs-lookup"><span data-stu-id="9dba4-178">a.</span></span> <span data-ttu-id="9dba4-179">Em **Método de Logon Único**, selecione **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="9dba4-180">b.</span><span class="sxs-lookup"><span data-stu-id="9dba4-180">b.</span></span> <span data-ttu-id="9dba4-181">Na caixa de texto **URL de Logon do IDP**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dba4-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9dba4-182">c.</span><span class="sxs-lookup"><span data-stu-id="9dba4-182">c.</span></span> <span data-ttu-id="9dba4-183">Na caixa de texto **URL de Logoff do IDP**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dba4-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9dba4-184">d.</span><span class="sxs-lookup"><span data-stu-id="9dba4-184">d.</span></span> <span data-ttu-id="9dba4-185">Na caixa de texto **Impressão Digital do Certificado do IDP**, cole o valor da **IMPRESSÃO DIGITAL** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9dba4-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="9dba4-186">e.</span><span class="sxs-lookup"><span data-stu-id="9dba4-186">e.</span></span> <span data-ttu-id="9dba4-187">Na caixa de texto Formato do Identificador de Nome, digite o valor **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="9dba4-188">f.</span><span class="sxs-lookup"><span data-stu-id="9dba4-188">f.</span></span> <span data-ttu-id="9dba4-189">Na caixa de texto Contexto de Autenticação, digite o valor **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="9dba4-190">g.</span><span class="sxs-lookup"><span data-stu-id="9dba4-190">g.</span></span> <span data-ttu-id="9dba4-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="9dba4-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="9dba4-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9dba4-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="9dba4-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9dba4-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9dba4-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9dba4-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="9dba4-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dba4-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9dba4-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9dba4-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9dba4-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9dba4-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9dba4-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9dba4-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9dba4-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9dba4-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9dba4-207">a.</span><span class="sxs-lookup"><span data-stu-id="9dba4-207">a.</span></span> <span data-ttu-id="9dba4-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9dba4-209">b.</span><span class="sxs-lookup"><span data-stu-id="9dba4-209">b.</span></span> <span data-ttu-id="9dba4-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="9dba4-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9dba4-211">c.</span><span class="sxs-lookup"><span data-stu-id="9dba4-211">c.</span></span> <span data-ttu-id="9dba4-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9dba4-213">d.</span><span class="sxs-lookup"><span data-stu-id="9dba4-213">d.</span></span> <span data-ttu-id="9dba4-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="9dba4-215">Criando um usuário de teste do LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9dba4-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="9dba4-216">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="9dba4-217">Trabalhe com o administrador do servidor do LiquidFiles para ser adicionado como um usuário antes de fazer logon no aplicativo LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9dba4-218">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9dba4-219">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9dba4-221">**Para atribuir Brenda Fernandes ao LiquidFiles, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="9dba4-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="9dba4-222">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9dba4-224">Na lista de aplicativos, selecione **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-224">In the applications list, select **LiquidFiles**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="9dba4-226">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9dba4-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9dba4-228">Click **Add** button.</span></span> <span data-ttu-id="9dba4-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9dba4-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="9dba4-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9dba4-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9dba4-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9dba4-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9dba4-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9dba4-234">Testing single sign-on</span></span>

<span data-ttu-id="9dba4-235">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="9dba4-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9dba4-236">Quando você clicar no bloco do LiquidFiles no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9dba4-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9dba4-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9dba4-237">Additional resources</span></span>

* [<span data-ttu-id="9dba4-238">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9dba4-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9dba4-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9dba4-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

