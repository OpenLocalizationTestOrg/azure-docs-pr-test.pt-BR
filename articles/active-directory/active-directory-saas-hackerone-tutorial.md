---
title: "Tutorial: integração do Azure Active Directory ao HackerOne | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o HackerOne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="f1022-103">Tutorial: Integração do Azure Active Directory ao HackerOne</span><span class="sxs-lookup"><span data-stu-id="f1022-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="f1022-104">Neste tutorial, você aprenderá a integrar o HackerOne ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f1022-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1022-105">A integração do HackerOne ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f1022-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1022-106">No Azure AD, é possível controlar quem tem acesso ao HackerOne</span><span class="sxs-lookup"><span data-stu-id="f1022-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="f1022-107">Você pode permitir que seus usuários façam logon automaticamente no HackerOne (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="f1022-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1022-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1022-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f1022-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1022-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f1022-110">Prerequisites</span></span>

<span data-ttu-id="f1022-111">Para configurar a integração do Azure AD ao HackerOne, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f1022-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="f1022-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1022-113">Uma assinatura habilitada para logon único do HackerOne</span><span class="sxs-lookup"><span data-stu-id="f1022-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1022-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f1022-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1022-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f1022-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1022-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f1022-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1022-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f1022-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1022-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f1022-118">Scenario description</span></span>
<span data-ttu-id="f1022-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f1022-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1022-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f1022-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1022-121">Adicionando o HackerOne da galeria</span><span class="sxs-lookup"><span data-stu-id="f1022-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="f1022-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="f1022-123">Adicionando o HackerOne da galeria</span><span class="sxs-lookup"><span data-stu-id="f1022-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="f1022-124">Para configurar a integração do HackerOne ao Azure AD, você precisará adicionar o HackerOne da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f1022-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1022-125">**Para adicionar o HackerOne da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1022-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1022-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1022-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1022-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f1022-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1022-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1022-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f1022-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1022-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f1022-133">Na caixa de pesquisa, digite **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="f1022-133">In the search box, type **HackerOne**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="f1022-135">No painel de resultados, selecione **HackerOne** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1022-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1022-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f1022-138">Nesta seção, você configurará e testará o logon único do Azure AD com o HackerOne, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f1022-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f1022-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do HackerOne é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1022-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="f1022-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do HackerOne.</span><span class="sxs-lookup"><span data-stu-id="f1022-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="f1022-141">No HackerOne, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f1022-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1022-142">Para configurar e testar o logon único do Azure AD com o HackerOne, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f1022-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1022-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f1022-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1022-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1022-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1022-145">**[Criação de um usuário de teste do HackerOne](#creating-a-hackerone-test-user)**: para ter um equivalente de Brenda Fernandes no HackerOne que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1022-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1022-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1022-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1022-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f1022-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1022-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1022-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1022-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo HackerOne.</span><span class="sxs-lookup"><span data-stu-id="f1022-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="f1022-150">**Para configurar o logon único do Azure AD com o HackerOne, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1022-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="f1022-151">No portal do Azure, na página de integração de aplicativos do **HackerOne**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f1022-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f1022-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f1022-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="f1022-155">Sobre a **URL de Logon único do HackerOne e o Identificador**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1022-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="f1022-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1022-157">a.</span></span> <span data-ttu-id="f1022-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="f1022-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="f1022-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1022-159">b.</span></span> <span data-ttu-id="f1022-160">Na caixa de texto **Identificador**, digite uma URL como:  `https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="f1022-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f1022-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="f1022-161">This value is not real.</span></span> <span data-ttu-id="f1022-162">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="f1022-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f1022-163">Para obter esse valor, entre em contato com a [equipe de suporte do HackerOne](mailto:support@hackerone.com).</span><span class="sxs-lookup"><span data-stu-id="f1022-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="f1022-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f1022-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="f1022-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f1022-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f1022-168">Na seção **Configuração do HackerOne**, clique em **Configurar HackerOne** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="f1022-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f1022-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="f1022-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="f1022-171">Faça logon no seu locatário do HackerOne como administrador.</span><span class="sxs-lookup"><span data-stu-id="f1022-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="f1022-172">Na parte superior do menu, clique em “**Configurações**”.</span><span class="sxs-lookup"><span data-stu-id="f1022-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="f1022-174">Navegue até "**Autenticação**" e clique em "**Adicionar configurações do SAML**".</span><span class="sxs-lookup"><span data-stu-id="f1022-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="f1022-176">Na caixa de diálogo **Configurações de SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1022-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="f1022-178">a.</span><span class="sxs-lookup"><span data-stu-id="f1022-178">a.</span></span> <span data-ttu-id="f1022-179">Na caixa de texto **Domínio de Email** , digite um domínio registrado.</span><span class="sxs-lookup"><span data-stu-id="f1022-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="f1022-180">b.</span><span class="sxs-lookup"><span data-stu-id="f1022-180">b.</span></span> <span data-ttu-id="f1022-181">Na caixa de texto **URL de Logon Único**, cole o valor da **URL do Serviço de Logon Único do SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1022-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f1022-182">c.</span><span class="sxs-lookup"><span data-stu-id="f1022-182">c.</span></span> <span data-ttu-id="f1022-183">Abra seu **Arquivo de certificado** no bloco de notas baixado do Portal do Azure, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado X509**.</span><span class="sxs-lookup"><span data-stu-id="f1022-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="f1022-184">d.</span><span class="sxs-lookup"><span data-stu-id="f1022-184">d.</span></span> <span data-ttu-id="f1022-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f1022-185">Click **Save**.</span></span>

11. <span data-ttu-id="f1022-186">No diálogo Configurações de Autenticação, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1022-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="f1022-188">a.</span><span class="sxs-lookup"><span data-stu-id="f1022-188">a.</span></span> <span data-ttu-id="f1022-189">Clique em **Executar teste**.</span><span class="sxs-lookup"><span data-stu-id="f1022-189">Click **Run test**.</span></span>

    <span data-ttu-id="f1022-190">b.</span><span class="sxs-lookup"><span data-stu-id="f1022-190">b.</span></span> <span data-ttu-id="f1022-191">Se o valor do campo **Status** for igual a **Status do último teste: criado**, contate sua [equipe de suporte do HackerOne](mailto:support@hackerone.com) para solicitar uma análise da sua configuração.</span><span class="sxs-lookup"><span data-stu-id="f1022-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="f1022-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f1022-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1022-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f1022-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1022-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1022-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1022-195">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1022-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1022-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f1022-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1022-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1022-199">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1022-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1022-201">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f1022-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1022-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1022-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1022-205">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f1022-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1022-207">a.</span><span class="sxs-lookup"><span data-stu-id="f1022-207">a.</span></span> <span data-ttu-id="f1022-208">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f1022-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1022-209">b.</span><span class="sxs-lookup"><span data-stu-id="f1022-209">b.</span></span> <span data-ttu-id="f1022-210">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f1022-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1022-211">c.</span><span class="sxs-lookup"><span data-stu-id="f1022-211">c.</span></span> <span data-ttu-id="f1022-212">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f1022-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1022-213">d.</span><span class="sxs-lookup"><span data-stu-id="f1022-213">d.</span></span> <span data-ttu-id="f1022-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f1022-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="f1022-215">Criação de um usuário de teste do HackerOne</span><span class="sxs-lookup"><span data-stu-id="f1022-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="f1022-216">Em seguida, você criará um usuário chamado Brenda Fernandes no HackerOne.</span><span class="sxs-lookup"><span data-stu-id="f1022-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="f1022-217">O HackerOne dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="f1022-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f1022-218">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="f1022-218">There is no action item for you in this section.</span></span> <span data-ttu-id="f1022-219">Quando você acessar HackerOne, um novo usuário será criado caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="f1022-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f1022-220">Se precisar criar um usuário manualmente, você precisará entrar em contato com a equipe de suporte do Certify.</span><span class="sxs-lookup"><span data-stu-id="f1022-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1022-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1022-222">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao HackerOne.</span><span class="sxs-lookup"><span data-stu-id="f1022-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f1022-224">**Para atribuir Brenda Fernandes ao HackerOne, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f1022-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="f1022-225">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f1022-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f1022-227">Na lista de aplicativos, selecione **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="f1022-227">In the applications list, select **HackerOne**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="f1022-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f1022-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f1022-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f1022-231">Click **Add** button.</span></span> <span data-ttu-id="f1022-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1022-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f1022-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f1022-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1022-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1022-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1022-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f1022-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1022-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f1022-237">Testing single sign-on</span></span>

<span data-ttu-id="f1022-238">Por fim, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f1022-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="f1022-239">Quando você clica no bloco HackerOne no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo HackerOne.</span><span class="sxs-lookup"><span data-stu-id="f1022-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1022-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f1022-240">Additional resources</span></span>

* [<span data-ttu-id="f1022-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f1022-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1022-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f1022-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

