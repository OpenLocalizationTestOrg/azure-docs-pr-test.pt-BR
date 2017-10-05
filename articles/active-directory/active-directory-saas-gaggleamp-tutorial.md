---
title: "Tutorial: integração do Azure Active Directory com o GaggleAMP | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="8bfec-103">Tutorial: Integração do Active Directory do Azure com o GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="8bfec-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="8bfec-104">Neste tutorial, você aprende a integrar o GaggleAMP ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8bfec-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bfec-105">A integração do GaggleAMP ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8bfec-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8bfec-106">No Azure AD, é possível controlar quem tem acesso ao GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="8bfec-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="8bfec-107">Você pode permitir seus usuários façam logon automaticamente no GaggleAMP (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfec-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bfec-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8bfec-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8bfec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bfec-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8bfec-110">Prerequisites</span></span>

<span data-ttu-id="8bfec-111">Para configurar a integração do Azure AD ao GaggleAMP, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8bfec-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="8bfec-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bfec-113">Uma assinatura do GaggleAMP com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="8bfec-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bfec-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8bfec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bfec-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8bfec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bfec-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8bfec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bfec-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bfec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bfec-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8bfec-118">Scenario description</span></span>
<span data-ttu-id="8bfec-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8bfec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bfec-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8bfec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bfec-121">Adição do GaggleAMP da galeria</span><span class="sxs-lookup"><span data-stu-id="8bfec-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="8bfec-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="8bfec-123">Adição do GaggleAMP da galeria</span><span class="sxs-lookup"><span data-stu-id="8bfec-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="8bfec-124">Para configurar a integração do GaggleAMP com o Azure AD, você precisa adicionar o GaggleAMP à sua lista de aplicativos SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="8bfec-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bfec-125">**Para adicionar o GaggleAMP a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8bfec-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bfec-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bfec-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8bfec-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8bfec-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8bfec-133">Na caixa de pesquisa, digite **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-133">In the search box, type **GaggleAMP**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="8bfec-135">No painel de resultados, selecione **GaggleAMP** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bfec-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8bfec-138">Nesta seção, você configura e testa o logon único do Azure AD com o GaggleAMP com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8bfec-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8bfec-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do GaggleAMP é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bfec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="8bfec-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="8bfec-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="8bfec-141">No GaggleAMP, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8bfec-142">Para configurar e testar o logon único do Azure AD com o GaggleAMP, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8bfec-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bfec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8bfec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bfec-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8bfec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bfec-145">**[Criação de um usuário de teste do GaggleAMP](#creating-a-gaggleamp-test-user)** – para ter um equivalente de Brenda Fernandes no GaggleAMP que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8bfec-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bfec-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bfec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bfec-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8bfec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bfec-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8bfec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bfec-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="8bfec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="8bfec-150">**Para configurar o logon único do Azure AD com o GaggleAMP, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8bfec-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="8bfec-151">No portal do Azure, na página de integração de aplicativos do **GaggleAMP**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8bfec-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8bfec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="8bfec-155">Na seção **URLs e Domínio do GaggleAMP**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8bfec-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="8bfec-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="8bfec-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8bfec-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="8bfec-158">The value is not real.</span></span> <span data-ttu-id="8bfec-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="8bfec-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="8bfec-160">Entre em contato com a [equipe de suporte ao Cliente do GaggleAMP](mailto:sales@gaggleamp.com) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="8bfec-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="8bfec-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8bfec-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="8bfec-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8bfec-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bfec-165">Na seção **Configuração do GaggleAMP**, clique em **Configurar GaggleAMP** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8bfec-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="8bfec-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="8bfec-168">Em outra instância do navegador, navegue até a página de SSO do SAML criada para você pela equipe de suporte do Gaggle (por exemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="8bfec-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="8bfec-169">Na página **SSO de SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8bfec-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![Logon único do GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="8bfec-171">a.</span><span class="sxs-lookup"><span data-stu-id="8bfec-171">a.</span></span> <span data-ttu-id="8bfec-172">Na caixa de texto **Emissor do Provedor de Identidade**, cole o valor da **URL do Emissor do Certificado** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bfec-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="8bfec-173">b.</span><span class="sxs-lookup"><span data-stu-id="8bfec-173">b.</span></span> <span data-ttu-id="8bfec-174">Na caixa de texto **URL de Logon Único do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bfec-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="8bfec-175">c.</span><span class="sxs-lookup"><span data-stu-id="8bfec-175">c.</span></span> <span data-ttu-id="8bfec-176">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="8bfec-176">Click **Save**</span></span>      

    <span data-ttu-id="8bfec-177">d.</span><span class="sxs-lookup"><span data-stu-id="8bfec-177">d.</span></span> <span data-ttu-id="8bfec-178">Envie o **Certificado (Base64)** para sua [equipe de suporte do GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="8bfec-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="8bfec-179">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8bfec-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8bfec-180">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8bfec-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8bfec-181">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8bfec-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bfec-182">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="8bfec-183">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8bfec-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8bfec-185">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8bfec-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bfec-186">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bfec-188">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8bfec-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bfec-190">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bfec-192">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8bfec-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bfec-194">a.</span><span class="sxs-lookup"><span data-stu-id="8bfec-194">a.</span></span> <span data-ttu-id="8bfec-195">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bfec-196">b.</span><span class="sxs-lookup"><span data-stu-id="8bfec-196">b.</span></span> <span data-ttu-id="8bfec-197">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8bfec-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bfec-198">c.</span><span class="sxs-lookup"><span data-stu-id="8bfec-198">c.</span></span> <span data-ttu-id="8bfec-199">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8bfec-200">d.</span><span class="sxs-lookup"><span data-stu-id="8bfec-200">d.</span></span> <span data-ttu-id="8bfec-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="8bfec-202">Criação de um usuário de teste do GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="8bfec-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="8bfec-203">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="8bfec-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="8bfec-204">O GaggleAMP dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8bfec-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8bfec-205">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8bfec-205">There is no action item for you in this section.</span></span> <span data-ttu-id="8bfec-206">Um novo usuário é criado durante uma tentativa de acessar o GaggleAMP, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="8bfec-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8bfec-207">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8bfec-208">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="8bfec-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8bfec-210">**Para atribuir Brenda Fernandes ao GaggleAMP, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8bfec-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="8bfec-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8bfec-213">Na lista de aplicativos, selecione **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="8bfec-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8bfec-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8bfec-217">Click **Add** button.</span></span> <span data-ttu-id="8bfec-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8bfec-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8bfec-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8bfec-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bfec-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8bfec-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bfec-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8bfec-223">Testing single sign-on</span></span>

<span data-ttu-id="8bfec-224">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8bfec-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8bfec-225">Ao clicar no bloco GaggleAMP no Painel de Acesso, você deve ser automaticamente conectado a seu aplicativo GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="8bfec-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bfec-226">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8bfec-226">Additional resources</span></span>

* [<span data-ttu-id="8bfec-227">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8bfec-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bfec-228">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8bfec-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

