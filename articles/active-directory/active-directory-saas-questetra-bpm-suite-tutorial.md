---
title: "Tutorial: Integração do Azure Active Directory com o Questetra BPM Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Questetra BPM Suite."
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
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="84bf7-103">Tutorial: Integração do Active Directory do Azure com o Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="84bf7-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="84bf7-104">Olá objetivo deste tutorial é tooshow você como toointegrate Questetra BPM Suite com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="84bf7-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="84bf7-105">Pacote de BPM Questetra integrando o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="84bf7-106">Você pode controlar no AD do Azure que tenha acesso tooQuestetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="84bf7-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="84bf7-107">Você pode habilitar seu usuários tooautomatically get conectado tooQuestetra BPM Suite (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="84bf7-108">Você pode gerenciar suas contas em um local central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="84bf7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="84bf7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84bf7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="84bf7-110">Prerequisites</span></span>
<span data-ttu-id="84bf7-111">tooconfigure integração do AD do Azure com Questetra BPM Suite, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="84bf7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="84bf7-113">Uma assinatura habilitada para logon único do [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)</span><span class="sxs-lookup"><span data-stu-id="84bf7-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84bf7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="84bf7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="84bf7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="84bf7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="84bf7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="84bf7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="84bf7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84bf7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="84bf7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="84bf7-118">Scenario Description</span></span>
<span data-ttu-id="84bf7-119">Olá objetivo deste tutorial é tooenable tootest logon único do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="84bf7-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="84bf7-120">cenário de saudação descrito neste tutorial consiste em três principais blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="84bf7-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="84bf7-121">Adicionar pacote de BPM Questetra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="84bf7-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="84bf7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="84bf7-123">Adicionar pacote de BPM Questetra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="84bf7-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="84bf7-124">integração de saudação tooconfigure do pacote de BPM Questetra no AD do Azure, você precisa tooadd Questetra BPM Suite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="84bf7-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84bf7-125">**tooadd Questetra BPM Suite da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84bf7-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84bf7-126">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="84bf7-128">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="84bf7-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="84bf7-129">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="84bf7-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="84bf7-131">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="84bf7-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="84bf7-133">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="84bf7-135">Na caixa de pesquisa hello, digite **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="84bf7-137">No painel de resultados de saudação, selecione **Questetra BPM Suite**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="84bf7-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84bf7-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84bf7-139">Olá o objetivo desta seção é tooshow como tooconfigure e teste de logon único do AD do Azure com o pacote de BPM Questetra com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="84bf7-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84bf7-140">Para toowork de logon único, o AD do Azure precisa tooknow é que usuário de contraparte saudação do usuário do pacote de BPM Questetra tooan no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="84bf7-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="84bf7-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no pacote de BPM Questetra precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="84bf7-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="84bf7-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no pacote de BPM Questetra.</span><span class="sxs-lookup"><span data-stu-id="84bf7-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="84bf7-143">tooconfigure e teste de logon único do AD do Azure com Questetra BPM Suite, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84bf7-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="84bf7-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84bf7-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84bf7-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84bf7-146">**[Criar um usuário de teste do pacote de BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave um equivalente do Britta Simon no pacote de BPM Questetra que é a representação toohello vinculado do Azure AD de seus.</span><span class="sxs-lookup"><span data-stu-id="84bf7-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="84bf7-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="84bf7-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84bf7-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="84bf7-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84bf7-149">Configuração do logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="84bf7-150">Olá objetivo desta seção é tooenable AD do Azure-logon único no hello portal clássico do Azure e tooconfigure logon único no aplicativo Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="84bf7-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="84bf7-151">**tooconfigure logon único do AD do Azure com o pacote de BPM Questetra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84bf7-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="84bf7-152">Em Olá portal clássico do Azure, em Olá **Questetra BPM Suite** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="84bf7-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][8]

2. <span data-ttu-id="84bf7-154">Em Olá **como você gostaria usuários toosign em tooQuestetra BPM Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][9]

3. <span data-ttu-id="84bf7-156">Em outra janela do navegador da Web, faça logon em seu site de empresa **Questetra BPM Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="84bf7-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="84bf7-157">No menu de saudação na parte superior de saudação, clique em **configurações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Logon Único do AD do Azure][10]

