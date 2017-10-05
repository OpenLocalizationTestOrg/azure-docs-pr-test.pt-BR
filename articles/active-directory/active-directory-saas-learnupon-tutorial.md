---
title: "Tutorial: integração do Azure Active Directory com o LearnUpon | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="7934a-103">Tutorial: Integração do Active Directory do Azure com o LearnUpon</span><span class="sxs-lookup"><span data-stu-id="7934a-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="7934a-104">Neste tutorial, você aprenderá a integrar o LearnUpon ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7934a-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7934a-105">A integração do LearnUpon ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7934a-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7934a-106">No AD do Azure, você pode controlar quem tem acesso ao LearnUpon</span><span class="sxs-lookup"><span data-stu-id="7934a-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="7934a-107">Você pode habilitar que usuários façam logon automaticamente no LearnUpon (logon único) com as respectivas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7934a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7934a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7934a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7934a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7934a-110">Prerequisites</span></span>

<span data-ttu-id="7934a-111">Para configurar a integração do AD do Azure ao LearnUpon, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7934a-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="7934a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7934a-113">Uma assinatura do LearnUpon habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="7934a-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7934a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7934a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7934a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7934a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7934a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7934a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7934a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7934a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7934a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7934a-118">Scenario description</span></span>
<span data-ttu-id="7934a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7934a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7934a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7934a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7934a-121">Adicionando o LearnUpon da galeria</span><span class="sxs-lookup"><span data-stu-id="7934a-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="7934a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="7934a-123">Adicionando o LearnUpon da galeria</span><span class="sxs-lookup"><span data-stu-id="7934a-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="7934a-124">Para configurar a integração do LearnUpon ao AD do Azure, você precisará adicionar o LearnUpon da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7934a-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7934a-125">**Para adicionar o LearnUpon da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7934a-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7934a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7934a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7934a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7934a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7934a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7934a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="7934a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7934a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="7934a-133">Na caixa de pesquisa, digite **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="7934a-133">In the search box, type **LearnUpon**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="7934a-135">No painel de resultados, selecione **LearnUpon** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7934a-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7934a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7934a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LearnUpon, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7934a-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7934a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do LearnUpon é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7934a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="7934a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="7934a-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="7934a-141">No LearnUpon, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7934a-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7934a-142">Para configurar e testar o logon único do AD do Azure com o LearnUpon, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7934a-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7934a-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7934a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7934a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7934a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7934a-145">**[Criar um usuário de teste do LearnUpon](#creating-a-learnupon-test-user)** – para ter um equivalente de Brenda Fernandes no LearnUpon que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7934a-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7934a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7934a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7934a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7934a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7934a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7934a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7934a-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="7934a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="7934a-150">**Para configurar o logon único do Azure AD com o LearnUpon, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7934a-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="7934a-151">No portal do Azure, na página de integração do aplicativo **LearnUpon**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7934a-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="7934a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7934a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="7934a-155">Na seção **Domínio e URLs do LearnUpon**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7934a-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="7934a-157">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="7934a-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7934a-158">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="7934a-158">Please note that this is not the real value.</span></span> <span data-ttu-id="7934a-159">você precisa atualizar esse valor com a URL de Resposta real.</span><span class="sxs-lookup"><span data-stu-id="7934a-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="7934a-160">Para obter esse valor, entre em contato com a [equipe de suporte do LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="7934a-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="7934a-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Bruto)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7934a-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="7934a-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7934a-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7934a-165">Na seção **Configuração do LearnUpon**, clique em **Configurar LearnUpon** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7934a-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7934a-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7934a-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="7934a-168">Abra outra instância do navegador e faça logon no LearnUpon com uma conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="7934a-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="7934a-169">Clique na guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="7934a-169">Click the **settings** tab.</span></span>
   
    ![Configurar o logon único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="7934a-171">Clique em **Logon Único - SAML** e em **Configurações Gerais** para definir configurações de SAML.</span><span class="sxs-lookup"><span data-stu-id="7934a-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="7934a-173">Na seção **Configurações Gerais** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7934a-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="7934a-175">a.</span><span class="sxs-lookup"><span data-stu-id="7934a-175">a.</span></span> <span data-ttu-id="7934a-176">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="7934a-176">Select **Enabled**.</span></span>

    <span data-ttu-id="7934a-177">b.</span><span class="sxs-lookup"><span data-stu-id="7934a-177">b.</span></span> <span data-ttu-id="7934a-178">Selecione **versão** como **2.0**.</span><span class="sxs-lookup"><span data-stu-id="7934a-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="7934a-179">c.</span><span class="sxs-lookup"><span data-stu-id="7934a-179">c.</span></span> <span data-ttu-id="7934a-180">Selecione **Ignorar condições** como **Não**.</span><span class="sxs-lookup"><span data-stu-id="7934a-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="7934a-181">d.</span><span class="sxs-lookup"><span data-stu-id="7934a-181">d.</span></span> <span data-ttu-id="7934a-182">Na caixa de texto **Nome do parâmetro Post de Token SAML**, digite o nome do parâmetro da solicitação post para a URL de consumidor SAML indicada acima, que contém a declaração SAML a ser verificada e autenticada. Por exemplo, **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="7934a-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="7934a-183">e.</span><span class="sxs-lookup"><span data-stu-id="7934a-183">e.</span></span> <span data-ttu-id="7934a-184">Na caixa de texto **Formato de Nome de Identificador**, digite o valor que indica onde em sua Declaração SAML o identificador de usuários (endereço de Email) reside. Por exemplo: **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="7934a-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="7934a-185">f.</span><span class="sxs-lookup"><span data-stu-id="7934a-185">f.</span></span> <span data-ttu-id="7934a-186">Na caixa de texto **Identificar o Local do Provedor**, digite o valor que indica para onde os usuários são enviados ao clicarem em seu ícone carregado na tela de logon do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7934a-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="7934a-187">g.</span><span class="sxs-lookup"><span data-stu-id="7934a-187">g.</span></span> <span data-ttu-id="7934a-188">Na caixa de texto **URL de Logoff**, cole a **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7934a-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="7934a-189">h.</span><span class="sxs-lookup"><span data-stu-id="7934a-189">h.</span></span> <span data-ttu-id="7934a-190">Clique em **Gerenciar impressões digitais**e carregue a impressão digital do certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="7934a-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="7934a-191">Clique em **Configurações de Usuário**e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7934a-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="7934a-193">a.</span><span class="sxs-lookup"><span data-stu-id="7934a-193">a.</span></span> <span data-ttu-id="7934a-194">Na caixa de texto **Formato do Identificador de Nome**, digite o valor que indica onde na instrução de sua declaração do SAML reside o nome dos usuários. Por exemplo, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="7934a-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="7934a-195">b.</span><span class="sxs-lookup"><span data-stu-id="7934a-195">b.</span></span> <span data-ttu-id="7934a-196">Na caixa de texto **Formato do Identificador de Sobrenome**, digite o valor que indica onde na sua instrução de declaração do SAML reside o sobrenome dos usuários. Por exemplo, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="7934a-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="7934a-197">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7934a-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7934a-198">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7934a-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7934a-199">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7934a-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7934a-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="7934a-201">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7934a-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="7934a-203">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7934a-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7934a-204">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7934a-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7934a-206">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7934a-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7934a-208">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7934a-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7934a-210">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7934a-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7934a-212">a.</span><span class="sxs-lookup"><span data-stu-id="7934a-212">a.</span></span> <span data-ttu-id="7934a-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="7934a-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7934a-214">b.</span><span class="sxs-lookup"><span data-stu-id="7934a-214">b.</span></span> <span data-ttu-id="7934a-215">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7934a-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7934a-216">c.</span><span class="sxs-lookup"><span data-stu-id="7934a-216">c.</span></span> <span data-ttu-id="7934a-217">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="7934a-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7934a-218">d.</span><span class="sxs-lookup"><span data-stu-id="7934a-218">d.</span></span> <span data-ttu-id="7934a-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7934a-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="7934a-220">Criar um usuário de teste do LearnUpon</span><span class="sxs-lookup"><span data-stu-id="7934a-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="7934a-221">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="7934a-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="7934a-222">O LearnUpon dá suporte ao provisionamento just-in-time, que é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="7934a-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7934a-223">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="7934a-223">There is no action item for you in this section.</span></span> <span data-ttu-id="7934a-224">Um novo usuário será criado durante uma tentativa de acessar o LearnUpon, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="7934a-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="7934a-225">[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7934a-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="7934a-226">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="7934a-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7934a-227">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7934a-228">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="7934a-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="7934a-230">**Para atribuir Brenda Fernandes ao LearnUpon, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7934a-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="7934a-231">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7934a-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7934a-233">Na lista de aplicativos, selecione **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="7934a-233">In the applications list, select **LearnUpon**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="7934a-235">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7934a-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="7934a-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7934a-237">Click **Add** button.</span></span> <span data-ttu-id="7934a-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7934a-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="7934a-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7934a-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7934a-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7934a-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7934a-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7934a-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7934a-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="7934a-243">Testing single sign-on</span></span>

<span data-ttu-id="7934a-244">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7934a-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7934a-245">Quando você clicar no bloco LearnUpon no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="7934a-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="7934a-246">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7934a-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7934a-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7934a-247">Additional resources</span></span>

* [<span data-ttu-id="7934a-248">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7934a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7934a-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7934a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

