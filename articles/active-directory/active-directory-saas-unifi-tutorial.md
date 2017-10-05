---
title: "Tutorial: Integração do Azure Active Directory ao UNIFI | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="3c12e-103">Tutorial: Integração do Azure Active Directory ao UNIFI</span><span class="sxs-lookup"><span data-stu-id="3c12e-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="3c12e-104">Neste tutorial, você aprenderá a integrar o UNIFI ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3c12e-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c12e-105">A integração do UNIFI ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3c12e-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3c12e-106">Você pode controlar no Azure AD quem terá acesso ao UNIFI</span><span class="sxs-lookup"><span data-stu-id="3c12e-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="3c12e-107">Você pode permitir que seus usuários façam logon automaticamente no UNIFI (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c12e-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c12e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3c12e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c12e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c12e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c12e-110">Prerequisites</span></span>

<span data-ttu-id="3c12e-111">Para configurar a integração do Azure AD ao UNIFI, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3c12e-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="3c12e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c12e-113">Uma assinatura habilitada para logon único do UNIFI</span><span class="sxs-lookup"><span data-stu-id="3c12e-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c12e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3c12e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c12e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3c12e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c12e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3c12e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c12e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c12e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c12e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3c12e-118">Scenario description</span></span>
<span data-ttu-id="3c12e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3c12e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c12e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3c12e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c12e-121">Adicionar o UNIFI da galeria</span><span class="sxs-lookup"><span data-stu-id="3c12e-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="3c12e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="3c12e-123">Adicionar o UNIFI da galeria</span><span class="sxs-lookup"><span data-stu-id="3c12e-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="3c12e-124">Para configurar a integração do UNIFI com o Azure AD, você precisará adicionar o UNIFI à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="3c12e-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3c12e-125">**Para adicionar o UNIFI por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c12e-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3c12e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c12e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3c12e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3c12e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3c12e-133">Na caixa de pesquisa, digite **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-133">In the search box, type **UNIFI**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="3c12e-135">No painel de resultados, selecione **UNIFI** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c12e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c12e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o UNIFI, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3c12e-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3c12e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do UNIFI é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c12e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="3c12e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no UNIFI.</span><span class="sxs-lookup"><span data-stu-id="3c12e-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="3c12e-141">No UNIFI, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3c12e-142">Para configurar e testar o logon único do Azure AD com o UNIFI, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3c12e-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3c12e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3c12e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3c12e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c12e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c12e-145">**[Criação um usuário de teste do UNIFI](#creating-a-unifi-test-user)** – para ter um equivalente de Brenda Fernandes no UNIFI que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c12e-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c12e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c12e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c12e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3c12e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c12e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c12e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c12e-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo UNIFI.</span><span class="sxs-lookup"><span data-stu-id="3c12e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="3c12e-150">**Para configurar o logon único do Azure AD com o UNIFI, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c12e-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="3c12e-151">No Portal do Azure, na página de integração de aplicativos do **UNIFI**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3c12e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3c12e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="3c12e-155">Na seção **Domínio e URLs do UNIFI**, se você desejar configurar o aplicativo no modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="3c12e-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="3c12e-157">Na caixa de texto **Identificador**, digite o valor: `INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="3c12e-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="3c12e-158">Marque **Mostrar configurações avançadas de URL** se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="3c12e-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="3c12e-160">Na caixa de texto **URL de Logon**, digite a URL: `https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="3c12e-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="3c12e-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="3c12e-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="3c12e-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3c12e-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3c12e-165">Na seção **Configuração do UNIFI**, clique em **Configurar o UNIFI** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3c12e-166">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3c12e-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="3c12e-168">Em outra janela do navegador da Web, entre em seu site de empresa do **UNIFI** como administrador.</span><span class="sxs-lookup"><span data-stu-id="3c12e-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="3c12e-169">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-169">Click on the **Users**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="3c12e-171">Clique em **Adicionar Novo Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-171">Click on the **Add New Identity Provider**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="3c12e-173">Na seção **Adicionar Provedor de Identidade**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3c12e-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="3c12e-175">a.</span><span class="sxs-lookup"><span data-stu-id="3c12e-175">a.</span></span> <span data-ttu-id="3c12e-176">Na caixa de texto **Nome do Provedor**, digite o nome do Provedor de Identidade.</span><span class="sxs-lookup"><span data-stu-id="3c12e-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="3c12e-177">b.</span><span class="sxs-lookup"><span data-stu-id="3c12e-177">b.</span></span> <span data-ttu-id="3c12e-178">Na caixa de texto **URL do Provedor**, cole o valor da **URL do Serviço de Logon Único do SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c12e-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3c12e-179">c.</span><span class="sxs-lookup"><span data-stu-id="3c12e-179">c.</span></span> <span data-ttu-id="3c12e-180">Abra o certificado que você baixou do Portal do Azure no bloco de notas, remova a marcação **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** e, em seguida, cole o conteúdo restante na caixa de texto **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="3c12e-181">d.</span><span class="sxs-lookup"><span data-stu-id="3c12e-181">d.</span></span> <span data-ttu-id="3c12e-182">Selecione a caixa de seleção **é o Provedor Padrão**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="3c12e-183">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3c12e-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3c12e-184">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3c12e-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3c12e-185">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c12e-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c12e-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c12e-187">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c12e-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3c12e-189">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c12e-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3c12e-190">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c12e-192">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3c12e-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c12e-194">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c12e-196">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3c12e-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c12e-198">a.</span><span class="sxs-lookup"><span data-stu-id="3c12e-198">a.</span></span> <span data-ttu-id="3c12e-199">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c12e-200">b.</span><span class="sxs-lookup"><span data-stu-id="3c12e-200">b.</span></span> <span data-ttu-id="3c12e-201">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c12e-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c12e-202">c.</span><span class="sxs-lookup"><span data-stu-id="3c12e-202">c.</span></span> <span data-ttu-id="3c12e-203">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3c12e-204">d.</span><span class="sxs-lookup"><span data-stu-id="3c12e-204">d.</span></span> <span data-ttu-id="3c12e-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="3c12e-206">Criação um usuário de teste do UNIFI</span><span class="sxs-lookup"><span data-stu-id="3c12e-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="3c12e-207">Nesta seção, você criará uma usuária chamada Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3c12e-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="3c12e-208">O **UNIFI** dá suporte ao provisionamento de usuário automático para que não seja necessária nenhuma etapa manual.</span><span class="sxs-lookup"><span data-stu-id="3c12e-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="3c12e-209">Os usuários são criados automaticamente após a autenticação bem-sucedida do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c12e-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3c12e-210">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3c12e-211">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao UNIFI.</span><span class="sxs-lookup"><span data-stu-id="3c12e-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3c12e-213">**Para atribuir Brenda Fernandes ao UNIFI, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c12e-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="3c12e-214">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3c12e-216">Na lista de aplicativos, selecione **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-216">In the applications list, select **UNIFI**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="3c12e-218">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3c12e-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c12e-220">Click **Add** button.</span></span> <span data-ttu-id="3c12e-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3c12e-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3c12e-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3c12e-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c12e-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c12e-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c12e-226">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3c12e-226">Testing single sign-on</span></span>

<span data-ttu-id="3c12e-227">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3c12e-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3c12e-228">Quando você clicar no bloco UNIFI no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo UNIFI.</span><span class="sxs-lookup"><span data-stu-id="3c12e-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="3c12e-229">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c12e-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3c12e-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3c12e-230">Additional resources</span></span>

* [<span data-ttu-id="3c12e-231">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12e-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c12e-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c12e-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

