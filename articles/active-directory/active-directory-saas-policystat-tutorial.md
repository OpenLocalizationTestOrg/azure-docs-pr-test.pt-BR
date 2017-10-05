---
title: "Tutorial: Integração do Azure Active Directory ao PolicyStat | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="a867f-103">Tutorial: Integração do Azure Active Directory ao PolicyStat</span><span class="sxs-lookup"><span data-stu-id="a867f-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="a867f-104">Neste tutorial, você aprende a integrar o PolicyStat ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a867f-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a867f-105">A integração do PolicyStat ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a867f-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a867f-106">No Azure AD, é possível controlar quem tem acesso ao PolicyStat</span><span class="sxs-lookup"><span data-stu-id="a867f-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="a867f-107">É possível permitir que os usuários se conectem automaticamente ao PolicyStat (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a867f-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a867f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a867f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a867f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a867f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a867f-110">Prerequisites</span></span>

<span data-ttu-id="a867f-111">Para configurar a integração do Azure AD ao PolicyStat, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a867f-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="a867f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a867f-113">Uma assinatura habilitada para logon único do PolicyStat</span><span class="sxs-lookup"><span data-stu-id="a867f-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a867f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a867f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a867f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a867f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a867f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a867f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a867f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a867f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a867f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a867f-118">Scenario description</span></span>
<span data-ttu-id="a867f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a867f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a867f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="a867f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a867f-121">Adicionando o PolicyStat por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="a867f-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="a867f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="a867f-123">Adicionando o PolicyStat por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="a867f-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="a867f-124">Para configurar a integração do PolicyStat ao Azure AD, é necessário adicionar o PolicyStat à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="a867f-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a867f-125">**Para adicionar o PolicyStat por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a867f-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a867f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a867f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a867f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a867f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a867f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a867f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a867f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a867f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a867f-133">Na caixa de pesquisa, digite **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="a867f-133">In the search box, type **PolicyStat**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="a867f-135">No painel de resultados, selecione **PolicyStat** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a867f-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a867f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a867f-138">Nesta seção, você configura e testa o logon único do Azure AD com o PolicyStat, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a867f-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a867f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do PolicyStat é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a867f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="a867f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="a867f-141">No PolicyStat, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="a867f-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a867f-142">Para configurar e testar o logon único do Azure AD com o PolicyStat, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="a867f-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a867f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a867f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a867f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a867f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a867f-145">**[Criando um usuário de teste do PolicyStat](#creating-a-policystat-test-user)** – para ter um equivalente de Brenda Fernandes no PolicyStat que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a867f-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a867f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a867f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a867f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="a867f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a867f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a867f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a867f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="a867f-150">**Para configurar o logon único do Azure AD com o PolicyStat, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a867f-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="a867f-151">No portal do Azure, na página de integração do aplicativo **PolicyStat**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="a867f-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a867f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="a867f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="a867f-155">Na seção **Domínio e URLs do PolicyStat**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a867f-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="a867f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a867f-157">a.</span></span> <span data-ttu-id="a867f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="a867f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="a867f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a867f-159">b.</span></span> <span data-ttu-id="a867f-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="a867f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a867f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="a867f-161">These values are not real.</span></span> <span data-ttu-id="a867f-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="a867f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a867f-163">Contate a [equipe de suporte ao Cliente do PolicyStat](http://www.policystat.com/support/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="a867f-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="a867f-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a867f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="a867f-166">O objetivo desta seção é descrever como permitir que os usuários se autentiquem no PolicyStat com sua conta do AD do Azure usando federação baseada em protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="a867f-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="a867f-167">O aplicativo PolicyStat espera que as declarações SAML estejam em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração de **Atributos do Token SAML**.</span><span class="sxs-lookup"><span data-stu-id="a867f-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="a867f-168">As capturas de tela a seguir mostram um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="a867f-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="a867f-169">![Atributos](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="a867f-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="a867f-170">Para adicionar os mapeamentos de atributo necessários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a867f-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="a867f-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="a867f-171">Attribute Name</span></span>    |   <span data-ttu-id="a867f-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="a867f-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="a867f-173">uid</span><span class="sxs-lookup"><span data-stu-id="a867f-173">uid</span></span> | <span data-ttu-id="a867f-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="a867f-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="a867f-175">a.</span><span class="sxs-lookup"><span data-stu-id="a867f-175">a.</span></span> <span data-ttu-id="a867f-176">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="a867f-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="a867f-179">b.</span><span class="sxs-lookup"><span data-stu-id="a867f-179">b.</span></span> <span data-ttu-id="a867f-180">Na caixa de texto **Nome do Atributo**, digite **uid**.</span><span class="sxs-lookup"><span data-stu-id="a867f-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="a867f-181">c.</span><span class="sxs-lookup"><span data-stu-id="a867f-181">c.</span></span> <span data-ttu-id="a867f-182">Na caixa de texto **Valor do Atributo**, selecione **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="a867f-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="a867f-183">d.</span><span class="sxs-lookup"><span data-stu-id="a867f-183">d.</span></span> <span data-ttu-id="a867f-184">Na lista **Email**, selecione **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="a867f-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="a867f-185">e.</span><span class="sxs-lookup"><span data-stu-id="a867f-185">e.</span></span> <span data-ttu-id="a867f-186">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="a867f-186">Click **Ok**</span></span>

7. <span data-ttu-id="a867f-187">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="a867f-187">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a867f-189">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do PolicyStat como administrador.</span><span class="sxs-lookup"><span data-stu-id="a867f-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="a867f-190">Clique na guia **Admin** e, em seguida, clique em **Configuração de Logon Único** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="a867f-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="a867f-191">![Menu Administrador](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu Administrador")</span><span class="sxs-lookup"><span data-stu-id="a867f-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="a867f-192">Na seção **Configuração**, selecione **Habilitar Integração de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="a867f-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="a867f-193">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a867f-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="a867f-194">Clique em **Configurar Atributos** e, em seguida, na seção **Configurar Atributos**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a867f-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a867f-195">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a867f-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="a867f-196">a.</span><span class="sxs-lookup"><span data-stu-id="a867f-196">a.</span></span> <span data-ttu-id="a867f-197">Na caixa de texto **Atributo do Nome de Usuário**, digite **uid**.</span><span class="sxs-lookup"><span data-stu-id="a867f-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="a867f-198">b.</span><span class="sxs-lookup"><span data-stu-id="a867f-198">b.</span></span> <span data-ttu-id="a867f-199">Na caixa de texto **Atributo de Nome**, digite o **firstname** do usuário **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="a867f-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="a867f-200">c.</span><span class="sxs-lookup"><span data-stu-id="a867f-200">c.</span></span> <span data-ttu-id="a867f-201">Na caixa de texto **Atributo de Sobrenome**, digite o **lastname** do usuário **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a867f-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="a867f-202">d.</span><span class="sxs-lookup"><span data-stu-id="a867f-202">d.</span></span> <span data-ttu-id="a867f-203">Na caixa de texto **Atributo de Email**, digite o **emailaddress** do usuário **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="a867f-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="a867f-204">e.</span><span class="sxs-lookup"><span data-stu-id="a867f-204">e.</span></span> <span data-ttu-id="a867f-205">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="a867f-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="a867f-206">Clique em **Seus Metadados do IDP** e, na seção **Seus Metadados do IDP**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a867f-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a867f-207">![Configuração de Logon Único](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuração de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="a867f-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="a867f-208">a.</span><span class="sxs-lookup"><span data-stu-id="a867f-208">a.</span></span> <span data-ttu-id="a867f-209">Abra o arquivo de metadados baixado, copie o conteúdo e, depois, cole-o na caixa de texto **Metadados do Provedor de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="a867f-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="a867f-210">b.</span><span class="sxs-lookup"><span data-stu-id="a867f-210">b.</span></span> <span data-ttu-id="a867f-211">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="a867f-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a867f-212">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="a867f-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a867f-213">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a867f-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a867f-214">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a867f-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a867f-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="a867f-216">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a867f-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a867f-218">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a867f-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a867f-219">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a867f-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a867f-221">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a867f-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a867f-223">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a867f-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a867f-225">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a867f-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a867f-227">a.</span><span class="sxs-lookup"><span data-stu-id="a867f-227">a.</span></span> <span data-ttu-id="a867f-228">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="a867f-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a867f-229">b.</span><span class="sxs-lookup"><span data-stu-id="a867f-229">b.</span></span> <span data-ttu-id="a867f-230">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="a867f-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a867f-231">c.</span><span class="sxs-lookup"><span data-stu-id="a867f-231">c.</span></span> <span data-ttu-id="a867f-232">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="a867f-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a867f-233">d.</span><span class="sxs-lookup"><span data-stu-id="a867f-233">d.</span></span> <span data-ttu-id="a867f-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a867f-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="a867f-235">Criando um usuário de teste do PolicyStat</span><span class="sxs-lookup"><span data-stu-id="a867f-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="a867f-236">Para permitir que os usuários do AD do Azure façam logon no PolicyStat, eles devem ser provisionados no PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="a867f-237">O PolicyStat dá suporte ao provisionamento de usuário just in time.</span><span class="sxs-lookup"><span data-stu-id="a867f-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="a867f-238">Isso significa que não é necessário adicionar usuários manualmente ao PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="a867f-239">Os usuários serão adicionados automaticamente ao fazerem seu primeiro logon por meio do SSO.</span><span class="sxs-lookup"><span data-stu-id="a867f-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="a867f-240">Você pode usar qualquer outra ferramenta de criação de conta de usuário do PolicyStat ou as APIs fornecidas pelo PolicyStat para provisionar contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a867f-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a867f-241">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a867f-242">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a867f-244">**Para atribuir Brenda Fernandes ao PolicyStat, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="a867f-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="a867f-245">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a867f-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a867f-247">Na lista de aplicativos, selecione **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="a867f-247">In the applications list, select **PolicyStat**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="a867f-249">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a867f-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a867f-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a867f-251">Click **Add** button.</span></span> <span data-ttu-id="a867f-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a867f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a867f-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="a867f-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a867f-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a867f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a867f-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a867f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a867f-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a867f-257">Testing single sign-on</span></span>

<span data-ttu-id="a867f-258">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="a867f-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a867f-259">Quando você clicar no bloco do PolicyStat no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="a867f-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="a867f-260">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a867f-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a867f-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a867f-261">Additional resources</span></span>

* [<span data-ttu-id="a867f-262">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a867f-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a867f-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a867f-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

