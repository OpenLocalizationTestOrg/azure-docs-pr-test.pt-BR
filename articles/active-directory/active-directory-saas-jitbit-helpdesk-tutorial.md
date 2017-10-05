---
title: "Tutorial: Integração do Azure Active Directory com o Jitbit Helpdesk | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="f4abe-103">Tutorial: Integração do Active Directory do Azure com o Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="f4abe-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="f4abe-104">Neste tutorial, você aprenderá a integrar o Jitbit Helpdesk ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f4abe-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4abe-105">A integração do Jitbit Helpdesk ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f4abe-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f4abe-106">No Azure AD, é possível controlar quem tem acesso ao Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="f4abe-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="f4abe-107">Você pode permitir que seus usuários façam logon automaticamente no Jitbit Helpdesk (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4abe-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4abe-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f4abe-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4abe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4abe-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f4abe-110">Prerequisites</span></span>

<span data-ttu-id="f4abe-111">Para configurar a integração do Azure AD ao Jitbit Helpdesk, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f4abe-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="f4abe-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4abe-113">Uma assinatura habilitada para logon único do Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="f4abe-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4abe-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f4abe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4abe-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f4abe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4abe-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f4abe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4abe-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4abe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4abe-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f4abe-118">Scenario description</span></span>
<span data-ttu-id="f4abe-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f4abe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4abe-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f4abe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4abe-121">Adicionando Jitbit Helpdesk da galeria</span><span class="sxs-lookup"><span data-stu-id="f4abe-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="f4abe-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="f4abe-123">Adicionando Jitbit Helpdesk da galeria</span><span class="sxs-lookup"><span data-stu-id="f4abe-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="f4abe-124">Para configurar a integração do Jitbit Helpdesk ao Azure AD, você precisará adicionar o Jitbit Helpdesk da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f4abe-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f4abe-125">**Para adicionar o Jitbit Helpdesk por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4abe-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f4abe-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f4abe-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f4abe-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f4abe-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f4abe-133">Na caixa de pesquisa, digite **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="f4abe-135">No painel de resultados, selecione **Jitbit Helpdesk** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4abe-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4abe-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Jitbit Helpdesk, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f4abe-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f4abe-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jitbit Helpdesk é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4abe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="f4abe-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="f4abe-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="f4abe-141">No Jitbit Helpdesk, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f4abe-142">Para configurar e testar o logon único do Azure AD com o Jitbit Helpdesk, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f4abe-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f4abe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f4abe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f4abe-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4abe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4abe-145">**[Criação de um usuário de teste do Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**: para ter um equivalente da Brenda Fernandes no Jitbit Helpdesk que está vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4abe-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4abe-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4abe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4abe-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f4abe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4abe-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4abe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4abe-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="f4abe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="f4abe-150">**Para configurar o logon único do Azure AD com o Jitbit Helpdesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4abe-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="f4abe-151">No portal do Azure, na página de integração de aplicativos do **Jitbit Helpdesk**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f4abe-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f4abe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="f4abe-155">Na seção **URLs e Domínio do Jitbit Helpdesk**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4abe-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="f4abe-157">a.</span><span class="sxs-lookup"><span data-stu-id="f4abe-157">a.</span></span> <span data-ttu-id="f4abe-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="f4abe-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="f4abe-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f4abe-159">This value is not real.</span></span> <span data-ttu-id="f4abe-160">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="f4abe-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f4abe-161">Para obter esse valor, entre em contato com a [equipe de suporte do cliente Jitbit Helpdesk](https://www.jitbit.com/support/).</span><span class="sxs-lookup"><span data-stu-id="f4abe-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="f4abe-162">b.</span><span class="sxs-lookup"><span data-stu-id="f4abe-162">b.</span></span>  <span data-ttu-id="f4abe-163">Na caixa de texto **Identificador**, digite uma URL conforme a seguir: `https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="f4abe-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="f4abe-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="f4abe-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="f4abe-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f4abe-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f4abe-168">Na seção **Configuração do Jitbit Helpdesk**, clique em **Configurar Jitbit Helpdesk** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f4abe-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="f4abe-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="f4abe-171">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Jitbit Helpdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="f4abe-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="f4abe-172">Na barra de ferramentas na parte superior, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="f4abe-173">![Administração](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="f4abe-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="f4abe-174">Clique em **Configurações gerais**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="f4abe-175">![Usuários, empresas e permissões](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Usuários, empresas e permissões")</span><span class="sxs-lookup"><span data-stu-id="f4abe-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="f4abe-176">Na seção de configuração **Configurações de autenticação** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4abe-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="f4abe-177">![Configurações de autenticação](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Configurações de autenticação")</span><span class="sxs-lookup"><span data-stu-id="f4abe-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="f4abe-178">a.</span><span class="sxs-lookup"><span data-stu-id="f4abe-178">a.</span></span> <span data-ttu-id="f4abe-179">Selecione **Habilitar logon único SAML 2.0** para entrar usando SSO (Logon Único) com **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="f4abe-180">b.</span><span class="sxs-lookup"><span data-stu-id="f4abe-180">b.</span></span> <span data-ttu-id="f4abe-181">Na caixa de texto **URL do Ponto de Extremidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4abe-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f4abe-182">c.</span><span class="sxs-lookup"><span data-stu-id="f4abe-182">c.</span></span> <span data-ttu-id="f4abe-183">Abra seu certificado codificado em **base 64** no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509**</span><span class="sxs-lookup"><span data-stu-id="f4abe-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="f4abe-184">d.</span><span class="sxs-lookup"><span data-stu-id="f4abe-184">d.</span></span> <span data-ttu-id="f4abe-185">Clique em **Salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f4abe-186">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f4abe-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f4abe-187">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f4abe-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f4abe-188">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4abe-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4abe-189">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4abe-190">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4abe-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f4abe-192">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4abe-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f4abe-193">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4abe-195">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f4abe-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4abe-197">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4abe-199">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f4abe-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4abe-201">a.</span><span class="sxs-lookup"><span data-stu-id="f4abe-201">a.</span></span> <span data-ttu-id="f4abe-202">Na caixa de texto **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="f4abe-203">b.</span><span class="sxs-lookup"><span data-stu-id="f4abe-203">b.</span></span> <span data-ttu-id="f4abe-204">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f4abe-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4abe-205">c.</span><span class="sxs-lookup"><span data-stu-id="f4abe-205">c.</span></span> <span data-ttu-id="f4abe-206">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f4abe-207">d.</span><span class="sxs-lookup"><span data-stu-id="f4abe-207">d.</span></span> <span data-ttu-id="f4abe-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="f4abe-209">Criação de um usuário de teste do Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="f4abe-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="f4abe-210">Para permitir que os usuários do AD do Azure façam logon no Jitbit Helpdesk, eles devem ser provisionados no Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="f4abe-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="f4abe-211">No caso do Jitbit Helpdesk, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f4abe-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="f4abe-212">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4abe-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f4abe-213">Faça logon em seu locatário do **Jitbit Helpdesk** .</span><span class="sxs-lookup"><span data-stu-id="f4abe-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="f4abe-214">No menu na parte superior, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="f4abe-215">![Administração](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="f4abe-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="f4abe-216">Clique em **Usuários, empresas e permissões**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="f4abe-217">![Usuários, empresas e permissões](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Usuários, empresas e permissões")</span><span class="sxs-lookup"><span data-stu-id="f4abe-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="f4abe-218">Clique em **Adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="f4abe-219">![Adicionar Usuário](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="f4abe-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="f4abe-220">Na seção Criar, digite os dados da conta do Azure AD que deseja provisionar da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f4abe-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="f4abe-221">![Criar](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="f4abe-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="f4abe-222">a.</span><span class="sxs-lookup"><span data-stu-id="f4abe-222">a.</span></span> <span data-ttu-id="f4abe-223">Na caixa de texto **Nome de Usuário**, digite **BrendaFernandes**, o nome de usuário como no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4abe-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="f4abe-224">b.</span><span class="sxs-lookup"><span data-stu-id="f4abe-224">b.</span></span> <span data-ttu-id="f4abe-225">Na caixa de texto **Email**, digite o email do usuário como **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="f4abe-226">c.</span><span class="sxs-lookup"><span data-stu-id="f4abe-226">c.</span></span> <span data-ttu-id="f4abe-227">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="f4abe-228">d.</span><span class="sxs-lookup"><span data-stu-id="f4abe-228">d.</span></span> <span data-ttu-id="f4abe-229">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="f4abe-230">e.</span><span class="sxs-lookup"><span data-stu-id="f4abe-230">e.</span></span> <span data-ttu-id="f4abe-231">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="f4abe-232">É possível usar qualquer outra ferramenta de criação da conta de usuário do Jitbit Helpdesk ou APIs fornecidas pelo Jitbit Helpdesk para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4abe-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f4abe-233">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f4abe-234">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="f4abe-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f4abe-236">**Para atribuir Brenda Fernandes ao Jitbit Helpdesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f4abe-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="f4abe-237">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f4abe-239">Na lista de aplicativos, selecione **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="f4abe-241">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f4abe-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f4abe-243">Click **Add** button.</span></span> <span data-ttu-id="f4abe-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f4abe-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f4abe-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f4abe-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4abe-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f4abe-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4abe-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f4abe-249">Testing single sign-on</span></span>

<span data-ttu-id="f4abe-250">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f4abe-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f4abe-251">Ao clicar no bloco Jitbit Helpdesk no Painel de Acesso, você deve acessar a página de logon do aplicativo Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="f4abe-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="f4abe-252">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4abe-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f4abe-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f4abe-253">Additional resources</span></span>

* [<span data-ttu-id="f4abe-254">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f4abe-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4abe-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4abe-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

