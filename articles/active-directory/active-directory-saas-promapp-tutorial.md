---
title: "Tutorial: integração do Azure Active Directory ao Promapp | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="6e84b-103">Tutorial: integração do Active Directory do Azure com o Promapp</span><span class="sxs-lookup"><span data-stu-id="6e84b-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="6e84b-104">Neste tutorial, você aprende a integrar o Promapp ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6e84b-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e84b-105">A integração do Promapp ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="6e84b-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e84b-106">Você pode controlar no Azure AD quem tem acesso ao Promapp</span><span class="sxs-lookup"><span data-stu-id="6e84b-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="6e84b-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Promapp (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e84b-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e84b-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e84b-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e84b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e84b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e84b-110">Prerequisites</span></span>

<span data-ttu-id="6e84b-111">Para configurar a integração do Azure AD com o Promapp, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6e84b-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="6e84b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e84b-113">Uma assinatura habilitada para logon único do Promapp</span><span class="sxs-lookup"><span data-stu-id="6e84b-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e84b-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6e84b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e84b-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6e84b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e84b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6e84b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e84b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e84b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e84b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6e84b-118">Scenario description</span></span>
<span data-ttu-id="6e84b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6e84b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e84b-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="6e84b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e84b-121">Adicionando Promapp da galeria</span><span class="sxs-lookup"><span data-stu-id="6e84b-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="6e84b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="6e84b-123">Adicionando Promapp da galeria</span><span class="sxs-lookup"><span data-stu-id="6e84b-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="6e84b-124">Para configurar a integração do Promapp ao Azure AD, você precisa adicionar o Promapp por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="6e84b-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e84b-125">**Para adicionar o Azure AD por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e84b-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e84b-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e84b-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e84b-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="6e84b-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="6e84b-133">Na caixa de pesquisa, digite **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-133">In the search box, type **Promapp**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="6e84b-135">No painel de resultados, selecione **Promapp** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e84b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e84b-138">Nesta seção, você configura e testa o logon único do Azure AD com o Promapp, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="6e84b-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e84b-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Promapp é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e84b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="6e84b-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Promapp.</span><span class="sxs-lookup"><span data-stu-id="6e84b-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="6e84b-141">No Promapp, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6e84b-142">Para configurar e testar o logon único do Azure AD com o Promapp, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="6e84b-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e84b-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6e84b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e84b-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e84b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e84b-145">**[Criando um usuário de teste do Promapp](#creating-a-promapp-test-user)** – para ter um equivalente de Brenda Fernandes no Promapp que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e84b-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e84b-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e84b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e84b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="6e84b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e84b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e84b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e84b-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Promapp.</span><span class="sxs-lookup"><span data-stu-id="6e84b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="6e84b-150">**Para configurar o logon único do Azure AD com o Promapp, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e84b-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="6e84b-151">No portal do Azure, na página de integração do aplicativo **Promapp**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="6e84b-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="6e84b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="6e84b-155">Na seção **Domínio e URLs do Promapp**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e84b-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="6e84b-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e84b-157">a.</span></span> <span data-ttu-id="6e84b-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="6e84b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="6e84b-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e84b-159">b.</span></span> <span data-ttu-id="6e84b-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="6e84b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e84b-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="6e84b-161">These values are not real.</span></span> <span data-ttu-id="6e84b-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="6e84b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6e84b-163">Contate a [equipe de suporte ao Cliente do Promapp](https://www.promapp.com/about-us/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="6e84b-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="6e84b-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="6e84b-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="6e84b-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="6e84b-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e84b-168">Na seção **Configuração do Promapp**, clique em **Configurar o Promapp** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e84b-169">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="6e84b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="6e84b-171">Faça logon no site da empresa Promapp como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e84b-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="6e84b-172">No menu na parte superior, clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Logon único do AD do Azure][12]

9. <span data-ttu-id="6e84b-174">Clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-174">Click **Configure**.</span></span> 
   
    ![Logon único do AD do Azure][13]

10. <span data-ttu-id="6e84b-176">No diálogo **Segurança** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e84b-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Logon único do AD do Azure][14]
    
    <span data-ttu-id="6e84b-178">a.</span><span class="sxs-lookup"><span data-stu-id="6e84b-178">a.</span></span> <span data-ttu-id="6e84b-179">Cole a **URL do Serviço de Logon Único SAML** copiada do portal do Azure na caixa de texto **URL de Logon SSO**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="6e84b-180">b.</span><span class="sxs-lookup"><span data-stu-id="6e84b-180">b.</span></span> <span data-ttu-id="6e84b-181">Para **SSO - Modo Logon Único**, selecione **Opcional** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="6e84b-182">c.</span><span class="sxs-lookup"><span data-stu-id="6e84b-182">c.</span></span> <span data-ttu-id="6e84b-183">Abra o certificado baixado no bloco de notas, copie o conteúdo do certificado, sem a primeira linha (-----BEGIN CERTIFICATE-----) e a última linha (-----END CERTIFICATE-----), cole-o na caixa de texto **Certificado x.509 de SSO** e, depois, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="6e84b-184">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="6e84b-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e84b-185">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6e84b-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e84b-186">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e84b-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e84b-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e84b-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e84b-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="6e84b-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e84b-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e84b-191">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e84b-193">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6e84b-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e84b-195">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e84b-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6e84b-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e84b-199">a.</span><span class="sxs-lookup"><span data-stu-id="6e84b-199">a.</span></span> <span data-ttu-id="6e84b-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e84b-201">b.</span><span class="sxs-lookup"><span data-stu-id="6e84b-201">b.</span></span> <span data-ttu-id="6e84b-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="6e84b-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e84b-203">c.</span><span class="sxs-lookup"><span data-stu-id="6e84b-203">c.</span></span> <span data-ttu-id="6e84b-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e84b-205">d.</span><span class="sxs-lookup"><span data-stu-id="6e84b-205">d.</span></span> <span data-ttu-id="6e84b-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="6e84b-207">Criar um usuário de teste Promapp</span><span class="sxs-lookup"><span data-stu-id="6e84b-207">Creating a Promapp test user</span></span>

<span data-ttu-id="6e84b-208">O aplicativo Promapp dá suporte ao provisionamento Just-in-Time.</span><span class="sxs-lookup"><span data-stu-id="6e84b-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="6e84b-209">Isso significa que uma conte de usuário será criada automaticamente se necessário durante uma tentativa de acessar o aplicativo usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6e84b-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e84b-210">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e84b-211">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Promapp.</span><span class="sxs-lookup"><span data-stu-id="6e84b-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="6e84b-213">**Para atribuir Brenda Fernandes ao Promapp, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="6e84b-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="6e84b-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="6e84b-216">Na lista de aplicativos, escolha **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-216">In the applications list, select **Promapp**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="6e84b-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="6e84b-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e84b-220">Click **Add** button.</span></span> <span data-ttu-id="6e84b-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="6e84b-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="6e84b-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e84b-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e84b-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e84b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e84b-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="6e84b-226">Testing single sign-on</span></span>

<span data-ttu-id="6e84b-227">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="6e84b-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6e84b-228">Quando você clica no bloco Promapp no Painel de Acesso, você deve ser conectado automaticamente ao seu aplicativo Promapp.</span><span class="sxs-lookup"><span data-stu-id="6e84b-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e84b-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6e84b-229">Additional resources</span></span>

* [<span data-ttu-id="6e84b-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6e84b-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e84b-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e84b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

