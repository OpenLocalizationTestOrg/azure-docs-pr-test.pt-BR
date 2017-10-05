---
title: "Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e SSO do SAML para Confluence da Resolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="2aeee-103">Tutorial: Integração do Azure Active Directory com o SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="2aeee-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="2aeee-104">Neste tutorial, você aprenderá a integrar o SSO do SAML para Confluence da Resolution GmbH com o Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2aeee-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2aeee-105">A integração de SSO do SAML para Confluence da Resolution GmbH com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="2aeee-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2aeee-106">Você pode controlar no Azure AD quem tem acesso ao SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="2aeee-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="2aeee-107">Você pode habilitar os usuários a entrarem automaticamente no SSO do SAML para Confluence da Resolution GmbH (logon único) com as próprias contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aeee-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2aeee-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2aeee-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2aeee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aeee-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2aeee-110">Prerequisites</span></span>

<span data-ttu-id="2aeee-111">Para configurar a integração do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2aeee-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="2aeee-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2aeee-113">Uma assinatura habilitada para logon único do SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="2aeee-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2aeee-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2aeee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2aeee-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2aeee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2aeee-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2aeee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2aeee-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2aeee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2aeee-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2aeee-118">Scenario description</span></span>
<span data-ttu-id="2aeee-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2aeee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2aeee-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="2aeee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2aeee-121">Adicionando o SSO do SAML para Confluence da Resolution GmbH da galeria</span><span class="sxs-lookup"><span data-stu-id="2aeee-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="2aeee-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="2aeee-123">Adicionando o SSO do SAML para Confluence da Resolution GmbH da galeria</span><span class="sxs-lookup"><span data-stu-id="2aeee-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="2aeee-124">Para configurar a integração do SSO do SAML para Confluence da Resolution GmbH no Azure AD, adicione o SSO do SAML para Confluence da Resolution GmbH da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2aeee-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2aeee-125">**Para adicionar SSO do SAML para Confluence da Resolution GmbH da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2aeee-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2aeee-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2aeee-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2aeee-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="2aeee-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="2aeee-133">Na caixa de pesquisa, digite **SSO do SAML para Confluence da Resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="2aeee-135">No painel resultados, selecione **SSO do SAML para Confluence da Resolution GmbH** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2aeee-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2aeee-138">Nesta seção, você configura e testa o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="2aeee-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2aeee-139">Para o logon único funcionar, o Azure AD precisa saber que o usuário da contraparte no SSO do SAML para Confluence da Resolution GmbH é para um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aeee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="2aeee-140">Em outras palavras, uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SSO do SAML para Confluence da Resolution GmbH precisa ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2aeee-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="2aeee-141">No SSO do SAML para Confluence da Resolution GmbH, atribua o valor de **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2aeee-142">Para configurar e testar o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, conclua os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="2aeee-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2aeee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2aeee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2aeee-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2aeee-145">**[Criar um usuário de teste de SSO do SAML para Confluence da Resolution GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  – para ter um equivalente de Brenda Fernandes no SSO do SAML para Confluence da Resolution GmbH vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2aeee-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2aeee-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="2aeee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2aeee-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="2aeee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2aeee-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aeee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2aeee-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo SSO do SAML para Confluence da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="2aeee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="2aeee-150">**Para configurar o logon único do Azure AD com o SSO de SAML para Confluence da Resolution GmbH, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2aeee-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="2aeee-151">No portal do Azure, na página de integração de aplicativo **SSO do SAML para Confluence da Resolution GmbH**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="2aeee-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="2aeee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="2aeee-155">Na seção **Domínio e URLs do SSO do SAML para Confluence da Resolution GmbH**, se quiser configurar o aplicativo no modo iniciado **IDP**:</span><span class="sxs-lookup"><span data-stu-id="2aeee-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="2aeee-157">a.</span><span class="sxs-lookup"><span data-stu-id="2aeee-157">a.</span></span> <span data-ttu-id="2aeee-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2aeee-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="2aeee-159">b.</span><span class="sxs-lookup"><span data-stu-id="2aeee-159">b.</span></span> <span data-ttu-id="2aeee-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2aeee-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="2aeee-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2aeee-162">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="2aeee-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="2aeee-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="2aeee-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2aeee-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="2aeee-165">These values are not real.</span></span> <span data-ttu-id="2aeee-166">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="2aeee-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2aeee-167">Entre em contato com a [equipe de suporte ao Cliente do SSO do SAML para Confluence da Resolution GmbH](https://www.resolution.de/go/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="2aeee-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="2aeee-168">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="2aeee-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="2aeee-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="2aeee-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="2aeee-172">Em uma janela diferente do navegador da Web, faça logon no **portal do administrador do SSO do SAML para Confluence da Resolution GmbH** como administrador.</span><span class="sxs-lookup"><span data-stu-id="2aeee-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="2aeee-173">Passe o cursor do mouse sobre a engrenagem e clique em **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="2aeee-175">Você é redirecionado à página de Acesso de Administrador.</span><span class="sxs-lookup"><span data-stu-id="2aeee-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="2aeee-176">Insira a Senha e clique no botão **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-176">Enter the password and click **Confirm** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="2aeee-178">Na guia **ATLASSIAN MARKETPLACE**, clique em **Localizar novos complementos**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="2aeee-180">Pesquise **SSO (Logon Único) do SAML para Confluence** e clique no botão **Instalar** para instalar o novo plug-in do SAML.</span><span class="sxs-lookup"><span data-stu-id="2aeee-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="2aeee-182">A instalação do plug-in será iniciada.</span><span class="sxs-lookup"><span data-stu-id="2aeee-182">The plugin installation will start.</span></span> <span data-ttu-id="2aeee-183">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="2aeee-183">Click **Close**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="2aeee-186">Clique em **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-186">Click **Manage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="2aeee-188">Clique em **Configurar** para configurar o novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="2aeee-188">Click **Configure** to configure the new plugin.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="2aeee-190">Este novo plug-in também pode ser encontrado na guia **USUÁRIOS E SEGURANÇA**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="2aeee-192">Em **Configuração de Plug-in de Logon Único do SAML**, clique no botão **Adicionar Provedor de Identidade adicional** para definir as configurações do Provedor de Identidade.</span><span class="sxs-lookup"><span data-stu-id="2aeee-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="2aeee-194">Execute as seguintes etapas nesta página:</span><span class="sxs-lookup"><span data-stu-id="2aeee-194">Perform following steps on this page:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="2aeee-196">a.</span><span class="sxs-lookup"><span data-stu-id="2aeee-196">a.</span></span> <span data-ttu-id="2aeee-197">Adicionar **Nome** do Provedor de Identidade (por exemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2aeee-197">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="2aeee-198">b.</span><span class="sxs-lookup"><span data-stu-id="2aeee-198">b.</span></span> <span data-ttu-id="2aeee-199">Adicionar **Descrição** do Provedor de Identidade (por exemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2aeee-199">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="2aeee-200">c.</span><span class="sxs-lookup"><span data-stu-id="2aeee-200">c.</span></span> <span data-ttu-id="2aeee-201">Clique em **XML** e selecione o arquivo **Metadados** que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2aeee-201">Click **XML** and select the **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2aeee-202">d.</span><span class="sxs-lookup"><span data-stu-id="2aeee-202">d.</span></span> <span data-ttu-id="2aeee-203">Clique no botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-203">Click **Load** button.</span></span>

    <span data-ttu-id="2aeee-204">e.</span><span class="sxs-lookup"><span data-stu-id="2aeee-204">e.</span></span> <span data-ttu-id="2aeee-205">Ele lê os metadados IdP e preenche os campos conforme destacado na captura de tela.</span><span class="sxs-lookup"><span data-stu-id="2aeee-205">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 
18. <span data-ttu-id="2aeee-206">Clique no botão **Salvar Configurações** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="2aeee-206">Click **Save settings** button to save the settings.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="2aeee-208">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="2aeee-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2aeee-209">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2aeee-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2aeee-210">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2aeee-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2aeee-211">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="2aeee-212">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="2aeee-214">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2aeee-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2aeee-215">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-215">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2aeee-217">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2aeee-217">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2aeee-219">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-219">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2aeee-221">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2aeee-221">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2aeee-223">a.</span><span class="sxs-lookup"><span data-stu-id="2aeee-223">a.</span></span> <span data-ttu-id="2aeee-224">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-224">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2aeee-225">b.</span><span class="sxs-lookup"><span data-stu-id="2aeee-225">b.</span></span> <span data-ttu-id="2aeee-226">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-226">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2aeee-227">c.</span><span class="sxs-lookup"><span data-stu-id="2aeee-227">c.</span></span> <span data-ttu-id="2aeee-228">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-228">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2aeee-229">d.</span><span class="sxs-lookup"><span data-stu-id="2aeee-229">d.</span></span> <span data-ttu-id="2aeee-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="2aeee-231">Criando um usuário de teste do SSO do SAML para Confluence da Resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="2aeee-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="2aeee-232">Para habilitar usuários do Azure AD a fazerem logon no SSO do SAML para Confluence da Resolution GmbH, eles devem ser provisionados no SSO do SAML para Confluence da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="2aeee-232">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="2aeee-233">No SSO do SAML para Confluence da Resolution GmbH, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="2aeee-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="2aeee-234">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2aeee-234">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2aeee-235">Faça logon no site da empresa do SAML SSO para Confluence da Resolution GmbH como administrador.</span><span class="sxs-lookup"><span data-stu-id="2aeee-235">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="2aeee-236">Passe o cursor do mouse sobre a engrenagem e clique em **Gerenciamento de usuário**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-236">Hover on cog and click the **User management**.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="2aeee-238">Na seção usuários, clique na guia **Adicionar usuários**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-238">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="2aeee-239">Na página do diálogo **“Adicionar um usuário”**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2aeee-239">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="2aeee-241">a.</span><span class="sxs-lookup"><span data-stu-id="2aeee-241">a.</span></span> <span data-ttu-id="2aeee-242">Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-242">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="2aeee-243">b.</span><span class="sxs-lookup"><span data-stu-id="2aeee-243">b.</span></span> <span data-ttu-id="2aeee-244">Na caixa de texto **Nome completo**, digite o nome completo do usuário, como Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-244">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="2aeee-245">c.</span><span class="sxs-lookup"><span data-stu-id="2aeee-245">c.</span></span> <span data-ttu-id="2aeee-246">Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2aeee-246">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2aeee-247">d.</span><span class="sxs-lookup"><span data-stu-id="2aeee-247">d.</span></span> <span data-ttu-id="2aeee-248">Na caixa de texto **Senha**, digite a senha de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="2aeee-248">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="2aeee-249">e.</span><span class="sxs-lookup"><span data-stu-id="2aeee-249">e.</span></span> <span data-ttu-id="2aeee-250">Clique em **Confirmar Senha** e redigite a senha.</span><span class="sxs-lookup"><span data-stu-id="2aeee-250">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="2aeee-251">f.</span><span class="sxs-lookup"><span data-stu-id="2aeee-251">f.</span></span> <span data-ttu-id="2aeee-252">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-252">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2aeee-253">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2aeee-254">Nesta seção, habilite Brenda Fernandes a usar o logon único do Azure concedendo acesso ao SSO do SAML para Confluence da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="2aeee-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="2aeee-256">**Para atribuir Brenda Fernandes ao SSO do SAML para Confluence da Resolution GmbH, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="2aeee-256">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="2aeee-257">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="2aeee-259">Na lista de aplicativos, selecione **SSO do SAML para Confluence da Resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-259">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="2aeee-261">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="2aeee-263">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="2aeee-263">Click **Add** button.</span></span> <span data-ttu-id="2aeee-264">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="2aeee-266">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="2aeee-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2aeee-267">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2aeee-268">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2aeee-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2aeee-269">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="2aeee-269">Testing single sign-on</span></span>

<span data-ttu-id="2aeee-270">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="2aeee-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2aeee-271">Ao clicar no bloco SSO do SAML para Confluence da Resolution GmbH no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo SSO do SAML para Confluence da Resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="2aeee-271">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="2aeee-272">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2aeee-272">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2aeee-273">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2aeee-273">Additional resources</span></span>

* [<span data-ttu-id="2aeee-274">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2aeee-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2aeee-275">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2aeee-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

