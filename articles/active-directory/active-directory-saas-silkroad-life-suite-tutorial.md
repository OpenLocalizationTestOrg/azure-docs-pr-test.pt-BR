---
title: "Tutorial: Integração do Azure Active Directory com o SilkRoad Life Suite | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o SilkRoad Life Suite."
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
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="26091-103">Tutorial: integração do Active Directory do Azure com o SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="26091-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="26091-104">O objetivo desse tutorial é mostrar como integrar o SilkRoad Life Suite ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="26091-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="26091-105">A integração do SilkRoad Life Suite ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="26091-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="26091-106">Você pode controlar no AD do Azure quem tem acesso ao SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="26091-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="26091-107">Você pode habilitar seus usuários a fazer logon automaticamente no SilkRoad Life Suite usando SSO (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="26091-108">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26091-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26091-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26091-109">Prerequisites</span></span>
<span data-ttu-id="26091-110">Para configurar a integração do AD do Azure com o SilkRoad Life Suite, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="26091-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="26091-111">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="26091-111">An Azure AD subscription</span></span>
* <span data-ttu-id="26091-112">Uma assinatura do SilkRoad Life Suite habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="26091-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="26091-113">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="26091-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="26091-114">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="26091-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="26091-115">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="26091-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="26091-116">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26091-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="26091-117">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="26091-117">Scenario Description</span></span>
<span data-ttu-id="26091-118">O objetivo deste tutorial é permitir que você teste o SSO do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="26091-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="26091-119">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="26091-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26091-120">Adicionando o SilkRoad Life Suite por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="26091-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="26091-121">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="26091-122">Adicionar o SilkRoad Life Suite da galeria</span><span class="sxs-lookup"><span data-stu-id="26091-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="26091-123">Para configurar a integração do SilkRoad Life Suite com o AD do Azure, você precisa adicionar o SilkRoad Life Suite por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="26091-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26091-124">**Para adicionar o SilkRoad Life Suite por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26091-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26091-125">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26091-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="26091-127">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="26091-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="26091-128">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="26091-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]

4. <span data-ttu-id="26091-130">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="26091-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]

5. <span data-ttu-id="26091-132">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="26091-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]

6. <span data-ttu-id="26091-134">Na caixa de pesquisa, digite **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="26091-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplicativos][5]

7. <span data-ttu-id="26091-136">No painel de resultados, selecione **SilkRoad Life Suite** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26091-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Aplicativos][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26091-138">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="26091-139">O objetivo desta seção é mostrar como configurar e testar o SSO do Azure AD com o SilkRoad Life Suite, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="26091-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26091-140">Para que o SSO funcione, o Azure AD precisa saber qual usuário do SilkRoad Life Suite é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26091-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="26091-141">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="26091-142">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="26091-143">Para configurar e testar o logon único do AD do Azure com o SilkRoad Life Suite, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="26091-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26091-144">**[Configurar logon único do Azure AD](#configuring-azure-ad-single-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="26091-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26091-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26091-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26091-146">**[Criando um usuário de teste do SilkRoad Life Suite](#creating-a-silkroad-life-suite-test-user)** - para ter um equivalente de Brenda Fernandes no SilkRoad Life Suite que esteja vinculado à representação dela no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="26091-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="26091-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="26091-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26091-148">**[Teste do logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="26091-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26091-149">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="26091-150">O objetivo desta seção é habilitar o SSO do Azure AD no Portal Clássico do Azure e configurar o SSO em seu aplicativo SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="26091-151">**Para configurar o logon único do AD do Azure com o SilkRoad Life Suite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26091-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="26091-152">Faça logon no site da empresa SilkRoad como administrador.</span><span class="sxs-lookup"><span data-stu-id="26091-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="26091-153">Para obter acesso ao aplicativo de Autenticação do SilkRoad Life Suite para configurar a federação com o AD do Microsoft Azure, entre em contato com o Suporte da SilkRoad ou com seu representante de Serviços da SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="26091-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="26091-154">Vá para **Provedor de Serviços** e clique em **Detalhes de Federação**.</span><span class="sxs-lookup"><span data-stu-id="26091-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Logon Único do AD do Azure][10] 

3. <span data-ttu-id="26091-156">Clique em **Baixar Metadados de Federação**e salve o arquivo de metadados no computador.</span><span class="sxs-lookup"><span data-stu-id="26091-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Logon Único do AD do Azure][11] 

4. <span data-ttu-id="26091-158">No portal clássico do Azure, na página de integração de aplicativos do **SilkRoad Life Suite**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="26091-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o logon único][6] 

5. <span data-ttu-id="26091-160">Na página **Como você deseja que os usuários façam logon no SilkRoad Life Suite**, selecione **Logon Único do Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][7] 

