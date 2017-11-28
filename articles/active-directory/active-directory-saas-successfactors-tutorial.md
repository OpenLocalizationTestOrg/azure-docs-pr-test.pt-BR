---
title: "Tutorial: integração do Azure Active Directory ao SuccessFactors | Microsoft Docs"
description: "Saiba como usar o SuccessFactors com o Active Directory do Azure para habilitar o logon único, provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="f46b3-103">Tutorial: Integração do Azure Active Directory com o SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f46b3-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="f46b3-104">O objetivo desse tutorial é mostrar como integrar o SuccessFactors ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f46b3-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f46b3-105">A integração do SuccessFactors ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f46b3-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="f46b3-106">No Azure AD, você pode controlar quem tem acesso ao SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f46b3-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="f46b3-107">Você pode habilitar seus usuários a fazerem logon automaticamente no SuccessFactors (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f46b3-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f46b3-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f46b3-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f46b3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f46b3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f46b3-110">Prerequisites</span></span>
<span data-ttu-id="f46b3-111">Para configurar a integração do Azure AD ao SuccessFactors, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f46b3-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="f46b3-112">Uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-112">A valid Azure subscription</span></span>
* <span data-ttu-id="f46b3-113">Um locatário no SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f46b3-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="f46b3-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f46b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f46b3-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f46b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f46b3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f46b3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f46b3-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f46b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f46b3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f46b3-118">Scenario description</span></span>
<span data-ttu-id="f46b3-119">O objetivo deste tutorial é permitir que você teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f46b3-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f46b3-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f46b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f46b3-121">Adição do SuccessFactors da galeria</span><span class="sxs-lookup"><span data-stu-id="f46b3-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="f46b3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="f46b3-123">Adição do SuccessFactors da galeria</span><span class="sxs-lookup"><span data-stu-id="f46b3-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="f46b3-124">Para configurar a integração do SuccessFactors ao Azure AD, você precisará adicionar o SuccessFactors da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f46b3-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f46b3-125">**Para adicionar o SuccessFactors da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f46b3-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f46b3-126">No portal clássico do Azure, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Configurando o logon único][1]
2. <span data-ttu-id="f46b3-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="f46b3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f46b3-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="f46b3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configurando o logon único][2]
4. <span data-ttu-id="f46b3-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="f46b3-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="f46b3-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configurando o logon único][4]
6. <span data-ttu-id="f46b3-135">Na **caixa de pesquisa**, digite **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Configurando o logon único][5]
7. <span data-ttu-id="f46b3-137">No painel de resultados, selecione **SuccessFactors** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f46b3-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Configurando o logon único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f46b3-139">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f46b3-140">O objetivo desta seção é mostrar como configurar e testar logon único do Azure AD com o SuccessFactors, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f46b3-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f46b3-141">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SuccessFactors é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f46b3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="f46b3-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="f46b3-143">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD ao valor do **Nome de Usuário** no SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="f46b3-144">Para configurar e testar o logon único do Azure AD com o SuccessFactors, é preciso concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f46b3-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f46b3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f46b3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f46b3-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f46b3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f46b3-147">**[Criação de um usuário de teste do SuccessFactors](#creating-a-successfactors-test-user)** : para ter um equivalente de Brenda Fernandes no SuccessFactors que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f46b3-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f46b3-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f46b3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f46b3-149">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f46b3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f46b3-150">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f46b3-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="f46b3-151">Nesta seção, você habilitará o logon único do Azure AD no portal clássico e configurará o logon único em seu aplicativo SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="f46b3-152">**Para configurar o logon único do Azure AD com o SuccessFactors, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f46b3-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="f46b3-153">No portal clássico do Azure, na página de integração do aplicativo **SuccessFactors**, clique em **Configurar logon único** para abrir o diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Configurando o logon único][7]
2. <span data-ttu-id="f46b3-155">Na página **Como você deseja que os usuários façam logon no SuccessFactors**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurando o logon único][8]
3. <span data-ttu-id="f46b3-157">Na página **Configurar URL do Aplicativo**, realize as etapas a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Configurando o logon único][9]
   
    <span data-ttu-id="f46b3-159">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-159">a.</span></span> <span data-ttu-id="f46b3-160">Na caixa de texto **URL de Entrada** , digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="f46b3-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="f46b3-161">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-161">b.</span></span> <span data-ttu-id="f46b3-162">Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="f46b3-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="f46b3-163">c.</span><span class="sxs-lookup"><span data-stu-id="f46b3-163">c.</span></span> <span data-ttu-id="f46b3-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="f46b3-165">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="f46b3-165">Please note that these are not the real values.</span></span> <span data-ttu-id="f46b3-166">Você precisa atualizar esses valores com a URL de Entrada e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="f46b3-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="f46b3-167">Para obter esses valores, entre em contato com a [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="f46b3-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="f46b3-168">Na página **Configurar logon único no SuccessFactors**, clique em **Baixar certificado** e salve o arquivo de certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="f46b3-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configurando o logon único][10]

