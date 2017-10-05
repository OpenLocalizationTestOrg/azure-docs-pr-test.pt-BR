---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e SSO do SAML para Jira da Resolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="1d769-103">Tutorial: Integração do Azure Active Directory com o SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="1d769-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="1d769-104">Neste tutorial, você aprenderá a integrar o SSO do SAML para Jira da Resolution GmbH com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1d769-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d769-105">A integração de SSO do SAML para Jira da Resolution GmbH com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1d769-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d769-106">Você pode controlar no Azure AD quem tem acesso ao SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="1d769-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="1d769-107">Você pode habilitar os usuários a entrarem automaticamente no SSO do SAML para Jira da Resolution GmbH (logon único) com as próprias contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d769-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d769-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1d769-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d769-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d769-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d769-110">Prerequisites</span></span>

<span data-ttu-id="1d769-111">Para configurar a integração do Azure AD com o SSO de SAML para Jira da Resolution GmbH, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1d769-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="1d769-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d769-113">Uma assinatura habilitada para logon único do SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="1d769-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d769-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1d769-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d769-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1d769-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d769-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1d769-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d769-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d769-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d769-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1d769-118">Scenario description</span></span>
<span data-ttu-id="1d769-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1d769-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d769-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1d769-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d769-121">Adicionar o SSO do SAML para Jira da Resolution GmbH da galeria</span><span class="sxs-lookup"><span data-stu-id="1d769-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="1d769-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="1d769-123">Adicionar o SSO do SAML para Jira da Resolution GmbH da galeria</span><span class="sxs-lookup"><span data-stu-id="1d769-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="1d769-124">Para configurar a integração do SSO do SAML para Jira da Resolution GmbH no Azure AD, adicione o SSO do SAML para Jira da Resolution GmbH da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1d769-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d769-125">**Para adicionar SSO do SAML para Jira da Resolution GmbH da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d769-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d769-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d769-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d769-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1d769-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d769-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1d769-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1d769-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1d769-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1d769-133">Na caixa de pesquisa, digite **SSO do SAML para Jira da Resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="1d769-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="1d769-135">No painel resultados, selecione **SSO do SAML para Jira da Resolution GmbH** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1d769-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d769-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d769-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Jira da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="1d769-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1d769-139">Para o logon único funcionar, o Azure AD precisa saber que o usuário da contraparte no SSO do SAML para Jira da Resolution GmbH é para um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d769-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="1d769-140">Em outras palavras, uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SSO do SAML para Jira da Resolution GmbH precisa ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1d769-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="1d769-141">No SSO do SAML para Jira da Resolution GmbH, atribua o valor de **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1d769-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1d769-142">Para configurar e testar o logon único do Azure AD com o SSO de SAML para Jira da Resolution GmbH, conclua os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1d769-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d769-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1d769-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d769-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d769-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d769-145">**[Criar um usuário de teste de SSO do SAML para Jira da Resolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  – para ter um equivalente de Brenda Fernandes no SSO do SAML para Jira da Resolution GmbH vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d769-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d769-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d769-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d769-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1d769-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d769-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d769-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d769-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo SSO do SAML para Jira da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="1d769-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="1d769-150">**Para configurar o logon único do Azure AD com o SSO de SAML para Jira da Resolution GmbH, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d769-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="1d769-151">No portal do Azure, na página de integração de aplicativo **SSO do SAML para Jira da Resolution GmbH**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1d769-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1d769-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1d769-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="1d769-155">Na seção **Domínio e URLs do SSO do SAML para Jira da Resolution GmbH**, se quiser configurar o aplicativo no modo iniciado **IDP**:</span><span class="sxs-lookup"><span data-stu-id="1d769-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="1d769-157">a.</span><span class="sxs-lookup"><span data-stu-id="1d769-157">a.</span></span> <span data-ttu-id="1d769-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1d769-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="1d769-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d769-159">b.</span></span> <span data-ttu-id="1d769-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1d769-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="1d769-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="1d769-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1d769-162">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="1d769-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="1d769-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1d769-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1d769-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1d769-165">These values are not real.</span></span> <span data-ttu-id="1d769-166">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="1d769-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1d769-167">Entre em contato com a [equipe de suporte ao Cliente do SSO do SAML para Jira da Resolution GmbH](https://www.resolution.de/go/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="1d769-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="1d769-168">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1d769-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="1d769-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1d769-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1d769-172">Em uma janela diferente do navegador da Web, faça logon no **portal do administrador do SSO do SAML para Jira da Resolution GmbH** como administrador.</span><span class="sxs-lookup"><span data-stu-id="1d769-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="1d769-173">Passe o cursor do mouse sobre a engrenagem e clique em **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="1d769-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="1d769-175">Você é redirecionado à página de Acesso de Administrador.</span><span class="sxs-lookup"><span data-stu-id="1d769-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="1d769-176">Insira a **Senha** e clique no botão **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="1d769-178">Na seção da guia Complementos, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="1d769-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="1d769-179">Pesquise **SSO (Logon Único) do SAML para JIRA** e clique no botão **Instalar** para instalar o novo plug-in do SAML.</span><span class="sxs-lookup"><span data-stu-id="1d769-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="1d769-181">A instalação do plug-in será iniciada.</span><span class="sxs-lookup"><span data-stu-id="1d769-181">The plugin installation will start.</span></span> <span data-ttu-id="1d769-182">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="1d769-182">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="1d769-185">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-185">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="1d769-187">Clique em **Configurar** para configurar o novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="1d769-187">Click **Configure** to configure the new plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="1d769-189">Em **Configuração de Plug-in de Logon Único do SAML**, clique no botão **Adicionar Provedor de Identidade adicional** para definir as configurações do Provedor de Identidade.</span><span class="sxs-lookup"><span data-stu-id="1d769-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="1d769-191">Execute as seguintes etapas nesta página:</span><span class="sxs-lookup"><span data-stu-id="1d769-191">Perform following steps on this page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="1d769-193">a.</span><span class="sxs-lookup"><span data-stu-id="1d769-193">a.</span></span> <span data-ttu-id="1d769-194">Adicionar **Nome** do Provedor de Identidade (por exemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d769-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="1d769-195">b.</span><span class="sxs-lookup"><span data-stu-id="1d769-195">b.</span></span> <span data-ttu-id="1d769-196">Adicionar **Descrição** do Provedor de Identidade (por exemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d769-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="1d769-197">c.</span><span class="sxs-lookup"><span data-stu-id="1d769-197">c.</span></span> <span data-ttu-id="1d769-198">Clique em **XML** e selecione o arquivo **Metadados**, que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d769-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1d769-199">d.</span><span class="sxs-lookup"><span data-stu-id="1d769-199">d.</span></span> <span data-ttu-id="1d769-200">Clique no botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-200">Click **Load** button.</span></span>

    <span data-ttu-id="1d769-201">e.</span><span class="sxs-lookup"><span data-stu-id="1d769-201">e.</span></span> <span data-ttu-id="1d769-202">Ele lê os metadados IdP e preenche os campos conforme destacado na captura de tela.</span><span class="sxs-lookup"><span data-stu-id="1d769-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="1d769-203">Clique no botão **Salvar Configurações** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="1d769-203">Click **Save settings** button to save the settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="1d769-205">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1d769-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d769-206">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1d769-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d769-207">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d769-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d769-208">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d769-209">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d769-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1d769-211">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d769-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d769-212">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d769-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d769-214">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1d769-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d769-216">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d769-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d769-218">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1d769-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d769-220">a.</span><span class="sxs-lookup"><span data-stu-id="1d769-220">a.</span></span> <span data-ttu-id="1d769-221">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1d769-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d769-222">b.</span><span class="sxs-lookup"><span data-stu-id="1d769-222">b.</span></span> <span data-ttu-id="1d769-223">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d769-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d769-224">c.</span><span class="sxs-lookup"><span data-stu-id="1d769-224">c.</span></span> <span data-ttu-id="1d769-225">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1d769-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d769-226">d.</span><span class="sxs-lookup"><span data-stu-id="1d769-226">d.</span></span> <span data-ttu-id="1d769-227">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="1d769-228">Criando um usuário de teste do SSO do SAML para Jira da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="1d769-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="1d769-229">Para habilitar usuários do Azure AD a fazerem logon no SSO do SAML para Jira da Resolution GmbH, eles devem ser provisionados no SSO do SAML para Jira da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="1d769-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="1d769-230">No SSO do SAML para Jira da Resolution GmbH, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="1d769-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="1d769-231">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d769-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1d769-232">Faça logon no site da empresa do SAML SSO para Jira da Resolution GmbH como administrador.</span><span class="sxs-lookup"><span data-stu-id="1d769-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="1d769-233">Passe o cursor do mouse sobre a engrenagem e clique em **Gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="1d769-233">Hover on cog and click the **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="1d769-235">Você será redirecionado à página de acesso de administrador para inserir a **Senha** e clicar no botão **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="1d769-237">Na seção da guia **Gerenciamento de usuário**, clique em **criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="1d769-237">Under **User management** tab section, click **create user**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="1d769-239">Na página da caixa de diálogo **"Criar novo usuário"**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1d769-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="1d769-241">a.</span><span class="sxs-lookup"><span data-stu-id="1d769-241">a.</span></span> <span data-ttu-id="1d769-242">Na caixa de texto **Endereço de email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1d769-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1d769-243">b.</span><span class="sxs-lookup"><span data-stu-id="1d769-243">b.</span></span> <span data-ttu-id="1d769-244">Na caixa de texto **Nome completo**, digite o nome completo do usuário, como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d769-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="1d769-245">c.</span><span class="sxs-lookup"><span data-stu-id="1d769-245">c.</span></span> <span data-ttu-id="1d769-246">Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1d769-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1d769-247">d.</span><span class="sxs-lookup"><span data-stu-id="1d769-247">d.</span></span> <span data-ttu-id="1d769-248">Na caixa de texto **Senha**, digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="1d769-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="1d769-249">e.</span><span class="sxs-lookup"><span data-stu-id="1d769-249">e.</span></span> <span data-ttu-id="1d769-250">Clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="1d769-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d769-251">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d769-252">Nesta seção, habilite Brenda Fernandes a usar o logon único do Azure concedendo acesso ao SSO do SAML para Jira da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="1d769-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1d769-254">**Para atribuir Brenda Fernandes ao SSO do SAML para Jira da Resolution GmbH, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d769-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="1d769-255">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1d769-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1d769-257">Na lista de aplicativos, selecione **SSO do SAML para Jira da Resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="1d769-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="1d769-259">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d769-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1d769-261">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1d769-261">Click **Add** button.</span></span> <span data-ttu-id="1d769-262">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d769-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1d769-264">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1d769-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d769-265">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d769-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d769-266">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d769-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d769-267">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1d769-267">Testing single sign-on</span></span>

<span data-ttu-id="1d769-268">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1d769-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d769-269">Ao clicar no bloco SSO do SAML para Jira da Resolution GmbH no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo SSO do SAML para Jira da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="1d769-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="1d769-270">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d769-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1d769-271">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1d769-271">Additional resources</span></span>

* [<span data-ttu-id="1d769-272">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1d769-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d769-273">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1d769-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

