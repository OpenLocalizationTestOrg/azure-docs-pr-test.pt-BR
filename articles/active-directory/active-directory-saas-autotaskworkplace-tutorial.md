---
title: "Tutorial: Integração do Azure Active Directory ao Autotask Workplace | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Autotask Workplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="d9127-103">Tutorial: Integração do Azure Active Directory ao Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="d9127-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="d9127-104">Neste tutorial, você aprende a integrar o Autotask Workplace ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d9127-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9127-105">A integração do Autotask Workplace ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d9127-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9127-106">No Azure AD, é possível controlar quem tem acesso ao Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="d9127-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="d9127-107">É possível permitir que os usuários se conectem automaticamente ao Autotask Workplace (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9127-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9127-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d9127-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9127-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9127-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9127-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9127-110">Prerequisites</span></span>

<span data-ttu-id="d9127-111">Para configurar a integração do Azure AD ao Autotask Workplace, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d9127-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="d9127-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9127-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9127-113">Uma assinatura habilitada para logon único do Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="d9127-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="d9127-114">Você deve ser um administrador ou superadministrador no local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d9127-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="d9127-115">Você deve ter uma conta Administrador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9127-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="d9127-116">Os usuários que utilizam esse recurso devem ter contas no local de trabalho e no Azure AD e os endereços de email deles para ambos devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="d9127-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="d9127-117">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d9127-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9127-118">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d9127-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9127-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d9127-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9127-120">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9127-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9127-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d9127-121">Scenario description</span></span>
<span data-ttu-id="d9127-122">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d9127-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9127-123">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d9127-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9127-124">Adicionando o Autotask Workplace por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="d9127-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="d9127-125">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d9127-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="d9127-126">Adicionando o Autotask Workplace por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="d9127-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="d9127-127">Para configurar a integração do Autotask Workplace ao Azure AD, você precisa adicionar o Autotask Workplace à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="d9127-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9127-128">**Para adicionar o Autotask Workplace por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9127-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9127-129">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9127-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="d9127-131">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d9127-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9127-132">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d9127-132">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="d9127-134">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9127-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="d9127-136">Na caixa de pesquisa, digite **Autotask Workplace**, selecione **Autotask Workplace** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d9127-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![Autotask Workplace na lista de resultados](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d9127-138">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9127-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d9127-139">Nesta seção, você configura e testa o logon único do Azure AD com o Autotask Workplace, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d9127-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9127-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Autotask Workplace é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9127-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="d9127-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="d9127-142">No Autotask Workplace, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="d9127-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d9127-143">Para configurar e testar o logon único do Azure AD com o Autotask Workplace, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d9127-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9127-144">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d9127-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9127-145">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9127-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9127-146">**[Criar um usuário de teste do Autotask Workplace](#create-an-autotask-workplace-test-user)** – para ter um equivalente de Brenda Fernandes no Autotask Workplace vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9127-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9127-147">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9127-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9127-148">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d9127-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d9127-149">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9127-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d9127-150">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="d9127-151">**Para configurar o logon único do Azure AD com o Autotask Workplace, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9127-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="d9127-152">No portal do Azure, na página de integração do aplicativo do **Autotask Workplace**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d9127-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="d9127-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d9127-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="d9127-156">Se desejar configurar o aplicativo no modo iniciado pelo **IDP**, realize as seguintes etapas na seção **Domínio e URLs do Autotask Workplace**:</span><span class="sxs-lookup"><span data-stu-id="d9127-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para IdP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="d9127-158">a.</span><span class="sxs-lookup"><span data-stu-id="d9127-158">a.</span></span> <span data-ttu-id="d9127-159">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="d9127-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="d9127-160">b.</span><span class="sxs-lookup"><span data-stu-id="d9127-160">b.</span></span> <span data-ttu-id="d9127-161">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="d9127-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="d9127-162">Se desejar configurar o aplicativo no modo iniciado pelo **SP**, marque a opção **Mostrar configurações de URL avançadas** e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d9127-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="d9127-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="d9127-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d9127-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="d9127-165">These values are not real.</span></span> <span data-ttu-id="d9127-166">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="d9127-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d9127-167">Contate a [equipe de suporte ao Cliente do Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="d9127-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="d9127-168">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d9127-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="d9127-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d9127-170">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d9127-172">Em uma janela de navegador da Web diferente, faça logon no Workplace Online usando as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="d9127-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="d9127-173">Ao configurar o IdP, um subdomínio precisará ser especificado.</span><span class="sxs-lookup"><span data-stu-id="d9127-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="d9127-174">Para confirmar o subdomínio correto, faça logon no Workplace Online.</span><span class="sxs-lookup"><span data-stu-id="d9127-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="d9127-175">Depois de conectado, tome nota do subdomínio na URL.</span><span class="sxs-lookup"><span data-stu-id="d9127-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="d9127-176">O subdomínio é a parte entre o "https://" e ".awp.autotask.net/" e deve ser us, eu, ca or au.</span><span class="sxs-lookup"><span data-stu-id="d9127-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="d9127-177">Vá até **Configuração** > **Logon Único** e execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d9127-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Configuração de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="d9127-179">a.</span><span class="sxs-lookup"><span data-stu-id="d9127-179">a.</span></span> <span data-ttu-id="d9127-180">Selecione a opção **Arquivo de Metadados XML** e, em seguida, carregue o **XML de Metadados** baixado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9127-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="d9127-181">b.</span><span class="sxs-lookup"><span data-stu-id="d9127-181">b.</span></span> <span data-ttu-id="d9127-182">Clique em **Habilitar SSO**.</span><span class="sxs-lookup"><span data-stu-id="d9127-182">Click **Enable SSO**.</span></span>
    
    ![Configuração de aprovação de Logon Único do Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="d9127-184">c.</span><span class="sxs-lookup"><span data-stu-id="d9127-184">c.</span></span> <span data-ttu-id="d9127-185">Selecione a caixa de seleção **Confirmo que essas informações estão corretas e eu confio neste IdP**.</span><span class="sxs-lookup"><span data-stu-id="d9127-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="d9127-186">d.</span><span class="sxs-lookup"><span data-stu-id="d9127-186">d.</span></span> <span data-ttu-id="d9127-187">Clique em **Aprovar**.</span><span class="sxs-lookup"><span data-stu-id="d9127-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="d9127-188">Se você precisar de assistência para configurar o Autotask Workplace, consulte [essa página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para obter ajuda com sua conta do Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="d9127-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d9127-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9127-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d9127-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9127-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9127-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d9127-192">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9127-192">Create an Azure AD test user</span></span>

<span data-ttu-id="d9127-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9127-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="d9127-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9127-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9127-196">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d9127-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d9127-198">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d9127-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d9127-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="d9127-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d9127-202">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d9127-202">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d9127-204">a.</span><span class="sxs-lookup"><span data-stu-id="d9127-204">a.</span></span> <span data-ttu-id="d9127-205">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="d9127-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9127-206">b.</span><span class="sxs-lookup"><span data-stu-id="d9127-206">b.</span></span> <span data-ttu-id="d9127-207">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d9127-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d9127-208">c.</span><span class="sxs-lookup"><span data-stu-id="d9127-208">c.</span></span> <span data-ttu-id="d9127-209">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="d9127-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d9127-210">d.</span><span class="sxs-lookup"><span data-stu-id="d9127-210">d.</span></span> <span data-ttu-id="d9127-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d9127-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="d9127-212">Criar um usuário de teste do Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="d9127-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="d9127-213">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Autotask.</span><span class="sxs-lookup"><span data-stu-id="d9127-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="d9127-214">Trabalhe com a [equipe de suporte do Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para adicionar os usuários à plataforma Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d9127-215">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9127-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="d9127-216">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="d9127-218">**Para atribuir Brenda Fernandes ao Autotask Workplace, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d9127-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="d9127-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d9127-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d9127-221">Na lista de aplicativos, selecione **Autotask Workplace**.</span><span class="sxs-lookup"><span data-stu-id="d9127-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![O link do Autotask Workplace na lista de Aplicativos](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="d9127-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d9127-223">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="d9127-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d9127-225">Click **Add** button.</span></span> <span data-ttu-id="d9127-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9127-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="d9127-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d9127-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9127-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9127-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9127-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d9127-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d9127-231">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="d9127-231">Test single sign-on</span></span>

<span data-ttu-id="d9127-232">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d9127-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d9127-233">Quando você clicar no bloco Autotask Workplace no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="d9127-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="d9127-234">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9127-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9127-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d9127-235">Additional resources</span></span>

* [<span data-ttu-id="d9127-236">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d9127-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9127-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9127-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

