---
title: "Tutorial: Integração do Azure Active Directory com o SilkRoad Life Suite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e SilkRoad vida Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="12f44-103">Tutorial: integração do Active Directory do Azure com o SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="12f44-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="12f44-104">Olá objetivo deste tutorial é tooshow você como toointegrate SilkRoad vida Suite com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="12f44-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="12f44-105">Integrando SilkRoad vida Suite AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="12f44-106">Você pode controlar no AD do Azure que tenha acesso tooSilkRoad Suite de vida</span><span class="sxs-lookup"><span data-stu-id="12f44-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="12f44-107">Você pode habilitar seu usuários tooautomatically get conectado tooSilkRoad vida Suite-logon único (SSO) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="12f44-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="12f44-108">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12f44-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12f44-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="12f44-109">Prerequisites</span></span>
<span data-ttu-id="12f44-110">tooconfigure integração do AD do Azure com SilkRoad vida Suite, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="12f44-111">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="12f44-111">An Azure AD subscription</span></span>
* <span data-ttu-id="12f44-112">Uma assinatura do SilkRoad Life Suite habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="12f44-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="12f44-113">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="12f44-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="12f44-114">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="12f44-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="12f44-115">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="12f44-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="12f44-116">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12f44-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="12f44-117">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="12f44-117">Scenario Description</span></span>
<span data-ttu-id="12f44-118">Olá objetivo deste tutorial é tooenable você tootest SSO do AD do Azure em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="12f44-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="12f44-119">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="12f44-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12f44-120">Adicionando SilkRoad vida Suite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="12f44-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="12f44-121">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="12f44-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="12f44-122">Adicionar conjunto de vida de SilkRoad da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="12f44-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="12f44-123">integração de Olá tooconfigure do conjunto de vida SilkRoad no AD do Azure, você precisa tooadd SilkRoad vida Suite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="12f44-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12f44-124">**tooadd SilkRoad Suite de vida da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="12f44-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12f44-125">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12f44-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="12f44-127">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="12f44-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="12f44-128">Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="12f44-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="12f44-130">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="12f44-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="12f44-132">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.</span><span class="sxs-lookup"><span data-stu-id="12f44-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="12f44-134">Na caixa de pesquisa hello, digite **SilkRoad vida Suite**.</span><span class="sxs-lookup"><span data-stu-id="12f44-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="12f44-136">No painel de resultados de saudação, selecione **SilkRoad vida Suite**e, em seguida, clique em **concluir** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="12f44-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicativos][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="12f44-138">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="12f44-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="12f44-139">Olá o objetivo desta seção é tooshow como tooconfigure e teste do Azure AD SSO com o pacote de vida SilkRoad com base em um usuário de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="12f44-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12f44-140">Para SSO toowork, o AD do Azure precisa tooknow que usuário de contraparte Olá no usuário de tooan SilkRoad vida Suite no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12f44-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="12f44-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no conjunto de vida SilkRoad precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="12f44-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="12f44-142">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no conjunto de vida SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="12f44-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="12f44-143">tooconfigure e teste de logon único do AD do Azure com SilkRoad vida Suite, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12f44-144">**[Configurar o logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="12f44-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12f44-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12f44-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12f44-146">**[Criar um usuário de teste de conjunto de vida SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave um equivalente do Britta Simon no conjunto de vida de SilkRoad toohello vinculado do Azure AD representação dela.</span><span class="sxs-lookup"><span data-stu-id="12f44-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="12f44-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="12f44-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12f44-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="12f44-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="12f44-149">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="12f44-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="12f44-150">objetivo Olá desta seção é tooenable SSO do AD do Azure no portal clássico do Azure do hello e tooconfigure SSO em seu aplicativo SilkRoad vida Suite.</span><span class="sxs-lookup"><span data-stu-id="12f44-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="12f44-151">**tooconfigure logon único do AD do Azure com o pacote de vida SilkRoad, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="12f44-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="12f44-152">Site de empresa de SilkRoad tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="12f44-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="12f44-153">acesso de tooobtain toohello aplicativo SilkRoad vida Suite autenticação para configurar a federação com o Microsoft Azure AD, entre em contato com suporte SilkRoad ou seu representante de serviços SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="12f44-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="12f44-154">Vá muito**provedor**e, em seguida, clique em **federação detalhes**.</span><span class="sxs-lookup"><span data-stu-id="12f44-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Logon Único do AD do Azure][10] 

3. <span data-ttu-id="12f44-156">Clique em **baixar metadados de Federação**e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="12f44-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Logon Único do AD do Azure][11] 

4. <span data-ttu-id="12f44-158">Em Olá portal clássico do Azure, em Olá **SilkRoad vida Suite** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="12f44-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 

5. <span data-ttu-id="12f44-160">Em Olá **como você gostaria usuários toosign em tooSilkRoad vida Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="12f44-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][7] 

6. <span data-ttu-id="12f44-162">Em Olá **definir configurações de aplicativo** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Logon Único do AD do Azure][8]   
 1. <span data-ttu-id="12f44-164">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada pelo seu site de conjunto de vida SilkRoad tooyour toosign em usuários (por exemplo: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="12f44-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="12f44-165">Abra Olá baixado **Silkroad** arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="12f44-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="12f44-166">Localizar Olá **AssertionConsumerService** marca e, em seguida, Olá cópia **local** atributo.</span><span class="sxs-lookup"><span data-stu-id="12f44-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Logon Único do AD do Azure][21] 
 4. <span data-ttu-id="12f44-168">Cole o valor de Olá Olá **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="12f44-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="12f44-169">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-169">Click **Next**.</span></span>

6. <span data-ttu-id="12f44-170">Em Olá **configurar logon único no conjunto de vida SilkRoad** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Logon Único do AD do Azure][9]  
 1. <span data-ttu-id="12f44-172">Clique em Download de certificado e, em seguida, salve o arquivo de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="12f44-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="12f44-173">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-173">Click **Next**.</span></span>

