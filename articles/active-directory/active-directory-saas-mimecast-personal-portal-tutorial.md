---
title: "Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Mimecast Personal Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="f0138-103">Tutorial: Integração do Azure Active Directory ao Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="f0138-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="f0138-104">Neste tutorial, você aprende a integrar o Mimecast Personal Portal ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f0138-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0138-105">A integração do Mimecast Personal Portal ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f0138-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0138-106">No Azure AD, é possível controlar quem tem acesso ao Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="f0138-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="f0138-107">É possível permitir que os usuários se conectem automaticamente ao Mimecast Personal Portal (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0138-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0138-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0138-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0138-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0138-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0138-110">Prerequisites</span></span>

<span data-ttu-id="f0138-111">Para configurar a integração do Azure AD ao Mimecast Personal Portal, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f0138-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="f0138-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0138-113">Uma assinatura do Mimecast Personal Portal com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="f0138-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0138-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f0138-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0138-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f0138-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0138-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f0138-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0138-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0138-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0138-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f0138-118">Scenario description</span></span>
<span data-ttu-id="f0138-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f0138-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0138-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f0138-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0138-121">Adicionando o Mimecast Personal Portal por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f0138-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="f0138-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="f0138-123">Adicionando o Mimecast Personal Portal por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="f0138-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="f0138-124">Para configurar a integração do Mimecast Personal Portal ao Azure AD, é necessário adicionar o Mimecast Personal Portal à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="f0138-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0138-125">**Para adicionar o Mimecast Personal Portal por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0138-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0138-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0138-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0138-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f0138-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0138-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0138-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f0138-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0138-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f0138-133">Na caixa de pesquisa, digite **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="f0138-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="f0138-135">No painel de resultados, selecione **Mimecast Personal Portal** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0138-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0138-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0138-138">Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Personal Portal, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="f0138-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0138-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Mimecast Personal Portal é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0138-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="f0138-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="f0138-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="f0138-141">No Mimecast Personal Portal, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f0138-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0138-142">Para configurar e testar o logon único do Azure AD com o Mimecast Personal Portal, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f0138-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0138-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f0138-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0138-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0138-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0138-145">**[Criando um usuário de teste do Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)** – para ter um equivalente de Brenda Fernandes no Mimecast Personal Portal que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0138-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0138-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0138-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0138-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f0138-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0138-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0138-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0138-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="f0138-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="f0138-150">**Para configurar o logon único do Azure AD com o Mimecast Personal Portal, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0138-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="f0138-151">No portal do Azure, na página de integração do aplicativo **Mimecast Personal Portal**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f0138-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f0138-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f0138-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="f0138-155">Na seção **Domínio e URLs do Mimecast Personal Portal**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f0138-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="f0138-157">a.</span><span class="sxs-lookup"><span data-stu-id="f0138-157">a.</span></span> <span data-ttu-id="f0138-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="f0138-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="f0138-159">b.</span><span class="sxs-lookup"><span data-stu-id="f0138-159">b.</span></span> <span data-ttu-id="f0138-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="f0138-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="f0138-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="f0138-161">These values are not real.</span></span> <span data-ttu-id="f0138-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="f0138-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f0138-163">Contate a [equipe de suporte ao Cliente do Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="f0138-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="f0138-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="f0138-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="f0138-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f0138-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0138-168">Na seção **Configuração do Mimecast Personal Portal**, clique em **Configurar o Mimecast Personal Portal** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f0138-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0138-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="f0138-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="f0138-171">Em outra janela do navegador da Web, faça logon em seu Mimecast Personal Portal como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f0138-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="f0138-172">Acesse **Serviços \> Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0138-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="f0138-173">![Aplicativos](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicativos")</span><span class="sxs-lookup"><span data-stu-id="f0138-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="f0138-174">Clique em **Perfis de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="f0138-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="f0138-175">![Perfis de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="f0138-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="f0138-176">Clique em **Novo Perfil de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="f0138-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="f0138-177">![Novo Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "Novo Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="f0138-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="f0138-178">Na seção **Perfil de Autenticação** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f0138-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f0138-179">![Perfil de Autenticação](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="f0138-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="f0138-180">a.</span><span class="sxs-lookup"><span data-stu-id="f0138-180">a.</span></span> <span data-ttu-id="f0138-181">Na caixa de texto **Descrição** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="f0138-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="f0138-182">b.</span><span class="sxs-lookup"><span data-stu-id="f0138-182">b.</span></span> <span data-ttu-id="f0138-183">Selecione **Impor Autenticação SAML para o Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="f0138-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="f0138-184">c.</span><span class="sxs-lookup"><span data-stu-id="f0138-184">c.</span></span> <span data-ttu-id="f0138-185">Como **Provedor**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0138-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="f0138-186">d.</span><span class="sxs-lookup"><span data-stu-id="f0138-186">d.</span></span> <span data-ttu-id="f0138-187">Na caixa de texto **URL do Emissor**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0138-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f0138-188">e.</span><span class="sxs-lookup"><span data-stu-id="f0138-188">e.</span></span> <span data-ttu-id="f0138-189">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0138-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f0138-190">f.</span><span class="sxs-lookup"><span data-stu-id="f0138-190">f.</span></span> <span data-ttu-id="f0138-191">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0138-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f0138-192">g.</span><span class="sxs-lookup"><span data-stu-id="f0138-192">g.</span></span> <span data-ttu-id="f0138-193">Abra o certificado codificado em **Base64** baixado no portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado do Provedor de Identidade (Metadados)**.</span><span class="sxs-lookup"><span data-stu-id="f0138-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="f0138-194">h.</span><span class="sxs-lookup"><span data-stu-id="f0138-194">h.</span></span> <span data-ttu-id="f0138-195">Selecione **Permitir Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f0138-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="f0138-196">i.</span><span class="sxs-lookup"><span data-stu-id="f0138-196">i.</span></span> <span data-ttu-id="f0138-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f0138-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f0138-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f0138-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0138-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f0138-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0138-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0138-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0138-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0138-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0138-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f0138-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0138-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0138-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0138-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0138-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f0138-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0138-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0138-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0138-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f0138-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0138-213">a.</span><span class="sxs-lookup"><span data-stu-id="f0138-213">a.</span></span> <span data-ttu-id="f0138-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f0138-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0138-215">b.</span><span class="sxs-lookup"><span data-stu-id="f0138-215">b.</span></span> <span data-ttu-id="f0138-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0138-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0138-217">c.</span><span class="sxs-lookup"><span data-stu-id="f0138-217">c.</span></span> <span data-ttu-id="f0138-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f0138-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0138-219">d.</span><span class="sxs-lookup"><span data-stu-id="f0138-219">d.</span></span> <span data-ttu-id="f0138-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f0138-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="f0138-221">Criando um usuário de teste do Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="f0138-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="f0138-222">Para permitir que os usuários do AD do Azure façam logon no Mimecast Personal Portal, eles devem ser provisionados no Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="f0138-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="f0138-223">No caso do Mimecast Personal Portal, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f0138-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="f0138-224">Você precisa registrar um domínio antes de criar usuários.</span><span class="sxs-lookup"><span data-stu-id="f0138-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="f0138-225">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0138-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="f0138-226">Faça logon no **Mimecast Personal Portal** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f0138-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="f0138-227">Vá para **Diretórios \> Interno**.</span><span class="sxs-lookup"><span data-stu-id="f0138-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="f0138-228">![Diretórios](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Diretórios")</span><span class="sxs-lookup"><span data-stu-id="f0138-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="f0138-229">Clique em **Registrar Novo Domínio**.</span><span class="sxs-lookup"><span data-stu-id="f0138-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="f0138-230">![Registrar Novo Domínio](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Registrar Novo Domínio")</span><span class="sxs-lookup"><span data-stu-id="f0138-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="f0138-231">Depois de criar o novo domínio, clique em **Novo Endereço**.</span><span class="sxs-lookup"><span data-stu-id="f0138-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="f0138-232">![Novo Endereço](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "Novo Endereço")</span><span class="sxs-lookup"><span data-stu-id="f0138-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="f0138-233">Na caixa de diálogo Novo endereço, realize as seguintes etapas de uma conta válida do Azure AD que você deseja provisionar:</span><span class="sxs-lookup"><span data-stu-id="f0138-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="f0138-234">![Salvar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="f0138-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="f0138-235">a.</span><span class="sxs-lookup"><span data-stu-id="f0138-235">a.</span></span> <span data-ttu-id="f0138-236">Na caixa de texto **Endereço de Email**, digite o **Endereço de Email** do usuário como **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f0138-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="f0138-237">b.</span><span class="sxs-lookup"><span data-stu-id="f0138-237">b.</span></span> <span data-ttu-id="f0138-238">Na caixa de texto **Nome Global**, digite o **nome de usuário** como **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f0138-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="f0138-239">c.</span><span class="sxs-lookup"><span data-stu-id="f0138-239">c.</span></span> <span data-ttu-id="f0138-240">Nas caixas de texto **Senha** e **Confirmar Senha**, digite a **Senha** do usuário.</span><span class="sxs-lookup"><span data-stu-id="f0138-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="f0138-241">b.</span><span class="sxs-lookup"><span data-stu-id="f0138-241">b.</span></span> <span data-ttu-id="f0138-242">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f0138-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f0138-243">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Mimecast Personal Portal ou as APIs fornecidas pelo Mimecast Personal Portal para provisionar contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0138-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0138-244">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0138-245">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="f0138-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f0138-247">**Para atribuir Brenda Fernandes ao Mimecast Personal Portal, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0138-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="f0138-248">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0138-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f0138-250">Na lista de aplicativos, selecione **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="f0138-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="f0138-252">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f0138-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f0138-254">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f0138-254">Click **Add** button.</span></span> <span data-ttu-id="f0138-255">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0138-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f0138-257">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f0138-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0138-258">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0138-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0138-259">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0138-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0138-260">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f0138-260">Testing single sign-on</span></span>
<span data-ttu-id="f0138-261">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f0138-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0138-262">Quando você clicar no bloco do Mimecast Personal Portal no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="f0138-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="f0138-263">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0138-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0138-264">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f0138-264">Additional resources</span></span>

* [<span data-ttu-id="f0138-265">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f0138-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0138-266">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0138-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

