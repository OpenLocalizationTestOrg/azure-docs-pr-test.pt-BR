---
title: "Tutorial: Integração do Azure Active Directory ao SumoLogic | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="c727f-103">Tutorial: Integração do Azure Active Directory ao SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c727f-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="c727f-104">Neste tutorial, você aprenderá a integrar o SumoLogic ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c727f-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c727f-105">A integração do SumoLogic ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c727f-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c727f-106">No Azure AD, é possível controlar quem tem acesso ao SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c727f-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="c727f-107">Você pode permitir que seus usuários façam logon automaticamente no SumoLogic (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="c727f-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c727f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c727f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c727f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c727f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c727f-110">Prerequisites</span></span>

<span data-ttu-id="c727f-111">Para configurar a integração do Azure AD ao SumoLogic, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c727f-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="c727f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c727f-113">Uma assinatura habilitada para logon único do SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c727f-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c727f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c727f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c727f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c727f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c727f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c727f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c727f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c727f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c727f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c727f-118">Scenario description</span></span>
<span data-ttu-id="c727f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c727f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c727f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c727f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c727f-121">Adicionando SumoLogic pela galeria</span><span class="sxs-lookup"><span data-stu-id="c727f-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="c727f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="c727f-123">Adicionando SumoLogic pela galeria</span><span class="sxs-lookup"><span data-stu-id="c727f-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="c727f-124">Para configurar a integração do SumoLogic ao Azure AD, você precisará adicionar o SumoLogic pela galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c727f-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c727f-125">**Para adicionar o SumoLogic pela galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c727f-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c727f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c727f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c727f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c727f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c727f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c727f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c727f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c727f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c727f-133">Na caixa de pesquisa, digite **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c727f-133">In the search box, type **SumoLogic**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="c727f-135">No painel de resultados, selecione **SumoLogic** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c727f-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c727f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c727f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SumoLogic, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c727f-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c727f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SumoLogic é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c727f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="c727f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c727f-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="c727f-141">No SumoLogic, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c727f-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c727f-142">Para configurar e testar o logon único do Azure AD com o SumoLogic, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c727f-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c727f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c727f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c727f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c727f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c727f-145">**[Criação de um usuário de teste do SumoLogic](#creating-a-sumologic-test-user)** – para ter um equivalente de Brenda Fernandes no SumoLogic que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c727f-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c727f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c727f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c727f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c727f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c727f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c727f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c727f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c727f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="c727f-150">**Para configurar o logon único do Azure AD com o SumoLogic, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c727f-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="c727f-151">No portal do Azure, na página de integração do aplicativo **SumoLogic**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c727f-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c727f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c727f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="c727f-155">Na seção **URLs e Domínio do SumoLogic**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c727f-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="c727f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c727f-157">a.</span></span> <span data-ttu-id="c727f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="c727f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="c727f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c727f-159">b.</span></span> <span data-ttu-id="c727f-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="c727f-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="c727f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c727f-161">These values are not real.</span></span> <span data-ttu-id="c727f-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="c727f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c727f-163">Contate a [equipe de suporte do Cliente do SumoLogic](https://www.sumologic.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c727f-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="c727f-164">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c727f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="c727f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c727f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c727f-168">Na seção **Configuração do SumoLogic**, clique em **Configurar o SumoLogic** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="c727f-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c727f-169">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="c727f-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="c727f-171">Em outra janela do navegador da Web, faça logon em seu site de empresa SumoLogic como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c727f-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="c727f-172">Vá para **Gerenciar \> Segurança**.</span><span class="sxs-lookup"><span data-stu-id="c727f-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="c727f-173">![Gerenciar](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gerenciar")</span><span class="sxs-lookup"><span data-stu-id="c727f-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="c727f-174">Clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c727f-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="c727f-175">![Configurações de segurança global](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Configurações de segurança global")</span><span class="sxs-lookup"><span data-stu-id="c727f-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="c727f-176">Na lista **Selecionar uma configuração ou criar uma nova**, selecione **Azure AD** e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="c727f-177">![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurar o SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="c727f-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="c727f-178">No diálogo **Configurar SAML 2.0** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c727f-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c727f-179">![Configurar o SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurar o SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="c727f-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="c727f-180">a.</span><span class="sxs-lookup"><span data-stu-id="c727f-180">a.</span></span> <span data-ttu-id="c727f-181">Na caixa de texto **Nome da Configuração**, digite **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c727f-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="c727f-182">b.</span><span class="sxs-lookup"><span data-stu-id="c727f-182">b.</span></span> <span data-ttu-id="c727f-183">Selecione **Modo de Depuração**.</span><span class="sxs-lookup"><span data-stu-id="c727f-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="c727f-184">c.</span><span class="sxs-lookup"><span data-stu-id="c727f-184">c.</span></span> <span data-ttu-id="c727f-185">Na caixa de texto **Emissor**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c727f-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c727f-186">d.</span><span class="sxs-lookup"><span data-stu-id="c727f-186">d.</span></span> <span data-ttu-id="c727f-187">Na caixa de texto **URL de Solicitação de Autenticação**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c727f-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c727f-188">e.</span><span class="sxs-lookup"><span data-stu-id="c727f-188">e.</span></span> <span data-ttu-id="c727f-189">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole todo o Certificado na caixa de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="c727f-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="c727f-190">f.</span><span class="sxs-lookup"><span data-stu-id="c727f-190">f.</span></span> <span data-ttu-id="c727f-191">Para **Atributo de Email**, selecione **Usar entidade do SAML**.</span><span class="sxs-lookup"><span data-stu-id="c727f-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="c727f-192">g.</span><span class="sxs-lookup"><span data-stu-id="c727f-192">g.</span></span> <span data-ttu-id="c727f-193">Selecione **Configuração de Logon iniciada pelo SP**.</span><span class="sxs-lookup"><span data-stu-id="c727f-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="c727f-194">h.</span><span class="sxs-lookup"><span data-stu-id="c727f-194">h.</span></span> <span data-ttu-id="c727f-195">Na caixa de texto **Caminho de Logon**, digite **Azure** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c727f-196">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c727f-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c727f-197">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c727f-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c727f-198">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c727f-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c727f-199">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="c727f-200">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c727f-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c727f-202">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c727f-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c727f-203">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c727f-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c727f-205">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c727f-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c727f-207">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c727f-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c727f-209">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c727f-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c727f-211">a.</span><span class="sxs-lookup"><span data-stu-id="c727f-211">a.</span></span> <span data-ttu-id="c727f-212">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="c727f-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c727f-213">b.</span><span class="sxs-lookup"><span data-stu-id="c727f-213">b.</span></span> <span data-ttu-id="c727f-214">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c727f-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c727f-215">c.</span><span class="sxs-lookup"><span data-stu-id="c727f-215">c.</span></span> <span data-ttu-id="c727f-216">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="c727f-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c727f-217">d.</span><span class="sxs-lookup"><span data-stu-id="c727f-217">d.</span></span> <span data-ttu-id="c727f-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="c727f-219">Criar um usuário de teste do SumoLogic</span><span class="sxs-lookup"><span data-stu-id="c727f-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="c727f-220">Para permitir que os usuários do AD do Azure façam logon no SumoLogic, eles deverão ser provisionados no SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c727f-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="c727f-221">No caso do SumoLogic, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c727f-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="c727f-222">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c727f-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c727f-223">Faça logon em seu locatário do **SumoLogic** .</span><span class="sxs-lookup"><span data-stu-id="c727f-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="c727f-224">Vá para **Gerenciar \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c727f-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="c727f-225">![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="c727f-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="c727f-226">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-226">Click **Add**.</span></span>
   
    <span data-ttu-id="c727f-227">![Usuários](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="c727f-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="c727f-228">No diálogo **Novo Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c727f-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="c727f-229">![Novo Usuário](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c727f-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="c727f-230">a.</span><span class="sxs-lookup"><span data-stu-id="c727f-230">a.</span></span> <span data-ttu-id="c727f-231">Digite as informações relacionadas da conta do Azure AD que você deseja provisionar nas caixas de texto **Nome**, **Sobrenome** e **Email**.</span><span class="sxs-lookup"><span data-stu-id="c727f-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="c727f-232">b.</span><span class="sxs-lookup"><span data-stu-id="c727f-232">b.</span></span> <span data-ttu-id="c727f-233">Selecione uma função.</span><span class="sxs-lookup"><span data-stu-id="c727f-233">Select a role.</span></span>
  
    <span data-ttu-id="c727f-234">c.</span><span class="sxs-lookup"><span data-stu-id="c727f-234">c.</span></span> <span data-ttu-id="c727f-235">Para **Status**, selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="c727f-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="c727f-236">d.</span><span class="sxs-lookup"><span data-stu-id="c727f-236">d.</span></span> <span data-ttu-id="c727f-237">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c727f-238">É possível usar qualquer outra ferramenta de criação da conta de usuário do SumoLogic ou as APIs fornecidas pelo SumoLogic para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c727f-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c727f-239">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c727f-240">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c727f-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c727f-242">**Para atribuir Brenda Fernandes ao SumoLogic, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c727f-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="c727f-243">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c727f-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c727f-245">Na lista de aplicativos, selecione **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="c727f-245">In the applications list, select **SumoLogic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="c727f-247">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c727f-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c727f-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c727f-249">Click **Add** button.</span></span> <span data-ttu-id="c727f-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c727f-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c727f-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c727f-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c727f-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c727f-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c727f-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c727f-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c727f-255">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c727f-255">Testing single sign-on</span></span>

<span data-ttu-id="c727f-256">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c727f-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c727f-257">Ao clicar no bloco do SumoLogic no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="c727f-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c727f-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c727f-258">Additional resources</span></span>

* [<span data-ttu-id="c727f-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c727f-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c727f-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c727f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

