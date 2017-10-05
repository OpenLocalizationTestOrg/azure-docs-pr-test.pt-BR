---
title: "Tutorial: Integração do Azure Active Directory com o Questetra BPM Suite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="99b2b-103">Tutorial: Integração do Active Directory do Azure com o Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="99b2b-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="99b2b-104">O objetivo desse tutorial é mostrar como integrar o Questetra BPM Suite ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="99b2b-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="99b2b-105">A integração do Questetra BPM Suite ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="99b2b-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="99b2b-106">Você pode controlar, no AD do Azure, quem tem acesso ao Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="99b2b-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="99b2b-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Questetra BPM Suite (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="99b2b-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="99b2b-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99b2b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99b2b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99b2b-110">Prerequisites</span></span>
<span data-ttu-id="99b2b-111">Para configurar a integração do AD do Azure com o Questetra BPM Suite, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="99b2b-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="99b2b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="99b2b-113">Uma assinatura habilitada para logon único do [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)</span><span class="sxs-lookup"><span data-stu-id="99b2b-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99b2b-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="99b2b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="99b2b-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="99b2b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="99b2b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="99b2b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="99b2b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99b2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="99b2b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="99b2b-118">Scenario Description</span></span>
<span data-ttu-id="99b2b-119">O objetivo deste tutorial é permitir que você teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="99b2b-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="99b2b-120">O cenário descrito neste tutorial consiste em três blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="99b2b-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="99b2b-121">Adicionar um Questetra BPM Suite da galeria</span><span class="sxs-lookup"><span data-stu-id="99b2b-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="99b2b-122">Configurar e testar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99b2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="99b2b-123">Adicionar um Questetra BPM Suite da galeria</span><span class="sxs-lookup"><span data-stu-id="99b2b-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="99b2b-124">Para configurar a integração do Questetra BPM Suite com o AD do Azure, você precisa adicionar o Questetra BPM Suite, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="99b2b-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99b2b-125">**Para adicionar o Questetra BPM Suite por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b2b-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99b2b-126">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="99b2b-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="99b2b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="99b2b-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="99b2b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="99b2b-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="99b2b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="99b2b-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="99b2b-135">Na caixa de pesquisa, digite **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="99b2b-137">No painel de resultados, selecione **Questetra BPM Suite** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99b2b-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99b2b-138">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99b2b-139">O objetivo desta seção é mostrar como configurar e testar logon único do AD do Azure com o Questetra BPM Suite, com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99b2b-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99b2b-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Questetra BPM Suite é equivalente a um usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="99b2b-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="99b2b-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado do Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="99b2b-142">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="99b2b-143">Para configurar e testar o logon único do AD do Azure com o Questetra BPM Suite, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="99b2b-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99b2b-144">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on)** - para habilitar seus usuários para usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="99b2b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99b2b-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="99b2b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99b2b-146">**[Criar um usuário de teste do Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)** - para ter um equivalente de Britta Simon no Questetra BPM Suite que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b2b-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99b2b-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="99b2b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99b2b-148">**[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="99b2b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99b2b-149">Configuração do logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="99b2b-150">O objetivo desta seção é habilitar o logon único do Azure AD no portal clássico do Azure e configurar o logon único em seu aplicativo do Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="99b2b-151">**Para configurar o logon único do AD do Azure com o Questetra BPM Suite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b2b-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="99b2b-152">No portal clássico do Azure, na página de integração de aplicativos do **Questetra BPM Suite**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o logon único][8]

2. <span data-ttu-id="99b2b-154">Na página **Como você deseja que os usuários façam logon no Questetra BPM Suite**, selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][9]

3. <span data-ttu-id="99b2b-156">Em outra janela do navegador da Web, faça logon em seu site de empresa **Questetra BPM Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="99b2b-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="99b2b-157">No menu na parte superior, clique em **Configurações do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Logon Único do AD do Azure][10]

5. <span data-ttu-id="99b2b-159">Para abrir a página **SingleSignOnSAML**, clique em **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Logon Único do AD do Azure][11]