2. <span data-ttu-id="f46b3-170">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do **portal de administração do SuccessFactors** como administrador.</span><span class="sxs-lookup"><span data-stu-id="f46b3-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="f46b3-171">Visite **Segurança de Aplicativo** e nativo do **Recurso Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="f46b3-172">Coloque qualquer valor em **Redefinir Token** e clique em **Salvar Token** para habilitar SSO do SAML.</span><span class="sxs-lookup"><span data-stu-id="f46b3-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configurar o logon único no lado do aplicativo][11]

    > [!NOTE] 
    > <span data-ttu-id="f46b3-174">Esse valor é usado apenas como chave liga/desliga.</span><span class="sxs-lookup"><span data-stu-id="f46b3-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="f46b3-175">Se nenhum valor for salvo, o SSO do SAML será ATIVADO.</span><span class="sxs-lookup"><span data-stu-id="f46b3-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="f46b3-176">Se um valor em branco for salvo, o SSO do SAML será DESATIVADO.</span><span class="sxs-lookup"><span data-stu-id="f46b3-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="f46b3-177">Nativo da captura de tela abaixo e execute as ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="f46b3-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Configurar o logon único no lado do aplicativo][12]
   
    <span data-ttu-id="f46b3-179">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-179">a.</span></span> <span data-ttu-id="f46b3-180">Selecione o botão de opção **SSO do SAML v2**</span><span class="sxs-lookup"><span data-stu-id="f46b3-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="f46b3-181">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-181">b.</span></span> <span data-ttu-id="f46b3-182">Defina o Nome da Parte de Declaração SAML (por exemplo, emissor SAml + nome da empresa).</span><span class="sxs-lookup"><span data-stu-id="f46b3-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="f46b3-183">c.</span><span class="sxs-lookup"><span data-stu-id="f46b3-183">c.</span></span> <span data-ttu-id="f46b3-184">Na caixa de texto **Emissor SAML**, coloque o valor de **URL do Emissor** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f46b3-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="f46b3-185">d.</span><span class="sxs-lookup"><span data-stu-id="f46b3-185">d.</span></span> <span data-ttu-id="f46b3-186">Selecione **Resposta(Gerada pelo Cliente/IdP/AP)** como **Exigir Assinatura Obrigatória**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="f46b3-187">e.</span><span class="sxs-lookup"><span data-stu-id="f46b3-187">e.</span></span> <span data-ttu-id="f46b3-188">Selecione **Habilitado** como **Habilitar Sinalizador SAML**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="f46b3-189">f.</span><span class="sxs-lookup"><span data-stu-id="f46b3-189">f.</span></span> <span data-ttu-id="f46b3-190">Selecione **Não** como **Assinatura da Solicitação de Logon (Gerado por SF/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="f46b3-191">g.</span><span class="sxs-lookup"><span data-stu-id="f46b3-191">g.</span></span> <span data-ttu-id="f46b3-192">Selecione **Perfil de Navegador/Postagem** como **Perfil SAML**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="f46b3-193">h.</span><span class="sxs-lookup"><span data-stu-id="f46b3-193">h.</span></span> <span data-ttu-id="f46b3-194">Selecione **Não** como **Impor Período de Certificado Válido**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="f46b3-195">i.</span><span class="sxs-lookup"><span data-stu-id="f46b3-195">i.</span></span> <span data-ttu-id="f46b3-196">Copie o conteúdo do arquivo do certificado baixado e, então, cole-o na caixa de texto **Certificado de Verificação SAML** .</span><span class="sxs-lookup"><span data-stu-id="f46b3-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f46b3-197">O conteúdo do certificado deve ter começar marcas de certificado do certificado e de fim.</span><span class="sxs-lookup"><span data-stu-id="f46b3-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="f46b3-198">Navegue até SAML V2 e então execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f46b3-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configurar o logon único no lado do aplicativo][13]
   
    <span data-ttu-id="f46b3-200">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-200">a.</span></span> <span data-ttu-id="f46b3-201">Selecione **Sim** como **Logoff Global iniciado por SP de suporte**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="f46b3-202">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-202">b.</span></span> <span data-ttu-id="f46b3-203">Na caixa de texto **URL de Serviço Logoff Global (destino de LogoutRequest)**, coloque o valor de **URL de Logoff Remoto** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f46b3-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="f46b3-204">c.</span><span class="sxs-lookup"><span data-stu-id="f46b3-204">c.</span></span> <span data-ttu-id="f46b3-205">Selecione **Não** como **Exigir que sp criptografe todos os elementos NameID**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="f46b3-206">d.</span><span class="sxs-lookup"><span data-stu-id="f46b3-206">d.</span></span> <span data-ttu-id="f46b3-207">Selecione **não especificado** como **Formato de NameID**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="f46b3-208">e.</span><span class="sxs-lookup"><span data-stu-id="f46b3-208">e.</span></span> <span data-ttu-id="f46b3-209">Selecione **Sim** como **Habilitar logon iniciado por sp (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="f46b3-210">f.</span><span class="sxs-lookup"><span data-stu-id="f46b3-210">f.</span></span> <span data-ttu-id="f46b3-211">Na caixa de texto **Enviar solicitação como emissor para Toda a Empresa**, insira o valor de **URL de Logon Remoto** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f46b3-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="f46b3-212">Execute estas etapas se quiser fazer com os nomes de usuário de logon diferenciem maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f46b3-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="f46b3-213">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-213">a.</span></span> <span data-ttu-id="f46b3-214">Visite **Configurações da Empresa**(próximo à parte inferior).</span><span class="sxs-lookup"><span data-stu-id="f46b3-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="f46b3-215">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-215">b.</span></span> <span data-ttu-id="f46b3-216">marque a caixa de seleção ao lado de **Habilitar Nome de Usuário que Não Diferencia Maiúsculas de Minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="f46b3-217">c.Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-217">c.Click **Save**.</span></span>
   
    ![Configurar o logon único][29]

    > [!NOTE] 
    > <span data-ttu-id="f46b3-219">Se você tentar habilitar essa opção, o sistema verificará se ele criará um nome de logon SAML duplicado.</span><span class="sxs-lookup"><span data-stu-id="f46b3-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="f46b3-220">Por exemplo, se o cliente tiver os nomes de usuário Usuário1 e usuário1.</span><span class="sxs-lookup"><span data-stu-id="f46b3-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="f46b3-221">Parar de diferenciar maiúsculas e minúsculas cria essas duplicatas.</span><span class="sxs-lookup"><span data-stu-id="f46b3-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="f46b3-222">O sistema fornecerá a você uma mensagem de erro e não habilitará o recurso.</span><span class="sxs-lookup"><span data-stu-id="f46b3-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="f46b3-223">O cliente precisará alterar um dos nomes de usuário para que ele realmente sela digitado diferentes.</span><span class="sxs-lookup"><span data-stu-id="f46b3-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="f46b3-224">No portal clássico do Azure, selecione a confirmação da configuração de logon único e clique em **Concluir** para fechar a caixa de diálogo **Configurar logon único**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Aplicativos][14]
2. <span data-ttu-id="f46b3-226">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplicativos][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f46b3-228">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="f46b3-229">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f46b3-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][16]

<span data-ttu-id="f46b3-231">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f46b3-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f46b3-232">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][17]
2. <span data-ttu-id="f46b3-234">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="f46b3-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="f46b3-235">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][18]
4. <span data-ttu-id="f46b3-237">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][19]
5. <span data-ttu-id="f46b3-239">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f46b3-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][20]
   
    <span data-ttu-id="f46b3-241">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-241">a.</span></span> <span data-ttu-id="f46b3-242">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="f46b3-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="f46b3-243">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-243">b.</span></span> <span data-ttu-id="f46b3-244">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f46b3-245">c.</span><span class="sxs-lookup"><span data-stu-id="f46b3-245">c.</span></span> <span data-ttu-id="f46b3-246">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-246">Click **Next**.</span></span>
