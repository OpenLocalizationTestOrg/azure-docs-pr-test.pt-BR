---
title: "Tutorial: integração do Azure Active Directory com o Igloo Software | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="988b9-103">Tutorial: integração do Active Directory do Azure ao Igloo Software</span><span class="sxs-lookup"><span data-stu-id="988b9-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="988b9-104">Neste tutorial, você aprenderá a integrar o Igloo Software ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="988b9-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="988b9-105">A integração do Igloo Software ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="988b9-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="988b9-106">Você pode controlar, no Azure AD, quem tem acesso ao Igloo Software</span><span class="sxs-lookup"><span data-stu-id="988b9-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="988b9-107">Você pode habilitar seus usuários a fazer logon automaticamente no Igloo Software (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="988b9-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="988b9-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="988b9-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="988b9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="988b9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="988b9-110">Prerequisites</span></span>

<span data-ttu-id="988b9-111">Para configurar a integração do Azure AD ao Igloo Software, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="988b9-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="988b9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="988b9-113">Uma assinatura do Igloo Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="988b9-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="988b9-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="988b9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="988b9-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="988b9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="988b9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="988b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="988b9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="988b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="988b9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="988b9-118">Scenario description</span></span>
<span data-ttu-id="988b9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="988b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="988b9-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="988b9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="988b9-121">Adicionando Igloo Software da galeria</span><span class="sxs-lookup"><span data-stu-id="988b9-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="988b9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="988b9-123">Adicionando Igloo Software da galeria</span><span class="sxs-lookup"><span data-stu-id="988b9-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="988b9-124">Para configurar a integração do Igloo Software ao Azure AD, você precisa adicionar o Igloo Software da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="988b9-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="988b9-125">**Para adicionar o Igloo Software da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="988b9-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="988b9-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="988b9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="988b9-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="988b9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="988b9-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="988b9-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="988b9-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="988b9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="988b9-133">Na caixa de pesquisa, digite **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="988b9-133">In the search box, type **Igloo Software**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="988b9-135">No painel de resultados, escolha **Igloo Software** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="988b9-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="988b9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="988b9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Igloo Software com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="988b9-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="988b9-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Igloo Software é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="988b9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="988b9-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="988b9-141">No Igloo Software, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="988b9-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="988b9-142">Para configurar e testar o logon único do Azure AD com o Igloo Software, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="988b9-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="988b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="988b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="988b9-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="988b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="988b9-145">**[Como criar um usuário de teste do Igloo Software](#creating-an-igloo-software-test-user)** – para ter um equivalente de Brenda Fernandes no Igloo Software que esteja vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="988b9-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="988b9-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="988b9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="988b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="988b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="988b9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="988b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="988b9-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo do Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="988b9-150">**Para configurar o logon único do Azure AD com o Igloo Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="988b9-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="988b9-151">No portal do Azure, na página de integração de aplicativo **Igloo Software**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="988b9-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="988b9-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="988b9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="988b9-155">Na seção **URLs e Domínio do Igloo Software**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="988b9-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="988b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="988b9-157">a.</span></span> <span data-ttu-id="988b9-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="988b9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="988b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="988b9-159">b.</span></span> <span data-ttu-id="988b9-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="988b9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="988b9-161">c.</span><span class="sxs-lookup"><span data-stu-id="988b9-161">c.</span></span> <span data-ttu-id="988b9-162">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="988b9-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="988b9-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="988b9-163">These values are not real.</span></span> <span data-ttu-id="988b9-164">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="988b9-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="988b9-165">Entre em contato com a [equipe de suporte ao Cliente do Igloo Software](https://www.igloosoftware.com/services/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="988b9-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="988b9-166">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="988b9-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="988b9-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="988b9-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="988b9-170">Na seção **Configuração do Igloo Software**, clique em **Configurar Igloo Software** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="988b9-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="988b9-171">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="988b9-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="988b9-173">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Igloo Software como administrador.</span><span class="sxs-lookup"><span data-stu-id="988b9-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="988b9-174">Vá para o **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="988b9-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="988b9-175">![Painel de controle](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Painel de controle")</span><span class="sxs-lookup"><span data-stu-id="988b9-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="988b9-176">Na guia **Associação**, clique em **Configurações de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="988b9-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="988b9-177">![Configurações de entrada](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Configurações de entrada")</span><span class="sxs-lookup"><span data-stu-id="988b9-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="988b9-178">Na seção Configuração do SAML, clique em **Configurar Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="988b9-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="988b9-179">![Configuração SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="988b9-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="988b9-180">Na seção **Configuração Geral** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="988b9-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="988b9-181">![Configuração geral](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Configuração geral")</span><span class="sxs-lookup"><span data-stu-id="988b9-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="988b9-182">a.</span><span class="sxs-lookup"><span data-stu-id="988b9-182">a.</span></span> <span data-ttu-id="988b9-183">Na caixa de texto **Nome da Conexão** , digite um nome personalizado para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="988b9-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="988b9-184">b.</span><span class="sxs-lookup"><span data-stu-id="988b9-184">b.</span></span> <span data-ttu-id="988b9-185">Na caixa de texto **URL de Logon do IdP**, cole o valor da **URL de Serviço de Logon Único do SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="988b9-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="988b9-186">c.</span><span class="sxs-lookup"><span data-stu-id="988b9-186">c.</span></span> <span data-ttu-id="988b9-187">Na caixa de texto **URL de Logoff do IdP**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="988b9-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="988b9-188">d.</span><span class="sxs-lookup"><span data-stu-id="988b9-188">d.</span></span> <span data-ttu-id="988b9-189">Selecione **Tipo HTTP de Solicitação e Resposta de Logoff** como **POST**.</span><span class="sxs-lookup"><span data-stu-id="988b9-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="988b9-190">e.</span><span class="sxs-lookup"><span data-stu-id="988b9-190">e.</span></span> <span data-ttu-id="988b9-191">Abra seu certificado codificado em **base-64** no bloco de notas baixado do portal do Azure, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado Público**.</span><span class="sxs-lookup"><span data-stu-id="988b9-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="988b9-192">Em **Configuração de Resposta e Autenticação**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="988b9-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="988b9-193">![Configuração de autenticação e resposta](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Configuração de autenticação e resposta")</span><span class="sxs-lookup"><span data-stu-id="988b9-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="988b9-194">a.</span><span class="sxs-lookup"><span data-stu-id="988b9-194">a.</span></span> <span data-ttu-id="988b9-195">Para **Provedor de Identidade**, selecione **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="988b9-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="988b9-196">b.</span><span class="sxs-lookup"><span data-stu-id="988b9-196">b.</span></span> <span data-ttu-id="988b9-197">Para **Tipo de Identificador**, selecione **Endereço de Email**.</span><span class="sxs-lookup"><span data-stu-id="988b9-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="988b9-198">c.</span><span class="sxs-lookup"><span data-stu-id="988b9-198">c.</span></span> <span data-ttu-id="988b9-199">Na caixa de texto **Atributo de Email**, digite **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="988b9-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="988b9-200">d.</span><span class="sxs-lookup"><span data-stu-id="988b9-200">d.</span></span> <span data-ttu-id="988b9-201">Na caixa de texto **Atributo de Nome**, digite **givenname**.</span><span class="sxs-lookup"><span data-stu-id="988b9-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="988b9-202">e.</span><span class="sxs-lookup"><span data-stu-id="988b9-202">e.</span></span> <span data-ttu-id="988b9-203">Na caixa de texto **Atributo de Sobrenome**, digite **surname**.</span><span class="sxs-lookup"><span data-stu-id="988b9-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="988b9-204">Execute as seguintes etapas para concluir a configuração:</span><span class="sxs-lookup"><span data-stu-id="988b9-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="988b9-205">![Criação de usuário na entrada](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Criação de usuário na entrada")</span><span class="sxs-lookup"><span data-stu-id="988b9-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="988b9-206">a.</span><span class="sxs-lookup"><span data-stu-id="988b9-206">a.</span></span> <span data-ttu-id="988b9-207">Para **Criação de usuário na Entrada**, selecione **Criar um novo usuário em seu site ao entrar**.</span><span class="sxs-lookup"><span data-stu-id="988b9-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="988b9-208">b.</span><span class="sxs-lookup"><span data-stu-id="988b9-208">b.</span></span> <span data-ttu-id="988b9-209">Para **Configurações de Entrada**, selecione **Usar botão do SAML na tela “Entrar”**.</span><span class="sxs-lookup"><span data-stu-id="988b9-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="988b9-210">c.</span><span class="sxs-lookup"><span data-stu-id="988b9-210">c.</span></span> <span data-ttu-id="988b9-211">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="988b9-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="988b9-212">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="988b9-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="988b9-213">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="988b9-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="988b9-214">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="988b9-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="988b9-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="988b9-216">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="988b9-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="988b9-218">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="988b9-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="988b9-219">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="988b9-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="988b9-221">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="988b9-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="988b9-223">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="988b9-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="988b9-225">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="988b9-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="988b9-227">a.</span><span class="sxs-lookup"><span data-stu-id="988b9-227">a.</span></span> <span data-ttu-id="988b9-228">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="988b9-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="988b9-229">b.</span><span class="sxs-lookup"><span data-stu-id="988b9-229">b.</span></span> <span data-ttu-id="988b9-230">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="988b9-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="988b9-231">c.</span><span class="sxs-lookup"><span data-stu-id="988b9-231">c.</span></span> <span data-ttu-id="988b9-232">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="988b9-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="988b9-233">d.</span><span class="sxs-lookup"><span data-stu-id="988b9-233">d.</span></span> <span data-ttu-id="988b9-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="988b9-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="988b9-235">Como criar um usuário de teste do Igloo Software</span><span class="sxs-lookup"><span data-stu-id="988b9-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="988b9-236">Não há item de ação para a configuração do provisionamento de usuário para o Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="988b9-237">Quando um usuário atribuído tenta fazer logon no Igloo Software usando o painel de acesso, o Igloo Software verifica se o usuário existe.</span><span class="sxs-lookup"><span data-stu-id="988b9-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="988b9-238">Se ainda não houver conta de usuário, ela será criada automaticamente pelo Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="988b9-239">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="988b9-240">Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo-lhe acesso ao Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="988b9-242">**Para atribuir Brenda Fernandes ao Igloo Software, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="988b9-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="988b9-243">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="988b9-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="988b9-245">Na lista de aplicativos, selecione **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="988b9-245">In the applications list, select **Igloo Software**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="988b9-247">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="988b9-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="988b9-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="988b9-249">Click **Add** button.</span></span> <span data-ttu-id="988b9-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="988b9-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="988b9-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="988b9-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="988b9-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="988b9-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="988b9-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="988b9-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="988b9-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="988b9-255">Testing single sign-on</span></span>

<span data-ttu-id="988b9-256">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="988b9-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="988b9-257">Ao clicar no bloco Igloo Software no Painel de Acesso, você deve fazer logon automaticamente no seu aplicativo Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="988b9-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="988b9-258">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="988b9-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="988b9-259">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="988b9-259">Additional resources</span></span>

* [<span data-ttu-id="988b9-260">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="988b9-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="988b9-261">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="988b9-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

