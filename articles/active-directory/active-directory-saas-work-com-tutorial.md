---
title: "Tutorial: Integração do Azure Active Directory com o Work.com | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="a99b8-103">Tutorial: Integração do Active Directory do Azure com o Work.com</span><span class="sxs-lookup"><span data-stu-id="a99b8-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="a99b8-104">Neste tutorial, você aprenderá a integrar o Work.com ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a99b8-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a99b8-105">A integração do Work.com ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a99b8-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a99b8-106">No Azure AD, é possível controlar quem tem acesso ao Work.com</span><span class="sxs-lookup"><span data-stu-id="a99b8-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="a99b8-107">Você pode permitir que os usuários façam logon automaticamente no Work.com (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a99b8-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a99b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a99b8-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a99b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a99b8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a99b8-110">Prerequisites</span></span>

<span data-ttu-id="a99b8-111">Para configurar a integração do Azure AD ao Work.com, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a99b8-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="a99b8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a99b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a99b8-113">Uma assinatura do Work.com habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="a99b8-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a99b8-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a99b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a99b8-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a99b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a99b8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a99b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a99b8-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a99b8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a99b8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a99b8-118">Scenario description</span></span>
<span data-ttu-id="a99b8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a99b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a99b8-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a99b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a99b8-121">Adicionar o Work.com da galeria</span><span class="sxs-lookup"><span data-stu-id="a99b8-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="a99b8-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="a99b8-123">Adicionar o Work.com da galeria</span><span class="sxs-lookup"><span data-stu-id="a99b8-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="a99b8-124">Para configurar a integração do Work.com ao Azure AD, você precisará adicionar o Work.com da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a99b8-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a99b8-125">**Para adicionar o Work.com da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a99b8-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a99b8-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a99b8-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a99b8-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a99b8-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a99b8-133">Na caixa de pesquisa, digite **Work.com**, selecione **Work.com** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Adicionar da galeria](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a99b8-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a99b8-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Work.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a99b8-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a99b8-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Work.com é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99b8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="a99b8-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="a99b8-139">No Work.com, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a99b8-140">Para configurar e testar o logon único do Azure AD com o Work.com, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a99b8-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a99b8-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a99b8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a99b8-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a99b8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a99b8-143">**[Criar um usuário de teste do Work.com](#create-a-workcom-test-user)** – para ter um equivalente de Brenda Fernandes no Work.com vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99b8-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a99b8-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99b8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a99b8-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a99b8-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a99b8-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a99b8-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="a99b8-148">Para configurar o logon único, você ainda precisa definir um nome de domínio personalizado Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="a99b8-149">Você precisa definir pelo menos um nome de domínio, testá-lo e implantá-lo em toda a sua organização.</span><span class="sxs-lookup"><span data-stu-id="a99b8-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="a99b8-150">**Para configurar o logon único do Azure AD com o Work.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a99b8-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="a99b8-151">No Portal do Azure, na página de integração de aplicativos do **Work.com**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a99b8-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a99b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Logon único baseado em SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="a99b8-155">Na seção **Domínio e URLs do Work.com**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a99b8-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Seção Domínio e URLs do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="a99b8-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="a99b8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a99b8-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="a99b8-158">This value is not real.</span></span> <span data-ttu-id="a99b8-159">Atualize esse valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="a99b8-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a99b8-160">Contate a [equipe de suporte ao cliente do Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="a99b8-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="a99b8-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a99b8-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Seção Certificado de Autenticação SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="a99b8-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a99b8-163">Click **Save** button.</span></span>

    ![Botão Salvar](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a99b8-165">Na seção **Configuração do Work.com**, clique em **Configurar o Work.com** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a99b8-166">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="a99b8-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Seção Configuração do Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="a99b8-168">Faça logon no seu locatário Work.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="a99b8-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="a99b8-169">Vá para **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="a99b8-170">![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="a99b8-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="a99b8-171">No painel de navegação à esquerda, na seção **Administrador**, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="a99b8-172">![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="a99b8-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="a99b8-173">Para confirmar se o domínio foi configurado corretamente, verifique se ele está em “**Etapa 4 Implantado nos Usuários**” e examine “**Minhas Configurações de Domínio**”.</span><span class="sxs-lookup"><span data-stu-id="a99b8-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="a99b8-174">![Domínio Implantado no Usuário](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domínio Implantado no Usuário")</span><span class="sxs-lookup"><span data-stu-id="a99b8-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="a99b8-175">Faça logon no seu locatário Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="a99b8-176">Vá para **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="a99b8-177">![Configuração](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="a99b8-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="a99b8-178">Expanda o menu **Controles de Segurança** e clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="a99b8-179">![Configurações de Logon Único](./media/active-directory-saas-work-com-tutorial/ic794113.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a99b8-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="a99b8-180">Na página do diálogo **Configurações de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a99b8-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="a99b8-181">![SAML habilitado](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML habilitado")</span><span class="sxs-lookup"><span data-stu-id="a99b8-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="a99b8-182">a.</span><span class="sxs-lookup"><span data-stu-id="a99b8-182">a.</span></span> <span data-ttu-id="a99b8-183">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="a99b8-184">b.</span><span class="sxs-lookup"><span data-stu-id="a99b8-184">b.</span></span> <span data-ttu-id="a99b8-185">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-185">Click **New**.</span></span>

15. <span data-ttu-id="a99b8-186">Na seção de **Configurações de Logon Único do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a99b8-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="a99b8-187">![Configurações de Logon Único do SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="a99b8-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="a99b8-188">a.</span><span class="sxs-lookup"><span data-stu-id="a99b8-188">a.</span></span> <span data-ttu-id="a99b8-189">Na caixa de texto **Nome** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="a99b8-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="a99b8-190">Fornecer um valor para **Nome** popula automaticamente a caixa de texto **Nome da API**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="a99b8-191">b.</span><span class="sxs-lookup"><span data-stu-id="a99b8-191">b.</span></span> <span data-ttu-id="a99b8-192">Na caixa de texto **Emissor**, cole o valor da **ID da Entidade SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a99b8-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a99b8-193">c.</span><span class="sxs-lookup"><span data-stu-id="a99b8-193">c.</span></span> <span data-ttu-id="a99b8-194">Para carregar o certificado baixado do Portal do Azure, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="a99b8-195">d.</span><span class="sxs-lookup"><span data-stu-id="a99b8-195">d.</span></span> <span data-ttu-id="a99b8-196">Na caixa de texto **ID da Entidade**, digite `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="a99b8-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="a99b8-197">e.</span><span class="sxs-lookup"><span data-stu-id="a99b8-197">e.</span></span> <span data-ttu-id="a99b8-198">Para o **Tipo de Identidade SAML**, selecione **A declaração contém a ID de Federação do objeto de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="a99b8-199">f.</span><span class="sxs-lookup"><span data-stu-id="a99b8-199">f.</span></span> <span data-ttu-id="a99b8-200">Para **Local de Identidade do SAML**, selecione **A identidade está contida no elemento NameIdentifier da instrução Subject**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="a99b8-201">g.</span><span class="sxs-lookup"><span data-stu-id="a99b8-201">g.</span></span> <span data-ttu-id="a99b8-202">Na caixa de texto **URL de Logon do Provedor de Identidade**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a99b8-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a99b8-203">h.</span><span class="sxs-lookup"><span data-stu-id="a99b8-203">h.</span></span> <span data-ttu-id="a99b8-204">Na caixa de texto **URL de Logoff do Provedor de Identidade**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a99b8-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a99b8-205">i.</span><span class="sxs-lookup"><span data-stu-id="a99b8-205">i.</span></span> <span data-ttu-id="a99b8-206">Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="a99b8-207">j.</span><span class="sxs-lookup"><span data-stu-id="a99b8-207">j.</span></span> <span data-ttu-id="a99b8-208">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-208">Click **Save**.</span></span>

16. <span data-ttu-id="a99b8-209">No painel de navegação à esquerda, no portal clássico do Work.com, clique em **Gerenciamento de Domínio** para expandir a seção correspondente e clique em **Meu Domínio** para abrir a página **Meu Domínio**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="a99b8-210">![Meu Domínio](./media/active-directory-saas-work-com-tutorial/ic794115.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="a99b8-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="a99b8-211">Na página **Meu Domínio**, na seção **Identidade Visual da Página de Logon**, clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="a99b8-212">![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic767826.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="a99b8-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="a99b8-213">Na página **Identidade Visual da Página de Logon**, na seção **Serviço de Autenticação**, o nome das **Configurações de SSO do SAML** é exibido.</span><span class="sxs-lookup"><span data-stu-id="a99b8-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="a99b8-214">Selecione-o e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="a99b8-215">![Identidade Visual da Página de Logon](./media/active-directory-saas-work-com-tutorial/ic784366.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="a99b8-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="a99b8-216">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a99b8-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a99b8-217">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a99b8-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a99b8-218">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a99b8-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a99b8-219">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-219">Create an Azure AD test user</span></span>
<span data-ttu-id="a99b8-220">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a99b8-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a99b8-222">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a99b8-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a99b8-223">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a99b8-225">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a99b8-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Usuários e grupos -> Todos os usuários](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a99b8-227">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Adicionar](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a99b8-229">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a99b8-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Página da caixa de diálogo do usuário](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a99b8-231">a.</span><span class="sxs-lookup"><span data-stu-id="a99b8-231">a.</span></span> <span data-ttu-id="a99b8-232">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a99b8-233">b.</span><span class="sxs-lookup"><span data-stu-id="a99b8-233">b.</span></span> <span data-ttu-id="a99b8-234">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a99b8-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a99b8-235">c.</span><span class="sxs-lookup"><span data-stu-id="a99b8-235">c.</span></span> <span data-ttu-id="a99b8-236">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a99b8-237">d.</span><span class="sxs-lookup"><span data-stu-id="a99b8-237">d.</span></span> <span data-ttu-id="a99b8-238">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="a99b8-239">Criar um usuário de teste do Work.com</span><span class="sxs-lookup"><span data-stu-id="a99b8-239">Create a Work.com test user</span></span>
<span data-ttu-id="a99b8-240">Para que os usuários do Active Directory do Azure possam entrar, eles devem ser provisionados para Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="a99b8-241">No caso do Work.com, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a99b8-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="a99b8-242">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a99b8-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="a99b8-243">Faça logon no site da sua empresa do Work.com como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a99b8-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="a99b8-244">Vá para **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="a99b8-245">![Configuração](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="a99b8-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="a99b8-246">Vá para **Gerenciar Usuários \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="a99b8-247">![Gerenciar Usuários](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="a99b8-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="a99b8-248">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-248">Click **New User**.</span></span>
   
    <span data-ttu-id="a99b8-249">![Todos os Usuários](./media/active-directory-saas-work-com-tutorial/IC794117.png "Todos os Usuários")</span><span class="sxs-lookup"><span data-stu-id="a99b8-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="a99b8-250">Na seção Editar Usuários, execute as etapas a seguir nos atributos de uma conta do Azure AD válida que você deseja provisionar nas caixas de texto relacionadas:</span><span class="sxs-lookup"><span data-stu-id="a99b8-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="a99b8-251">![Editar Usuário](./media/active-directory-saas-work-com-tutorial/ic794118.png "Editar Usuário")</span><span class="sxs-lookup"><span data-stu-id="a99b8-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="a99b8-252">a.</span><span class="sxs-lookup"><span data-stu-id="a99b8-252">a.</span></span> <span data-ttu-id="a99b8-253">Na caixa de texto **Nome**, digite o **nome** do usuário, **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="a99b8-254">b.</span><span class="sxs-lookup"><span data-stu-id="a99b8-254">b.</span></span> <span data-ttu-id="a99b8-255">Na caixa de texto **Sobrenome**, digite o **sobrenome** do usuário, **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="a99b8-256">c.</span><span class="sxs-lookup"><span data-stu-id="a99b8-256">c.</span></span> <span data-ttu-id="a99b8-257">Na caixa de texto **Alias**, digite o **nome** do usuário, **BrendaF**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="a99b8-258">d.</span><span class="sxs-lookup"><span data-stu-id="a99b8-258">d.</span></span> <span data-ttu-id="a99b8-259">Na caixa de texto **Email**, digite o **endereço de email** do usuário, **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="a99b8-260">e.</span><span class="sxs-lookup"><span data-stu-id="a99b8-260">e.</span></span> <span data-ttu-id="a99b8-261">Na caixa de texto **Nome de Usuário**, digite um nome de usuário do usuário, assim como **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="a99b8-262">f.</span><span class="sxs-lookup"><span data-stu-id="a99b8-262">f.</span></span> <span data-ttu-id="a99b8-263">Na caixa de texto **Apelido**, digite um **apelido** para o usuário, assim como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="a99b8-264">g.</span><span class="sxs-lookup"><span data-stu-id="a99b8-264">g.</span></span> <span data-ttu-id="a99b8-265">Selecione **Função**, **Licença de Usuário** e **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="a99b8-266">h.</span><span class="sxs-lookup"><span data-stu-id="a99b8-266">h.</span></span> <span data-ttu-id="a99b8-267">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="a99b8-268">O titular da conta do Azure AD receberá um email com um link de confirmação de conta para que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="a99b8-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a99b8-269">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99b8-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="a99b8-270">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a99b8-272">**Para atribuir Brenda Fernandes ao Work.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a99b8-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="a99b8-273">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a99b8-275">Na lista de aplicativos, selecione **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com na lista do aplicativo](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="a99b8-277">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a99b8-279">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a99b8-279">Click **Add** button.</span></span> <span data-ttu-id="a99b8-280">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a99b8-282">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a99b8-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a99b8-283">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a99b8-284">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a99b8-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a99b8-285">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="a99b8-285">Test single sign-on</span></span>

<span data-ttu-id="a99b8-286">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a99b8-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a99b8-287">Quando você clica no bloco Work.com no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Work.com.</span><span class="sxs-lookup"><span data-stu-id="a99b8-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="a99b8-288">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a99b8-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a99b8-289">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a99b8-289">Additional resources</span></span>

* [<span data-ttu-id="a99b8-290">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a99b8-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a99b8-291">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a99b8-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

