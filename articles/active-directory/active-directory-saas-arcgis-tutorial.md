---
title: "Tutorial: Integração do Azure Active Directory ao ArcGIS Online | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="4b5be-103">Tutorial: Integração do Azure Active Directory ao ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="4b5be-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="4b5be-104">Neste tutorial, você aprende a integrar o ArcGIS Online ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4b5be-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b5be-105">A integração do ArcGIS Online ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4b5be-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b5be-106">No Azure AD, é possível controlar quem tem acesso ao ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="4b5be-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="4b5be-107">É possível permitir que os usuários se conectem automaticamente ao ArcGIS Online (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b5be-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b5be-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b5be-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b5be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="4b5be-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b5be-110">Prerequisites</span></span>

<span data-ttu-id="4b5be-111">Para configurar a integração do Azure AD ao ArcGIS Online, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4b5be-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="4b5be-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b5be-113">Uma assinatura habilitada para logon único do ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="4b5be-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b5be-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4b5be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b5be-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4b5be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b5be-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4b5be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b5be-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b5be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b5be-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4b5be-118">Scenario description</span></span>
<span data-ttu-id="4b5be-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4b5be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b5be-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4b5be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b5be-121">Adicionando o ArcGIS Online por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4b5be-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="4b5be-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="4b5be-123">Adicionando o ArcGIS Online por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="4b5be-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="4b5be-124">Para configurar a integração do ArcGIS Online ao Azure AD, você precisa adicionar o ArcGIS Online à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="4b5be-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b5be-125">**Para adicionar o ArcGIS Online por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b5be-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b5be-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b5be-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b5be-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4b5be-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4b5be-133">Na caixa de pesquisa, digite **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="4b5be-135">No painel de resultados, selecione **ArcGIS Online** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b5be-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b5be-138">Nesta seção, você configura e testa o logon único do Azure AD com o ArcGIS Online, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4b5be-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b5be-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ArcGIS Online é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b5be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="4b5be-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="4b5be-141">Essa relação de vínculo é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="4b5be-142">Para configurar e testar o logon único do Azure AD com o ArcGIS Online, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4b5be-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b5be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4b5be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b5be-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b5be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b5be-145">**[Criando um usuário de teste do ArcGIS Online](#creating-an-arcgis-online-test-user)** – para ter um equivalente de Brenda Fernandes no ArcGIS Online que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b5be-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b5be-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b5be-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4b5be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b5be-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b5be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b5be-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="4b5be-150">**Para configurar o logon único do Azure AD com o ArcGIS Online, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b5be-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="4b5be-151">No portal do Azure, na página de integração do aplicativo do **ArcGIS Online**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4b5be-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4b5be-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="4b5be-155">Na seção **Domínio e URLs do ArcGIS Online**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b5be-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="4b5be-157">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="4b5be-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b5be-158">Esse valor não é o real.</span><span class="sxs-lookup"><span data-stu-id="4b5be-158">This value is not the real.</span></span> <span data-ttu-id="4b5be-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="4b5be-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4b5be-160">Contate a [equipe de suporte ao Cliente do ArcGIS Online](http://support.esri.com/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="4b5be-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="4b5be-161">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4b5be-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="4b5be-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4b5be-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b5be-165">Em outra janela do navegador da Web, faça logon em seu site de empresa ArcGIS como um administrador.</span><span class="sxs-lookup"><span data-stu-id="4b5be-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="4b5be-166">Clique em **EDITAR CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="4b5be-167">![Editar Configurações](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Editar Configurações")</span><span class="sxs-lookup"><span data-stu-id="4b5be-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="4b5be-168">Clique em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-168">Click **Security**.</span></span>

    <span data-ttu-id="4b5be-169">![Segurança](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="4b5be-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="4b5be-170">Em **Logons Corporativos**, clique em **DEFINIR PROVEDOR DE IDENTIDADE**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="4b5be-171">![Logons Corporativos](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Logons Corporativos")</span><span class="sxs-lookup"><span data-stu-id="4b5be-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="4b5be-172">Na página de configuração **Definir Provedor de Identidade** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b5be-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="4b5be-173">![Definir Provedor de Identidade](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Definir Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="4b5be-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="4b5be-174">a.</span><span class="sxs-lookup"><span data-stu-id="4b5be-174">a.</span></span> <span data-ttu-id="4b5be-175">Na caixa de texto **Nome**, digite o nome de sua organização.</span><span class="sxs-lookup"><span data-stu-id="4b5be-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="4b5be-176">b.</span><span class="sxs-lookup"><span data-stu-id="4b5be-176">b.</span></span> <span data-ttu-id="4b5be-177">Para **Os metadados do Provedor de Identidade Corporativo serão fornecidos usando**, selecione **Um Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="4b5be-178">c.</span><span class="sxs-lookup"><span data-stu-id="4b5be-178">c.</span></span> <span data-ttu-id="4b5be-179">Para carregar seu arquivo de metadados baixado, clique em **Escolher arquivo**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="4b5be-180">d.</span><span class="sxs-lookup"><span data-stu-id="4b5be-180">d.</span></span> <span data-ttu-id="4b5be-181">Clique em **DEFINIR PROVEDOR DE IDENTIDADE**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="4b5be-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4b5be-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b5be-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4b5be-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b5be-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b5be-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b5be-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b5be-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b5be-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4b5be-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b5be-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b5be-189">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b5be-191">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4b5be-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b5be-193">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b5be-195">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b5be-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b5be-197">a.</span><span class="sxs-lookup"><span data-stu-id="4b5be-197">a.</span></span> <span data-ttu-id="4b5be-198">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b5be-199">b.</span><span class="sxs-lookup"><span data-stu-id="4b5be-199">b.</span></span> <span data-ttu-id="4b5be-200">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4b5be-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="4b5be-201">c.</span><span class="sxs-lookup"><span data-stu-id="4b5be-201">c.</span></span> <span data-ttu-id="4b5be-202">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b5be-203">d.</span><span class="sxs-lookup"><span data-stu-id="4b5be-203">d.</span></span> <span data-ttu-id="4b5be-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="4b5be-205">Criando um usuário de teste do ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="4b5be-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="4b5be-206">Para permitir que os usuários do Azure AD façam logon no ArcGIS Online, eles devem ser provisionados no ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="4b5be-207">No caso do ArcGIS Online, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4b5be-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="4b5be-208">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b5be-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="4b5be-209">Faça logon em seu locatário do **ArcGIS** .</span><span class="sxs-lookup"><span data-stu-id="4b5be-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="4b5be-210">Clique em **CONVIDAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="4b5be-211">![Convidar Membros](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Convidar Membros")</span><span class="sxs-lookup"><span data-stu-id="4b5be-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="4b5be-212">Selecione **Adicionar membros automaticamente sem enviar um email** e, depois, clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4b5be-213">![Adicionar Membros Automaticamente](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Adicionar Membros Automaticamente")</span><span class="sxs-lookup"><span data-stu-id="4b5be-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="4b5be-214">Na página do diálogo **Membros** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4b5be-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="4b5be-215">![Adicionar e examinar](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Adicionar e examinar")</span><span class="sxs-lookup"><span data-stu-id="4b5be-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="4b5be-216">a.</span><span class="sxs-lookup"><span data-stu-id="4b5be-216">a.</span></span> <span data-ttu-id="4b5be-217">Insira o **Email**, o **Nome** e o **Sobrenome** de uma conta válida do AAD que deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="4b5be-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="4b5be-218">b.</span><span class="sxs-lookup"><span data-stu-id="4b5be-218">b.</span></span> <span data-ttu-id="4b5be-219">Clique em **ADICIONAR E EXAMINAR**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="4b5be-220">Examine os dados inseridos e, depois, clique em **ADICIONAR MEMBROS**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="4b5be-221">![Adicionar membro](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Adicionar membro")</span><span class="sxs-lookup"><span data-stu-id="4b5be-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="4b5be-222">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="4b5be-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b5be-223">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b5be-224">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4b5be-226">**Para atribuir Brenda Fernandes ao ArcGIS Online, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4b5be-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="4b5be-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4b5be-229">Na lista de aplicativos, selecione **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="4b5be-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4b5be-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4b5be-233">Click **Add** button.</span></span> <span data-ttu-id="4b5be-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4b5be-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4b5be-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b5be-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b5be-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4b5be-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b5be-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4b5be-239">Testing single sign-on</span></span>

<span data-ttu-id="4b5be-240">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4b5be-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b5be-241">Quando você clicar no bloco ArcGIS Online no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="4b5be-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="4b5be-242">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b5be-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b5be-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4b5be-243">Additional resources</span></span>

* [<span data-ttu-id="4b5be-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5be-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b5be-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b5be-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

