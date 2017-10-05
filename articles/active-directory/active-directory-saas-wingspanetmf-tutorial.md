---
title: "Tutorial: integração do Azure Active Directory com o Wingspan eTMF | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 8c76fb64229abcad0cabb910e7c170979a79d839
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="51c2d-103">Tutorial: integração do Azure Active Directory com o Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="51c2d-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="51c2d-104">Neste tutorial, você aprenderá a integrar o Wingspan eTMF ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="51c2d-104">In this tutorial, you learn how to integrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51c2d-105">A integração do Wingspan eTMF ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="51c2d-105">Integrating Wingspan eTMF with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51c2d-106">Você pode controlar no Azure AD quem tem acesso ao Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="51c2d-106">You can control in Azure AD who has access to Wingspan eTMF</span></span>
- <span data-ttu-id="51c2d-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Wingspan eTMF (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="51c2d-107">You can enable your users to automatically get signed-on to Wingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51c2d-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="51c2d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51c2d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51c2d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="51c2d-110">Prerequisites</span></span>

<span data-ttu-id="51c2d-111">Para configurar a integração do Azure AD ao Wingspan eTMF, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="51c2d-111">To configure Azure AD integration with Wingspan eTMF, you need the following items:</span></span>

- <span data-ttu-id="51c2d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51c2d-113">Uma assinatura do Wingspan eTMF habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="51c2d-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51c2d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="51c2d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51c2d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="51c2d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51c2d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="51c2d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51c2d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51c2d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51c2d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="51c2d-118">Scenario description</span></span>
<span data-ttu-id="51c2d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="51c2d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51c2d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="51c2d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51c2d-121">Adicionar o Wingspan eTMF da galeria</span><span class="sxs-lookup"><span data-stu-id="51c2d-121">Adding Wingspan eTMF from the gallery</span></span>
2. <span data-ttu-id="51c2d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-the-gallery"></a><span data-ttu-id="51c2d-123">Adicionar o Wingspan eTMF da galeria</span><span class="sxs-lookup"><span data-stu-id="51c2d-123">Adding Wingspan eTMF from the gallery</span></span>
<span data-ttu-id="51c2d-124">Para configurar a integração do Wingspan eTMF ao Azure AD, você precisa adicionar o Wingspan eTMF por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="51c2d-124">To configure the integration of Wingspan eTMF into Azure AD, you need to add Wingspan eTMF from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51c2d-125">**Para adicionar o Wingspan eTMF por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="51c2d-125">**To add Wingspan eTMF from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51c2d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51c2d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51c2d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="51c2d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="51c2d-133">Na caixa de pesquisa, digite **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-133">In the search box, type **Wingspan eTMF**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="51c2d-135">No painel de resultados, selecione **Wingspan eTMF** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-135">In the results panel, select **Wingspan eTMF**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51c2d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51c2d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Wingspan eTMF, com base em um usuário de teste chamado "Brenda Fernandes."</span><span class="sxs-lookup"><span data-stu-id="51c2d-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51c2d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Wingspan eTMF é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51c2d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wingspan eTMF is to a user in Azure AD.</span></span> <span data-ttu-id="51c2d-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-140">In other words, a link relationship between an Azure AD user and the related user in Wingspan eTMF needs to be established.</span></span>