7. <span data-ttu-id="12f44-174">No aplicativo **SilkRoad**, clique em **Fontes de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="12f44-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Logon Único do AD do Azure][12] 

8. <span data-ttu-id="12f44-176">Clique em **Adicionar Fonte de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="12f44-176">Click **Add Authentication Source**.</span></span> 
   
    ![Logon Único do AD do Azure][13] 

9. <span data-ttu-id="12f44-178">Em Olá **adicionar fonte de autenticação** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Logon Único do AD do Azure][14]  
 1. <span data-ttu-id="12f44-180">Em **opção 2 - arquivo de metadados**, clique em **procurar** Olá tooupload baixou o arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="12f44-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="12f44-181">Clique em **Criar Provedor de Identidade usando Dados de Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="12f44-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="12f44-182">Em Olá **fontes de autenticação** seção, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Logon Único do AD do Azure][15] 

11. <span data-ttu-id="12f44-184">Em Olá **Editar autenticação fonte** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Logon Único do AD do Azure][16] 
 1. <span data-ttu-id="12f44-186">Para **Habilitado**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="12f44-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="12f44-187">Em Olá **IdP descrição** caixa de texto, digite uma descrição para a sua configuração (por exemplo: *SSO do AD do Azure*).</span><span class="sxs-lookup"><span data-stu-id="12f44-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="12f44-188">Em Olá **nome IdP** caixa de texto, digite um nome de configuração específico tooyour (por exemplo: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="12f44-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="12f44-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-189">Click **Save**.</span></span>

12. <span data-ttu-id="12f44-190">Desabilite todas as outras fontes de autenticação.</span><span class="sxs-lookup"><span data-stu-id="12f44-190">Disable all other authentication sources.</span></span> 
    
     ![Logon Único do AD do Azure][17]

13. <span data-ttu-id="12f44-192">Em Olá portal clássico do Azure, em Olá **único logon confirmação** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="12f44-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Logon Único do AD do Azure][18]

14. <span data-ttu-id="12f44-194">Em Olá **único logon confirmação** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="12f44-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Logon Único do AD do Azure][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="12f44-196">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="12f44-196">Create an Azure AD test user</span></span>
<span data-ttu-id="12f44-197">Olá objetivo desta seção é toocreate um usuário de teste no hello portal clássico do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12f44-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="12f44-199">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="12f44-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12f44-200">Em Olá **portal clássico do Azure**, em Olá painel de navegação esquerdo, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12f44-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="12f44-202">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="12f44-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="12f44-203">lista de saudação toodisplay de usuários, no menu de saudação na parte superior do hello, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="12f44-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12f44-205">Olá tooopen **adicionar usuário** caixa de diálogo, na barra de ferramentas Olá inferior hello, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="12f44-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="12f44-207">Em Olá **Conte-nos sobre este usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="12f44-209">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="12f44-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="12f44-210">Em nome de usuário de saudação **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12f44-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="12f44-211">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-211">Click **Next**.</span></span>

6. <span data-ttu-id="12f44-212">Em Olá **perfil de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="12f44-214">Em Olá **nome** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="12f44-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="12f44-215">Em Olá **Sobrenome** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="12f44-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="12f44-216">Em Olá **nome de exibição** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="12f44-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="12f44-217">Em Olá **função** lista, selecione **usuário**.</span><span class="sxs-lookup"><span data-stu-id="12f44-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="12f44-218">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-218">Click **Next**.</span></span>

7. <span data-ttu-id="12f44-219">Em Olá **obter senha temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="12f44-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="12f44-221">Em Olá **obter senha temporária** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="12f44-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="12f44-223">Anote o valor Olá Olá **nova senha**.</span><span class="sxs-lookup"><span data-stu-id="12f44-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="12f44-224">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="12f44-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="12f44-225">Criar um usuário de teste do SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="12f44-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="12f44-226">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon SilkRoad vida conjunto.</span><span class="sxs-lookup"><span data-stu-id="12f44-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="12f44-227">Britta deve ter uma ID de SSO (às vezes chamado tooas um *AuthParam*) que faz a correspondência de Britta **emailaddress** no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12f44-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="12f44-228">**toocreate um usuário chamado Britta Simon no conjunto de vida SilkRoad, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="12f44-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="12f44-229">Peça para um usuário que tem como seu toocreate de equipe de suporte SilkRoad vida Suite **identificação do SSO** Olá atributo mesmo valor Olá **emailaddress** de Britta Simon no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="12f44-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="12f44-230">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="12f44-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="12f44-231">Olá objetivo desta seção é tooenable Britta Simon toouse Azure SSO concedendo tooSilkRoad seu acesso vida Suite.</span><span class="sxs-lookup"><span data-stu-id="12f44-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="12f44-233">**tooassign Britta Simon tooSilkRoad vida Suite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="12f44-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="12f44-234">No hello Azure portal clássico, exibição de aplicativos tooopen hello, no modo de exibição de diretório hello, clique em **aplicativos** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="12f44-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribuir usuário][201] 

2. <span data-ttu-id="12f44-236">Na lista de aplicativos hello, selecione **SilkRoad vida Suite**.</span><span class="sxs-lookup"><span data-stu-id="12f44-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Atribuir usuário][202] 

3. <span data-ttu-id="12f44-238">No menu de saudação na parte superior de saudação, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="12f44-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 

4. <span data-ttu-id="12f44-240">Na lista de usuários hello, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="12f44-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="12f44-241">Na barra de ferramentas de saudação na parte inferior do hello, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="12f44-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="12f44-243">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="12f44-243">Test single sign-on</span></span>
<span data-ttu-id="12f44-244">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="12f44-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="12f44-245">Quando você clica em bloco SilkRoad vida Suite Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de SilkRoad vida Suite.</span><span class="sxs-lookup"><span data-stu-id="12f44-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12f44-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="12f44-246">Additional Resources</span></span>
* [<span data-ttu-id="12f44-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="12f44-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12f44-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12f44-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





