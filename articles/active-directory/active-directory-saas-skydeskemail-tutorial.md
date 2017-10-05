---
title: "Tutorial: Integração do Azure Active Directory ao SkyDesk Email | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SkyDesk Email."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="e0da2-103">Tutorial: integração do Azure Active Directory ao SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="e0da2-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="e0da2-104">Neste tutorial, você aprende a integrar o SkyDesk Email ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e0da2-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0da2-105">A integração do SkyDesk Email ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="e0da2-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0da2-106">No Azure AD, você pode controlar quem tem acesso ao SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="e0da2-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="e0da2-107">É possível permitir que os usuários se conectem automaticamente ao SkyDesk Email (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0da2-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0da2-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0da2-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0da2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0da2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0da2-110">Prerequisites</span></span>

<span data-ttu-id="e0da2-111">Para configurar a integração do Azure AD ao SkyDesk Email, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e0da2-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="e0da2-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0da2-113">Uma assinatura habilitada para logon único do SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="e0da2-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0da2-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e0da2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0da2-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e0da2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0da2-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e0da2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0da2-117">Caso não tenha um ambiente de avaliação do Azure AD, obtenha uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0da2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0da2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e0da2-118">Scenario description</span></span>
<span data-ttu-id="e0da2-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e0da2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0da2-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="e0da2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0da2-121">Adicionar o SkyDesk Email a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="e0da2-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="e0da2-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="e0da2-123">Adicionar o SkyDesk Email a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="e0da2-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="e0da2-124">Para configurar a integração do SkyDesk Email ao Azure AD, você precisará adicionar o SkyDesk Email da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e0da2-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0da2-125">**Para adicionar o SkyDesk Email a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0da2-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0da2-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0da2-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0da2-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e0da2-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e0da2-133">Na caixa de pesquisa, digite **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-133">In the search box, type **SkyDesk Email**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="e0da2-135">No painel de resultados, selecione **SkyDesk Email** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0da2-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0da2-138">Nesta seção, você configura e testa o logon único do Azure AD com o SkyDesk Email, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e0da2-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0da2-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SkyDesk Email é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0da2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="e0da2-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="e0da2-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="e0da2-141">No SkyDesk Email, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0da2-142">Para configurar e testar o logon único do Azure AD com o SkyDesk Email, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="e0da2-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0da2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e0da2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0da2-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0da2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0da2-145">**[Criando um usuário de teste do SkyDesk Email](#creating-a-skydesk-email-test-user)** – para ter um equivalente de Brenda Fernandes no SkyDesk Email que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0da2-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0da2-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0da2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0da2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="e0da2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0da2-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0da2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0da2-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="e0da2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="e0da2-150">**Para configurar o logon único do Azure AD com o SkyDesk Email, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0da2-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="e0da2-151">No portal do Azure, na página de integração do aplicativo **SkyDesk Email**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e0da2-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="e0da2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="e0da2-155">Na seção **Domínio e URLs do SkyDesk Email**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0da2-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="e0da2-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="e0da2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e0da2-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="e0da2-158">The value is not real.</span></span> <span data-ttu-id="e0da2-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="e0da2-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="e0da2-160">Contate a [equipe de suporte ao Cliente do SkyDesk Email](https://www.skydesk.sg/support/) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="e0da2-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="e0da2-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e0da2-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="e0da2-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e0da2-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0da2-165">Na seção **Configuração do SkyDesk Email**, clique em **Configurar o SkyDesk Email** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e0da2-166">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="e0da2-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="e0da2-168">Para habilitar o SSO no **SkyDesk Email**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0da2-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="e0da2-169">a.</span><span class="sxs-lookup"><span data-stu-id="e0da2-169">a.</span></span> <span data-ttu-id="e0da2-170">Entre na sua conta do SkyDesk Email como administrador.</span><span class="sxs-lookup"><span data-stu-id="e0da2-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="e0da2-171">b.</span><span class="sxs-lookup"><span data-stu-id="e0da2-171">b.</span></span> <span data-ttu-id="e0da2-172">No menu na parte superior, clique em **Configuração** e selecione **Organização**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="e0da2-174">c.</span><span class="sxs-lookup"><span data-stu-id="e0da2-174">c.</span></span> <span data-ttu-id="e0da2-175">Clique em **Domínios** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-175">Click on **Domains** from the left panel.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="e0da2-177">d.</span><span class="sxs-lookup"><span data-stu-id="e0da2-177">d.</span></span> <span data-ttu-id="e0da2-178">Clique em **Adicionar Domínio**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-178">Click on **Add Domain**.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="e0da2-180">e.</span><span class="sxs-lookup"><span data-stu-id="e0da2-180">e.</span></span> <span data-ttu-id="e0da2-181">Insira seu nome de Domínio e verifique o Domínio.</span><span class="sxs-lookup"><span data-stu-id="e0da2-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="e0da2-183">f.</span><span class="sxs-lookup"><span data-stu-id="e0da2-183">f.</span></span> <span data-ttu-id="e0da2-184">Clique em **Autenticação SAML** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="e0da2-186">Na página de diálogo **Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0da2-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Configurar o logon único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="e0da2-188">Para usar a autenticação baseada em SAML, você deve configurar um **domínio verificado** ou uma **URL de portal**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="e0da2-189">Você pode definir a URL de portal com o nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="e0da2-191">a.</span><span class="sxs-lookup"><span data-stu-id="e0da2-191">a.</span></span> <span data-ttu-id="e0da2-192">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0da2-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e0da2-193">b.</span><span class="sxs-lookup"><span data-stu-id="e0da2-193">b.</span></span> <span data-ttu-id="e0da2-194">Na caixa de texto **URL de Logoff**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0da2-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e0da2-195">c.</span><span class="sxs-lookup"><span data-stu-id="e0da2-195">c.</span></span> <span data-ttu-id="e0da2-196">A **URL de Alteração de Senha** é opcional, portanto, deixe-a em branco.</span><span class="sxs-lookup"><span data-stu-id="e0da2-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="e0da2-197">d.</span><span class="sxs-lookup"><span data-stu-id="e0da2-197">d.</span></span> <span data-ttu-id="e0da2-198">Clique em **Obter Chave de Arquivo** para selecionar o certificado baixado no portal do Azure e, em seguida, clique em **Abrir** para carregar o certificado.</span><span class="sxs-lookup"><span data-stu-id="e0da2-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="e0da2-199">e.</span><span class="sxs-lookup"><span data-stu-id="e0da2-199">e.</span></span> <span data-ttu-id="e0da2-200">Para **Algoritmo**, selecione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="e0da2-201">f.</span><span class="sxs-lookup"><span data-stu-id="e0da2-201">f.</span></span> <span data-ttu-id="e0da2-202">Clique em **Ok** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="e0da2-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="e0da2-203">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="e0da2-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0da2-204">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e0da2-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0da2-205">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e0da2-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0da2-206">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0da2-207">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0da2-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e0da2-209">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0da2-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0da2-210">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0da2-212">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e0da2-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0da2-214">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0da2-216">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e0da2-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0da2-218">a.</span><span class="sxs-lookup"><span data-stu-id="e0da2-218">a.</span></span> <span data-ttu-id="e0da2-219">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0da2-220">b.</span><span class="sxs-lookup"><span data-stu-id="e0da2-220">b.</span></span> <span data-ttu-id="e0da2-221">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="e0da2-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0da2-222">c.</span><span class="sxs-lookup"><span data-stu-id="e0da2-222">c.</span></span> <span data-ttu-id="e0da2-223">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0da2-224">d.</span><span class="sxs-lookup"><span data-stu-id="e0da2-224">d.</span></span> <span data-ttu-id="e0da2-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="e0da2-226">Criar um usuário de teste do SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="e0da2-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="e0da2-227">Nesta seção, você criará uma usuária chamada Brenda Fernandes no SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="e0da2-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="e0da2-228">Clique em **Acesso de Usuário** no painel esquerdo do SkyDesk Email e digite seu nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="e0da2-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="e0da2-230">Se você precisar criar usuários em massa, contate a [equipe de suporte ao Cliente do SkyDesk Email](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="e0da2-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0da2-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0da2-232">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="e0da2-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e0da2-234">**Para atribuir Brenda Fernandes ao SkyDesk Email, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="e0da2-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="e0da2-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e0da2-237">Na lista de aplicativos, selecione  **Email**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="e0da2-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e0da2-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e0da2-241">Click **Add** button.</span></span> <span data-ttu-id="e0da2-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e0da2-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="e0da2-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0da2-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0da2-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e0da2-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0da2-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e0da2-247">Testing single sign-on</span></span>

<span data-ttu-id="e0da2-248">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e0da2-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e0da2-249">Ao clicar no bloco do SkyDesk Email no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="e0da2-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0da2-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e0da2-250">Additional resources</span></span>

* [<span data-ttu-id="e0da2-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e0da2-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0da2-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0da2-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