<span data-ttu-id="51c2d-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor de **Nome de Usuário** no Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="51c2d-142">Para configurar e testar o logon único do Azure AD com o Wingspan eTMF, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="51c2d-142">To configure and test Azure AD single sign-on with Wingspan eTMF, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51c2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="51c2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51c2d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="51c2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51c2d-145">**[Criar um usuário de teste do Wingspan eTMF](#creating-a-wingspan-etmf-test-user)** – para ter um equivalente de Brenda Fernandes no Wingspan eTMF que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51c2d-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - to have a counterpart of Britta Simon in Wingspan eTMF that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51c2d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="51c2d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51c2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="51c2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51c2d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="51c2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51c2d-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="51c2d-150">**Para configurar o logon único do Azure AD com o Wingspan eTMF, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="51c2d-150">**To configure Azure AD single sign-on with Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="51c2d-151">No Portal do Azure, na página de integração de aplicativos do **Wingspan eTMF**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-151">In the Azure portal, on the **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="51c2d-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="51c2d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="51c2d-155">Na seção **URLs e Domínio do Wingspan eTMF**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="51c2d-155">On the **Wingspan eTMF Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="51c2d-157">a.</span><span class="sxs-lookup"><span data-stu-id="51c2d-157">a.</span></span> <span data-ttu-id="51c2d-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="51c2d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="51c2d-159">b.</span><span class="sxs-lookup"><span data-stu-id="51c2d-159">b.</span></span> <span data-ttu-id="51c2d-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="51c2d-160">In the **Identifier** textbox, type a URL using the following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="51c2d-161">c.</span><span class="sxs-lookup"><span data-stu-id="51c2d-161">c.</span></span> <span data-ttu-id="51c2d-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="51c2d-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="51c2d-163">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="51c2d-163">These values are not the real.</span></span> <span data-ttu-id="51c2d-164">Atualize esses valores com a URL de logon, o Identificador e URL de resposta, incluindo o nome do cliente e o nome da instância reais.</span><span class="sxs-lookup"><span data-stu-id="51c2d-164">Update these values with the actual Sign-On URL, Identifier and Reply URL including the actual customer name and instance name.</span></span> <span data-ttu-id="51c2d-165">Contate a [equipe de suporte do Cliente Wingspan eTMF](http://www.wingspan.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="51c2d-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="51c2d-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="51c2d-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="51c2d-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="51c2d-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51c2d-170">Para configurar o logon único no lado do **Wingspan eTMF**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do Wingspan eTMF](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="51c2d-170">To configure single sign-on on **Wingspan eTMF** side, you need to send the downloaded **Metadata XML** to [Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="51c2d-171">Eles configuram isso para terem a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="51c2d-171">They set this up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="51c2d-172">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="51c2d-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51c2d-173">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="51c2d-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51c2d-174">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51c2d-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51c2d-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="51c2d-176">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="51c2d-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="51c2d-178">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="51c2d-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51c2d-179">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51c2d-181">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="51c2d-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51c2d-183">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51c2d-185">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="51c2d-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51c2d-187">a.</span><span class="sxs-lookup"><span data-stu-id="51c2d-187">a.</span></span> <span data-ttu-id="51c2d-188">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51c2d-189">b.</span><span class="sxs-lookup"><span data-stu-id="51c2d-189">b.</span></span> <span data-ttu-id="51c2d-190">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="51c2d-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51c2d-191">c.</span><span class="sxs-lookup"><span data-stu-id="51c2d-191">c.</span></span> <span data-ttu-id="51c2d-192">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="51c2d-193">d.</span><span class="sxs-lookup"><span data-stu-id="51c2d-193">d.</span></span> <span data-ttu-id="51c2d-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="51c2d-195">Criar um usuário de teste Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="51c2d-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="51c2d-196">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="51c2d-197">Trabalhe com o [suporte do eTMF Wingspan](http://www.wingspan.com/contact-us/) para adicionar os usuários no aplicativo eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="51c2d-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) to add the users in the Wingspan eTMF application.</span></span> <span data-ttu-id="51c2d-198">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="51c2d-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="51c2d-199">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="51c2d-200">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wingspan eTMF.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="51c2d-202">**Para atribuir Brenda Fernandes ao Wingspan eTMF, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="51c2d-202">**To assign Britta Simon to Wingspan eTMF, perform the following steps:**</span></span>

1. <span data-ttu-id="51c2d-203">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="51c2d-205">Na lista de aplicativos, escolha **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-205">In the applications list, select **Wingspan eTMF**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="51c2d-207">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="51c2d-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="51c2d-209">Click **Add** button.</span></span> <span data-ttu-id="51c2d-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="51c2d-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="51c2d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51c2d-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51c2d-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="51c2d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51c2d-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="51c2d-215">Testing single sign-on</span></span>

<span data-ttu-id="51c2d-216">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="51c2d-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="51c2d-217">Clique no bloco Wingspan eTMF no Painel de Acesso e você será redirecionado para a página de logon Organização.</span><span class="sxs-lookup"><span data-stu-id="51c2d-217">Click the Wingspan eTMF tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="51c2d-218">Após fazer logon com êxito, você entrará no aplicativo Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="51c2d-218">After successful login, you will be signed-on to your Wingspan eTMF application.</span></span> <span data-ttu-id="51c2d-219">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="51c2d-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51c2d-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="51c2d-220">Additional resources</span></span>

* [<span data-ttu-id="51c2d-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="51c2d-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51c2d-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51c2d-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

