---
title: "Tutorial: Integração do Azure Active Directory ao ServiceNow | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ServiceNow e o ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="45380-103">Tutorial: Integração do Active Directory do Azure com o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="45380-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="45380-104">Neste tutorial, você aprenderá a integrar o ServiceNow e o ServiceNow Express ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="45380-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="45380-105">A integração do ServiceNow e do ServiceNow Express ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="45380-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="45380-106">Você pode controlar no Azure AD quem tem acesso ao ServiceNow e ao ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="45380-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="45380-107">Você pode habilitar seus usuários a fazerem logon automaticamente no ServiceNow e ServiceNow Express (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="45380-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="45380-108">Você pode gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="45380-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="45380-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45380-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45380-110">Prerequisites</span></span>
<span data-ttu-id="45380-111">Para configurar a integração do Azure AD ao ServiceNow e ao ServiceNow Express, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="45380-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="45380-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-112">An Azure AD subscription</span></span>
* <span data-ttu-id="45380-113">Para o ServiceNow, uma instância ou um locatário do ServiceNow, versão Calgary ou superior</span><span class="sxs-lookup"><span data-stu-id="45380-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="45380-114">Para o ServiceNow Express, uma instância do ServiceNow Express, versão Helsinki ou superior</span><span class="sxs-lookup"><span data-stu-id="45380-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="45380-115">O locatário ServiceNow deve ter o [Plug-in de Logon Único de Provedor Múltiplo](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) habilitado.</span><span class="sxs-lookup"><span data-stu-id="45380-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="45380-116">Isso pode ser feito [enviando uma solicitação de serviço](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="45380-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="45380-117">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="45380-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="45380-118">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="45380-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="45380-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="45380-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="45380-120">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45380-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="45380-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="45380-121">Scenario description</span></span>
<span data-ttu-id="45380-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="45380-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="45380-123">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="45380-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="45380-124">Adicionando o ServiceNow da galeria</span><span class="sxs-lookup"><span data-stu-id="45380-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="45380-125">Configurando e testando o logon único do Azure AD para o ServiceNow ou para o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="45380-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="45380-126">Adicionando o ServiceNow da galeria</span><span class="sxs-lookup"><span data-stu-id="45380-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="45380-127">Para configurar a integração do ServiceNow ou do ServiceNow Express no Azure AD, você precisa adicionar o ServiceNow da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="45380-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="45380-128">**Para adicionar o ServiceNow da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="45380-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="45380-129">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45380-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="45380-131">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="45380-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="45380-132">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="45380-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="45380-134">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="45380-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="45380-136">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="45380-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="45380-138">Na caixa de pesquisa, digite**ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="45380-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="45380-140">No painel de resultados, selecione **ServiceNow** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45380-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="45380-142">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="45380-143">Nesta seção, você configurará e testará o logon único do Azure AD com o ServiceNow ou o ServiceNow Express, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="45380-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="45380-144">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ServiceNow é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45380-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="45380-145">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="45380-146">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como sendo o valor de **Nome de Usuário** no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="45380-147">Para configurar e testar o logon único do Azure AD com o ServiceNow, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="45380-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="45380-148">**[Configuração do logon único do Azure AD para o ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="45380-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="45380-149">**[Configuração do logon único do Azure AD para o ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="45380-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="45380-150">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="45380-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="45380-151">**[Criação de um usuário de teste do ServiceNow](#creating-a-servicenow-test-user)** - para ter um equivalente de Brenda Fernandes no ServiceNow que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45380-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="45380-152">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="45380-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="45380-153">**[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="45380-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="45380-154">Se você quiser configurar o ServiceNow, ignore a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="45380-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="45380-155">Da mesma forma, se você quiser configurar o ServiceNow Express, ignore a etapa 1.</span><span class="sxs-lookup"><span data-stu-id="45380-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="45380-156">Configuração do logon único do Azure AD para o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="45380-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="45380-157">No portal clássico do Azure AD, na página de integração de aplicativos do **ServiceNow**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="45380-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="45380-158">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="45380-159">Na página **Como você deseja que os usuários façam logon no ServiceNow**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="45380-160">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="45380-161">Na página **Definir Configurações do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="45380-162">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="45380-163">a.</span><span class="sxs-lookup"><span data-stu-id="45380-163">a.</span></span> <span data-ttu-id="45380-164">na caixa de texto **URL de Entrada no ServiceNow**, digite a URL usada pelos usuários para entrar no seu aplicativo ServiceNow seguindo o padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="45380-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="45380-165">b.</span><span class="sxs-lookup"><span data-stu-id="45380-165">b.</span></span> <span data-ttu-id="45380-166">Na caixa de texto **Identificador**, digite a URL usada pelos usuários para entrar em seu aplicativo do ServiceNow usando o seguinte padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="45380-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="45380-167">c.</span><span class="sxs-lookup"><span data-stu-id="45380-167">c.</span></span> <span data-ttu-id="45380-168">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="45380-168">Click **Next**</span></span>

4. <span data-ttu-id="45380-169">Para que o Azure AD configure automaticamente o ServiceNow para autenticação baseada em SAML, insira o nome da instância do ServiceNow, o nome de usuário do administrador e a senha de administrador no formulário **Configurar automaticamente o logon único** e clique em *Configurar*.</span><span class="sxs-lookup"><span data-stu-id="45380-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="45380-170">Observe que o nome de usuário do administrador informado deve ter a função **security_admin** atribuída no ServiceNow para que isso funcione.</span><span class="sxs-lookup"><span data-stu-id="45380-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="45380-171">Caso contrário, para configurar manualmente o ServiceNow para usar o Azure AD como provedor de identidade SAML, clique em **Configurar manualmente o aplicativo para o logon único**, em **Avançar** e conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="45380-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="45380-172">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="45380-173">Na página **Configurar logon único no ServiceNow**, clique em **Baixar certificado**, salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="45380-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="45380-174">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="45380-175">Entre no seu aplicativo ServiceNow como administrador.</span><span class="sxs-lookup"><span data-stu-id="45380-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="45380-176">Ative o plug-in *Integração - Instalador de Logon Único de Vários Provedores* ao seguir as próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="45380-177">a.</span><span class="sxs-lookup"><span data-stu-id="45380-177">a.</span></span> <span data-ttu-id="45380-178">No painel de navegação à esquerda, vá para a seção **Definição do Sistema** e, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="45380-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="45380-179">![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Ativar o plug-in")</span><span class="sxs-lookup"><span data-stu-id="45380-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="45380-180">b.</span><span class="sxs-lookup"><span data-stu-id="45380-180">b.</span></span> <span data-ttu-id="45380-181">Procure *Integração - Instalador de Logon Único de Vários Provedores*.</span><span class="sxs-lookup"><span data-stu-id="45380-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="45380-182">![Configurar URL do aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Ativar o plug-in")</span><span class="sxs-lookup"><span data-stu-id="45380-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="45380-183">c.</span><span class="sxs-lookup"><span data-stu-id="45380-183">c.</span></span> <span data-ttu-id="45380-184">Selecione o plugin.</span><span class="sxs-lookup"><span data-stu-id="45380-184">Select the plugin.</span></span> <span data-ttu-id="45380-185">Clique com o botão direito do mouse e selecione **Ativar/Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="45380-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="45380-186">d.</span><span class="sxs-lookup"><span data-stu-id="45380-186">d.</span></span> <span data-ttu-id="45380-187">Clique no botão **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="45380-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="45380-188">No painel de navegação à esquerda, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="45380-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="45380-189">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="45380-190">No diálogo **Várias propriedades de SSO do provedor** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="45380-191">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="45380-192">a.</span><span class="sxs-lookup"><span data-stu-id="45380-192">a.</span></span> <span data-ttu-id="45380-193">Como **Habilitar vários provedores SSO**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="45380-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="45380-194">b.</span><span class="sxs-lookup"><span data-stu-id="45380-194">b.</span></span> <span data-ttu-id="45380-195">Como **Habilitar log de depuração com integração SSO de vários provedores**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="45380-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="45380-196">c.</span><span class="sxs-lookup"><span data-stu-id="45380-196">c.</span></span> <span data-ttu-id="45380-197">Na caixa de texto **O campo na tabela de usuário que...**, digite **nome_de_usuário**.</span><span class="sxs-lookup"><span data-stu-id="45380-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="45380-198">d.</span><span class="sxs-lookup"><span data-stu-id="45380-198">d.</span></span> <span data-ttu-id="45380-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="45380-199">Click **Save**.</span></span>

10. <span data-ttu-id="45380-200">No painel de navegação à esquerda, clique em **Certificados x509**.</span><span class="sxs-lookup"><span data-stu-id="45380-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="45380-201">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="45380-202">No diálogo **Certificados x. 509**, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="45380-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="45380-203">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="45380-204">No diálogo **Certificados x. 509** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="45380-205">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="45380-206">a.</span><span class="sxs-lookup"><span data-stu-id="45380-206">a.</span></span> <span data-ttu-id="45380-207">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="45380-207">Click **New**.</span></span>
    
     <span data-ttu-id="45380-208">b.</span><span class="sxs-lookup"><span data-stu-id="45380-208">b.</span></span> <span data-ttu-id="45380-209">Na caixa de texto **Nome**, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="45380-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="45380-210">c.</span><span class="sxs-lookup"><span data-stu-id="45380-210">c.</span></span> <span data-ttu-id="45380-211">Selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="45380-211">Select **Active**.</span></span>
    
     <span data-ttu-id="45380-212">d.</span><span class="sxs-lookup"><span data-stu-id="45380-212">d.</span></span> <span data-ttu-id="45380-213">Para **Formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="45380-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="45380-214">e.</span><span class="sxs-lookup"><span data-stu-id="45380-214">e.</span></span> <span data-ttu-id="45380-215">Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="45380-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="45380-216">f.</span><span class="sxs-lookup"><span data-stu-id="45380-216">f.</span></span> <span data-ttu-id="45380-217">Abra seu certificado codificado base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado PEM**.</span><span class="sxs-lookup"><span data-stu-id="45380-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="45380-218">g.</span><span class="sxs-lookup"><span data-stu-id="45380-218">g.</span></span> <span data-ttu-id="45380-219">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="45380-219">Click **Update**.</span></span>

13. <span data-ttu-id="45380-220">No painel de navegação à esquerda, clique em **Provedores de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="45380-221">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="45380-222">No diálogo **Provedores de Identidade**, clique em **Novo**:</span><span class="sxs-lookup"><span data-stu-id="45380-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="45380-223">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="45380-224">No diálogo **Provedores de Identidade**, clique em **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="45380-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="45380-225">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="45380-226">No diálogo Propriedades de SAML2 Atualização1, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="45380-227">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="45380-228">a.</span><span class="sxs-lookup"><span data-stu-id="45380-228">a.</span></span> <span data-ttu-id="45380-229">Na caixa de texto **Nome** , digite um nome para a sua configuração (por exemplo: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="45380-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="45380-230">b.</span><span class="sxs-lookup"><span data-stu-id="45380-230">b.</span></span> <span data-ttu-id="45380-231">Na caixa de texto **Campo de Usuário**, digite **email** ou **user_name**, dependendo de qual campo é usado para identificar exclusivamente os usuários em sua implantação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="45380-232">Você pode configurar o Azure AD para emitir a ID de usuário (nome UPN) do Azure AD ou o endereço de email como o identificador exclusivo no token SAML acessando a seção **ServiceNow > Atributos > Logon Único** do portal clássico do Azure e mapeando o campo desejado para o atributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="45380-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="45380-233">O valor armazenado para o atributo selecionado no Azure AD (por exemplo, nome UPN) deve corresponder ao valor armazenado no ServiceNow para o campo inserido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="45380-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="45380-234">c.</span><span class="sxs-lookup"><span data-stu-id="45380-234">c.</span></span> <span data-ttu-id="45380-235">No portal clássico do Azure AD, copie o valor de **ID do Provedor de Identidade** e cole-o na caixa de texto **URL do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="45380-236">d.</span><span class="sxs-lookup"><span data-stu-id="45380-236">d.</span></span> <span data-ttu-id="45380-237">No portal clássico do Azure AD, copie o valor de **URL de Solicitação de Autenticação** e cole-o na caixa de texto **Solicitação de Autenticação do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="45380-238">e.</span><span class="sxs-lookup"><span data-stu-id="45380-238">e.</span></span> <span data-ttu-id="45380-239">No portal clássico do Azure AD, copie o valor de **URL de Serviço de Saída Única** e cole-o na caixa de texto **Solicitação de Logoff Único do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="45380-240">f.</span><span class="sxs-lookup"><span data-stu-id="45380-240">f.</span></span> <span data-ttu-id="45380-241">Na caixa de texto **Home page do ServiceNow** , digite a URL da sua página inicial de instância do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="45380-242">A home page da instância do ServiceNow é uma concatenação da **URL do locatário do ServiceNow** e **/navpage.do** (por exemplo: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="45380-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="45380-243">g.</span><span class="sxs-lookup"><span data-stu-id="45380-243">g.</span></span> <span data-ttu-id="45380-244">Na caixa de texto **ID da entidade/emissor** , digite a URL do seu locatário do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="45380-245">h.</span><span class="sxs-lookup"><span data-stu-id="45380-245">h.</span></span> <span data-ttu-id="45380-246">Na caixa de texto **URL do Público-alvo** , digite a URL do seu locatário do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="45380-247">i.</span><span class="sxs-lookup"><span data-stu-id="45380-247">i.</span></span> <span data-ttu-id="45380-248">Na caixa de texto **associação de protocolo SingleLogoutRequest do IDP**, digite **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="45380-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="45380-249">j.</span><span class="sxs-lookup"><span data-stu-id="45380-249">j.</span></span> <span data-ttu-id="45380-250">Na caixa de texto Política da NameID, digite **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="45380-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="45380-251">k.</span><span class="sxs-lookup"><span data-stu-id="45380-251">k.</span></span> <span data-ttu-id="45380-252">Desmarque **Criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="45380-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="45380-253">l.</span><span class="sxs-lookup"><span data-stu-id="45380-253">l.</span></span> <span data-ttu-id="45380-254">No **Método AuthnContextClassRef**, digite `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="45380-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="45380-255">Isso só será necessário se você for uma organização que esteja somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="45380-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="45380-256">Se você estiver usando o ADFS ou o MFA local para autenticação, não deverá configurar esse valor.</span><span class="sxs-lookup"><span data-stu-id="45380-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="45380-257">m.</span><span class="sxs-lookup"><span data-stu-id="45380-257">m.</span></span> <span data-ttu-id="45380-258">Na caixa de texto **Distorção do Relógio**, digite **60**.</span><span class="sxs-lookup"><span data-stu-id="45380-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="45380-259">n.</span><span class="sxs-lookup"><span data-stu-id="45380-259">n.</span></span> <span data-ttu-id="45380-260">Como **Script de Logon Único**, selecione **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="45380-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="45380-261">o.</span><span class="sxs-lookup"><span data-stu-id="45380-261">o.</span></span> <span data-ttu-id="45380-262">Como **Certificado x509**, selecione o certificado que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="45380-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="45380-263">p.</span><span class="sxs-lookup"><span data-stu-id="45380-263">p.</span></span> <span data-ttu-id="45380-264">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="45380-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="45380-265">No portal clássico do Azure AD, selecione a confirmação de configuração do logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="45380-266">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="45380-267">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="45380-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="45380-268">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="45380-269">Configuração do logon único do Azure AD para o ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="45380-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="45380-270">No portal clássico do Azure AD, na página de integração de aplicativos do **ServiceNow**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="45380-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="45380-271">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="45380-272">Na página **Como você deseja que os usuários façam logon no ServiceNow**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="45380-273">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="45380-274">Na página **Definir Configurações do Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="45380-275">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="45380-276">a.</span><span class="sxs-lookup"><span data-stu-id="45380-276">a.</span></span> <span data-ttu-id="45380-277">na caixa de texto **URL de Entrada no ServiceNow**, digite a URL usada pelos usuários para entrar no seu aplicativo ServiceNow seguindo o padrão: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="45380-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="45380-278">b.</span><span class="sxs-lookup"><span data-stu-id="45380-278">b.</span></span> <span data-ttu-id="45380-279">Na caixa de texto **URL do Emissor**, digite a URL usada pelos usuários para entrar no seu aplicativo ServiceNow seguindo o padrão `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="45380-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="45380-280">c.</span><span class="sxs-lookup"><span data-stu-id="45380-280">c.</span></span> <span data-ttu-id="45380-281">Clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="45380-281">Click **Next**</span></span>

4. <span data-ttu-id="45380-282">Clique em **Configurar manualmente o aplicativo para logon único**, então clique em **Avançar** e conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="45380-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="45380-283">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="45380-284">Na página **Configurar logon único no ServiceNow**, clique em **Baixar certificado**, salve o arquivo de certificado no computador e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="45380-285">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="45380-286">Entre no seu aplicativo ServiceNow Express como administrador.</span><span class="sxs-lookup"><span data-stu-id="45380-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="45380-287">No painel de navegação à esquerda, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="45380-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="45380-288">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="45380-289">No diálogo **Logon Único**, clique no ícone de configuração no canto superior direito e defina as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="45380-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="45380-290">![Configurar URL do Aplicativo](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurar URL do Aplicativo")</span><span class="sxs-lookup"><span data-stu-id="45380-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="45380-291">a.</span><span class="sxs-lookup"><span data-stu-id="45380-291">a.</span></span> <span data-ttu-id="45380-292">Ative/desative **Habilitar SSO de vários provedores** à direita.</span><span class="sxs-lookup"><span data-stu-id="45380-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="45380-293">b.</span><span class="sxs-lookup"><span data-stu-id="45380-293">b.</span></span> <span data-ttu-id="45380-294">Ative/desative **Habilitar registro em log de depuração para a integração de SSO de vários provedores** à direita.</span><span class="sxs-lookup"><span data-stu-id="45380-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="45380-295">c.</span><span class="sxs-lookup"><span data-stu-id="45380-295">c.</span></span> <span data-ttu-id="45380-296">Na caixa de texto **O campo na tabela de usuário que...**, digite **nome_de_usuário**.</span><span class="sxs-lookup"><span data-stu-id="45380-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="45380-297">No diálogo **Logon Único**, clique em **Adicionar Novo Certificado**.</span><span class="sxs-lookup"><span data-stu-id="45380-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="45380-298">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="45380-299">No diálogo **Certificados x. 509** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="45380-300">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="45380-301">a.</span><span class="sxs-lookup"><span data-stu-id="45380-301">a.</span></span> <span data-ttu-id="45380-302">Na caixa de texto **Nome**, digite um nome para a sua configuração (por exemplo: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="45380-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="45380-303">b.</span><span class="sxs-lookup"><span data-stu-id="45380-303">b.</span></span> <span data-ttu-id="45380-304">Selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="45380-304">Select **Active**.</span></span>
    
    <span data-ttu-id="45380-305">c.</span><span class="sxs-lookup"><span data-stu-id="45380-305">c.</span></span> <span data-ttu-id="45380-306">Para **Formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="45380-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="45380-307">d.</span><span class="sxs-lookup"><span data-stu-id="45380-307">d.</span></span> <span data-ttu-id="45380-308">Como **Tipo**, selecione **Confiar nos Certificados do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="45380-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="45380-309">e.</span><span class="sxs-lookup"><span data-stu-id="45380-309">e.</span></span> <span data-ttu-id="45380-310">Crie um arquivo codificado em Base64 usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="45380-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="45380-311">Para obter mais detalhes, consulte [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="45380-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="45380-312">f.</span><span class="sxs-lookup"><span data-stu-id="45380-312">f.</span></span> <span data-ttu-id="45380-313">Abra seu certificado codificado base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado PEM**.</span><span class="sxs-lookup"><span data-stu-id="45380-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="45380-314">g.</span><span class="sxs-lookup"><span data-stu-id="45380-314">g.</span></span> <span data-ttu-id="45380-315">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="45380-315">Click **Update**.</span></span>
11. <span data-ttu-id="45380-316">No diálogo **Logon Único**, clique em **Adicionar novo IdP**.</span><span class="sxs-lookup"><span data-stu-id="45380-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="45380-317">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="45380-318">No diálogo **Adicionar Novo Provedor de Identidade**, em **Configurar Provedor de Identidade**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="45380-319">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="45380-320">a.</span><span class="sxs-lookup"><span data-stu-id="45380-320">a.</span></span> <span data-ttu-id="45380-321">Na caixa de texto **Nome** , digite um nome para a sua configuração (por exemplo: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="45380-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="45380-322">b.</span><span class="sxs-lookup"><span data-stu-id="45380-322">b.</span></span> <span data-ttu-id="45380-323">No portal clássico do Azure AD, copie o valor de **ID do Provedor de Identidade** e cole-o na caixa de texto **URL do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="45380-324">c.</span><span class="sxs-lookup"><span data-stu-id="45380-324">c.</span></span> <span data-ttu-id="45380-325">No portal clássico do Azure AD, copie o valor de **URL de Solicitação de Autenticação** e cole-o na caixa de texto **Solicitação de Autenticação do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="45380-326">d.</span><span class="sxs-lookup"><span data-stu-id="45380-326">d.</span></span> <span data-ttu-id="45380-327">No portal clássico do Azure AD, copie o valor de **URL de Serviço de Saída Única** e cole-o na caixa de texto **Solicitação de Logoff Único do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="45380-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="45380-328">e.</span><span class="sxs-lookup"><span data-stu-id="45380-328">e.</span></span> <span data-ttu-id="45380-329">Como **Certificado de Provedor de Identidade**, selecione o certificado que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="45380-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="45380-330">Clique em **Configurações Avançadas** e, em **Propriedades Adicionais do Provedor de Identidade**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="45380-331">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="45380-332">a.</span><span class="sxs-lookup"><span data-stu-id="45380-332">a.</span></span> <span data-ttu-id="45380-333">Na caixa de texto **associação de protocolo SingleLogoutRequest do IDP**, digite **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="45380-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="45380-334">b.</span><span class="sxs-lookup"><span data-stu-id="45380-334">b.</span></span> <span data-ttu-id="45380-335">Na caixa de texto **Política da NameID**, digite **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="45380-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="45380-336">c.</span><span class="sxs-lookup"><span data-stu-id="45380-336">c.</span></span> <span data-ttu-id="45380-337">No **método AuthnContextClassRef**, digite **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="45380-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="45380-338">d.</span><span class="sxs-lookup"><span data-stu-id="45380-338">d.</span></span> <span data-ttu-id="45380-339">Desmarque **Criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="45380-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="45380-340">Em **Propriedades Adicionais do Provedor de Serviço**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="45380-341">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="45380-342">a.</span><span class="sxs-lookup"><span data-stu-id="45380-342">a.</span></span> <span data-ttu-id="45380-343">Na caixa de texto **Home page do ServiceNow** , digite a URL da sua página inicial de instância do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="45380-344">A home page da instância do ServiceNow é uma concatenação da **URL do locatário do ServiceNow** e **/navpage.do** (por exemplo: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="45380-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="45380-345">b.</span><span class="sxs-lookup"><span data-stu-id="45380-345">b.</span></span> <span data-ttu-id="45380-346">Na caixa de texto **ID da entidade/emissor** , digite a URL do seu locatário do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="45380-347">c.</span><span class="sxs-lookup"><span data-stu-id="45380-347">c.</span></span> <span data-ttu-id="45380-348">Na caixa de texto **URI do Público-alvo** , digite a URL do seu locatário do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="45380-349">d.</span><span class="sxs-lookup"><span data-stu-id="45380-349">d.</span></span> <span data-ttu-id="45380-350">Na caixa de texto **Distorção do Relógio**, digite **60**.</span><span class="sxs-lookup"><span data-stu-id="45380-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="45380-351">e.</span><span class="sxs-lookup"><span data-stu-id="45380-351">e.</span></span> <span data-ttu-id="45380-352">Na caixa de texto **Campo de Usuário**, digite **email** ou **user_name**, dependendo de qual campo é usado para identificar exclusivamente os usuários em sua implantação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="45380-353">Você pode configurar o Azure AD para emitir a ID de usuário (nome UPN) do Azure AD ou o endereço de email como o identificador exclusivo no token SAML acessando a seção **ServiceNow > Atributos > Logon Único** do portal clássico do Azure e mapeando o campo desejado para o atributo **nameidentifier**.</span><span class="sxs-lookup"><span data-stu-id="45380-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="45380-354">O valor armazenado para o atributo selecionado no Azure AD (por exemplo, nome UPN) deve corresponder ao valor armazenado no ServiceNow para o campo inserido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="45380-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="45380-355">f.</span><span class="sxs-lookup"><span data-stu-id="45380-355">f.</span></span> <span data-ttu-id="45380-356">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="45380-356">Click **Save**.</span></span> 

3. <span data-ttu-id="45380-357">No portal clássico do Azure AD, selecione a confirmação de configuração do logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="45380-358">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="45380-359">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="45380-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="45380-360">![Configurar logon único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="45380-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="45380-361">Configurando o provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="45380-361">Configuring user provisioning</span></span>
<span data-ttu-id="45380-362">O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="45380-363">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="45380-364">No portal clássico de Gerenciamento do Azure, na página de integração de aplicativos do **ServiceNow**, clique em **Configurar provisionamento de usuários**.</span><span class="sxs-lookup"><span data-stu-id="45380-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="45380-365">![Provisionamento do usuário](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Provisionamento do usuário")</span><span class="sxs-lookup"><span data-stu-id="45380-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="45380-366">Na página **Inserir suas credenciais do ServiceNow para habilitar o provisionamento automático de usuário**, forneça as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="45380-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="45380-367">a.</span><span class="sxs-lookup"><span data-stu-id="45380-367">a.</span></span> <span data-ttu-id="45380-368">Na caixa de texto **Nome de Instância do ServiceNow** , digite o nome da instância do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="45380-369">b.</span><span class="sxs-lookup"><span data-stu-id="45380-369">b.</span></span> <span data-ttu-id="45380-370">Na caixa de texto **Nome de Usuário Administrador do ServiceNow** , digite o nome da conta de administrador do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="45380-371">c.</span><span class="sxs-lookup"><span data-stu-id="45380-371">c.</span></span> <span data-ttu-id="45380-372">Na caixa de texto **Senha de Administrador do ServiceNow** , digite a senha desta conta.</span><span class="sxs-lookup"><span data-stu-id="45380-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="45380-373">d.</span><span class="sxs-lookup"><span data-stu-id="45380-373">d.</span></span> <span data-ttu-id="45380-374">Clique em **validar** para verificar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="45380-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="45380-375">e.</span><span class="sxs-lookup"><span data-stu-id="45380-375">e.</span></span> <span data-ttu-id="45380-376">Clique no botão **Avançar** para abrir a página **Próximas etapas**.</span><span class="sxs-lookup"><span data-stu-id="45380-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="45380-377">f.</span><span class="sxs-lookup"><span data-stu-id="45380-377">f.</span></span> <span data-ttu-id="45380-378">Se você deseja provisionar todos os usuários neste aplicativo, escolha "**Provisionar automaticamente todas as contas de usuário no diretório para este aplicativo**".</span><span class="sxs-lookup"><span data-stu-id="45380-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="45380-379">![Próximas etapas](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Próximas etapas")</span><span class="sxs-lookup"><span data-stu-id="45380-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="45380-380">g.</span><span class="sxs-lookup"><span data-stu-id="45380-380">g.</span></span> <span data-ttu-id="45380-381">Na página **Próximas etapas**, clique em **Concluir** para salvar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="45380-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="45380-382">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="45380-383">Nesta seção, você criará uma usuária de teste no portal clássico chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="45380-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="45380-385">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="45380-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="45380-386">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45380-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="45380-388">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="45380-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="45380-389">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="45380-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="45380-391">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="45380-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="45380-393">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="45380-395">a.</span><span class="sxs-lookup"><span data-stu-id="45380-395">a.</span></span> <span data-ttu-id="45380-396">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="45380-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="45380-397">b.</span><span class="sxs-lookup"><span data-stu-id="45380-397">b.</span></span> <span data-ttu-id="45380-398">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="45380-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="45380-399">c.</span><span class="sxs-lookup"><span data-stu-id="45380-399">c.</span></span> <span data-ttu-id="45380-400">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-400">Click **Next**.</span></span>

6. <span data-ttu-id="45380-401">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="45380-403">a.</span><span class="sxs-lookup"><span data-stu-id="45380-403">a.</span></span> <span data-ttu-id="45380-404">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="45380-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="45380-405">b.</span><span class="sxs-lookup"><span data-stu-id="45380-405">b.</span></span> <span data-ttu-id="45380-406">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="45380-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="45380-407">c.</span><span class="sxs-lookup"><span data-stu-id="45380-407">c.</span></span> <span data-ttu-id="45380-408">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="45380-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="45380-409">d.</span><span class="sxs-lookup"><span data-stu-id="45380-409">d.</span></span> <span data-ttu-id="45380-410">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="45380-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="45380-411">e.</span><span class="sxs-lookup"><span data-stu-id="45380-411">e.</span></span> <span data-ttu-id="45380-412">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45380-412">Click **Next**.</span></span>

7. <span data-ttu-id="45380-413">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="45380-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="45380-415">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="45380-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="45380-417">a.</span><span class="sxs-lookup"><span data-stu-id="45380-417">a.</span></span> <span data-ttu-id="45380-418">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="45380-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="45380-419">b.</span><span class="sxs-lookup"><span data-stu-id="45380-419">b.</span></span> <span data-ttu-id="45380-420">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="45380-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="45380-421">Criar um usuário de teste do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="45380-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="45380-422">Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="45380-423">Nesta seção, você criará uma usuária chamada Brenda Fernandes no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="45380-424">Se você não souber como adicionar um usuário em sua conta do ServiceNow ou do ServiceNow Express, contate a equipe de suporte do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="45380-425">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="45380-426">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="45380-428">**Para atribuir Brenda Fernandes ao ServiceNow, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="45380-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="45380-429">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="45380-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][201] 

2. <span data-ttu-id="45380-431">Na lista de aplicativos, selecione **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="45380-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="45380-433">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="45380-433">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 

4. <span data-ttu-id="45380-435">Na lista Todos os Usuários, escolha **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="45380-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="45380-436">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="45380-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="45380-438">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="45380-438">Testing single sign-on</span></span>
<span data-ttu-id="45380-439">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="45380-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="45380-440">Ao clicar no bloco do ServiceNow no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="45380-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="45380-441">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="45380-441">Additional resources</span></span>
* [<span data-ttu-id="45380-442">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="45380-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="45380-443">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45380-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
