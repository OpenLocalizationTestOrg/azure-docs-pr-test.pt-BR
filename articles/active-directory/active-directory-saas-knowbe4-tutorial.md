---
title: "Tutorial: integração do Azure Active Directory com o Treinamento de Reconhecimento de Segurança do KnowBe4 | Microsoft Docs"
description: "Aprenda como configurar o logon único entre o Azure Active Directory e o Treinamento de Reconhecimento de Segurança do KnowBe4."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 3b18737112a8aef101fab7fac1904f7c2e194d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="5ee9a-103">Tutorial: integração do Azure Active Directory com o Treinamento de Reconhecimento de Segurança do KnowBe4</span><span class="sxs-lookup"><span data-stu-id="5ee9a-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="5ee9a-104">Neste tutorial, você aprenderá a integrar o Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5ee9a-104">In this tutorial, you learn how to integrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ee9a-105">A integração do Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ee9a-106">No Azure AD, você pode controlar quem tem acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4</span><span class="sxs-lookup"><span data-stu-id="5ee9a-106">You can control in Azure AD who has access to KnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="5ee9a-107">Você pode permitir que seus usuários façam logon automaticamente no Treinamento de Reconhecimento de Segurança do KnowBe4 (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee9a-107">You can enable your users to automatically get signed-on to KnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ee9a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5ee9a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ee9a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ee9a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5ee9a-110">Prerequisites</span></span>

<span data-ttu-id="5ee9a-111">Para configurar a integração do Azure AD ao Treinamento de Reconhecimento de Segurança do KnowBe4, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-111">To configure Azure AD integration with KnowBe4 Security Awareness Training, you need the following items:</span></span>

- <span data-ttu-id="5ee9a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ee9a-113">Uma assinatura habilitada de logon único do Treinamento de Reconhecimento de Segurança do KnowBe4</span><span class="sxs-lookup"><span data-stu-id="5ee9a-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ee9a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ee9a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ee9a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ee9a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ee9a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ee9a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5ee9a-118">Scenario description</span></span>
<span data-ttu-id="5ee9a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ee9a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ee9a-121">Como adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="5ee9a-121">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
2. <span data-ttu-id="5ee9a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-the-gallery"></a><span data-ttu-id="5ee9a-123">Como adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="5ee9a-123">Adding KnowBe4 Security Awareness Training from the gallery</span></span>
<span data-ttu-id="5ee9a-124">Para configurar a integração do Treinamento de Reconhecimento de Segurança do KnowBe4 ao Azure AD, você precisará adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-124">To configure the integration of KnowBe4 Security Awareness Training into Azure AD, you need to add KnowBe4 Security Awareness Training from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ee9a-125">**Para adicionar o Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5ee9a-125">**To add KnowBe4 Security Awareness Training from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ee9a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ee9a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ee9a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5ee9a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5ee9a-133">Na caixa de pesquisa, digite **Treinamento de Reconhecimento de Segurança do KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-133">In the search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="5ee9a-135">No painel de resultados, selecione **Treinamento de Reconhecimento de Segurança do KnowBe4** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-135">In the results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ee9a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ee9a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4 com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ee9a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Treinamento de Reconhecimento de Segurança do KnowBe4 é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 Security Awareness Training is to a user in Azure AD.</span></span> <span data-ttu-id="5ee9a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Treinamento de Reconhecimento de Segurança do KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-140">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 Security Awareness Training needs to be established.</span></span>

<span data-ttu-id="5ee9a-141">No Treinamento de Reconhecimento de Segurança do KnowBe4, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-141">In KnowBe4 Security Awareness Training, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ee9a-142">Para configurar e testar o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-142">To configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ee9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ee9a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ee9a-145">**[Criando um usuário de teste do Treinamento de Reconhecimento de Segurança do KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)**: para ter um equivalente de Brenda Fernandes no Treinamento de Reconhecimento de Segurança do KnowBe4 vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - to have a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ee9a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ee9a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ee9a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ee9a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ee9a-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Treinamento de Reconhecimento de Segurança do KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="5ee9a-150">**Para configurar o logon único do Azure AD com o Treinamento de Reconhecimento de Segurança do KnowBe4, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5ee9a-150">**To configure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="5ee9a-151">No Portal do Azure, na página de integração de aplicativos do **Treinamento de Reconhecimento de Segurança do KnowBe4**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-151">In the Azure portal, on the **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5ee9a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="5ee9a-155">Na seção **URLs e Domínio do Treinamento de Reconhecimento de Segurança do KnowBe4**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-155">On the **KnowBe4 Security Awareness Training Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="5ee9a-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="5ee9a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ee9a-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-158">The value is not real.</span></span> <span data-ttu-id="5ee9a-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="5ee9a-160">Entre em contato com a [equipe de suporte do Cliente de Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) to get the value.</span></span> 
 

4. <span data-ttu-id="5ee9a-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="5ee9a-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5ee9a-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ee9a-165">Na seção **Configuração do Treinamento de Reconhecimento de Segurança do KnowBe4**, clique em **Configurar Treinamento de Reconhecimento de Segurança do KnowBe4** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-165">On the **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5ee9a-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5ee9a-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="5ee9a-168">Para configurar o logon único no lado do **Treinamento de Reconhecimento de Segurança do KnowBe4**, é necessário enviar o **Certificado (Bruto)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para a [equipe de suporte do Cliente do Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="5ee9a-168">To configure single sign-on on **KnowBe4 Security Awareness Training** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="5ee9a-169">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5ee9a-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ee9a-170">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ee9a-171">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ee9a-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ee9a-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ee9a-173">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5ee9a-175">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5ee9a-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ee9a-176">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ee9a-178">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ee9a-180">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ee9a-182">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5ee9a-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ee9a-184">a.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-184">a.</span></span> <span data-ttu-id="5ee9a-185">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ee9a-186">b.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-186">b.</span></span> <span data-ttu-id="5ee9a-187">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ee9a-188">c.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-188">c.</span></span> <span data-ttu-id="5ee9a-189">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ee9a-190">d.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-190">d.</span></span> <span data-ttu-id="5ee9a-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="5ee9a-192">Criação de um usuário de teste do Treinamento de Reconhecimento de Segurança do KnowBe4</span><span class="sxs-lookup"><span data-stu-id="5ee9a-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="5ee9a-193">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Treinamento de Reconhecimento de Segurança do KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-193">The objective of this section is to create a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="5ee9a-194">O Treinamento de Reconhecimento de Segurança do KnowBe4 dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5ee9a-195">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-195">There is no action item for you in this section.</span></span> <span data-ttu-id="5ee9a-196">Um novo usuário será criado durante uma tentativa de acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-196">A new user is created during an attempt to access KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="5ee9a-197">Se precisar criar um usuário manualmente, entre em contato com a equipe de suporte do [Treinamento de Reconhecimento de Segurança do KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="5ee9a-197">If you need to create a user manually, you need to contact the [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5ee9a-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5ee9a-199">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, ao conceder acesso ao Treinamento de Reconhecimento de Segurança do KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to KnowBe4 Security Awareness Training.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5ee9a-201">**Para atribuir Brenda Fernandes ao Treinamento de Reconhecimento de Segurança do KnowBe4 por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5ee9a-201">**To assign Britta Simon to KnowBe4 Security Awareness Training, perform the following steps:**</span></span>

1. <span data-ttu-id="5ee9a-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5ee9a-204">Na lista de aplicativos, selecione **Treinamento de Reconhecimento de Segurança do KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-204">In the applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="5ee9a-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5ee9a-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-208">Click **Add** button.</span></span> <span data-ttu-id="5ee9a-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5ee9a-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ee9a-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ee9a-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ee9a-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5ee9a-214">Testing single sign-on</span></span>

<span data-ttu-id="5ee9a-215">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="5ee9a-216">Ao clicar no bloco Treinamento de Reconhecimento de Segurança do KnowBe4 no Painel de Acesso, você deverá fazer logon automaticamente no seu aplicativo Treinamento de Reconhecimento de Segurança do KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="5ee9a-216">When you click the KnowBe4 Security Awareness Training tile in the Access Panel, you should get automatically signed-on to your KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ee9a-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5ee9a-217">Additional resources</span></span>

* [<span data-ttu-id="5ee9a-218">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5ee9a-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ee9a-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ee9a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