6. <span data-ttu-id="99b2b-161">No portal clássico do Azure, na página de diálogo **Definir Configurações de Aplicativo** , execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Definir Configurações de Aplicativo][13]
   
    <span data-ttu-id="99b2b-163">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-163">a.</span></span> <span data-ttu-id="99b2b-164">No site de empresa do **Questetra BPM Suite**, na seção Informações do SP, copie a **URL de ACS** e cole-a na caixa de texto **URL de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="99b2b-165">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-165">b.</span></span> <span data-ttu-id="99b2b-166">No site de empresa do **Questetra BPM Suite**, na seção Informações do SP, copie a **ID de Entidade** e cole-a na caixa de texto **URL do Emissor**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="99b2b-167">c.</span><span class="sxs-lookup"><span data-stu-id="99b2b-167">c.</span></span> <span data-ttu-id="99b2b-168">No site de empresa do **Questetra BPM Suite**, na seção Informações do SP, copie a **URL de ACS** e cole-a na caixa de texto **URL de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="99b2b-169">d.</span><span class="sxs-lookup"><span data-stu-id="99b2b-169">d.</span></span> <span data-ttu-id="99b2b-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-170">Click **Next**.</span></span>

7. <span data-ttu-id="99b2b-171">Na página **Configurar logon único no Questetra BPM Suite**, clique em **Baixar certificado** e salve o arquivo de certificado localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="99b2b-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configurar o logon único][14]

8. <span data-ttu-id="99b2b-173">No seu site da empresa **Questetra BPM Suite** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configurar Logon Único][15]
   
    <span data-ttu-id="99b2b-175">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-175">a.</span></span> <span data-ttu-id="99b2b-176">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="99b2b-177">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-177">b.</span></span> <span data-ttu-id="99b2b-178">No portal clássico do Azure, copie o valor da **URL do Emissor** e cole-o na caixa de texto **ID de Entidade**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="99b2b-179">c.</span><span class="sxs-lookup"><span data-stu-id="99b2b-179">c.</span></span> <span data-ttu-id="99b2b-180">No portal clássico do Azure, copie o valor da **URL do Serviço de Logon Único** e cole-o na caixa de texto **URL da página de conexão**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="99b2b-181">d.</span><span class="sxs-lookup"><span data-stu-id="99b2b-181">d.</span></span> <span data-ttu-id="99b2b-182">No portal clássico do Azure, copie o valor da **URL do Serviço de Saída Único** e cole-o na caixa de texto **URL da página de saída**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="99b2b-183">e.</span><span class="sxs-lookup"><span data-stu-id="99b2b-183">e.</span></span> <span data-ttu-id="99b2b-184">Na caixa de texto **Formato da NameID**, digite **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="99b2b-185">f.</span><span class="sxs-lookup"><span data-stu-id="99b2b-185">f.</span></span> <span data-ttu-id="99b2b-186">Crie um arquivo codificado em base 64 usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="99b2b-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="99b2b-187">Para obter mais detalhes, consulte [Como converter um certificado binário em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="99b2b-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="99b2b-188">g.</span><span class="sxs-lookup"><span data-stu-id="99b2b-188">g.</span></span> <span data-ttu-id="99b2b-189">Abra seu certificado codificado em base-64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado de validação** .</span><span class="sxs-lookup"><span data-stu-id="99b2b-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="99b2b-190">h.</span><span class="sxs-lookup"><span data-stu-id="99b2b-190">h.</span></span> <span data-ttu-id="99b2b-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-191">Click **Save**.</span></span>

1. <span data-ttu-id="99b2b-192">No portal clássico do Azure, selecione a confirmação de configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][17]

2. <span data-ttu-id="99b2b-194">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99b2b-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="99b2b-197">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="99b2b-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="99b2b-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b2b-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99b2b-199">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][100] 

2. <span data-ttu-id="99b2b-201">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="99b2b-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="99b2b-202">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][101] 

4. <span data-ttu-id="99b2b-204">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Criar um usuário de teste do AD do Azure][102] 

5. <span data-ttu-id="99b2b-206">Na página do diálogo **Conte-nos sobre este usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Criar um usuário de teste do AD do Azure][103]
   
    <span data-ttu-id="99b2b-208">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-208">a.</span></span> <span data-ttu-id="99b2b-209">Em **Tipo de Usuário**, selecione **Novo usuário na organização**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="99b2b-210">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-210">b.</span></span> <span data-ttu-id="99b2b-211">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="99b2b-212">c.</span><span class="sxs-lookup"><span data-stu-id="99b2b-212">c.</span></span> <span data-ttu-id="99b2b-213">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="99b2b-213">Click Next.</span></span>