6. <span data-ttu-id="26091-162">Na página de diálogo **Definir Configurações de Aplicativo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Logon Único do AD do Azure][8]   
 1. <span data-ttu-id="26091-164">Na caixa de texto **URL de Entrada**, digite a URL usada pelos usuários para fazer logon em seu site do SilkRoad Life Suite (por ex.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="26091-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="26091-165">Abra o arquivo de metadados do **Silkroad** baixado.</span><span class="sxs-lookup"><span data-stu-id="26091-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="26091-166">Localize a marca **AssertionConsumerService** e copie o atributo **Location**.</span><span class="sxs-lookup"><span data-stu-id="26091-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Logon Único do AD do Azure][21] 
 4. <span data-ttu-id="26091-168">Cole o valor na caixa de texto **URL de Resposta** .</span><span class="sxs-lookup"><span data-stu-id="26091-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="26091-169">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-169">Click **Next**.</span></span>

6. <span data-ttu-id="26091-170">Na página **Configurar logon único no SilkRoad Life Suite** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Logon Único do AD do Azure][9]  
 1. <span data-ttu-id="26091-172">Clique em Baixar certificado e salve o certificado localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="26091-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="26091-173">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-173">Click **Next**.</span></span>

7. <span data-ttu-id="26091-174">No aplicativo **SilkRoad**, clique em **Fontes de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="26091-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Logon Único do AD do Azure][12] 

8. <span data-ttu-id="26091-176">Clique em **Adicionar Fonte de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="26091-176">Click **Add Authentication Source**.</span></span> 
   
    ![Logon único do AD do Azure][13] 

9. <span data-ttu-id="26091-178">Na seção **Adicionar Fonte de Autenticação** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Logon Único do AD do Azure][14]  
 1. <span data-ttu-id="26091-180">Em **Opção 2 – Arquivo de Metadados**, clique em **Procurar** para carregar o arquivo de metadados baixado.</span><span class="sxs-lookup"><span data-stu-id="26091-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="26091-181">Clique em **Criar Provedor de Identidade usando Dados de Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="26091-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="26091-182">Na seção **Fontes de Autenticação**, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="26091-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Logon Único do AD do Azure][15] 

11. <span data-ttu-id="26091-184">No diálogo **Editar Fonte de Autenticação** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Logon Único do AD do Azure][16] 
 1. <span data-ttu-id="26091-186">Para **Habilitado**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="26091-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="26091-187">Na caixa de texto **Descrição do IdP** , digite uma descrição para a sua configuração (por exemplo: *SSO do Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="26091-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="26091-188">Na caixa de texto **Nome do IdP** , digite um nome específico para a sua configuração (por exemplo: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="26091-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="26091-189">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="26091-189">Click **Save**.</span></span>

12. <span data-ttu-id="26091-190">Desabilite todas as outras fontes de autenticação.</span><span class="sxs-lookup"><span data-stu-id="26091-190">Disable all other authentication sources.</span></span> 
    
     ![Logon Único do AD do Azure][17]

13. <span data-ttu-id="26091-192">No portal clássico do Azure, na página **Confirmação de logon único**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Logon Único do AD do Azure][18]

14. <span data-ttu-id="26091-194">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="26091-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Logon Único do AD do Azure][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26091-196">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-196">Create an Azure AD test user</span></span>
<span data-ttu-id="26091-197">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="26091-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="26091-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26091-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26091-200">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26091-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="26091-202">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="26091-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="26091-203">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="26091-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26091-205">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="26091-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="26091-207">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="26091-209">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="26091-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="26091-210">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="26091-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="26091-211">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-211">Click **Next**.</span></span>

6. <span data-ttu-id="26091-212">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="26091-214">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="26091-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="26091-215">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="26091-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="26091-216">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="26091-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="26091-217">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="26091-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="26091-218">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26091-218">Click **Next**.</span></span>

7. <span data-ttu-id="26091-219">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="26091-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="26091-221">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26091-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="26091-223">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="26091-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="26091-224">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="26091-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="26091-225">Criar um usuário de teste do SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="26091-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="26091-226">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="26091-227">Brenda deve ter uma ID de SSO (às vezes chamada um *AuthParam*) que corresponde ao **emailaddress** de Brenda no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26091-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="26091-228">**Para criar um usuário chamado Brenda Fernandes no SilkRoad Life Suite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26091-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="26091-229">Peça à sua equipe de suporte do SilkRoad Life Suite para criar um usuário que tenha o atributo **ID de SSO** com o mesmo valor que **emailaddress** de Brenda Fernandes no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26091-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="26091-230">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26091-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="26091-231">O objetivo desta seção é permitir que Brenda Fernandes use o SSO do Azure, concedendo a ela acesso ao SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="26091-233">**Para atribuir Brenda Fernandes ao SilkRoad Life Suite, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="26091-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="26091-234">No portal clássico do Azure, para abrir o modo de exibição de aplicativos, na exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="26091-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][201] 

2. <span data-ttu-id="26091-236">Na lista de aplicativos, selecione **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="26091-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Atribuir usuário][202] 

3. <span data-ttu-id="26091-238">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="26091-238">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][203] 

4. <span data-ttu-id="26091-240">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="26091-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="26091-241">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="26091-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="26091-243">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="26091-243">Test single sign-on</span></span>
<span data-ttu-id="26091-244">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="26091-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="26091-245">Quando clica no bloco SilkRoad Life Suite no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="26091-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26091-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="26091-246">Additional Resources</span></span>
* [<span data-ttu-id="26091-247">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="26091-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26091-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26091-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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