6. <span data-ttu-id="f46b3-247">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f46b3-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][21]
   
    <span data-ttu-id="f46b3-249">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-249">a.</span></span> <span data-ttu-id="f46b3-250">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="f46b3-251">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-251">b.</span></span> <span data-ttu-id="f46b3-252">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f46b3-253">c.</span><span class="sxs-lookup"><span data-stu-id="f46b3-253">c.</span></span> <span data-ttu-id="f46b3-254">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f46b3-255">d.</span><span class="sxs-lookup"><span data-stu-id="f46b3-255">d.</span></span> <span data-ttu-id="f46b3-256">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f46b3-257">e.</span><span class="sxs-lookup"><span data-stu-id="f46b3-257">e.</span></span> <span data-ttu-id="f46b3-258">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-258">Click **Next**.</span></span>
7. <span data-ttu-id="f46b3-259">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][22]
8. <span data-ttu-id="f46b3-261">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f46b3-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure][23]
   
    <span data-ttu-id="f46b3-263">a.</span><span class="sxs-lookup"><span data-stu-id="f46b3-263">a.</span></span> <span data-ttu-id="f46b3-264">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="f46b3-265">b.</span><span class="sxs-lookup"><span data-stu-id="f46b3-265">b.</span></span> <span data-ttu-id="f46b3-266">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="f46b3-267">Criação de um usuário de teste do SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="f46b3-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="f46b3-268">Para permitir que os usuários do AD do Azure façam logon no SuccessFactors, eles deverão ser provisionados no SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="f46b3-269">No caso do SuccessFactors, o provisionamento será uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f46b3-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="f46b3-270">Para obter os usuários criados no SuccessFactors, você precisará entrar em contato com a [equipe de suporte do SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="f46b3-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f46b3-271">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="f46b3-272">O objetivo desta seção é permitir que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Atribuir usuário][24]

<span data-ttu-id="f46b3-274">**Para atribuir Brenda Fernandes ao SuccessFactors, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f46b3-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="f46b3-275">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="f46b3-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][25]
2. <span data-ttu-id="f46b3-277">Na lista de aplicativos, selecione **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Configurar o logon único][26]
3. <span data-ttu-id="f46b3-279">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-279">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][27]
4. <span data-ttu-id="f46b3-281">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="f46b3-282">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f46b3-284">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f46b3-284">Testing single sign-on</span></span>
<span data-ttu-id="f46b3-285">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f46b3-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f46b3-286">Quando você clicar no bloco SuccessFactors no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="f46b3-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f46b3-287">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f46b3-287">Additional resources</span></span>
* [<span data-ttu-id="f46b3-288">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f46b3-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f46b3-289">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f46b3-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
