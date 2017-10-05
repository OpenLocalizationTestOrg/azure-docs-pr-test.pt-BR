---
title: "Tutorial: Integração do Azure Active Directory com o Recognize | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Recognize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="1f282-103">Tutorial: integração do Azure Active Directory com o Recognize</span><span class="sxs-lookup"><span data-stu-id="1f282-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="1f282-104">Neste tutorial, você aprende a integrar o Recognize ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1f282-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f282-105">A integração do Recognize ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1f282-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f282-106">Você pode controlar no Azure AD quem tem acesso ao Recognize</span><span class="sxs-lookup"><span data-stu-id="1f282-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="1f282-107">Você pode permitir que os usuários façam logon automaticamente no Recognize (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f282-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f282-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f282-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f282-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f282-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f282-110">Prerequisites</span></span>

<span data-ttu-id="1f282-111">Para configurar a integração do Azure AD ao Recognize, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1f282-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="1f282-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f282-113">Uma assinatura habilitada para logon único do Recognize</span><span class="sxs-lookup"><span data-stu-id="1f282-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f282-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1f282-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f282-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1f282-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f282-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1f282-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f282-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f282-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f282-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1f282-118">Scenario description</span></span>
<span data-ttu-id="1f282-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1f282-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f282-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1f282-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f282-121">Adicionando o Recognize da galeria</span><span class="sxs-lookup"><span data-stu-id="1f282-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="1f282-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="1f282-123">Adicionando o Recognize da galeria</span><span class="sxs-lookup"><span data-stu-id="1f282-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="1f282-124">Para configurar a integração do Recognize ao Azure AD, você precisará adicionar o Recognize da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1f282-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f282-125">**Para adicionar o Recognize da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f282-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f282-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f282-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f282-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1f282-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f282-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f282-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1f282-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f282-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1f282-133">Na caixa de pesquisa, digite **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="1f282-133">In the search box, type **Recognize**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="1f282-135">No painel de resultados, selecione **Recognize** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f282-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f282-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f282-138">Nesta seção, você configura e testa o logon único do Azure AD com o Recognize, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1f282-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f282-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Recognize é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f282-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="1f282-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Recognize.</span><span class="sxs-lookup"><span data-stu-id="1f282-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="1f282-141">No Recognize, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="1f282-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1f282-142">Para configurar e testar o logon único do Azure AD com o Recognize, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1f282-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f282-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1f282-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f282-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f282-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f282-145">**[Criando um usuário de teste do Recognize](#creating-a-recognize-test-user)** – para ter um equivalente de Brenda Fernandes no Recognize que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f282-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f282-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f282-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f282-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1f282-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f282-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f282-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f282-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Recognize.</span><span class="sxs-lookup"><span data-stu-id="1f282-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="1f282-150">**Para configurar o logon único do Azure AD com o Recognize, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f282-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="1f282-151">No portal do Azure, na página de integração do aplicativo **Recognize**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1f282-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1f282-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1f282-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="1f282-155">Na seção **Domínio e URLs do Recognize**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1f282-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="1f282-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f282-157">a.</span></span> <span data-ttu-id="1f282-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="1f282-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="1f282-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f282-159">b.</span></span> <span data-ttu-id="1f282-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="1f282-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1f282-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1f282-161">These values are not real.</span></span> <span data-ttu-id="1f282-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="1f282-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1f282-163">Contate a [equipe de suporte ao Cliente do Recognize](mailto:support@recognizeapp.com) para obter a URL de Logon. Você pode obter o valor do Identificador abrindo a URL de Metadados do Provedor de Serviços na seção Configurações de SSO, explicada adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="1f282-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="1f282-164">.</span><span class="sxs-lookup"><span data-stu-id="1f282-164">.</span></span> 
 