6. <span data-ttu-id="99b2b-214">Na página da caixa de diálogo **Perfil do Usuário** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Criar um usuário de teste do AD do Azure][104] 
   
    <span data-ttu-id="99b2b-216">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-216">a.</span></span> <span data-ttu-id="99b2b-217">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="99b2b-218">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-218">b.</span></span> <span data-ttu-id="99b2b-219">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="99b2b-220">c.</span><span class="sxs-lookup"><span data-stu-id="99b2b-220">c.</span></span> <span data-ttu-id="99b2b-221">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="99b2b-222">d.</span><span class="sxs-lookup"><span data-stu-id="99b2b-222">d.</span></span> <span data-ttu-id="99b2b-223">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="99b2b-224">e.</span><span class="sxs-lookup"><span data-stu-id="99b2b-224">e.</span></span> <span data-ttu-id="99b2b-225">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-225">Click **Next**.</span></span>

7. <span data-ttu-id="99b2b-226">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][105]  

8. <span data-ttu-id="99b2b-228">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criar um usuário de teste do AD do Azure][106]   
   
    <span data-ttu-id="99b2b-230">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-230">a.</span></span> <span data-ttu-id="99b2b-231">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="99b2b-232">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-232">b.</span></span> <span data-ttu-id="99b2b-233">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="99b2b-234">Criar um usuário de teste do Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="99b2b-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="99b2b-235">O objetivo desta seção é criar um usuário chamado Britta Simon no Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="99b2b-236">**Para criar um usuário chamado Brenda Fernandes no Questetra BPM Suite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b2b-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="99b2b-237">Faça logon no site da sua empresa do Questetra BPM Suite como um administrador.</span><span class="sxs-lookup"><span data-stu-id="99b2b-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="99b2b-238">Vá para **Configurações do Sistema > Lista de Usuários > Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="99b2b-239">Na caixa de diálogo Novo Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="99b2b-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Criar um usuário de teste][300] 
   
    <span data-ttu-id="99b2b-241">a.</span><span class="sxs-lookup"><span data-stu-id="99b2b-241">a.</span></span> <span data-ttu-id="99b2b-242">Na caixa de texto **Nome** , digite o nome de usuário Britta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b2b-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="99b2b-243">b.</span><span class="sxs-lookup"><span data-stu-id="99b2b-243">b.</span></span> <span data-ttu-id="99b2b-244">Na caixa de texto **Email** , digite o nome de usuário Britta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99b2b-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="99b2b-245">c.</span><span class="sxs-lookup"><span data-stu-id="99b2b-245">c.</span></span> <span data-ttu-id="99b2b-246">Na caixa de texto **Senha** , digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="99b2b-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="99b2b-247">Clique em **Adicionar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="99b2b-248">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="99b2b-249">O objetivo desta seção é habilitar Brenda Fernandes a usar o logon único do Azure, concedendo a ela acesso ao Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![O que é o Azure AD Connect][200]

<span data-ttu-id="99b2b-251">**Para atribuir Britta Simon ao Questetra BPM Suite, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="99b2b-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="99b2b-252">No portal clássico do Azure, para abrir o modo de exibição de aplicativos, na exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="99b2b-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![O que é o Azure AD Connect][201]
2. <span data-ttu-id="99b2b-254">Na lista de aplicativos, selecione **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![O que é o Azure AD Connect][205]
3. <span data-ttu-id="99b2b-256">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-256">In the menu on the top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][202]
4. <span data-ttu-id="99b2b-258">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![O que é o Azure AD Connect][203]
5. <span data-ttu-id="99b2b-260">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="99b2b-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![O que é o Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="99b2b-262">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="99b2b-262">Testing Single Sign-On</span></span>
<span data-ttu-id="99b2b-263">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="99b2b-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="99b2b-264">Quando clica no bloco Questetra BPM Suite no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="99b2b-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99b2b-265">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="99b2b-265">Additional Resources</span></span>
* [<span data-ttu-id="99b2b-266">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="99b2b-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99b2b-267">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99b2b-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
