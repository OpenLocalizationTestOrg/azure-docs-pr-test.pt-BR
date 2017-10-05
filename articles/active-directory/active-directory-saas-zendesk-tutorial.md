---
title: "Tutorial: Integração do Azure Active Directory com o Zendesk | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 51c06d838c5ed6286dfb99ea25faaaf33bad5f3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="1dac5-103">Tutorial: Integração do Active Directory do Azure com o Zendesk</span><span class="sxs-lookup"><span data-stu-id="1dac5-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="1dac5-104">Neste tutorial, você aprenderá a integrar o Zendesk ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1dac5-104">In this tutorial, you learn how to integrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dac5-105">A integração do Zendesk ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1dac5-105">Integrating Zendesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1dac5-106">Você pode controlar no Azure AD quem tem acesso ao Zendesk</span><span class="sxs-lookup"><span data-stu-id="1dac5-106">You can control in Azure AD who has access to Zendesk</span></span>
- <span data-ttu-id="1dac5-107">Você pode permitir que seus usuários façam logon automaticamente no Zendesk (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac5-107">You can enable your users to automatically get signed-on to Zendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dac5-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1dac5-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1dac5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dac5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1dac5-110">Prerequisites</span></span>

<span data-ttu-id="1dac5-111">Para configurar a integração do Azure AD com o Zendesk, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1dac5-111">To configure Azure AD integration with Zendesk, you need the following items:</span></span>

- <span data-ttu-id="1dac5-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dac5-113">Uma assinatura habilitada para logon único do Zendesk</span><span class="sxs-lookup"><span data-stu-id="1dac5-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="1dac5-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1dac5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="1dac5-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1dac5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dac5-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1dac5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dac5-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dac5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="1dac5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1dac5-118">Scenario description</span></span>
<span data-ttu-id="1dac5-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1dac5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dac5-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1dac5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dac5-121">Adicionar o Zendesk da galeria</span><span class="sxs-lookup"><span data-stu-id="1dac5-121">Adding Zendesk from the gallery</span></span>
2. <span data-ttu-id="1dac5-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="1dac5-123">Adicionar o Zendesk da galeria</span><span class="sxs-lookup"><span data-stu-id="1dac5-123">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="1dac5-124">Para configurar a integração do Zendesk ao Azure AD, você precisa adicionar o Zendesk por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1dac5-124">To configure the integration of Zendesk into Azure AD, you need to add Zendesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1dac5-125">**Para adicionar o Zendesk por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1dac5-125">**To add Zendesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac5-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dac5-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1dac5-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1dac5-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac5-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1dac5-133">Na caixa de pesquisa, digite **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-133">In the search box, type **Zendesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="1dac5-135">No painel de resultados, selecione **Zendesk** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1dac5-135">In the results panel, select **Zendesk**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dac5-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dac5-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zendesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1dac5-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dac5-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Zendesk é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zendesk is to a user in Azure AD.</span></span> <span data-ttu-id="1dac5-140">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado no Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1dac5-140">In other words, a link relationship between an Azure AD user and the related user in Zendesk needs to be established.</span></span>

<span data-ttu-id="1dac5-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como sendo o valor de **nome de usuário** no Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1dac5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zendesk.</span></span>

<span data-ttu-id="1dac5-142">Para configurar e testar o logon único do Azure AD com o Zendesk, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1dac5-142">To configure and test Azure AD single sign-on with Zendesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1dac5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1dac5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1dac5-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1dac5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dac5-145">**[Criação de um usuário de teste do Zendesk](#creating-a-zendesk-test-user)** – para ter um equivalente de Brenda Fernandes no Zendesk vinculado à representação de um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1dac5-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - to have a counterpart of Britta Simon in Zendesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dac5-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1dac5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dac5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1dac5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dac5-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1dac5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dac5-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1dac5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="1dac5-150">**Para configurar o logon único do Azure AD com o Zendesk, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1dac5-150">**To configure Azure AD single sign-on with Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac5-151">No Portal do Azure, na página de integração de aplicativos do **Zendesk**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-151">In the Azure portal, on the **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1dac5-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1dac5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="1dac5-155">Na seção **URLs e Domínio do Zendesk**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1dac5-155">On the **Zendesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="1dac5-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dac5-157">a.</span></span> <span data-ttu-id="1dac5-158">Na caixa de texto **URL de Logon**, digite o valor usando o seguinte padrão: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="1dac5-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="1dac5-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dac5-159">b.</span></span> <span data-ttu-id="1dac5-160">Na caixa de texto **Identificador**, digite o valor usando o seguinte padrão: `https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="1dac5-160">In the **Identifier** textbox, type the value using the following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1dac5-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1dac5-161">These values are not real.</span></span> <span data-ttu-id="1dac5-162">Atualize esses valores com a URL de Entrada e a URL do Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="1dac5-162">Update these values with the actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="1dac5-163">Entre em contato com a [equipe de suporte do Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="1dac5-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) to get these values.</span></span> 

4. <span data-ttu-id="1dac5-164">O Zendesk espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="1dac5-164">Zendesk expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1dac5-165">Não há nenhum atributo SAML obrigatório, mas opcionalmente você pode adicionar um atributo da seção **Atributos de Usuário** seguindo as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="1dac5-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following the below steps:</span></span> 

     ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="1dac5-167">a.</span><span class="sxs-lookup"><span data-stu-id="1dac5-167">a.</span></span> <span data-ttu-id="1dac5-168">Clique na caixa de seleção **Exibir e editar todos os outros atributos**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-168">Click the **View and edit all the other attributes** check box.</span></span>
     
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="1dac5-170">b.</span><span class="sxs-lookup"><span data-stu-id="1dac5-170">b.</span></span> <span data-ttu-id="1dac5-171">Clique em **Adicionar Atributo** para abrir a caixa de diálogo **Adicionar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-171">Click the **Add Attribute** to open **Add attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1dac5-173">c.</span><span class="sxs-lookup"><span data-stu-id="1dac5-173">c.</span></span> <span data-ttu-id="1dac5-174">Na caixa de texto **Nome**, digite o nome do atributo (por exemplo, **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="1dac5-174">In the **Name** textbox, type the attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="1dac5-175">d.</span><span class="sxs-lookup"><span data-stu-id="1dac5-175">d.</span></span> <span data-ttu-id="1dac5-176">Na lista **Valor**, selecione o valor do atributo (como **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="1dac5-176">From the **Value** list, select the attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="1dac5-177">e.</span><span class="sxs-lookup"><span data-stu-id="1dac5-177">e.</span></span> <span data-ttu-id="1dac5-178">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="1dac5-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="1dac5-179">Você pode usar atributos de extensão para adicionar atributos que não estão no Azure AD por padrão.</span><span class="sxs-lookup"><span data-stu-id="1dac5-179">You use extension attributes to add attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="1dac5-180">Clique em [Atributos do usuário que podem ser definidos no SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) para obter a lista completa de atributos SAML que o **Zendesk** aceita.</span><span class="sxs-lookup"><span data-stu-id="1dac5-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) to get the complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="1dac5-181">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="1dac5-181">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="1dac5-183">Na seção **Configuração do Zendesk**, clique em **Configurar o Zendesk** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-183">On the **Zendesk Configuration** section, click **Configure Zendesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1dac5-184">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1dac5-184">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="1dac5-186">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zendesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="1dac5-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="1dac5-187">Clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-187">Click **Admin**.</span></span>

9. <span data-ttu-id="1dac5-188">No painel de navegação à esquerda, clique em **Configurações** e em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-188">In the left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="1dac5-189">Na página **Segurança**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1dac5-189">On the **Security** page, perform the following steps:</span></span> 
   
     <span data-ttu-id="1dac5-190">![Segurança](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="1dac5-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="1dac5-191">![Logon Único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="1dac5-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="1dac5-192">a.</span><span class="sxs-lookup"><span data-stu-id="1dac5-192">a.</span></span> <span data-ttu-id="1dac5-193">Clique na guia **Administrador e Agentes**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-193">Click the **Admin & Agents** tab.</span></span>

     <span data-ttu-id="1dac5-194">b.</span><span class="sxs-lookup"><span data-stu-id="1dac5-194">b.</span></span> <span data-ttu-id="1dac5-195">Selecione **SSO (logon único) e SAML** e, em seguida, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="1dac5-196">c.</span><span class="sxs-lookup"><span data-stu-id="1dac5-196">c.</span></span> <span data-ttu-id="1dac5-197">Na caixa de texto **URL do SSO do SAML**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1dac5-197">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="1dac5-198">d.</span><span class="sxs-lookup"><span data-stu-id="1dac5-198">d.</span></span> <span data-ttu-id="1dac5-199">Na caixa de texto **URL de Logoff Remoto**, cole o valor da **URL de Saída** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1dac5-199">In **Remote Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="1dac5-200">e.</span><span class="sxs-lookup"><span data-stu-id="1dac5-200">e.</span></span> <span data-ttu-id="1dac5-201">Na caixa de texto **Impressão Digital do Certificado**, cole o valor de **Impressão Digital** do certificado copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1dac5-201">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="1dac5-202">f.</span><span class="sxs-lookup"><span data-stu-id="1dac5-202">f.</span></span> <span data-ttu-id="1dac5-203">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dac5-204">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dac5-205">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1dac5-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1dac5-207">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1dac5-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac5-208">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-208">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dac5-210">Para exibir a lista de usuários, vá para **Usuários e grupos** e clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-210">To display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dac5-212">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-212">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dac5-214">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1dac5-214">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dac5-216">a.</span><span class="sxs-lookup"><span data-stu-id="1dac5-216">a.</span></span> <span data-ttu-id="1dac5-217">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-217">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dac5-218">b.</span><span class="sxs-lookup"><span data-stu-id="1dac5-218">b.</span></span> <span data-ttu-id="1dac5-219">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1dac5-219">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dac5-220">c.</span><span class="sxs-lookup"><span data-stu-id="1dac5-220">c.</span></span> <span data-ttu-id="1dac5-221">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-221">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1dac5-222">d.</span><span class="sxs-lookup"><span data-stu-id="1dac5-222">d.</span></span> <span data-ttu-id="1dac5-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="1dac5-224">Criação de um usuário de teste do Zendesk</span><span class="sxs-lookup"><span data-stu-id="1dac5-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="1dac5-225">Para permitir que os usuários do Azure AD façam logon no **Zendesk**, eles devem ser provisionados no **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-225">To enable Azure AD users to log into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="1dac5-226">Dependendo da função atribuída nos aplicativos, esse é o comportamento esperado:</span><span class="sxs-lookup"><span data-stu-id="1dac5-226">Depending on the role assigned in the apps, it's the expected behavior:</span></span>

 1. <span data-ttu-id="1dac5-227">As contas de **Usuário final** são provisionadas automaticamente ao entrar.</span><span class="sxs-lookup"><span data-stu-id="1dac5-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="1dac5-228">Contas de **Agente** e **Admin** precisam ser provisionadas manualmente no **Zendesk** antes de entrar.</span><span class="sxs-lookup"><span data-stu-id="1dac5-228">**Agent** and **Admin** accounts need to be manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="1dac5-229">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1dac5-229">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac5-230">Faça logon em seu locatário do **Zendesk** .</span><span class="sxs-lookup"><span data-stu-id="1dac5-230">Log in to your **Zendesk** tenant.</span></span>

2. <span data-ttu-id="1dac5-231">Selecione a guia **Lista de Clientes** .</span><span class="sxs-lookup"><span data-stu-id="1dac5-231">Select the **Customer List** tab.</span></span>

3. <span data-ttu-id="1dac5-232">Selecione a guia **Usuário** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-232">Select the **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="1dac5-233">![Adicionar Usuário](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="1dac5-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="1dac5-234">Digite o endereço de uma conta existente do Azure AD que você deseja provisionar e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-234">Type the email address of an existing Azure AD account you want to provision, and then click **Save**.</span></span>
   
    <span data-ttu-id="1dac5-235">![Novo Usuário](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="1dac5-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="1dac5-236">É possível usar qualquer outra ferramenta de criação da conta de usuário do Zendesk ou APIs fornecidas pelo Zendesk para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="1dac5-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1dac5-237">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1dac5-238">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1dac5-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zendesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1dac5-240">**Para atribuir Brenda Fernandes ao Zendesk, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1dac5-240">**To assign Britta Simon to Zendesk, perform the following steps:**</span></span>

1. <span data-ttu-id="1dac5-241">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1dac5-243">Na lista de aplicativos, selecione **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-243">In the applications list, select **Zendesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="1dac5-245">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1dac5-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1dac5-247">Click **Add** button.</span></span> <span data-ttu-id="1dac5-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac5-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1dac5-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1dac5-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1dac5-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac5-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dac5-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1dac5-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dac5-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1dac5-253">Testing single sign-on</span></span>

<span data-ttu-id="1dac5-254">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1dac5-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1dac5-255">Ao clicar no bloco Zendesk no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Zendesk.</span><span class="sxs-lookup"><span data-stu-id="1dac5-255">When you click the Zendesk tile in the Access Panel, you should get automatically signed-on to your Zendesk application.</span></span>
<span data-ttu-id="1dac5-256">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1dac5-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dac5-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1dac5-257">Additional resources</span></span>

* [<span data-ttu-id="1dac5-258">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1dac5-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dac5-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1dac5-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