5. <span data-ttu-id="84bf7-159">Olá tooopen **SingleSignOnSAML** , clique em **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Logon Único do AD do Azure][11]

6. <span data-ttu-id="84bf7-161">Em Olá portal clássico do Azure, em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Definir configurações de aplicativo][13]
   
    <span data-ttu-id="84bf7-163">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-163">a.</span></span> <span data-ttu-id="84bf7-164">Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **URL do ACS**e, em seguida, cole-Olá **URL de logon** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="84bf7-165">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-165">b.</span></span> <span data-ttu-id="84bf7-166">Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **ID da entidade**e, em seguida, cole-Olá **URL do emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="84bf7-167">c.</span><span class="sxs-lookup"><span data-stu-id="84bf7-167">c.</span></span> <span data-ttu-id="84bf7-168">Você **Questetra BPM Suite** Olá seção SP informações do site de empresa, Olá cópia **URL do ACS**e, em seguida, cole-Olá **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="84bf7-169">d.</span><span class="sxs-lookup"><span data-stu-id="84bf7-169">d.</span></span> <span data-ttu-id="84bf7-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-170">Click **Next**.</span></span>

7. <span data-ttu-id="84bf7-171">Em Olá **configurar logon único no pacote de BPM Questetra** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="84bf7-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurar Logon Único][14]

8. <span data-ttu-id="84bf7-173">Você **Questetra BPM Suite** site da empresa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Configurar Logon Único][15]
   
    <span data-ttu-id="84bf7-175">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-175">a.</span></span> <span data-ttu-id="84bf7-176">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="84bf7-177">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-177">b.</span></span> <span data-ttu-id="84bf7-178">No hello portal clássico do Azure, copie Olá **URL do emissor** valor e, em seguida, cole-o em Olá **ID da entidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="84bf7-179">c.</span><span class="sxs-lookup"><span data-stu-id="84bf7-179">c.</span></span> <span data-ttu-id="84bf7-180">No hello portal clássico do Azure, copie Olá **o URL de serviço de logon único** valor e, em seguida, cole-o em Olá **URL da página de entrada** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="84bf7-181">d.</span><span class="sxs-lookup"><span data-stu-id="84bf7-181">d.</span></span> <span data-ttu-id="84bf7-182">No hello portal clássico do Azure, copie Olá **URL do serviço de logon único** valor e, em seguida, cole-o em Olá **URL da página de logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="84bf7-183">e.</span><span class="sxs-lookup"><span data-stu-id="84bf7-183">e.</span></span> <span data-ttu-id="84bf7-184">Em Olá **formato NameID** caixa de texto, tipo **urn: oasis: nomes: tc: SAML: 1.1 nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="84bf7-185">f.</span><span class="sxs-lookup"><span data-stu-id="84bf7-185">f.</span></span> <span data-ttu-id="84bf7-186">Crie um arquivo codificado em base 64 usando o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="84bf7-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="84bf7-187">Para obter mais detalhes, consulte [como tooconvert um binário de certificado em um arquivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="84bf7-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="84bf7-188">g.</span><span class="sxs-lookup"><span data-stu-id="84bf7-188">g.</span></span> <span data-ttu-id="84bf7-189">Abra seu certificado codificado em base 64 no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-Olá **certificado de validação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="84bf7-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="84bf7-190">h.</span><span class="sxs-lookup"><span data-stu-id="84bf7-190">h.</span></span> <span data-ttu-id="84bf7-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-191">Click **Save**.</span></span>

1. <span data-ttu-id="84bf7-192">Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][17]

2. <span data-ttu-id="84bf7-194">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84bf7-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="84bf7-197">Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="84bf7-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="84bf7-198">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84bf7-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84bf7-199">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][100] 

2. <span data-ttu-id="84bf7-201">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="84bf7-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="84bf7-202">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][101] 

4. <span data-ttu-id="84bf7-204">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Criar um usuário de teste do AD do Azure][102] 

5. <span data-ttu-id="84bf7-206">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criar um usuário de teste do AD do Azure][103]
   
    <span data-ttu-id="84bf7-208">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-208">a.</span></span> <span data-ttu-id="84bf7-209">Em **Tipo de Usuário**, selecione **Novo usuário na organização**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="84bf7-210">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-210">b.</span></span> <span data-ttu-id="84bf7-211">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="84bf7-212">c.</span><span class="sxs-lookup"><span data-stu-id="84bf7-212">c.</span></span> <span data-ttu-id="84bf7-213">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="84bf7-213">Click Next.</span></span>