4. <span data-ttu-id="1f282-165">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1f282-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="1f282-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1f282-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f282-169">Na seção **Configuração do Recognize**, clique em **Configurar o Recognize** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1f282-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f282-170">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1f282-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="1f282-172">Em uma janela diferente do navegador da Web, faça logon em seu locatário do Recognize como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1f282-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="1f282-173">No canto superior direito, clique em **Menu**.</span><span class="sxs-lookup"><span data-stu-id="1f282-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="1f282-174">Vá para **Administrador da Empresa**.</span><span class="sxs-lookup"><span data-stu-id="1f282-174">Go to **Company Admin**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="1f282-176">No painel de navegação esquerdo, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1f282-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="1f282-178">Realize as seguintes etapas na seção **Configurações do SSO**.</span><span class="sxs-lookup"><span data-stu-id="1f282-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="1f282-180">a.</span><span class="sxs-lookup"><span data-stu-id="1f282-180">a.</span></span> <span data-ttu-id="1f282-181">Em **Habilitar SSO**, selecione **ATIVADO**.</span><span class="sxs-lookup"><span data-stu-id="1f282-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="1f282-182">b.</span><span class="sxs-lookup"><span data-stu-id="1f282-182">b.</span></span> <span data-ttu-id="1f282-183">Na caixa de texto **ID da Entidade IDP**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f282-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1f282-184">c.</span><span class="sxs-lookup"><span data-stu-id="1f282-184">c.</span></span> <span data-ttu-id="1f282-185">Na caixa de texto **URL de destino do SSO**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f282-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1f282-186">d.</span><span class="sxs-lookup"><span data-stu-id="1f282-186">d.</span></span> <span data-ttu-id="1f282-187">Na caixa de texto **URL de destino do SLO**, cole o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f282-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="1f282-188">e.</span><span class="sxs-lookup"><span data-stu-id="1f282-188">e.</span></span> <span data-ttu-id="1f282-189">Abra o arquivo de **Certificado (Base64)** baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="1f282-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="1f282-190">f.</span><span class="sxs-lookup"><span data-stu-id="1f282-190">f.</span></span> <span data-ttu-id="1f282-191">Clique no botão **Salvar configurações**.</span><span class="sxs-lookup"><span data-stu-id="1f282-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="1f282-192">Ao lado da seção **Configurações de SSO**, copie a URL em **URL de metadados do provedor de serviço**.</span><span class="sxs-lookup"><span data-stu-id="1f282-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="1f282-194">Abra o **link da URL de metadados** em um navegador em branco para baixar o documento de metadados.</span><span class="sxs-lookup"><span data-stu-id="1f282-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="1f282-195">Em seguida, copie o value(entityID) do EntityDescriptor do arquivo e cole-o na caixa de texto **Identificador** na **seção Domínio e URLs do Recognize** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f282-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="1f282-197">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1f282-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f282-198">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1f282-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f282-199">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f282-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f282-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f282-201">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f282-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1f282-203">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f282-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f282-204">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f282-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f282-206">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1f282-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f282-208">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f282-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f282-210">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1f282-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f282-212">a.</span><span class="sxs-lookup"><span data-stu-id="1f282-212">a.</span></span> <span data-ttu-id="1f282-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1f282-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f282-214">b.</span><span class="sxs-lookup"><span data-stu-id="1f282-214">b.</span></span> <span data-ttu-id="1f282-215">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1f282-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f282-216">c.</span><span class="sxs-lookup"><span data-stu-id="1f282-216">c.</span></span> <span data-ttu-id="1f282-217">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1f282-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f282-218">d.</span><span class="sxs-lookup"><span data-stu-id="1f282-218">d.</span></span> <span data-ttu-id="1f282-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1f282-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="1f282-220">Criando um usuário de teste do Recognize</span><span class="sxs-lookup"><span data-stu-id="1f282-220">Creating a Recognize test user</span></span>

<span data-ttu-id="1f282-221">Para permitir que os usuários do Azure AD façam logon no Recognize, eles deverão ser provisionados no Recognize.</span><span class="sxs-lookup"><span data-stu-id="1f282-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="1f282-222">No caso do Recognize, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="1f282-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="1f282-223">Este aplicativo não dá suporte ao provisionamento de SCIM, mas tem uma sincronização de usuário alternativa que provisiona usuários.</span><span class="sxs-lookup"><span data-stu-id="1f282-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="1f282-224">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f282-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1f282-225">Faça logon em seu site de empresa Recognize como um administrador.</span><span class="sxs-lookup"><span data-stu-id="1f282-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="1f282-226">No canto superior direito, clique em **Menu**.</span><span class="sxs-lookup"><span data-stu-id="1f282-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="1f282-227">Vá para **Administrador da Empresa**.</span><span class="sxs-lookup"><span data-stu-id="1f282-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="1f282-228">No painel de navegação esquerdo, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1f282-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="1f282-229">Execute as seguintes etapas na seção **Sincronização de usuário**.</span><span class="sxs-lookup"><span data-stu-id="1f282-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="1f282-230">![Novo Usuário](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="1f282-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="1f282-231">a.</span><span class="sxs-lookup"><span data-stu-id="1f282-231">a.</span></span> <span data-ttu-id="1f282-232">Em **Sincronização habilitada**, selecione **ATIVADO**.</span><span class="sxs-lookup"><span data-stu-id="1f282-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="1f282-233">b.</span><span class="sxs-lookup"><span data-stu-id="1f282-233">b.</span></span> <span data-ttu-id="1f282-234">Em **Escolher o provedor de sincronização**, selecione **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1f282-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="1f282-235">c.</span><span class="sxs-lookup"><span data-stu-id="1f282-235">c.</span></span> <span data-ttu-id="1f282-236">Clique em **Executar Sincronização de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1f282-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f282-237">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f282-238">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Recognize.</span><span class="sxs-lookup"><span data-stu-id="1f282-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1f282-240">**Para atribuir Brenda Fernandes ao Recognize, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1f282-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="1f282-241">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1f282-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1f282-243">Na lista de aplicativos, escolha **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="1f282-243">In the applications list, select **Recognize**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="1f282-245">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1f282-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1f282-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1f282-247">Click **Add** button.</span></span> <span data-ttu-id="1f282-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f282-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1f282-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1f282-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f282-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f282-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f282-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1f282-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f282-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1f282-253">Testing single sign-on</span></span>

<span data-ttu-id="1f282-254">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1f282-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f282-255">Ao clicar no bloco do Recognize no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do Recognize.</span><span class="sxs-lookup"><span data-stu-id="1f282-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="1f282-256">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1f282-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f282-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1f282-257">Additional resources</span></span>

* [<span data-ttu-id="1f282-258">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1f282-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f282-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f282-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

