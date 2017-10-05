---
title: "Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o JIRA | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SSO do Kantega para o JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 06a1d301818f025270137f7eaa9f40e5e4503112
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="c55d1-103">Tutorial: Integração do Azure Active Directory ao SSO do Kantega para o JIRA</span><span class="sxs-lookup"><span data-stu-id="c55d1-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="c55d1-104">Neste tutorial, você aprende a integrar o SSO do Kantega para o JIRA ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c55d1-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c55d1-105">A integração do SSO do Kantega para o JIRA ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c55d1-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c55d1-106">No Azure AD, é possível controlar quem tem acesso ao SSO do Kantega para o JIRA</span><span class="sxs-lookup"><span data-stu-id="c55d1-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span></span>
- <span data-ttu-id="c55d1-107">É possível permitir que os usuários se conectem automaticamente ao SSO do Kantega para o JIRA (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c55d1-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c55d1-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c55d1-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c55d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c55d1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c55d1-110">Prerequisites</span></span>

<span data-ttu-id="c55d1-111">Para configurar a integração do Azure AD ao SSO do Kantega para o JIRA, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c55d1-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span></span>

- <span data-ttu-id="c55d1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c55d1-113">Uma assinatura habilitada para logon único do SSO do Kantega para o JIRA</span><span class="sxs-lookup"><span data-stu-id="c55d1-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c55d1-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c55d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c55d1-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c55d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c55d1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c55d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c55d1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c55d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c55d1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c55d1-118">Scenario description</span></span>
<span data-ttu-id="c55d1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c55d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c55d1-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c55d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c55d1-121">Adicionando o SSO do Kantega para o JIRA por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c55d1-121">Adding Kantega SSO for JIRA from the gallery</span></span>
2. <span data-ttu-id="c55d1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-the-gallery"></a><span data-ttu-id="c55d1-123">Adicionando o SSO do Kantega para o JIRA por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="c55d1-123">Adding Kantega SSO for JIRA from the gallery</span></span>
<span data-ttu-id="c55d1-124">Para configurar a integração do SSO do Kantega para o JIRA ao Azure AD, é necessário adicionar o SSO do Kantega para o JIRA à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="c55d1-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c55d1-125">**Para adicionar o SSO do Kantega para o JIRA por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c55d1-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c55d1-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c55d1-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c55d1-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c55d1-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c55d1-133">Na caixa de pesquisa, digite **SSO do Kantega para o JIRA**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-133">In the search box, type **Kantega SSO for JIRA**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="c55d1-135">No painel de resultados, selecione **SSO do Kantega para o JIRA** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c55d1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c55d1-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO do Kantega para o JIRA, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c55d1-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c55d1-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SSO do Kantega para o JIRA é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c55d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span></span> <span data-ttu-id="c55d1-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SSO do Kantega para o JIRA.</span><span class="sxs-lookup"><span data-stu-id="c55d1-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span></span>

<span data-ttu-id="c55d1-141">No SSO do Kantega para o JIRA, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c55d1-142">Para configurar e testar o logon único do Azure AD com o SSO do Kantega para o JIRA, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c55d1-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c55d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c55d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c55d1-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c55d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c55d1-145">**[Criando um usuário de teste do SSO do Kantega para o JIRA](#creating-a-kantega-sso-for-jira-test-user)** – para ter um equivalente de Brenda Fernandes no SSO do Kantega para o JIRA que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c55d1-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c55d1-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c55d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c55d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c55d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c55d1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c55d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c55d1-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SSO do Kantega para o JIRA.</span><span class="sxs-lookup"><span data-stu-id="c55d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="c55d1-150">**Para configurar o logon único do Azure AD com o SSO do Kantega para o JIRA, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c55d1-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="c55d1-151">No portal do Azure, na página de integração do aplicativo **SSO do Kantega para o JIRA**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c55d1-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c55d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="c55d1-155">No modo iniciado pelo **IDP**, na seção **Domínio e URLs do SSO do Kantega para o JIRA**, realize a seguinte etapa:</span><span class="sxs-lookup"><span data-stu-id="c55d1-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="c55d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-157">a.</span></span> <span data-ttu-id="c55d1-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="c55d1-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="c55d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-159">b.</span></span> <span data-ttu-id="c55d1-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="c55d1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="c55d1-161">No modo iniciado pelo **SP**, marque a opção **Mostrar configurações de URL avançadas** e realize a seguinte etapa:</span><span class="sxs-lookup"><span data-stu-id="c55d1-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="c55d1-163">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="c55d1-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c55d1-164">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c55d1-164">These values are not real.</span></span> <span data-ttu-id="c55d1-165">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="c55d1-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c55d1-166">Esses valores são recebidos durante a configuração do plug-in do Jira, que é explicada adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="c55d1-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="c55d1-167">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c55d1-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="c55d1-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c55d1-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c55d1-171">Em outra janela do navegador da Web, faça logon no servidor local do JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="c55d1-171">In a different web browser window, log in to your JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="c55d1-172">Passe o cursor do mouse sobre a engrenagem e clique em **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="c55d1-174">Na seção da guia Complementos, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="c55d1-175">Pesquise **SSO do Kantega para o JIRA (SAML e Kerberos)** e clique no botão **Instalar** para instalar o novo plug-in do SAML.</span><span class="sxs-lookup"><span data-stu-id="c55d1-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="c55d1-177">A instalação do plug-in é iniciada.</span><span class="sxs-lookup"><span data-stu-id="c55d1-177">The plugin installation starts.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="c55d1-179">Quando a instalação for concluída.</span><span class="sxs-lookup"><span data-stu-id="c55d1-179">Once the installation is complete.</span></span> <span data-ttu-id="c55d1-180">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="c55d1-180">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="c55d1-182">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-182">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="c55d1-184">O novo plug-in é listado em **INTEGRAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="c55d1-185">Clique em **Configurar** para configurar o novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="c55d1-185">Click **Configure** to configure the new plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="c55d1-187">Na seção **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-187">In the **SAML** section.</span></span> <span data-ttu-id="c55d1-188">Selecione **Azure AD (Azure Active Directory)** na lista suspensa **Adicionar provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="c55d1-190">Selecione o nível de assinatura como **Básico**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-190">Select subscription level as **Basic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="c55d1-192">Na seção **Propriedades do aplicativo**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-192">On the **App properties** section, perform following steps:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="c55d1-194">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-194">a.</span></span> <span data-ttu-id="c55d1-195">Copie o valor da **URI da ID do Aplicativo** e use-o como **o Identificador, a URL de Resposta e a URL de Logon** na seção **Domínio e URLs do SSO do Kantega para o JIRA** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c55d1-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="c55d1-196">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-196">b.</span></span> <span data-ttu-id="c55d1-197">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-197">Click **Next**.</span></span>

17. <span data-ttu-id="c55d1-198">Na seção **Importação de metadados**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-198">On the **Metadata import** section, perform following steps:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="c55d1-200">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-200">a.</span></span> <span data-ttu-id="c55d1-201">Selecione **Arquivo de metadados no meu computador** e carregue um arquivo de metadados baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c55d1-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c55d1-202">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-202">b.</span></span> <span data-ttu-id="c55d1-203">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-203">Click **Next**.</span></span>

18. <span data-ttu-id="c55d1-204">Na seção **Nome e localização de SSO**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="c55d1-206">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-206">a.</span></span> <span data-ttu-id="c55d1-207">Adicione Nome do Provedor de Identidade à caixa de texto **Nome do provedor de identidade** (por exemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c55d1-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="c55d1-208">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-208">b.</span></span> <span data-ttu-id="c55d1-209">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-209">Click **Next**.</span></span>

19. <span data-ttu-id="c55d1-210">Verifique o Certificado de autenticação e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-210">Verify the Signing certificate and click **Next**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="c55d1-212">Na seção **Contas de usuário do JIRA**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-212">On the **JIRA user accounts** section, perform following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="c55d1-214">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-214">a.</span></span> <span data-ttu-id="c55d1-215">Selecione **Criar usuários no Diretório interno do JIRA, se necessário** e insira o nome apropriado do grupo de usuários (podem ser vários números</span><span class="sxs-lookup"><span data-stu-id="c55d1-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="c55d1-216">de grupos separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="c55d1-216">of groups separated by comma).</span></span>

    <span data-ttu-id="c55d1-217">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-217">b.</span></span> <span data-ttu-id="c55d1-218">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-218">Click **Next**.</span></span>

21. <span data-ttu-id="c55d1-219">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-219">Click **Finish**.</span></span>   

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="c55d1-221">Na seção **Domínios conhecidos do Azure AD**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="c55d1-223">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-223">a.</span></span> <span data-ttu-id="c55d1-224">Selecione **Domínios conhecidos** no painel esquerdo da página.</span><span class="sxs-lookup"><span data-stu-id="c55d1-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="c55d1-225">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-225">b.</span></span> <span data-ttu-id="c55d1-226">Insira o nome de domínio na caixa de texto **Domínios conhecidos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="c55d1-227">c.</span><span class="sxs-lookup"><span data-stu-id="c55d1-227">c.</span></span> <span data-ttu-id="c55d1-228">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="c55d1-229">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c55d1-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c55d1-230">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c55d1-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c55d1-231">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c55d1-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c55d1-232">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="c55d1-233">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c55d1-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c55d1-235">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c55d1-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c55d1-236">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c55d1-238">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c55d1-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c55d1-240">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c55d1-242">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c55d1-244">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-244">a.</span></span> <span data-ttu-id="c55d1-245">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c55d1-246">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-246">b.</span></span> <span data-ttu-id="c55d1-247">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c55d1-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c55d1-248">c.</span><span class="sxs-lookup"><span data-stu-id="c55d1-248">c.</span></span> <span data-ttu-id="c55d1-249">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c55d1-250">d.</span><span class="sxs-lookup"><span data-stu-id="c55d1-250">d.</span></span> <span data-ttu-id="c55d1-251">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="c55d1-252">Criando um usuário de teste do SSO do Kantega para o JIRA</span><span class="sxs-lookup"><span data-stu-id="c55d1-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="c55d1-253">Para permitir que os usuários do Azure AD façam logon no JIRA, eles devem ser provisionados no JIRA.</span><span class="sxs-lookup"><span data-stu-id="c55d1-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="c55d1-254">No SSO do Kantega para o JIRA, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c55d1-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="c55d1-255">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c55d1-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c55d1-256">Faça logon no servidor local do JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="c55d1-256">Log in to your JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="c55d1-257">Passe o cursor do mouse sobre a engrenagem e clique em **Gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-257">Hover on cog and click the **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="c55d1-259">Na seção da guia **Gerenciamento de usuário**, clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="c55d1-261">Na página da caixa de diálogo **"Criar novo usuário"**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c55d1-261">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="c55d1-263">a.</span><span class="sxs-lookup"><span data-stu-id="c55d1-263">a.</span></span> <span data-ttu-id="c55d1-264">Na caixa de texto **Endereço de email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c55d1-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="c55d1-265">b.</span><span class="sxs-lookup"><span data-stu-id="c55d1-265">b.</span></span> <span data-ttu-id="c55d1-266">Na caixa de texto **Nome completo**, digite o nome completo do usuário, como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c55d1-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="c55d1-267">c.</span><span class="sxs-lookup"><span data-stu-id="c55d1-267">c.</span></span> <span data-ttu-id="c55d1-268">Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c55d1-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="c55d1-269">d.</span><span class="sxs-lookup"><span data-stu-id="c55d1-269">d.</span></span> <span data-ttu-id="c55d1-270">Na caixa de texto **Senha**, digite a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="c55d1-270">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="c55d1-271">e.</span><span class="sxs-lookup"><span data-stu-id="c55d1-271">e.</span></span> <span data-ttu-id="c55d1-272">Clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-272">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c55d1-273">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c55d1-274">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao SSO do Kantega para o JIRA.</span><span class="sxs-lookup"><span data-stu-id="c55d1-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c55d1-276">**Para atribuir Brenda Fernandes ao SSO do Kantega para o JIRA, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c55d1-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="c55d1-277">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c55d1-279">Na lista de aplicativos, selecione **SSO do Kantega para o JIRA**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-279">In the applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="c55d1-281">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c55d1-283">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c55d1-283">Click **Add** button.</span></span> <span data-ttu-id="c55d1-284">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c55d1-286">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c55d1-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c55d1-287">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c55d1-288">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c55d1-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c55d1-289">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c55d1-289">Testing single sign-on</span></span>

<span data-ttu-id="c55d1-290">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c55d1-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c55d1-291">Quando você clicar no bloco do SSO do Kantega para o JIRA no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo SSO do Kantega para o JIRA.</span><span class="sxs-lookup"><span data-stu-id="c55d1-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="c55d1-292">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c55d1-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c55d1-293">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c55d1-293">Additional resources</span></span>

* [<span data-ttu-id="c55d1-294">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c55d1-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c55d1-295">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c55d1-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

