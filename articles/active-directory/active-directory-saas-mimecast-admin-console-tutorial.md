---
title: "Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Mimecast Admin Console."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="7f63f-103">Tutorial: Integração do Azure Active Directory com o Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="7f63f-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="7f63f-104">Neste tutorial, você aprende a integrar o Mimecast Admin Console ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="7f63f-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f63f-105">A integração do Mimecast Admin Console ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="7f63f-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f63f-106">No Azure AD, é possível controlar quem tem acesso ao Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="7f63f-107">Você pode permitir que seus usuários façam logon automaticamente no Mimecast Admin Console usando logon único com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f63f-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7f63f-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f63f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7f63f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f63f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f63f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f63f-110">Prerequisites</span></span>

<span data-ttu-id="7f63f-111">Para configurar a integração do Azure AD ao Mimecast Admin Console, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7f63f-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="7f63f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f63f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f63f-113">Uma assinatura do Mimecast Admin Console com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="7f63f-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f63f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7f63f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f63f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7f63f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f63f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7f63f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f63f-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f63f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f63f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7f63f-118">Scenario description</span></span>
<span data-ttu-id="7f63f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7f63f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f63f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="7f63f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f63f-121">Adicionar o Mimecast Admin Console por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7f63f-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="7f63f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="7f63f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="7f63f-123">Adicionar o Mimecast Admin Console por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="7f63f-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="7f63f-124">Para configurar a integração do Mimecast Admin Console com o Azure AD, você precisará adicionar o Mimecast Admin Console à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="7f63f-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f63f-125">**Para adicionar o Mimecast Admin Console por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7f63f-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f63f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="7f63f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f63f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="7f63f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="7f63f-133">Na caixa de pesquisa, digite **Mimecast Admin Console**, selecione **Mimecast Admin Console** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Admin Console na lista de resultados](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7f63f-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f63f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7f63f-136">Nesta seção, você configura e testa o logon único do Azure AD com o Mimecast Admin Console, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="7f63f-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f63f-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Mimecast Admin Console é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f63f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="7f63f-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="7f63f-139">No Mimecast Admin Console, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7f63f-140">Para configurar e testar o logon único do Azure AD com o Mimecast Admin Console, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="7f63f-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f63f-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="7f63f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f63f-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7f63f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f63f-143">**[Criando um usuário de teste do Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)** – para ter um equivalente de Brenda Fernandes no Mimecast Admin Console que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f63f-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f63f-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f63f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f63f-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="7f63f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7f63f-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f63f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7f63f-147">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="7f63f-148">**Para configurar o logon único do Azure AD com o Mimecast Admin Console, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7f63f-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="7f63f-149">No Portal do Azure, na página de integração do aplicativo **Mimecast Admin Console**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="7f63f-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="7f63f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="7f63f-153">Na seção **Domínio e URLs do Mimecast Admin Console**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7f63f-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="7f63f-155">Na caixa de texto **URL de Logon**, digite a URL:</span><span class="sxs-lookup"><span data-stu-id="7f63f-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="7f63f-156">A URL de logon é específica para a região.</span><span class="sxs-lookup"><span data-stu-id="7f63f-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="7f63f-157">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="7f63f-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="7f63f-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="7f63f-159">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7f63f-161">Na seção **Configuração do Mimecast Admin Console**, clique em **Configurar o Mimecast Admin Console** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7f63f-162">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="7f63f-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="7f63f-164">Em outra janela do navegador da Web, faça logon em seu Mimecast Admin Console como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7f63f-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="7f63f-165">Vá para **Serviços \> Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="7f63f-166">![Serviços](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Serviços")</span><span class="sxs-lookup"><span data-stu-id="7f63f-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="7f63f-167">Clique em **Perfis de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="7f63f-168">![Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="7f63f-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="7f63f-169">Clique em **Novo Perfil de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="7f63f-170">![Novos Perfis de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Novos Perfis de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="7f63f-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="7f63f-171">Na seção **Perfil de Autenticação** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7f63f-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="7f63f-172">![Perfil de Autenticação](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Perfil de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="7f63f-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="7f63f-173">a.</span><span class="sxs-lookup"><span data-stu-id="7f63f-173">a.</span></span> <span data-ttu-id="7f63f-174">Na caixa de texto **Descrição** , digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="7f63f-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="7f63f-175">b.</span><span class="sxs-lookup"><span data-stu-id="7f63f-175">b.</span></span> <span data-ttu-id="7f63f-176">Selecione **Impor Autenticação SAML para o Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="7f63f-177">c.</span><span class="sxs-lookup"><span data-stu-id="7f63f-177">c.</span></span> <span data-ttu-id="7f63f-178">Como **Provedor**, selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="7f63f-179">d.</span><span class="sxs-lookup"><span data-stu-id="7f63f-179">d.</span></span> <span data-ttu-id="7f63f-180">Cole a **ID de Entidade do SAML** que você copiou do Portal do Azure na caixa de texto **URL do Emissor**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="7f63f-181">e.</span><span class="sxs-lookup"><span data-stu-id="7f63f-181">e.</span></span> <span data-ttu-id="7f63f-182">Cole a **URL do Serviço de Logon Único SAML**, que você copiou do Portal do Azure na a caixa de texto **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="7f63f-183">f.</span><span class="sxs-lookup"><span data-stu-id="7f63f-183">f.</span></span> <span data-ttu-id="7f63f-184">Cole a **URL do Serviço de Logon Único SAML**, que você copiou do Portal do Azure na a caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="7f63f-185">O valor da URL de logon e da URL de logoff para o Mimecast Admin Console são as mesmas.</span><span class="sxs-lookup"><span data-stu-id="7f63f-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="7f63f-186">g.</span><span class="sxs-lookup"><span data-stu-id="7f63f-186">g.</span></span> <span data-ttu-id="7f63f-187">Abra seu certificado codificado em base 64 baixado do Portal do Azure no bloco de notas, remova a primeira linha ("*--*") e a última linha ("*--*"), copie o conteúdo restante para a área de transferência e cole-o na caixa de texto **Certificado de Provedor de Identidade (Metadados)**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="7f63f-188">h.</span><span class="sxs-lookup"><span data-stu-id="7f63f-188">h.</span></span> <span data-ttu-id="7f63f-189">Selecione **Permitir Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="7f63f-190">i.</span><span class="sxs-lookup"><span data-stu-id="7f63f-190">i.</span></span> <span data-ttu-id="7f63f-191">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f63f-192">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="7f63f-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7f63f-193">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="7f63f-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7f63f-194">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7f63f-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7f63f-195">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f63f-195">Create an Azure AD test user</span></span>

<span data-ttu-id="7f63f-196">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7f63f-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="7f63f-198">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7f63f-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f63f-199">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7f63f-201">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7f63f-203">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7f63f-205">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7f63f-205">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7f63f-207">a.</span><span class="sxs-lookup"><span data-stu-id="7f63f-207">a.</span></span> <span data-ttu-id="7f63f-208">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f63f-209">b.</span><span class="sxs-lookup"><span data-stu-id="7f63f-209">b.</span></span> <span data-ttu-id="7f63f-210">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="7f63f-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7f63f-211">c.</span><span class="sxs-lookup"><span data-stu-id="7f63f-211">c.</span></span> <span data-ttu-id="7f63f-212">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7f63f-213">d.</span><span class="sxs-lookup"><span data-stu-id="7f63f-213">d.</span></span> <span data-ttu-id="7f63f-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="7f63f-215">Criar um usuário de teste do Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="7f63f-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="7f63f-216">Para permitir que os usuários do Azure AD façam logon no Mimecast Admin Console, eles devem ser provisionados no Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="7f63f-217">No caso do Mimecast Admin Console, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="7f63f-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="7f63f-218">Você precisa registrar um domínio antes de criar usuários.</span><span class="sxs-lookup"><span data-stu-id="7f63f-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="7f63f-219">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7f63f-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7f63f-220">Faça logon no **Mimecast Admin Console** como administrador.</span><span class="sxs-lookup"><span data-stu-id="7f63f-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="7f63f-221">Vá para **Diretórios \> Interno**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="7f63f-222">![Diretórios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Diretórios")</span><span class="sxs-lookup"><span data-stu-id="7f63f-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="7f63f-223">Clique em **Registrar Novo Domínio**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="7f63f-224">![Registrar Novo Domínio](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Registrar Novo Domínio")</span><span class="sxs-lookup"><span data-stu-id="7f63f-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="7f63f-225">Depois de criar o novo domínio, clique em **Novo Endereço**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="7f63f-226">![Novo Endereço](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Novo Endereço")</span><span class="sxs-lookup"><span data-stu-id="7f63f-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="7f63f-227">Na caixa de diálogo do novo endereço, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7f63f-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="7f63f-228">![Salvar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Salvar")</span><span class="sxs-lookup"><span data-stu-id="7f63f-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="7f63f-229">a.</span><span class="sxs-lookup"><span data-stu-id="7f63f-229">a.</span></span> <span data-ttu-id="7f63f-230">Digite os atributos de **Endereço de Email**, **Nome Global**, **Senha** e **Confirmar Senha** de uma conta válida do Azure AD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7f63f-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="7f63f-231">b.</span><span class="sxs-lookup"><span data-stu-id="7f63f-231">b.</span></span> <span data-ttu-id="7f63f-232">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="7f63f-233">É possível usar qualquer outra ferramenta de criação da conta de usuário do Mimecast Admin Console ou as APIs fornecidas pelo Mimecast Admin Console para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f63f-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7f63f-234">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f63f-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="7f63f-235">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="7f63f-237">**Para atribuir Brenda Fernandes ao Mimecast Admin Console, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="7f63f-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="7f63f-238">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="7f63f-240">Na lista de aplicativos, selecione **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![O link do Mimecast Admin Console na lista de Aplicativos](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="7f63f-242">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-242">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="7f63f-244">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7f63f-244">Click **Add** button.</span></span> <span data-ttu-id="7f63f-245">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="7f63f-247">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7f63f-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7f63f-248">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f63f-249">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7f63f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7f63f-250">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="7f63f-250">Test single sign-on</span></span>

<span data-ttu-id="7f63f-251">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="7f63f-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7f63f-252">Quando você clicar no bloco do Mimecast Admin Console no Painel de Acesso, deverá ser conectado automaticamente ao aplicativo Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="7f63f-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="7f63f-253">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f63f-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7f63f-254">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7f63f-254">Additional resources</span></span>

* [<span data-ttu-id="7f63f-255">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7f63f-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f63f-256">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f63f-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

