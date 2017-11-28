---
title: "Tutorial: integração do Azure Active Directory com o TOPdesk - Público | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o TOPdesk – Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="ccb85-103">Tutorial: integração do Azure Active Directory com o TOPdesk – Public</span><span class="sxs-lookup"><span data-stu-id="ccb85-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="ccb85-104">Neste tutorial, você aprenderá a integrar o TOPdesk – Public ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ccb85-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ccb85-105">A integração do TOPdesk – Public ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ccb85-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ccb85-106">No Azure AD, é possível controlar quem tem acesso ao TOPdesk – Public.</span><span class="sxs-lookup"><span data-stu-id="ccb85-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="ccb85-107">Você pode permitir que os usuários façam logon automaticamente no TOPdesk – Public (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccb85-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ccb85-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb85-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ccb85-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ccb85-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccb85-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ccb85-110">Prerequisites</span></span>

<span data-ttu-id="ccb85-111">Para configurar a integração do Azure AD ao TOPdesk – Public, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ccb85-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="ccb85-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ccb85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ccb85-113">Uma assinatura do TOPdesk – Public habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ccb85-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ccb85-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ccb85-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ccb85-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ccb85-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ccb85-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ccb85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ccb85-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ccb85-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ccb85-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ccb85-118">Scenario description</span></span>
<span data-ttu-id="ccb85-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ccb85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ccb85-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ccb85-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ccb85-121">Adicionar o TOPdesk – Public da galeria</span><span class="sxs-lookup"><span data-stu-id="ccb85-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="ccb85-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ccb85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="ccb85-123">Adicionar o TOPdesk – Public da galeria</span><span class="sxs-lookup"><span data-stu-id="ccb85-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="ccb85-124">Para configurar a integração do TOPdesk – Public ao Azure AD, é necessário adicionar o TOPdesk – Public da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ccb85-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ccb85-125">**Para adicionar o TOPdesk – Public da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ccb85-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ccb85-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="ccb85-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ccb85-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="ccb85-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="ccb85-133">Na caixa de pesquisa, digite **TOPdesk – Public**, selecione **TOPdesk – Public** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk – Public na lista de resultados](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ccb85-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccb85-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ccb85-136">Nesta seção, você configurará e testará o logon único do Azure AD com o TOPdesk – Public, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ccb85-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ccb85-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do TOPdesk – Public é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccb85-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="ccb85-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no TOPdesk – Public.</span><span class="sxs-lookup"><span data-stu-id="ccb85-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="ccb85-139">No TOPdesk – Public, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ccb85-140">Para configurar e testar o logon único do Azure AD com o TOPdesk – Public, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ccb85-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ccb85-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ccb85-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ccb85-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ccb85-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ccb85-143">**[Criar um usuário de teste do TOPdesk – Public](#create-a-topdesk---public-test-user)** – para ter um equivalente de Brenda Fernandes no TOPdesk – Public vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccb85-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ccb85-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccb85-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ccb85-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ccb85-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ccb85-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccb85-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ccb85-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo TOPdesk – Public.</span><span class="sxs-lookup"><span data-stu-id="ccb85-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="ccb85-148">**Para configurar o logon único do Azure AD com o TOPdesk – Public, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ccb85-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="ccb85-149">No Portal do Azure, na página de integração de aplicativos do **TOPdesk – Public**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="ccb85-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ccb85-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="ccb85-153">Na seção **Domínio e URLs do TOPdesk – Public**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="ccb85-155">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-155">a.</span></span> <span data-ttu-id="ccb85-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="ccb85-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="ccb85-157">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-157">b.</span></span> <span data-ttu-id="ccb85-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="ccb85-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="ccb85-159">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-159">c.</span></span> <span data-ttu-id="ccb85-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="ccb85-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="ccb85-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ccb85-161">These values are not real.</span></span> <span data-ttu-id="ccb85-162">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="ccb85-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ccb85-163">A URL de resposta é explicada posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ccb85-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="ccb85-164">Contate a [equipe de suporte ao cliente do TOPdesk – Public](https://help.topdesk.com/saas/enterprise/user/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="ccb85-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="ccb85-165">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ccb85-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="ccb85-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ccb85-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ccb85-169">Na seção **Configuração do TOPdesk – Public**, clique em **Configurar o TOPdesk – Public** para abrir a janela **Configurar o logon**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ccb85-170">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="ccb85-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do TOPdesk – Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="ccb85-172">Faça logon em seu site de empresa do **TOPdesk - Public** como administrador.</span><span class="sxs-lookup"><span data-stu-id="ccb85-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="ccb85-173">No menu **TOPdesk**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="ccb85-174">![Configurações](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="ccb85-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="ccb85-175">Clique em **Configurações de Logon**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="ccb85-176">![Configurações de logon](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Configurações de logon")</span><span class="sxs-lookup"><span data-stu-id="ccb85-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="ccb85-177">Expanda o menu **Configurações de Logon** e clique em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="ccb85-178">![Geral](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Geral")</span><span class="sxs-lookup"><span data-stu-id="ccb85-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="ccb85-179">Na seção **Público** da seção de configuração de **Logon do SAML**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="ccb85-180">![Configurações técnicas](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Configurações técnicas")</span><span class="sxs-lookup"><span data-stu-id="ccb85-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="ccb85-181">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-181">a.</span></span> <span data-ttu-id="ccb85-182">Clique em **Baixar** para baixar o arquivo de metadados públicos e salve-o localmente no computador.</span><span class="sxs-lookup"><span data-stu-id="ccb85-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="ccb85-183">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-183">b.</span></span> <span data-ttu-id="ccb85-184">Abra o arquivo de metadados baixado e localize o nó **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="ccb85-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="ccb85-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="ccb85-186">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-186">c.</span></span> <span data-ttu-id="ccb85-187">Copie o valor **AssertionConsumerService**, cole-o na caixa de texto **URL de resposta** na seção **Domínio e URLs do TOPdesk – Public**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="ccb85-188">Execute as seguintes etapas para criar um arquivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="ccb85-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="ccb85-189">![Certificado](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="ccb85-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="ccb85-190">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-190">a.</span></span> <span data-ttu-id="ccb85-191">Abra o arquivo de metadados baixado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb85-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="ccb85-192">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-192">b.</span></span> <span data-ttu-id="ccb85-193">Expanda o nó **RoleDescriptor** que contém um **xsi:type** de **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="ccb85-194">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-194">c.</span></span> <span data-ttu-id="ccb85-195">Copie o valor do nó **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="ccb85-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="ccb85-196">d.</span><span class="sxs-lookup"><span data-stu-id="ccb85-196">d.</span></span> <span data-ttu-id="ccb85-197">Salve o valor copiado de **X509Certificate** localmente no computador em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="ccb85-198">Na seção **Público**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="ccb85-199">![Logon SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "logon SAML")</span><span class="sxs-lookup"><span data-stu-id="ccb85-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="ccb85-200">Na página do diálogo **Assistente de configuração do SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="ccb85-201">![Assistente de configuração SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistente de configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="ccb85-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="ccb85-202">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-202">a.</span></span> <span data-ttu-id="ccb85-203">Para carregar o arquivo de metadados baixado do Portal do Azure, em **Metadados de Federação**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="ccb85-204">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-204">b.</span></span> <span data-ttu-id="ccb85-205">Para carregar o arquivo de certificado, em **Certificado (RSA)**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="ccb85-206">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-206">c.</span></span> <span data-ttu-id="ccb85-207">Para carregar o arquivo de logotipo que você recebeu da equipe de suporte do TOPdesk, em **Ícone do logotipo**, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="ccb85-208">d.</span><span class="sxs-lookup"><span data-stu-id="ccb85-208">d.</span></span> <span data-ttu-id="ccb85-209">Na caixa de texto **Atributo de nome de usuário**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ccb85-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="ccb85-210">e.</span><span class="sxs-lookup"><span data-stu-id="ccb85-210">e.</span></span> <span data-ttu-id="ccb85-211">Na caixa de texto **Nome de exibição** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="ccb85-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ccb85-212">f.</span><span class="sxs-lookup"><span data-stu-id="ccb85-212">f.</span></span> <span data-ttu-id="ccb85-213">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ccb85-214">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ccb85-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ccb85-215">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ccb85-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ccb85-216">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ccb85-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ccb85-217">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccb85-217">Create an Azure AD test user</span></span>

<span data-ttu-id="ccb85-218">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ccb85-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="ccb85-220">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ccb85-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ccb85-221">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ccb85-223">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ccb85-225">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ccb85-227">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-227">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ccb85-229">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-229">a.</span></span> <span data-ttu-id="ccb85-230">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ccb85-231">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-231">b.</span></span> <span data-ttu-id="ccb85-232">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ccb85-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ccb85-233">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-233">c.</span></span> <span data-ttu-id="ccb85-234">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ccb85-235">d.</span><span class="sxs-lookup"><span data-stu-id="ccb85-235">d.</span></span> <span data-ttu-id="ccb85-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="ccb85-237">Criar um usuário de teste do TOPdesk – Public</span><span class="sxs-lookup"><span data-stu-id="ccb85-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="ccb85-238">Para permitir que os usuários do AD do Azure façam logon no TOPdesk - Público, eles deverão ser provisionados no TOPdesk - Público.</span><span class="sxs-lookup"><span data-stu-id="ccb85-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="ccb85-239">No caso do TOPdesk - Público, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ccb85-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="ccb85-240">Para configurar o provisionamento de usuários, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="ccb85-241">Faça logon em seu site de empresa do **TOPdesk - Public** como administrador.</span><span class="sxs-lookup"><span data-stu-id="ccb85-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="ccb85-242">No menu na parte superior, clique em **TOPdesk \> Novo \> Arquivos de Suporte \> Pessoa**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="ccb85-243">![Pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Pessoa")</span><span class="sxs-lookup"><span data-stu-id="ccb85-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="ccb85-244">Na caixa de diálogo Nova Pessoa, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccb85-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="ccb85-245">![Nova pessoa](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nova pessoa")</span><span class="sxs-lookup"><span data-stu-id="ccb85-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="ccb85-246">a.</span><span class="sxs-lookup"><span data-stu-id="ccb85-246">a.</span></span> <span data-ttu-id="ccb85-247">Clique na guia Geral.</span><span class="sxs-lookup"><span data-stu-id="ccb85-247">Click the General tab.</span></span>

    <span data-ttu-id="ccb85-248">b.</span><span class="sxs-lookup"><span data-stu-id="ccb85-248">b.</span></span> <span data-ttu-id="ccb85-249">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, tal como Fernandes</span><span class="sxs-lookup"><span data-stu-id="ccb85-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="ccb85-250">c.</span><span class="sxs-lookup"><span data-stu-id="ccb85-250">c.</span></span> <span data-ttu-id="ccb85-251">Selecione um **Site** para a conta.</span><span class="sxs-lookup"><span data-stu-id="ccb85-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="ccb85-252">d.</span><span class="sxs-lookup"><span data-stu-id="ccb85-252">d.</span></span> <span data-ttu-id="ccb85-253">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ccb85-254">É possível usar qualquer outra ferramenta de criação da conta de usuário do TOPdesk – Público ou APIs fornecidas pelo TOPdesk – Público para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccb85-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ccb85-255">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccb85-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="ccb85-256">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao TOPdesk – Public.</span><span class="sxs-lookup"><span data-stu-id="ccb85-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="ccb85-258">**Para atribuir Brenda Fernandes ao TOPdesk – Public, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ccb85-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="ccb85-259">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ccb85-261">Na lista de aplicativos, selecione **TOPdesk – Public**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![O link do TOPdesk – Public na lista de Aplicativos](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="ccb85-263">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-263">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="ccb85-265">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ccb85-265">Click **Add** button.</span></span> <span data-ttu-id="ccb85-266">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="ccb85-268">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ccb85-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ccb85-269">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ccb85-270">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ccb85-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ccb85-271">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="ccb85-271">Test single sign-on</span></span>

<span data-ttu-id="ccb85-272">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ccb85-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ccb85-273">Ao clicar no bloco TOPdesk – Public no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo TOPdesk – Public.</span><span class="sxs-lookup"><span data-stu-id="ccb85-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="ccb85-274">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ccb85-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ccb85-275">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ccb85-275">Additional resources</span></span>

* [<span data-ttu-id="ccb85-276">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ccb85-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ccb85-277">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ccb85-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

