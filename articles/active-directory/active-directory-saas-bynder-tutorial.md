---
title: "Tutorial: Integração do Azure Active Directory ao Bynder | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="4c984-103">Tutorial: Integração do Azure Active Directory ao Bynder</span><span class="sxs-lookup"><span data-stu-id="4c984-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="4c984-104">O objetivo desse tutorial é mostrar como integrar o Bynder com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4c984-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c984-105">A integração do Bynder ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4c984-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4c984-106">Você pode controlar no Azure AD quem terá acesso ao Bynder</span><span class="sxs-lookup"><span data-stu-id="4c984-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="4c984-107">Você pode permitir que seus usuários faça logon automaticamente no Bynder usando SSO (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="4c984-108">Gerenciar suas contas em um único local: o Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4c984-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4c984-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c984-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c984-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c984-110">Prerequisites</span></span>
<span data-ttu-id="4c984-111">Para configurar a integração do Azure AD ao Bynder, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4c984-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="4c984-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c984-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4c984-113">Uma assinatura habilitada para SSO (logon único) do Bynder</span><span class="sxs-lookup"><span data-stu-id="4c984-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="4c984-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4c984-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="4c984-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4c984-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4c984-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4c984-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4c984-117">Se não tiver um ambiente de avaliação do Azure AD, você pode obter uma [versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c984-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c984-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4c984-118">Scenario description</span></span>
<span data-ttu-id="4c984-119">O objetivo deste tutorial é permitir que você teste o SSO do Microsoft Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4c984-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="4c984-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4c984-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c984-121">Adicionando o Bynder da galeria</span><span class="sxs-lookup"><span data-stu-id="4c984-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="4c984-122">Configuração e testes do SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="4c984-123">Adicionar o Bynder da galeria</span><span class="sxs-lookup"><span data-stu-id="4c984-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="4c984-124">Para configurar a integração do Bynder ao Azure AD, você precisará adicionar o Bynder da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4c984-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c984-125">**Para adicionar o Bynder da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c984-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c984-126">No **portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c984-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="4c984-128">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="4c984-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4c984-129">Para abrir a visualização dos aplicativos, na exibição do diretório, clique em **Aplicativos** no menu principal.</span><span class="sxs-lookup"><span data-stu-id="4c984-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplicativos][2]
4. <span data-ttu-id="4c984-131">Clique em **Adicionar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="4c984-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicativos][3]
5. <span data-ttu-id="4c984-133">Na caixa de diálogo **O que você deseja fazer**, clique em **Adicionar um aplicativo da galeria**.</span><span class="sxs-lookup"><span data-stu-id="4c984-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicativos][4]
6. <span data-ttu-id="4c984-135">Na caixa de pesquisa, digite **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="4c984-135">In the search box, type **Bynder**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="4c984-137">No painel de resultados, selecione **Bynder** e clique em **Concluir** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4c984-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Seleção do aplicativo na galeria](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="4c984-139">Configurar e testar o SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="4c984-140">O objetivo desta seção é mostrar como configurar e testar o Logon Único (SSO) do Microsoft Azure AD com o Bynder, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4c984-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c984-141">Para que o SSO funcione, o Azure AD precisa saber qual usuário do Bynder é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c984-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="4c984-142">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="4c984-143">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="4c984-144">Para configurar e testar o SSO do Microsoft Azure AD com o Bynder, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4c984-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c984-145">**[Configuração do logon único do Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)** – para habilitar os usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4c984-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c984-146">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o Logon Único do Microsoft Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c984-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="4c984-147">**[Criar um usuário de teste do Bynder](#creating-a-bynder-test-user)** - para ter um equivalente de Brenda Fernandes no Bynder que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c984-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4c984-148">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para permitir que Brenda Fernandes use o Logon Único do Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c984-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="4c984-149">**[Teste do logon único](#testing-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4c984-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="4c984-150">Configuração do SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="4c984-151">Nesta seção, você habilita o SSO do Microsoft Azure AD no portal clássico e configura o SSO no aplicativo Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="4c984-152">**Para configurar o SSO do Microsoft Azure AD com o Bynder, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c984-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="4c984-153">No portal clássico do Azure, na página de integração do aplicativo **Bynder**, clique em **Configurar logon único** para abrir a caixa de diálogo **Configurar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="4c984-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar Logon Único][6] 
2. <span data-ttu-id="4c984-155">Na página **Como você deseja que os usuários façam logon no Bynder**, selecione **Logon Único do Microsoft Azure AD** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="4c984-157">Na página de diálogo **Definir Configurações de Aplicativo**, se quiser configurar o aplicativo no **modo iniciado pelo IDP**, execute as seguintes etapas e clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="4c984-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="4c984-159">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="4c984-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="4c984-160">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-160">Click **Next**.</span></span>
4. <span data-ttu-id="4c984-161">Se quiser configurar o aplicativo no **modo iniciado pelo SP**, na página de diálogo **Definir Configurações do Aplicativo**, clique em **"Mostrar configurações avançadas (opcional)"**, insira a **URL de Logon** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="4c984-163">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="4c984-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="4c984-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="4c984-165">O valor para a URL de Entrada neste tutorial é apenas um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="4c984-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="4c984-166">Para obter o valor real de seu ambiente, entre em contato com a Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="4c984-167">Na página **Configurar logon único no Bynder**, execute as seguintes etapas e clique em **Avançar**:</span><span class="sxs-lookup"><span data-stu-id="4c984-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="4c984-169">Clique em **Baixar metadados**e salve o arquivo no computador.</span><span class="sxs-lookup"><span data-stu-id="4c984-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="4c984-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-170">Click **Next**.</span></span>
6. <span data-ttu-id="4c984-171">Para que o SSO seja configurado para seu aplicativo, contate a equipe de suporte do Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="4c984-172">Anexe o arquivo de metadados baixado e compartilhe-o com a equipe do Bynder para configurar o SSO no lado dela.</span><span class="sxs-lookup"><span data-stu-id="4c984-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="4c984-173">No portal clássico, selecione a confirmação da configuração de logon único e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Logon Único do AD do Azure][10]
8. <span data-ttu-id="4c984-175">Na página **Confirmação de logon único**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4c984-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Logon Único do AD do Azure][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4c984-177">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-177">Create an Azure AD test user</span></span>
<span data-ttu-id="4c984-178">O objetivo desta seção é criar um usuário de teste no Portal Clássico do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4c984-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][20]

<span data-ttu-id="4c984-180">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c984-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c984-181">No **Portal clássico do Azure**, no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c984-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="4c984-183">Na lista **Diretório** , selecione o diretório para o qual você deseja habilitar a integração de diretórios.</span><span class="sxs-lookup"><span data-stu-id="4c984-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4c984-184">Para exibir a lista de usuários, no menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4c984-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="4c984-186">Para abrir a caixa de diálogo **Adicionar Usuário**, na barra de ferramentas na parte inferior, clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4c984-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="4c984-188">Na página do diálogo **Conte-nos sobre este usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c984-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="4c984-190">Em Tipo de Usuário, selecione Novo usuário na organização.</span><span class="sxs-lookup"><span data-stu-id="4c984-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="4c984-191">Na **caixa de texto** Nome do Usuário, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c984-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="4c984-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-192">Click **Next**.</span></span>
6. <span data-ttu-id="4c984-193">Na página do diálogo **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c984-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="4c984-195">Na caixa de texto **Nome**, digite **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="4c984-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="4c984-196">Na caixa de texto **Sobrenome**, digite **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c984-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="4c984-197">Na caixa de texto **Nome de Exibição**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c984-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="4c984-198">Na lista **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4c984-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="4c984-199">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-199">Click **Next**.</span></span>
7. <span data-ttu-id="4c984-200">Na página de diálogo **Obter senha temporária**, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="4c984-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="4c984-202">Na página de caixa de diálogo **Obter senha temporária** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4c984-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="4c984-204">Anote o valor da **Nova Senha**.</span><span class="sxs-lookup"><span data-stu-id="4c984-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="4c984-205">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="4c984-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="4c984-206">Criar um usuário de teste do Bynder</span><span class="sxs-lookup"><span data-stu-id="4c984-206">Create a Bynder test user</span></span>
<span data-ttu-id="4c984-207">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="4c984-208">O Bynder dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="4c984-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="4c984-209">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="4c984-209">There is no action item for you in this section.</span></span> <span data-ttu-id="4c984-210">Um novo usuário será criado durante uma tentativa de acessar o Bynder, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="4c984-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4c984-211">Se precisar criar um usuário manualmente, entre em contato com a equipe de suporte do Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4c984-212">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c984-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="4c984-213">O objetivo desta seção é permitir que Brenda Fernandes use o SSO do Azure, concedendo a ela acesso ao Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Atribuir usuário][200]

<span data-ttu-id="4c984-215">**Para atribuir Brenda Fernandes ao Bynder, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4c984-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="4c984-216">No portal clássico, para abrir o modo de exibição de aplicativos, no modo de exibição de diretório, clique em **Aplicativos** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="4c984-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Atribuir usuário][201]
2. <span data-ttu-id="4c984-218">Na lista de aplicativos, escolha **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="4c984-218">In the applications list, select **Bynder**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="4c984-220">No menu na parte superior, clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4c984-220">In the menu on the top, click **Users**.</span></span>
   
    ![Atribuir usuário][203]
4. <span data-ttu-id="4c984-222">Na lista de usuários, selecione **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4c984-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="4c984-223">Na barra de ferramentas na parte inferior, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="4c984-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Atribuir usuário][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="4c984-225">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="4c984-225">Test single sign-on</span></span>
<span data-ttu-id="4c984-226">O objetivo desta seção é testar sua configuração de SSO do Microsoft Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4c984-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4c984-227">Quando você clicar no bloco do Bynder no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo do Bynder.</span><span class="sxs-lookup"><span data-stu-id="4c984-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c984-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4c984-228">Additional resources</span></span>
* [<span data-ttu-id="4c984-229">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4c984-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c984-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c984-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
