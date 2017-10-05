---
title: "Tutorial: integração do Azure Active Directory ao PerformanceCentre | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="31c67-103">Tutorial: Integração do Active Directory do Azure com o PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="31c67-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="31c67-104">Neste tutorial, você aprenderá a integrar o PerformanceCentre ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="31c67-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31c67-105">A integração do PerformanceCentre ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="31c67-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31c67-106">No AD do Azure, você pode controlar quem tem acesso ao PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="31c67-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="31c67-107">Você pode permitir que seus usuários façam logon automaticamente no PerformanceCentre (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31c67-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="31c67-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31c67-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31c67-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="31c67-110">Prerequisites</span></span>

<span data-ttu-id="31c67-111">Para configurar a integração do AD do Azure com o PerformanceCentre, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="31c67-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="31c67-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31c67-113">Uma assinatura do PerformanceCentre com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="31c67-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31c67-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="31c67-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31c67-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="31c67-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31c67-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="31c67-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31c67-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31c67-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31c67-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="31c67-118">Scenario description</span></span>
<span data-ttu-id="31c67-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="31c67-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31c67-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="31c67-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31c67-121">Adicionando o PerformanceCentre da galeria</span><span class="sxs-lookup"><span data-stu-id="31c67-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="31c67-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="31c67-123">Adicionando o PerformanceCentre da galeria</span><span class="sxs-lookup"><span data-stu-id="31c67-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="31c67-124">Para configurar a integração do PerformanceCentre ao AD do Azure, você precisará adicionar o PerformanceCentre da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="31c67-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31c67-125">**Para adicionar o PerformanceCentre da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="31c67-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31c67-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31c67-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="31c67-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31c67-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="31c67-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="31c67-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31c67-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="31c67-133">Na caixa de pesquisa, digite **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="31c67-133">In the search box, type **PerformanceCentre**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="31c67-135">No painel de resultados, selecione **PerformanceCentre** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="31c67-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31c67-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31c67-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PerformanceCentre, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="31c67-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31c67-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do PerformanceCentre é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31c67-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="31c67-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="31c67-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="31c67-141">No PerformanceCentre, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="31c67-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="31c67-142">Para configurar e testar o logon único do AD do Azure com o PerformanceCentre, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="31c67-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31c67-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="31c67-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31c67-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="31c67-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31c67-145">**[Criação de um usuário de teste do PerformanceCentre](#creating-a-performancecentre-test-user)** – para ter um equivalente de Brenda Fernandes no PerformanceCentre que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31c67-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="31c67-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="31c67-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31c67-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="31c67-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31c67-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="31c67-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31c67-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="31c67-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="31c67-150">**Para configurar o logon único do AD do Azure com o PerformanceCentre, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="31c67-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-151">No Portal do Azure, na página de integração de aplicativos do **PerformanceCentre**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="31c67-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="31c67-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="31c67-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="31c67-155">Na seção **URLs e Domínio do PerformanceCentre**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="31c67-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="31c67-157">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-157">a.</span></span> <span data-ttu-id="31c67-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="31c67-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="31c67-159">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-159">b.</span></span> <span data-ttu-id="31c67-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="31c67-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31c67-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="31c67-161">These values are not real.</span></span> <span data-ttu-id="31c67-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="31c67-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="31c67-163">Entre em contato com a [equipe de suporte ao cliente do PerformanceCentre](https://www.performancecentre.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="31c67-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="31c67-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="31c67-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="31c67-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="31c67-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31c67-168">Na seção **Configuração do PerformanceCentre**, clique em **Configurar o PerformanceCentre** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="31c67-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31c67-169">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="31c67-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="31c67-171">Faça logon no site da empresa **PerformanceCentre** como administrador.</span><span class="sxs-lookup"><span data-stu-id="31c67-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="31c67-172">Na guia à esquerda, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="31c67-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Logon Único do AD do Azure][10]

9. <span data-ttu-id="31c67-174">Na guia à esquerda, clique em **Diversos** e em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="31c67-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Logon Único do AD do Azure][11]

10. <span data-ttu-id="31c67-176">Para o **Protocolo**, escolha **SAML**.</span><span class="sxs-lookup"><span data-stu-id="31c67-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Logon Único do AD do Azure][12]

11. <span data-ttu-id="31c67-178">Abra o arquivo de metadados baixado no bloco de notas, copie o conteúdo e cole-o na caixa de texto **Metadados do Provedor de Identidade** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="31c67-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Logon Único do AD do Azure][13]

12. <span data-ttu-id="31c67-180">Verifique se os valores para **URL Base da Entidade** e **URL da ID da Entidade** estão corretos.</span><span class="sxs-lookup"><span data-stu-id="31c67-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Logon Único do AD do Azure][14]

> [!TIP]
> <span data-ttu-id="31c67-182">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="31c67-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="31c67-183">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="31c67-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="31c67-184">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31c67-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31c67-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="31c67-186">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="31c67-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="31c67-188">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="31c67-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-189">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31c67-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31c67-191">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="31c67-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31c67-193">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31c67-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31c67-195">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="31c67-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31c67-197">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-197">a.</span></span> <span data-ttu-id="31c67-198">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="31c67-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31c67-199">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-199">b.</span></span> <span data-ttu-id="31c67-200">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="31c67-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31c67-201">c.</span><span class="sxs-lookup"><span data-stu-id="31c67-201">c.</span></span> <span data-ttu-id="31c67-202">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="31c67-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31c67-203">d.</span><span class="sxs-lookup"><span data-stu-id="31c67-203">d.</span></span> <span data-ttu-id="31c67-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="31c67-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="31c67-205">Criar um usuário de teste do PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="31c67-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="31c67-206">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="31c67-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="31c67-207">**Para criar um usuário chamado Brenda Fernandes no PerformanceCentre, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="31c67-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-208">Faça logon no site da empresa PerformanceCentre como administrador.</span><span class="sxs-lookup"><span data-stu-id="31c67-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="31c67-209">No menu à esquerda, clique em **Inter-relacionado**, e clique em **Criar Participante**.</span><span class="sxs-lookup"><span data-stu-id="31c67-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Criar Usuário][400]

3. <span data-ttu-id="31c67-211">No diálogo **Inter-relacionado – Criar Participante** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="31c67-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Criar Usuário][401]
    
    <span data-ttu-id="31c67-213">a.</span><span class="sxs-lookup"><span data-stu-id="31c67-213">a.</span></span> <span data-ttu-id="31c67-214">Digite os atributos necessários para Brenda Fernandes nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="31c67-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="31c67-215">O atributo Nome de Usuário de Brenda no PerformanceCentre deve ser igual ao Nome de Usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="31c67-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="31c67-216">b.</span><span class="sxs-lookup"><span data-stu-id="31c67-216">b.</span></span> <span data-ttu-id="31c67-217">Selecione **Administrador Cliente** como **Escolher Função**.</span><span class="sxs-lookup"><span data-stu-id="31c67-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="31c67-218">c.</span><span class="sxs-lookup"><span data-stu-id="31c67-218">c.</span></span> <span data-ttu-id="31c67-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="31c67-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31c67-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31c67-221">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="31c67-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="31c67-223">**Para atribuir Brenda Fernandes ao PerformanceCentre, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="31c67-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="31c67-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="31c67-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="31c67-226">Na lista de aplicativos, escolha **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="31c67-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="31c67-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="31c67-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="31c67-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="31c67-230">Click **Add** button.</span></span> <span data-ttu-id="31c67-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31c67-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="31c67-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="31c67-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31c67-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31c67-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31c67-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31c67-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31c67-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="31c67-236">Testing single sign-on</span></span>

<span data-ttu-id="31c67-237">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="31c67-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="31c67-238">Quando clica no bloco PerformanceCentre no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo do PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="31c67-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31c67-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="31c67-239">Additional resources</span></span>

* [<span data-ttu-id="31c67-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="31c67-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31c67-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31c67-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

