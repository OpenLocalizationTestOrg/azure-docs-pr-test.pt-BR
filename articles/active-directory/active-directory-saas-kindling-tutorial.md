---
title: "Tutorial: integração do Azure Active Directory com o Kindling | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 131c2c3f46c60193d512b1779e917c8322732fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="41405-103">Tutorial: integração do Active Directory do Azure com o Kindling</span><span class="sxs-lookup"><span data-stu-id="41405-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="41405-104">Neste tutorial, você aprende a integrar o Kindling ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="41405-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41405-105">A integração do Kindling ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="41405-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41405-106">Você pode controlar no AD do Azure quem tem acesso ao Kindling</span><span class="sxs-lookup"><span data-stu-id="41405-106">You can control in Azure AD who has access to Kindling</span></span>
- <span data-ttu-id="41405-107">Você pode permitir que seus usuários façam logon automaticamente no Kindling (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41405-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41405-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="41405-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="41405-110">[o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41405-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41405-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41405-111">Prerequisites</span></span>

<span data-ttu-id="41405-112">Para configurar a integração do AD do Azure ao Kindling, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="41405-112">To configure Azure AD integration with Kindling, you need the following items:</span></span>

- <span data-ttu-id="41405-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-113">An Azure AD subscription</span></span>
- <span data-ttu-id="41405-114">Uma assinatura habilitada para logon único do Kindling</span><span class="sxs-lookup"><span data-stu-id="41405-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41405-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="41405-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41405-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="41405-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41405-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="41405-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41405-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41405-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41405-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="41405-119">Scenario description</span></span>
<span data-ttu-id="41405-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="41405-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41405-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="41405-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41405-122">Adicionando o Kindling da galeria</span><span class="sxs-lookup"><span data-stu-id="41405-122">Adding Kindling from the gallery</span></span>
2. <span data-ttu-id="41405-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="41405-124">Adicionando o Kindling da galeria</span><span class="sxs-lookup"><span data-stu-id="41405-124">Adding Kindling from the gallery</span></span>
<span data-ttu-id="41405-125">Para configurar a integração do Kindling ao AD do Azure, você precisará adicionar o Kidling da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="41405-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41405-126">**Para adicionar o Kidling da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41405-126">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41405-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41405-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41405-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="41405-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41405-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="41405-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="41405-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41405-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="41405-134">Na caixa de pesquisa, digite **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="41405-134">In the search box, type **Kindling**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="41405-136">No painel de resultados, selecione **Kindling** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="41405-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41405-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41405-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Kindling, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="41405-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="41405-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Kindling é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41405-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span></span> <span data-ttu-id="41405-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>

<span data-ttu-id="41405-142">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no AD do Azure ao valor do **Nome de Usuário** no Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="41405-143">Para configurar e testar o logon único do AD do Azur com o Kindling, conclua os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="41405-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41405-144">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="41405-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41405-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41405-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41405-146">**[Como criar um usuário de teste do Kindling](#creating-a-kindling-test-user)** – para ter um equivalente de Brenda Fernandes no Kindling vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41405-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41405-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="41405-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41405-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="41405-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41405-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="41405-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41405-150">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="41405-151">**Para configurar o logon único do AD do Azure AD com o Kindling, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41405-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="41405-152">No portal do Azure, na página de integração de aplicativos do **Kindling**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="41405-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="41405-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="41405-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="41405-156">Na seção **URLs e Domínio do Kindling**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41405-156">On the **Kindling Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="41405-158">a.</span><span class="sxs-lookup"><span data-stu-id="41405-158">a.</span></span> <span data-ttu-id="41405-159">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="41405-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="41405-160">b.</span><span class="sxs-lookup"><span data-stu-id="41405-160">b.</span></span>  <span data-ttu-id="41405-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="41405-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41405-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="41405-162">These values are not the real.</span></span> <span data-ttu-id="41405-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="41405-163">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="41405-164">Entre em contato com a [equipe de suporte do Kindling](mailto:support@kindlingapp.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="41405-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span></span>
 
4. <span data-ttu-id="41405-165">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="41405-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="41405-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="41405-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41405-169">Na seção **Configuração do Kindling**, clique em **Configurar Kindling** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="41405-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41405-170">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="41405-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="41405-172">Para configurar o logon único no lado do **Kindling**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** para a [equipe de suporte do Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="41405-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="41405-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="41405-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41405-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="41405-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41405-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41405-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41405-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="41405-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41405-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="41405-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41405-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41405-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41405-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41405-182">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="41405-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41405-184">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41405-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41405-186">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="41405-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41405-188">a.</span><span class="sxs-lookup"><span data-stu-id="41405-188">a.</span></span> <span data-ttu-id="41405-189">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="41405-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41405-190">b.</span><span class="sxs-lookup"><span data-stu-id="41405-190">b.</span></span> <span data-ttu-id="41405-191">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="41405-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41405-192">c.</span><span class="sxs-lookup"><span data-stu-id="41405-192">c.</span></span> <span data-ttu-id="41405-193">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="41405-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41405-194">d.</span><span class="sxs-lookup"><span data-stu-id="41405-194">d.</span></span> <span data-ttu-id="41405-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="41405-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="41405-196">Criar um usuário de teste Kindling</span><span class="sxs-lookup"><span data-stu-id="41405-196">Creating a Kindling test user</span></span>

<span data-ttu-id="41405-197">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-197">The objective of this section is to create a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="41405-198">O Kindling dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="41405-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="41405-199">Você já habilitou isso em [Configurar o logon único do AD do Azure](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="41405-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="41405-200">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="41405-200">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41405-201">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41405-202">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="41405-204">**Para atribuir Brenda Fernandes ao Kindling, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="41405-204">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="41405-205">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="41405-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="41405-207">Na lista de aplicativos, selecione **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="41405-207">In the applications list, select **Kindling**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="41405-209">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="41405-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="41405-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="41405-211">Click **Add** button.</span></span> <span data-ttu-id="41405-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41405-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="41405-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="41405-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41405-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41405-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41405-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="41405-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41405-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="41405-217">Testing single sign-on</span></span>

<span data-ttu-id="41405-218">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="41405-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="41405-219">Quando você clica no bloco Kindling no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Kindling.</span><span class="sxs-lookup"><span data-stu-id="41405-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="41405-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="41405-220">Additional resources</span></span>

* [<span data-ttu-id="41405-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="41405-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41405-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41405-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

