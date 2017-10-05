---
title: "Tutorial: integração do Azure Active Directory ao Mixpanel | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="5d89e-103">Tutorial: Integração do Active Directory do Azure com o Mixpanel</span><span class="sxs-lookup"><span data-stu-id="5d89e-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="5d89e-104">Neste tutorial, você aprenderá a integrar o Mixpanel ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5d89e-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d89e-105">A integração do Mixpanel ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5d89e-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5d89e-106">No Azure AD, é possível controlar quem tem acesso ao Mixpanel</span><span class="sxs-lookup"><span data-stu-id="5d89e-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="5d89e-107">Você pode permitir que os usuários façam logon automaticamente no Mixpanel (Logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d89e-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d89e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5d89e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d89e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d89e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5d89e-110">Prerequisites</span></span>

<span data-ttu-id="5d89e-111">Para configurar a integração do Azure AD ao Mixpanel, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5d89e-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="5d89e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d89e-113">Uma assinatura habilitada para logon único do Mixpanel</span><span class="sxs-lookup"><span data-stu-id="5d89e-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d89e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5d89e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d89e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5d89e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d89e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5d89e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d89e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d89e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d89e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5d89e-118">Scenario description</span></span>
<span data-ttu-id="5d89e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5d89e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d89e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5d89e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d89e-121">Adição do Mixpanel da galeria</span><span class="sxs-lookup"><span data-stu-id="5d89e-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="5d89e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="5d89e-123">Adição do Mixpanel da galeria</span><span class="sxs-lookup"><span data-stu-id="5d89e-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="5d89e-124">Para configurar a integração do Mixpanel ao Azure AD, você precisará adicionar o Mixpanel à sua lista de aplicativos SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="5d89e-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5d89e-125">**Para adicionar o Mixpanel a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5d89e-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5d89e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5d89e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5d89e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5d89e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5d89e-133">Na caixa de pesquisa, digite **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-133">In the search box, type **Mixpanel**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="5d89e-135">No painel de resultados, selecione **Mixpanel** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d89e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d89e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Mixpanel, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5d89e-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d89e-139">Para que o logon único funcione, o Azure AD precisará saber qual usuário do Mixpanel é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d89e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="5d89e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="5d89e-141">No Mixpanel, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5d89e-142">Para configurar e testar o logon único do Azure AD com o Mixpanel, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5d89e-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5d89e-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** - para permitir que seus usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5d89e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5d89e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5d89e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d89e-145">**[Criação de um usuário de teste do Mixpanel](#creating-a-mixpanel-test-user)**: para ter um equivalente de Brenda Fernandes no Mixpanel que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d89e-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d89e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d89e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d89e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5d89e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d89e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d89e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d89e-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="5d89e-150">**Para configurar o logon único do Azure AD com o Mixpanel, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5d89e-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="5d89e-151">No Portal do Azure, na página de integração de aplicativos do **Mixpanel**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5d89e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5d89e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="5d89e-155">Na seção **Domínio e URLs do Mixpanel**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5d89e-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="5d89e-157">Na caixa de texto **URL de Logon**, digite uma URL como: `https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="5d89e-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d89e-158">Registre-se em [https://mixpanel.com/register/](https://mixpanel.com/register/) para configurar suas credenciais de logon e entre em contato com a [equipe de suporte do Mixpanel](mailto:support@mixpanel.com) para habilitar as configurações de SSO para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="5d89e-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="5d89e-159">Você também poderá obter o valor da URL de Entrada, se for necessário, da equipe de suporte do Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="5d89e-160">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="5d89e-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="5d89e-162">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5d89e-162">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5d89e-164">Na seção **Configuração do Mixpanel**, clique em **Configurar Mixpanel** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5d89e-165">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5d89e-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="5d89e-167">Em uma janela diferente do navegador, faça logon no aplicativo Mixpanel como administrador.</span><span class="sxs-lookup"><span data-stu-id="5d89e-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="5d89e-168">Na parte inferior da página, clique no ícone de **engrenagem** no canto esquerdo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Logon único do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="5d89e-170">Clique na guia **Segurança de acesso** e clique em **Alterar configurações**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="5d89e-172">Na página de diálogo **Alterar seu certificado**, clique em **Escolher arquivo** para carregar o certificado baixado e, em seguida, clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="5d89e-174">Na caixa de texto da URL de autenticação na página de diálogo **Alterar a URL de autenticação**, cole o valor de **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure e, em seguida, clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="5d89e-176">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="5d89e-177">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5d89e-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5d89e-178">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5d89e-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5d89e-179">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d89e-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d89e-180">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d89e-181">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5d89e-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5d89e-183">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5d89e-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5d89e-184">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d89e-186">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5d89e-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d89e-188">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d89e-190">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5d89e-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d89e-192">a.</span><span class="sxs-lookup"><span data-stu-id="5d89e-192">a.</span></span> <span data-ttu-id="5d89e-193">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d89e-194">b.</span><span class="sxs-lookup"><span data-stu-id="5d89e-194">b.</span></span> <span data-ttu-id="5d89e-195">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5d89e-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d89e-196">c.</span><span class="sxs-lookup"><span data-stu-id="5d89e-196">c.</span></span> <span data-ttu-id="5d89e-197">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5d89e-198">d.</span><span class="sxs-lookup"><span data-stu-id="5d89e-198">d.</span></span> <span data-ttu-id="5d89e-199">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="5d89e-200">Criação de um usuário de teste do Mixpanel</span><span class="sxs-lookup"><span data-stu-id="5d89e-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="5d89e-201">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="5d89e-202">Faça logon em seu site de empresa do Mixpanel como administrador.</span><span class="sxs-lookup"><span data-stu-id="5d89e-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="5d89e-203">Na parte inferior da página, clique no pequeno botão de engrenagem no canto esquerdo para abrir a janela **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="5d89e-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="5d89e-204">Clique na guia **Equipe** .</span><span class="sxs-lookup"><span data-stu-id="5d89e-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="5d89e-205">Na caixa de texto **membro da equipe** , digite o endereço de email de Brenda no Azure.</span><span class="sxs-lookup"><span data-stu-id="5d89e-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Configurações do Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="5d89e-207">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="5d89e-208">O usuário receberá um email para configurar o perfil.</span><span class="sxs-lookup"><span data-stu-id="5d89e-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5d89e-209">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5d89e-210">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5d89e-212">**Para atribuir Brenda Fernandes ao Mixpanel, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5d89e-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="5d89e-213">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5d89e-215">Na lista de aplicativos, selecione **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-215">In the applications list, select **Mixpanel**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="5d89e-217">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5d89e-219">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5d89e-219">Click **Add** button.</span></span> <span data-ttu-id="5d89e-220">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5d89e-222">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5d89e-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5d89e-223">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d89e-224">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5d89e-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d89e-225">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5d89e-225">Testing single sign-on</span></span>

<span data-ttu-id="5d89e-226">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5d89e-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5d89e-227">Ao clicar no bloco do Mixpanel no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="5d89e-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="5d89e-228">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5d89e-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5d89e-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5d89e-229">Additional resources</span></span>

* [<span data-ttu-id="5d89e-230">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5d89e-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d89e-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d89e-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

