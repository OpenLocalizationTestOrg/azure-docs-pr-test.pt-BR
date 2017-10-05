---
title: "Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="ea19a-103">Tutorial: Integração do Azure Active Directory ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific</span><span class="sxs-lookup"><span data-stu-id="ea19a-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="ea19a-104">Neste tutorial, você aprende a integrar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ea19a-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea19a-105">A integração do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ea19a-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea19a-106">No Azure AD, você pode controlar quem tem acesso ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific</span><span class="sxs-lookup"><span data-stu-id="ea19a-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="ea19a-107">Você pode permitir que os usuários sejam conectados automaticamente ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea19a-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea19a-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea19a-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea19a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea19a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ea19a-110">Prerequisites</span></span>

<span data-ttu-id="ea19a-111">Para configurar a integração do Azure AD ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ea19a-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="ea19a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea19a-113">Uma assinatura do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ea19a-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea19a-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ea19a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea19a-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ea19a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea19a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ea19a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea19a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea19a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea19a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ea19a-118">Scenario description</span></span>
<span data-ttu-id="ea19a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ea19a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea19a-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ea19a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea19a-121">Adicionar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ea19a-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="ea19a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="ea19a-123">Adicionar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="ea19a-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="ea19a-124">Para configurar a integração do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific no Azure AD, você precisa adicionar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="ea19a-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea19a-125">**Para adicionar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ea19a-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea19a-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea19a-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea19a-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ea19a-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ea19a-133">Na caixa de pesquisa, digite **Sistema de Monitoramento de Temperatura Sem Fio SensoScientific**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="ea19a-135">No painel de resultados, selecione **Sistema de Monitoramento de Temperatura Sem Fio SensoScientific** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea19a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea19a-138">Nesta seção, você configura e testa o logon único do Azure AD com o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ea19a-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea19a-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea19a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="ea19a-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="ea19a-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD ao valor de **Nome de Usuário** no Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="ea19a-142">Para configurar e testar o logon único do Azure AD com o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ea19a-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea19a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ea19a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea19a-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ea19a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea19a-145">**[Criar um usuário de teste do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** – para ter um equivalente de Brenda Fernandes no Sistema de Monitoramento de Temperatura Sem Fio SensoScientific que está vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea19a-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea19a-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea19a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea19a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ea19a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea19a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea19a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea19a-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="ea19a-150">**Para configurar o logon único do Azure AD com o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ea19a-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="ea19a-151">No portal do Azure, na página de integração de aplicativos do **Sistema de Monitoramento de Temperatura Sem Fio SensoScientific**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ea19a-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ea19a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="ea19a-155">Na seção **Domínio e URLs do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific**, não é necessário executar nenhuma etapa, pois o aplicativo já está pré-integrado ao Azure:</span><span class="sxs-lookup"><span data-stu-id="ea19a-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="ea19a-157">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="ea19a-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="ea19a-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ea19a-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea19a-161">Na seção **Sistema de Monitoramento de Temperatura Sem Fio SensoScientific**, clique em **Configurar o Sistema de Monitoramento de Temperatura Sem Fio SensoScientific** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ea19a-162">Copie a **URL de Logoff, a ID de Entidade do SAML** e a **URL do Serviço de Logon Único do SAML** da **seção Referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ea19a-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="ea19a-164">Faça logon no aplicativo Sistema de Monitoramento de Temperatura Sem Fio SensoScientific como administrador.</span><span class="sxs-lookup"><span data-stu-id="ea19a-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="ea19a-165">No menu de navegação na parte superior, clique em **Configuração** e acesse **Configurar** em **Logon Único** para abrir as Configurações de Logon Único.</span><span class="sxs-lookup"><span data-stu-id="ea19a-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="ea19a-167">No formulário **Configurações de Logon Único**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ea19a-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="ea19a-168">a.</span><span class="sxs-lookup"><span data-stu-id="ea19a-168">a.</span></span> <span data-ttu-id="ea19a-169">Selecione **Nome do Emissor** como Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea19a-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="ea19a-170">b.</span><span class="sxs-lookup"><span data-stu-id="ea19a-170">b.</span></span> <span data-ttu-id="ea19a-171">Cole a **ID de Entidade do SAML** que você copiou do portal do Azure na caixa de texto URL do Emissor.</span><span class="sxs-lookup"><span data-stu-id="ea19a-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="ea19a-172">c.</span><span class="sxs-lookup"><span data-stu-id="ea19a-172">c.</span></span> <span data-ttu-id="ea19a-173">Cole a **URL de Serviço de Logon Único do SAML** que você copiou do portal do Azure na caixa de texto URL de Serviço de Logon Único.</span><span class="sxs-lookup"><span data-stu-id="ea19a-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="ea19a-174">d.</span><span class="sxs-lookup"><span data-stu-id="ea19a-174">d.</span></span> <span data-ttu-id="ea19a-175">Cole a **URL de Logoff** que você copiou do portal do Azure na caixa de texto URL de Serviço de Logon Único.</span><span class="sxs-lookup"><span data-stu-id="ea19a-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="ea19a-176">e.</span><span class="sxs-lookup"><span data-stu-id="ea19a-176">e.</span></span> <span data-ttu-id="ea19a-177">Procure o certificado que você baixou do portal do Azure e carregue-o aqui.</span><span class="sxs-lookup"><span data-stu-id="ea19a-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="ea19a-178">f.</span><span class="sxs-lookup"><span data-stu-id="ea19a-178">f.</span></span> <span data-ttu-id="ea19a-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="ea19a-180">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ea19a-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea19a-181">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ea19a-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea19a-182">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea19a-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea19a-183">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea19a-184">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ea19a-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ea19a-186">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ea19a-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea19a-187">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea19a-189">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ea19a-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea19a-191">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea19a-193">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ea19a-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea19a-195">a.</span><span class="sxs-lookup"><span data-stu-id="ea19a-195">a.</span></span> <span data-ttu-id="ea19a-196">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea19a-197">b.</span><span class="sxs-lookup"><span data-stu-id="ea19a-197">b.</span></span> <span data-ttu-id="ea19a-198">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ea19a-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea19a-199">c.</span><span class="sxs-lookup"><span data-stu-id="ea19a-199">c.</span></span> <span data-ttu-id="ea19a-200">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea19a-201">d.</span><span class="sxs-lookup"><span data-stu-id="ea19a-201">d.</span></span> <span data-ttu-id="ea19a-202">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="ea19a-203">Criando um usuário de teste do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific</span><span class="sxs-lookup"><span data-stu-id="ea19a-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="ea19a-204">Para permitir que os usuários do Azure AD façam logon no Sistema de Monitoramento de Temperatura Sem Fio SensoScientific, eles devem ser provisionados no Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="ea19a-205">Trabalhe com a [equipe de suporte do Sistema de Monitoramento de Temperatura Sem Fio SensoScientific](https://www.sensoscientific.com/contact-us/) para adicionar os usuários à plataforma Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="ea19a-206">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ea19a-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea19a-207">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea19a-208">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ea19a-210">**Para atribuir Brenda Fernandes ao Sistema de Monitoramento de Temperatura Sem Fio SensoScientific, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ea19a-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="ea19a-211">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ea19a-213">Na lista de aplicativos, selecione **Sistema de Monitoramento de Temperatura Sem Fio SensoScientific**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="ea19a-215">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ea19a-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ea19a-217">Click **Add** button.</span></span> <span data-ttu-id="ea19a-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ea19a-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ea19a-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea19a-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea19a-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea19a-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea19a-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ea19a-223">Testing single sign-on</span></span>

<span data-ttu-id="ea19a-224">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ea19a-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="ea19a-225">Clique no bloco Sistema de Monitoramento de Temperatura Sem Fio SensoScientific no Painel de Acesso e você será automaticamente conectado ao aplicativo Sistema de Monitoramento de Temperatura Sem Fio SensoScientific.</span><span class="sxs-lookup"><span data-stu-id="ea19a-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="ea19a-226">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ea19a-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea19a-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ea19a-227">Additional resources</span></span>

* [<span data-ttu-id="ea19a-228">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ea19a-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea19a-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea19a-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

