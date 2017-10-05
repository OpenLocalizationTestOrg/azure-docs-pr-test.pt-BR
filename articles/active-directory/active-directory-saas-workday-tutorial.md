---
title: "Tutorial: integração do Azure Active Directory com o Workday | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Workday."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="5bab7-103">Tutorial: Integração do Active Directory do Azure com o Workday</span><span class="sxs-lookup"><span data-stu-id="5bab7-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="5bab7-104">Neste tutorial, você aprenderá como integrar o Workday ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5bab7-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bab7-105">A integração do Workday com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5bab7-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bab7-106">No Azure AD, é possível controlar quem tem acesso ao Workday</span><span class="sxs-lookup"><span data-stu-id="5bab7-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="5bab7-107">É possível permitir que seus usuários entrem automaticamente no Workday (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bab7-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bab7-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bab7-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bab7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bab7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bab7-110">Prerequisites</span></span>

<span data-ttu-id="5bab7-111">Para configurar a integração do Azure AD ao Workday, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5bab7-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="5bab7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bab7-113">Uma assinatura do Workday habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5bab7-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bab7-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5bab7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bab7-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5bab7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bab7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5bab7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bab7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bab7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bab7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5bab7-118">Scenario description</span></span>
<span data-ttu-id="5bab7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5bab7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bab7-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5bab7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bab7-121">Adicionar o Workday da galeria</span><span class="sxs-lookup"><span data-stu-id="5bab7-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="5bab7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="5bab7-123">Adicionar o Workday da galeria</span><span class="sxs-lookup"><span data-stu-id="5bab7-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="5bab7-124">Para configurar a integração do Workday com o Azure AD, é necessário adicionar o Workday da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5bab7-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bab7-125">**Para adicionar o Workday da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="5bab7-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bab7-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bab7-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bab7-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5bab7-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5bab7-133">Na caixa de pesquisa, digite **Workday**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-133">In the search box, type **Workday**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="5bab7-135">No painel de resultados, selecione **Workday** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bab7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bab7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Workday com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5bab7-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bab7-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Workday é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bab7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="5bab7-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Workday.</span><span class="sxs-lookup"><span data-stu-id="5bab7-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="5bab7-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como o valor de **Nome de usuário** no Workday.</span><span class="sxs-lookup"><span data-stu-id="5bab7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="5bab7-142">Para configurar e testar o logon único do Azure AD com o Workday, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5bab7-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bab7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5bab7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bab7-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bab7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bab7-145">**[Criação de um usuário de teste do Workday](#creating-a-workday-test-user)** – para ter um equivalente de Brenda Fernandes no Workday que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bab7-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bab7-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bab7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bab7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5bab7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bab7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bab7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bab7-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Workday.</span><span class="sxs-lookup"><span data-stu-id="5bab7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="5bab7-150">**Para configurar o logon único do Azure AD com o Workday, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="5bab7-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="5bab7-151">No Portal do Azure, na página de integração de aplicativos do **Workday**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5bab7-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5bab7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="5bab7-155">Na seção **URLs e Domínio do Workday**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="5bab7-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="5bab7-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-157">a.</span></span> <span data-ttu-id="5bab7-158">Na caixa de texto **URL de Logon**, digite o valor como: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="5bab7-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="5bab7-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-159">b.</span></span> <span data-ttu-id="5bab7-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="5bab7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bab7-161">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="5bab7-161">These values are not the real.</span></span> <span data-ttu-id="5bab7-162">Atualize esses valores com a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="5bab7-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="5bab7-163">Sua URL de resposta deve ter um subdomínio, por exemplo: www, wd2, wd3, wd3-impl, wd5, wd5-impl.</span><span class="sxs-lookup"><span data-stu-id="5bab7-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="5bab7-164">O uso de algo como "*http://www.myworkday.com*" funciona, mas "*http://myworkday.com*", não.</span><span class="sxs-lookup"><span data-stu-id="5bab7-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="5bab7-165">Contate a [equipe de suporte ao cliente do Workday](https://www.workday.com/en-us/partners-services/services/support.html) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="5bab7-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="5bab7-166">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5bab7-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="5bab7-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5bab7-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bab7-170">Na seção **Configuração do Workday**, clique em **Configurar o Workday** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5bab7-171">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5bab7-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="5bab7-172">![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="5bab7-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="5bab7-173">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Workday como administrador.</span><span class="sxs-lookup"><span data-stu-id="5bab7-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="5bab7-174">Vá para **Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="5bab7-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="5bab7-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="5bab7-176">Vá para **Administração de Conta**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="5bab7-177">![Administração de Conta](./media/active-directory-saas-workday-tutorial/IC782924.png "Administração de Conta")</span><span class="sxs-lookup"><span data-stu-id="5bab7-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="5bab7-178">Vá para **Editar Configuração de Locatário – Segurança**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="5bab7-179">![Editar segurança de locatário](./media/active-directory-saas-workday-tutorial/IC782925.png "Editar segurança de locatário")</span><span class="sxs-lookup"><span data-stu-id="5bab7-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="5bab7-180">Na seção **URLs de Redirecionamento** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5bab7-181">![URLs de redirecionamento](./media/active-directory-saas-workday-tutorial/IC7829581.png "URLs de redirecionamento")</span><span class="sxs-lookup"><span data-stu-id="5bab7-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="5bab7-182">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-182">a.</span></span> <span data-ttu-id="5bab7-183">Clique em **Adicionar Linha**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="5bab7-184">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-184">b.</span></span> <span data-ttu-id="5bab7-185">Nas caixas de texto **URL de Redirecionamento de Logon** e **URL de Redirecionamento Móvel**, digite a **URL de Entrada** inserida na página **URLs e Domínio do Workday** do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bab7-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="5bab7-186">c.</span><span class="sxs-lookup"><span data-stu-id="5bab7-186">c.</span></span> <span data-ttu-id="5bab7-187">No Portal do Azure, na janela **Configurar logon**, copie a **URL de Saída** e, em seguida, cole-a na caixa de texto **URL de Redirecionamento de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="5bab7-188">d.</span><span class="sxs-lookup"><span data-stu-id="5bab7-188">d.</span></span>  <span data-ttu-id="5bab7-189">Na caixa de texto **Ambiente** , digite o nome do ambiente.</span><span class="sxs-lookup"><span data-stu-id="5bab7-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="5bab7-190">O valor do atributo Ambiente é vinculado ao valor da URL do locatário:</span><span class="sxs-lookup"><span data-stu-id="5bab7-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="5bab7-191">–Se o nome de domínio da URL do locatário do Workday começar com impl, por exemplo, *https://impl.workday.com/\<tenant\>/login-saml2.htmld*, o atributo **Ambiente** deverá ser definido como Implementação.</span><span class="sxs-lookup"><span data-stu-id="5bab7-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="5bab7-192">–Se o nome de domínio começar de outra forma, será necessário contatar a [equipe de suporte ao cliente do Workday](https://www.workday.com/en-us/partners-services/services/support.html) para obter o valor de **Ambiente** correspondente.</span><span class="sxs-lookup"><span data-stu-id="5bab7-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="5bab7-193">Na seção **Configuração do SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5bab7-194">![Instalação do SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="5bab7-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="5bab7-195">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-195">a.</span></span>  <span data-ttu-id="5bab7-196">Selecione **Habilitar Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="5bab7-197">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-197">b.</span></span>  <span data-ttu-id="5bab7-198">Clique em **Adicionar Linha**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="5bab7-199">Na seção Provedores de Identidade do SAML, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="5bab7-200">![Provedores de Identidade SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Provedores de Identidade SAML")</span><span class="sxs-lookup"><span data-stu-id="5bab7-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="5bab7-201">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-201">a.</span></span> <span data-ttu-id="5bab7-202">Na caixa de texto Nome do Provedor de Identidade, digite um nome de provedor (por exemplo: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="5bab7-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="5bab7-203">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-203">b.</span></span> <span data-ttu-id="5bab7-204">No Portal do Azure, na janela **Configurar logon**, copie o valor da **ID da Entidade SAML** e, em seguida, cole-o na caixa de texto **Emissor do Certificado**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="5bab7-205">c.</span><span class="sxs-lookup"><span data-stu-id="5bab7-205">c.</span></span> <span data-ttu-id="5bab7-206">Selecione **Habilitar Logoff Iniciado pelo Workday**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="5bab7-207">d.</span><span class="sxs-lookup"><span data-stu-id="5bab7-207">d.</span></span> <span data-ttu-id="5bab7-208">No Portal do Azure, na janela **Configurar logon**, copie o valor da **URL de Saída** e, em seguida, cole-a na caixa de texto **URL de Solicitação de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="5bab7-209">e.</span><span class="sxs-lookup"><span data-stu-id="5bab7-209">e.</span></span> <span data-ttu-id="5bab7-210">Clique em **Certificado de Chave Pública do Provedor de Identidade** e em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="5bab7-211">![Criar](./media/active-directory-saas-workday-tutorial/IC782928.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="5bab7-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="5bab7-212">f.</span><span class="sxs-lookup"><span data-stu-id="5bab7-212">f.</span></span> <span data-ttu-id="5bab7-213">Clique em **Criar Chave Pública x509**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="5bab7-214">![Criar](./media/active-directory-saas-workday-tutorial/IC782929.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="5bab7-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="5bab7-215">Na seção **Exibir Chave Pública x509** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="5bab7-216">![Exibir chave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Exibir chave pública x509")</span><span class="sxs-lookup"><span data-stu-id="5bab7-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="5bab7-217">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-217">a.</span></span> <span data-ttu-id="5bab7-218">Na caixa de texto **Nome**, digite um nome para o seu certificado (por exemplo: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="5bab7-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="5bab7-219">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-219">b.</span></span> <span data-ttu-id="5bab7-220">Na caixa de texto **Válido de** , digite o valor do atributo “válido de” do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="5bab7-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="5bab7-221">c.</span><span class="sxs-lookup"><span data-stu-id="5bab7-221">c.</span></span>  <span data-ttu-id="5bab7-222">Na caixa de texto **Válido até** , digite o valor do atributo “válido até” do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="5bab7-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5bab7-223">Você pode obter as datas de “válido a partir de” e “válido até” do certificado baixado clicando duas vezes nele.</span><span class="sxs-lookup"><span data-stu-id="5bab7-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="5bab7-224">As datas são listadas na guia **Detalhes** .</span><span class="sxs-lookup"><span data-stu-id="5bab7-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="5bab7-225">d.</span><span class="sxs-lookup"><span data-stu-id="5bab7-225">d.</span></span>  <span data-ttu-id="5bab7-226">Abra seu certificado codificado em base-64 no bloco de notas e copie o conteúdo dele.</span><span class="sxs-lookup"><span data-stu-id="5bab7-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="5bab7-227">e.</span><span class="sxs-lookup"><span data-stu-id="5bab7-227">e.</span></span>  <span data-ttu-id="5bab7-228">Na caixa de texto **Certificado** , cole o conteúdo da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="5bab7-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="5bab7-229">f.</span><span class="sxs-lookup"><span data-stu-id="5bab7-229">f.</span></span>  <span data-ttu-id="5bab7-230">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-230">Click **OK**.</span></span>

15. <span data-ttu-id="5bab7-231">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="5bab7-232">![Configuração de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="5bab7-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="5bab7-233">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-233">a.</span></span>  <span data-ttu-id="5bab7-234">Habilite o **Par de Chaves Privadas x509**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="5bab7-235">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-235">b.</span></span>  <span data-ttu-id="5bab7-236">Na caixa de texto **ID do provedor de serviço**, digite **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="5bab7-237">c.</span><span class="sxs-lookup"><span data-stu-id="5bab7-237">c.</span></span>  <span data-ttu-id="5bab7-238">Selecione **Habilitar a Autenticação do SAML Iniciada por SP**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="5bab7-239">d.</span><span class="sxs-lookup"><span data-stu-id="5bab7-239">d.</span></span>  <span data-ttu-id="5bab7-240">No Portal do Azure, na janela **Configurar logon**, copie o valor da **URL do Serviço de Logon Único SAML** e, em seguida, cole-o na caixa de texto **URL do Serviço de SSO IdP**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="5bab7-241">e.</span><span class="sxs-lookup"><span data-stu-id="5bab7-241">e.</span></span> <span data-ttu-id="5bab7-242">Selecione **Não Esvazie a Solicitação de Autenticação iniciada por SP**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="5bab7-243">f.</span><span class="sxs-lookup"><span data-stu-id="5bab7-243">f.</span></span> <span data-ttu-id="5bab7-244">Para **Solicitação de Método de Autenticação de Assinatura** , selecione **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="5bab7-245">![Método de assinatura da solicitação de autenticação](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de assinatura da solicitação de autenticação")</span><span class="sxs-lookup"><span data-stu-id="5bab7-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="5bab7-246">g.</span><span class="sxs-lookup"><span data-stu-id="5bab7-246">g.</span></span> <span data-ttu-id="5bab7-247">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="5bab7-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="5bab7-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="5bab7-249">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5bab7-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bab7-250">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5bab7-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bab7-251">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bab7-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bab7-252">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bab7-253">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bab7-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5bab7-255">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5bab7-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bab7-256">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bab7-258">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5bab7-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bab7-260">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bab7-262">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5bab7-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bab7-264">a.</span><span class="sxs-lookup"><span data-stu-id="5bab7-264">a.</span></span> <span data-ttu-id="5bab7-265">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bab7-266">b.</span><span class="sxs-lookup"><span data-stu-id="5bab7-266">b.</span></span> <span data-ttu-id="5bab7-267">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5bab7-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bab7-268">c.</span><span class="sxs-lookup"><span data-stu-id="5bab7-268">c.</span></span> <span data-ttu-id="5bab7-269">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bab7-270">d.</span><span class="sxs-lookup"><span data-stu-id="5bab7-270">d.</span></span> <span data-ttu-id="5bab7-271">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="5bab7-272">Criação de um usuário de teste do Workday</span><span class="sxs-lookup"><span data-stu-id="5bab7-272">Creating a Workday test user</span></span>

<span data-ttu-id="5bab7-273">Para obter um usuário de teste provisionado no Workday, é necessário contatar a [equipe de suporte do Cliente do Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="5bab7-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="5bab7-274">A [equipe de suporte ao cliente do Workday](https://www.workday.com/en-us/partners-services/services/support.html) cria o usuário para você.</span><span class="sxs-lookup"><span data-stu-id="5bab7-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bab7-275">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bab7-276">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Workday.</span><span class="sxs-lookup"><span data-stu-id="5bab7-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5bab7-278">**Para atribuir Brenda Fernandes ao Workday, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="5bab7-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="5bab7-279">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5bab7-281">Na lista de aplicativos, selecione **Workday**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-281">In the applications list, select **Workday**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="5bab7-283">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5bab7-285">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5bab7-285">Click **Add** button.</span></span> <span data-ttu-id="5bab7-286">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5bab7-288">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5bab7-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bab7-289">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bab7-290">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5bab7-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bab7-291">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5bab7-291">Testing single sign-on</span></span>

<span data-ttu-id="5bab7-292">Se você quiser testar suas configurações de logon único, abra o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5bab7-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5bab7-293">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5bab7-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bab7-294">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5bab7-294">Additional resources</span></span>

* [<span data-ttu-id="5bab7-295">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5bab7-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bab7-296">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bab7-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5bab7-297">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="5bab7-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