6. <span data-ttu-id="84bf7-214">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Criar um usuário de teste do AD do Azure][104] 
   
    <span data-ttu-id="84bf7-216">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-216">a.</span></span> <span data-ttu-id="84bf7-217">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="84bf7-218">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-218">b.</span></span> <span data-ttu-id="84bf7-219">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="84bf7-220">c.</span><span class="sxs-lookup"><span data-stu-id="84bf7-220">c.</span></span> <span data-ttu-id="84bf7-221">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="84bf7-222">d.</span><span class="sxs-lookup"><span data-stu-id="84bf7-222">d.</span></span> <span data-ttu-id="84bf7-223">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="84bf7-224">e.</span><span class="sxs-lookup"><span data-stu-id="84bf7-224">e.</span></span> <span data-ttu-id="84bf7-225">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-225">Click **Next**.</span></span>

7. <span data-ttu-id="84bf7-226">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um usuário de teste do AD do Azure][105]  

8. <span data-ttu-id="84bf7-228">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar um usuário de teste do AD do Azure][106]   
   
    <span data-ttu-id="84bf7-230">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-230">a.</span></span> <span data-ttu-id="84bf7-231">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="84bf7-232">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-232">b.</span></span> <span data-ttu-id="84bf7-233">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="84bf7-234">Criar um usuário de teste do Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="84bf7-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="84bf7-235">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no pacote de BPM Questetra.</span><span class="sxs-lookup"><span data-stu-id="84bf7-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="84bf7-236">**toocreate um usuário chamado Britta Simon no pacote de BPM Questetra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84bf7-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="84bf7-237">Site de empresa de Questetra BPM Suite tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="84bf7-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="84bf7-238">Vá muito**configurações do sistema > lista de usuários > novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="84bf7-239">Na caixa de diálogo de novo usuário hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="84bf7-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Criar um usuário de teste][300] 
   
    <span data-ttu-id="84bf7-241">a.</span><span class="sxs-lookup"><span data-stu-id="84bf7-241">a.</span></span> <span data-ttu-id="84bf7-242">Em Olá **nome** caixa de texto, digite o nome de usuário de Britta no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="84bf7-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="84bf7-243">b.</span><span class="sxs-lookup"><span data-stu-id="84bf7-243">b.</span></span> <span data-ttu-id="84bf7-244">Em Olá **Email** caixa de texto, digite o nome de usuário de Britta no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="84bf7-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="84bf7-245">c.</span><span class="sxs-lookup"><span data-stu-id="84bf7-245">c.</span></span> <span data-ttu-id="84bf7-246">Em Olá **senha** caixa de texto, digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="84bf7-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="84bf7-247">Clique em **Adicionar novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="84bf7-248">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="84bf7-249">Olá objetivo desta seção é tooenabling Britta Simon toouse logon único do Azure concedendo tooQuestetra seu acesso BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="84bf7-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![O que é o Azure AD Connect][200]

<span data-ttu-id="84bf7-251">**tooassign Britta Simon tooQuestetra BPM Suite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="84bf7-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="84bf7-252">No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="84bf7-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![O que é o Azure AD Connect][201]
2. <span data-ttu-id="84bf7-254">Na lista de aplicativos hello, selecione **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![O que é o Azure AD Connect][205]
3. <span data-ttu-id="84bf7-256">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][202]
4. <span data-ttu-id="84bf7-258">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![O que é o Azure AD Connect][203]
5. <span data-ttu-id="84bf7-260">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="84bf7-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![O que é o Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="84bf7-262">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="84bf7-262">Testing Single Sign-On</span></span>
<span data-ttu-id="84bf7-263">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="84bf7-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="84bf7-264">Quando você clica em bloco Questetra BPM Suite Olá Olá painel de acesso, você deve obter um aplicativo do pacote de BPM Questetra tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="84bf7-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84bf7-265">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="84bf7-265">Additional Resources</span></span>
* [<span data-ttu-id="84bf7-266">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="84bf7-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84bf7-267">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="84bf7-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
