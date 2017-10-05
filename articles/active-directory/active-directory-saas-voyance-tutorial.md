---
title: "Tutorial: Integração do Azure Active Directory com o Voyance | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="23396-103">Tutorial: Integração do Azure Active Directory com o Voyance</span><span class="sxs-lookup"><span data-stu-id="23396-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="23396-104">Neste tutorial, você aprenderá a integrar o Voyance ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="23396-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23396-105">A integração do Voyance ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="23396-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23396-106">Você pode controlar no Azure AD quem tem acesso ao Voyance</span><span class="sxs-lookup"><span data-stu-id="23396-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="23396-107">Você pode permitir que seus usuários façam logon automaticamente no Voyance (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23396-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23396-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="23396-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="23396-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23396-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23396-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23396-110">Prerequisites</span></span>

<span data-ttu-id="23396-111">Para configurar a integração do Azure AD ao Voyance, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="23396-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="23396-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23396-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23396-113">Uma assinatura do Voyance habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="23396-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23396-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="23396-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23396-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="23396-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23396-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="23396-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23396-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23396-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23396-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="23396-118">Scenario description</span></span>
<span data-ttu-id="23396-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="23396-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23396-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="23396-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23396-121">Adição do Voyance da galeria</span><span class="sxs-lookup"><span data-stu-id="23396-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="23396-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="23396-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="23396-123">Adição do Voyance da galeria</span><span class="sxs-lookup"><span data-stu-id="23396-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="23396-124">Para configurar a integração do Voyance ao Azure AD, você precisará adicionar o Voyance da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="23396-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23396-125">**Para adicionar o Voyance por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23396-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23396-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23396-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="23396-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="23396-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23396-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23396-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="23396-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="23396-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="23396-133">Na caixa de pesquisa, digite **Voyance**, selecione **Voyance** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="23396-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance na lista de resultados](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="23396-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23396-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="23396-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Voyance, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="23396-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="23396-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Voyance é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23396-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="23396-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Voyance.</span><span class="sxs-lookup"><span data-stu-id="23396-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="23396-139">No Voyance, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="23396-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="23396-140">Para configurar e testar o logon único do Azure AD com o Voyance, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="23396-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23396-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="23396-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23396-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23396-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23396-143">**[Criar um usuário de teste do Voyance](#create-a-voyance-test-user)** – para ter um equivalente de Brenda Fernandes no Voyance vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23396-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="23396-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23396-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23396-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="23396-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="23396-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23396-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="23396-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Voyance.</span><span class="sxs-lookup"><span data-stu-id="23396-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="23396-148">**Para configurar o logon único do Azure AD com o Voyance, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23396-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="23396-149">No Portal do Azure, na página de integração de aplicativos do **Voyance**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="23396-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="23396-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="23396-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="23396-153">Na seção **Domínio e URLs do Voyance**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IdP**:</span><span class="sxs-lookup"><span data-stu-id="23396-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Voyance para IdP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="23396-155">a.</span><span class="sxs-lookup"><span data-stu-id="23396-155">a.</span></span> <span data-ttu-id="23396-156">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="23396-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="23396-157">b.</span><span class="sxs-lookup"><span data-stu-id="23396-157">b.</span></span> <span data-ttu-id="23396-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="23396-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="23396-159">Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:</span><span class="sxs-lookup"><span data-stu-id="23396-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informações de logon único de Domínio e URLs do Voyance para SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="23396-161">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="23396-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="23396-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="23396-162">These values are not real.</span></span> <span data-ttu-id="23396-163">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="23396-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="23396-164">Contate a [equipe de suporte ao cliente do Voyance](mailto:support@nyansa.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="23396-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="23396-165">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="23396-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="23396-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="23396-167">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="23396-169">Na seção **Configuração do Voyance**, clique em **Configurar o Voyance** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="23396-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23396-170">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="23396-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="23396-172">Em uma janela diferente do navegador da Web, faça logon em seu locatário do Voyance como um administrador.</span><span class="sxs-lookup"><span data-stu-id="23396-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="23396-173">Vá para o canto superior direito da barra de navegação e clique no menu suspenso que indica "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="23396-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Configurar o logon único no lado do aplicativo – Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="23396-175">Clique em "**Configurações de Administração**".</span><span class="sxs-lookup"><span data-stu-id="23396-175">Click "**Admin Settings**".</span></span>

    ![Configurar o logon único no lado do aplicativo – Configurações do Administrador](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="23396-177">Clique na guia "**Acesso do Usuário**".</span><span class="sxs-lookup"><span data-stu-id="23396-177">Click "**User Access**" tab.</span></span>

    ![Configurar o logon único no lado do aplicativo – Acesso do Usuário](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="23396-179">Clique no botão "**SSO está desabilitado**" para configurar o Azure AD como um IdP que usa SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="23396-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurar o logon único no lado do aplicativo – SSO está desabilitado](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="23396-181">Acesse a seção **SAML v2** e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="23396-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configurar o logon único no lado do aplicativo – SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="23396-183">a.</span><span class="sxs-lookup"><span data-stu-id="23396-183">a.</span></span> <span data-ttu-id="23396-184">Selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="23396-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="23396-185">b.</span><span class="sxs-lookup"><span data-stu-id="23396-185">b.</span></span> <span data-ttu-id="23396-186">Cole a **URL do Serviço de Logon Único SAML** copiada no Portal do Azure na a caixa de texto **URL de Logon do IdP**.</span><span class="sxs-lookup"><span data-stu-id="23396-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="23396-187">c.</span><span class="sxs-lookup"><span data-stu-id="23396-187">c.</span></span> <span data-ttu-id="23396-188">Abra seu certificado codificado com Base64 baixado no bloco de notas, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado IdP**.</span><span class="sxs-lookup"><span data-stu-id="23396-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="23396-189">d.</span><span class="sxs-lookup"><span data-stu-id="23396-189">d.</span></span> <span data-ttu-id="23396-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="23396-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="23396-191">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="23396-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23396-192">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="23396-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23396-193">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23396-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="23396-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23396-194">Create an Azure AD test user</span></span>

<span data-ttu-id="23396-195">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23396-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="23396-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23396-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23396-198">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23396-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23396-200">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23396-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23396-202">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23396-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23396-204">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="23396-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23396-206">a.</span><span class="sxs-lookup"><span data-stu-id="23396-206">a.</span></span> <span data-ttu-id="23396-207">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="23396-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23396-208">b.</span><span class="sxs-lookup"><span data-stu-id="23396-208">b.</span></span> <span data-ttu-id="23396-209">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="23396-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23396-210">c.</span><span class="sxs-lookup"><span data-stu-id="23396-210">c.</span></span> <span data-ttu-id="23396-211">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="23396-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23396-212">d.</span><span class="sxs-lookup"><span data-stu-id="23396-212">d.</span></span> <span data-ttu-id="23396-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="23396-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="23396-214">Criar um usuário de teste do Voyance</span><span class="sxs-lookup"><span data-stu-id="23396-214">Create a Voyance test user</span></span>

<span data-ttu-id="23396-215">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Voyance.</span><span class="sxs-lookup"><span data-stu-id="23396-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="23396-216">O Voyance dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="23396-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="23396-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="23396-217">There is no action item for you in this section.</span></span> <span data-ttu-id="23396-218">Um novo usuário será criado durante uma tentativa de acessar o Voyance, caso ele ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="23396-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="23396-219">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="23396-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="23396-220">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="23396-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="23396-221">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Voyance.</span><span class="sxs-lookup"><span data-stu-id="23396-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="23396-223">**Para atribuir Brenda Fernandes ao Voyance, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="23396-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="23396-224">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="23396-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="23396-226">Na lista de aplicativos, selecione **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="23396-226">In the applications list, select **Voyance**.</span></span>

    ![O link do Voyance na lista de Aplicativos](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="23396-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="23396-228">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="23396-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23396-230">Click **Add** button.</span></span> <span data-ttu-id="23396-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23396-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="23396-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="23396-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23396-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23396-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23396-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23396-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="23396-236">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="23396-236">Test single sign-on</span></span>

<span data-ttu-id="23396-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="23396-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23396-238">Ao clicar no bloco do Voyance no Painel de Acesso, você deverá fazer logon automaticamente no aplicativo do Voyance.</span><span class="sxs-lookup"><span data-stu-id="23396-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23396-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="23396-239">Additional resources</span></span>

* [<span data-ttu-id="23396-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="23396-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23396-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23396-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

