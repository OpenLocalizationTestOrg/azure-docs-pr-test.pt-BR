---
title: "Tutorial: Integração do Azure Active Directory ao Bambu by Sprout Social | Microsoft Docs"
description: "Saiba como configurar logon único entre o Azure Active Directory e o Bambu by Sprout Social."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="4aa5d-103">Tutorial: Integração do Azure Active Directory com Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="4aa5d-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="4aa5d-104">Neste tutorial, você aprenderá a integrar o Bambu by Sprout Social ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4aa5d-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4aa5d-105">A integração do Bambu by Sprout Social ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4aa5d-106">No Azure AD, você poderá controlar quem tem acesso ao Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="4aa5d-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="4aa5d-107">Você pode permitir que seus usuários façam logon automaticamente no Bambu by Sprout Social (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4aa5d-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4aa5d-108">Você pode gerenciar suas contas em um único local: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4aa5d-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4aa5d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="4aa5d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4aa5d-110">Prerequisites</span></span>

<span data-ttu-id="4aa5d-111">Para configurar a integração do Azure AD com o Bambu by Sprout Social, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="4aa5d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4aa5d-113">Uma assinatura habilitada de logon único do Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="4aa5d-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4aa5d-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4aa5d-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4aa5d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4aa5d-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4aa5d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4aa5d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4aa5d-118">Scenario description</span></span>
<span data-ttu-id="4aa5d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4aa5d-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4aa5d-121">Adicionar Bambu by Sprout Social da galeria</span><span class="sxs-lookup"><span data-stu-id="4aa5d-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="4aa5d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="4aa5d-123">Adicionar Bambu by Sprout Social da galeria</span><span class="sxs-lookup"><span data-stu-id="4aa5d-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="4aa5d-124">Para configurar a integração do Bambu by Sprout Social ao Azure AD, você precisa adicionar o Bambu by Sprout Social por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4aa5d-125">**Para adicionar o Bambu by Sprout Social da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4aa5d-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4aa5d-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4aa5d-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4aa5d-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4aa5d-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4aa5d-133">Na caixa de pesquisa, digite **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="4aa5d-135">No painel de resultados, selecione **Bambu by Sprout** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4aa5d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4aa5d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Bambu by Sprout Social, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4aa5d-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Bambu by Sprout Social é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="4aa5d-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="4aa5d-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="4aa5d-142">Para configurar e testar logon único do Azure AD com o Bambu by Sprout Social, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4aa5d-143">**[Configuração do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4aa5d-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4aa5d-145">**[Criando um usuário de teste do Bambu by Sprout Social](#creating-a-bambu-by-sprout-social-test-user)** : para ter um equivalente de Brenda Fernandes no Bambu by Sprout Social que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4aa5d-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4aa5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4aa5d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4aa5d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4aa5d-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="4aa5d-150">**Para configurar logon único do Azure AD com o Bambu by Sprout Social, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4aa5d-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="4aa5d-151">No portal do Azure, na página de integração de aplicativos do **Bambu by Sprout Social**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="4aa5d-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="4aa5d-155">Na seção **URLs e Domínio do Bambu by Sprout Social**, o usuário não precisa executar as etapas já que o aplicativo está previamente integrado com o Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configurar o logon único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="4aa5d-157">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="4aa5d-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4aa5d-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4aa5d-161">Na seção **Configuração do Bambu by Sprout Social**, clique em **Configurar Bambu by Sprout Social** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4aa5d-162">Copie a **URL de serviço logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4aa5d-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar o logon único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="4aa5d-164">Para configurar logon único em **Bambu by Sprout Social**, é necessário enviar o **XML de metadados** e a **URL de serviço logon único SAML** baixados para [suporte do Bambu by Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="4aa5d-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="4aa5d-165">Isso será configurado para que a conexão de SSO do SAML seja definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4aa5d-166">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4aa5d-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4aa5d-167">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, simplesmente clique na guia **Logon Único** e acesse a documentação inserida através da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4aa5d-168">Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4aa5d-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4aa5d-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="4aa5d-170">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4aa5d-172">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4aa5d-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4aa5d-173">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4aa5d-175">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4aa5d-177">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4aa5d-179">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4aa5d-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4aa5d-181">a.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-181">a.</span></span> <span data-ttu-id="4aa5d-182">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="4aa5d-183">b.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-183">b.</span></span> <span data-ttu-id="4aa5d-184">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="4aa5d-185">c.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-185">c.</span></span> <span data-ttu-id="4aa5d-186">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4aa5d-187">d.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-187">d.</span></span> <span data-ttu-id="4aa5d-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="4aa5d-189">Criando um usuário de teste Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="4aa5d-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="4aa5d-190">O aplicativo oferece suporte de provisionamento de usuário just-in-time e após a autenticação os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4aa5d-191">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4aa5d-192">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4aa5d-194">**Para atribuir Brenda Fernandes ao Bambu by Sprout Social, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4aa5d-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="4aa5d-195">No portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4aa5d-197">Na lista de aplicativos, escolha **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="4aa5d-199">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4aa5d-201">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-201">Click **Add** button.</span></span> <span data-ttu-id="4aa5d-202">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4aa5d-204">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4aa5d-205">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4aa5d-206">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4aa5d-207">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4aa5d-207">Testing single sign-on</span></span>

<span data-ttu-id="4aa5d-208">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4aa5d-209">Ao clicar no bloco Bambu by Sprout Social no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="4aa5d-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="4aa5d-210">Para obter mais detalhes sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4aa5d-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4aa5d-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4aa5d-211">Additional resources</span></span>

* [<span data-ttu-id="4aa5d-212">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa5d-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4aa5d-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4aa5d-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

