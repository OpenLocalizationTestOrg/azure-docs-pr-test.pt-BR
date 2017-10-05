---
title: "Tutorial: Integração do Azure Active Directory ao BambooHR | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="7897d-103">Tutorial: Integração do Azure Active Directory ao BambooHR</span><span class="sxs-lookup"><span data-stu-id="7897d-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="7897d-104">Neste tutorial, você aprende a integrar o BambooHR ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7897d-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7897d-105">A integração do BambooHR ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7897d-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7897d-106">No Azure AD, é possível controlar quem tem acesso ao BambooHR</span><span class="sxs-lookup"><span data-stu-id="7897d-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="7897d-107">É possível permitir que os usuários se conectem automaticamente ao BambooHR (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7897d-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7897d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7897d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7897d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7897d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7897d-110">Prerequisites</span></span>

<span data-ttu-id="7897d-111">Para configurar a integração do Azure AD ao BambooHR, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7897d-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="7897d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7897d-113">Uma assinatura habilitada para logon único do BambooHR</span><span class="sxs-lookup"><span data-stu-id="7897d-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7897d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7897d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7897d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7897d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7897d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7897d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7897d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7897d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7897d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7897d-118">Scenario description</span></span>
<span data-ttu-id="7897d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7897d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7897d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7897d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7897d-121">Adicionando o BambooHR por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7897d-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="7897d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="7897d-123">Adicionando o BambooHR por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7897d-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="7897d-124">Para configurar a integração do BambooHR ao Azure AD, você precisa adicionar o BambooHR à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="7897d-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7897d-125">**Para adicionar o BambooHR por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7897d-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7897d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7897d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7897d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7897d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7897d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7897d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7897d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7897d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7897d-133">Na caixa de pesquisa, digite **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="7897d-133">In the search box, type **BambooHR**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="7897d-135">No painel de resultados, selecione **BambooHR** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7897d-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7897d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7897d-138">Nesta seção, você configura e testa o logon único do Azure AD com o BambooHR, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7897d-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7897d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BambooHR é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7897d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="7897d-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do BambooHR.</span><span class="sxs-lookup"><span data-stu-id="7897d-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="7897d-141">No BambooHR, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7897d-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7897d-142">Para configurar e testar o logon único do Azure AD com o BambooHR, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7897d-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7897d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7897d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7897d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7897d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7897d-145">**[Criando um usuário de teste do BambooHR](#creating-a-bamboohr-test-user)** – para ter um equivalente de Brenda Fernandes no BambooHR que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7897d-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7897d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7897d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7897d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7897d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7897d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7897d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7897d-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo BambooHR.</span><span class="sxs-lookup"><span data-stu-id="7897d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="7897d-150">**Para configurar o logon único do Azure AD com o BambooHR, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7897d-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="7897d-151">No portal do Azure, na página de integração do aplicativo do **BambooHR**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7897d-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7897d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7897d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="7897d-155">Na seção **Domínio e URLs do BambooHR**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7897d-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="7897d-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="7897d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="7897d-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="7897d-158">This value is not real.</span></span> <span data-ttu-id="7897d-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="7897d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7897d-160">Contate a [equipe de suporte ao Cliente do BambooHR](https://www.bamboohr.com/contact.php) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="7897d-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="7897d-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7897d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="7897d-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7897d-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7897d-165">Na seção **Configuração do BambooHR**, clique em **Configurar o BambooHR** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7897d-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7897d-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7897d-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="7897d-168">Em outra janela do navegador da Web, faça logon em seu site de empresa BambooHR como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7897d-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="7897d-169">Na página inicial, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7897d-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="7897d-170">![Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="7897d-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="7897d-171">a.</span><span class="sxs-lookup"><span data-stu-id="7897d-171">a.</span></span> <span data-ttu-id="7897d-172">Clique em **Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7897d-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="7897d-173">b.</span><span class="sxs-lookup"><span data-stu-id="7897d-173">b.</span></span> <span data-ttu-id="7897d-174">No menu de aplicativos à esquerda, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7897d-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="7897d-175">c.</span><span class="sxs-lookup"><span data-stu-id="7897d-175">c.</span></span> <span data-ttu-id="7897d-176">Clique em **Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="7897d-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="7897d-177">Na seção **Logon Único do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7897d-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="7897d-178">![Logon Único do SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="7897d-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="7897d-179">a.</span><span class="sxs-lookup"><span data-stu-id="7897d-179">a.</span></span> <span data-ttu-id="7897d-180">Cole o valor da **URL do Serviço de Logon Único SAML** na caixa de texto **URL de Logon SSO**.</span><span class="sxs-lookup"><span data-stu-id="7897d-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="7897d-181">b.</span><span class="sxs-lookup"><span data-stu-id="7897d-181">b.</span></span> <span data-ttu-id="7897d-182">Abra o certificado codificado em Base 64 baixado no portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado X.509**</span><span class="sxs-lookup"><span data-stu-id="7897d-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="7897d-183">c.</span><span class="sxs-lookup"><span data-stu-id="7897d-183">c.</span></span> <span data-ttu-id="7897d-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7897d-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7897d-185">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7897d-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7897d-186">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7897d-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7897d-187">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7897d-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7897d-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="7897d-189">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7897d-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7897d-191">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7897d-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7897d-192">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7897d-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7897d-194">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7897d-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7897d-196">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7897d-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7897d-198">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7897d-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7897d-200">a.</span><span class="sxs-lookup"><span data-stu-id="7897d-200">a.</span></span> <span data-ttu-id="7897d-201">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7897d-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7897d-202">b.</span><span class="sxs-lookup"><span data-stu-id="7897d-202">b.</span></span> <span data-ttu-id="7897d-203">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7897d-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7897d-204">c.</span><span class="sxs-lookup"><span data-stu-id="7897d-204">c.</span></span> <span data-ttu-id="7897d-205">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7897d-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7897d-206">d.</span><span class="sxs-lookup"><span data-stu-id="7897d-206">d.</span></span> <span data-ttu-id="7897d-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7897d-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="7897d-208">Criando um usuário de teste do BambooHR</span><span class="sxs-lookup"><span data-stu-id="7897d-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="7897d-209">Para permitir que os usuários do Azure AD façam logon no BambooHR, eles devem ser provisionados no BambooHR.</span><span class="sxs-lookup"><span data-stu-id="7897d-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="7897d-210">No caso do BambooHR, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7897d-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="7897d-211">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7897d-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7897d-212">Faça logon em seu site de empresa do **BambooHR** como administrador.</span><span class="sxs-lookup"><span data-stu-id="7897d-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="7897d-213">Na barra de ferramentas na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="7897d-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="7897d-214">![Configuração](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="7897d-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="7897d-215">Clique em **Visão Geral**.</span><span class="sxs-lookup"><span data-stu-id="7897d-215">Click **Overview**.</span></span>

4. <span data-ttu-id="7897d-216">No painel de navegação à esquerda, vá para **Segurança \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="7897d-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="7897d-217">Digite o nome de usuário, a senha e o endereço de email de uma conta válida do AAD que deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7897d-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="7897d-218">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7897d-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="7897d-219">É possível usar qualquer outra ferramenta de criação da conta de usuário do BambooHR ou as APIs fornecidas pelo BambooHR para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="7897d-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7897d-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7897d-221">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao BambooHR.</span><span class="sxs-lookup"><span data-stu-id="7897d-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7897d-223">**Para atribuir Brenda Fernandes ao BambooHR, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7897d-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="7897d-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7897d-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7897d-226">Na lista de aplicativos, selecione **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="7897d-226">In the applications list, select **BambooHR**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="7897d-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7897d-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7897d-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7897d-230">Click **Add** button.</span></span> <span data-ttu-id="7897d-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7897d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7897d-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7897d-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7897d-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7897d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7897d-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7897d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7897d-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7897d-236">Testing single sign-on</span></span>

<span data-ttu-id="7897d-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7897d-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7897d-238">Quando você clicar no bloco BambooHR no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo BambooHR.</span><span class="sxs-lookup"><span data-stu-id="7897d-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="7897d-239">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7897d-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7897d-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7897d-240">Additional resources</span></span>

* [<span data-ttu-id="7897d-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7897d-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7897d-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7897d-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

