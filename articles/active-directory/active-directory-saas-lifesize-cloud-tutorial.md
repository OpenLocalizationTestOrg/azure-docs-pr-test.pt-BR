---
title: "Tutorial: integração do Azure Active Directory ao Lifesize Cloud | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Lifesize Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="b12dc-103">Tutorial: Integração do Azure Active Directory com o Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="b12dc-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="b12dc-104">Neste tutorial, você aprenderá a integrar o Lifesize Cloud ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b12dc-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b12dc-105">A integração do Lifesize Cloud ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="b12dc-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b12dc-106">No Azure AD, você pode controlar quem tem acesso ao Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="b12dc-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="b12dc-107">Você pode habilitar os usuários a fazer logon automaticamente no Lifesize Cloud (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b12dc-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b12dc-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b12dc-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b12dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b12dc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b12dc-110">Prerequisites</span></span>

<span data-ttu-id="b12dc-111">Para configurar a integração do Azure AD com o Lifesize Cloud, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b12dc-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="b12dc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b12dc-113">Uma assinatura habilitada para logon único do Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="b12dc-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b12dc-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b12dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b12dc-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b12dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b12dc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b12dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b12dc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b12dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b12dc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b12dc-118">Scenario description</span></span>
<span data-ttu-id="b12dc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b12dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b12dc-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="b12dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b12dc-121">Adição do Lifesize Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="b12dc-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="b12dc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="b12dc-123">Adição do Lifesize Cloud da galeria</span><span class="sxs-lookup"><span data-stu-id="b12dc-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="b12dc-124">Para configurar a integração do Lifesize Cloud ao Azure AD, você precisará adicionar o Lifesize Cloud da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b12dc-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b12dc-125">**Para adicionar o Lifesize Cloud da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b12dc-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b12dc-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b12dc-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b12dc-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b12dc-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b12dc-133">Na caixa de pesquisa, digite **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="b12dc-135">No painel de resultados, selecione **Lifesize Cloud** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b12dc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b12dc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lifesize Cloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b12dc-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b12dc-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Lifesize Cloud é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b12dc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="b12dc-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="b12dc-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="b12dc-141">No Lifesize Cloud, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b12dc-142">Para configurar e testar o logon único do Azure AD com o Lifesize Cloud, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b12dc-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b12dc-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b12dc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b12dc-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b12dc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b12dc-145">**[Criar um usuário de teste do Lifesize Cloud](#creating-a-lifesize-cloud-test-user)** – para ter um equivalente de Brenda Fernandes no Lifesize Cloud que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b12dc-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b12dc-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12dc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b12dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="b12dc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b12dc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b12dc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b12dc-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="b12dc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="b12dc-150">**Para configurar o logon único do Azure AD com o Lifesize Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b12dc-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b12dc-151">No portal do Azure, na página de integração do aplicativo do **Lifesize Cloud**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b12dc-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b12dc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="b12dc-155">Na seção **Domínio e URLs do Lifesize Cloud**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b12dc-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="b12dc-157">a.</span><span class="sxs-lookup"><span data-stu-id="b12dc-157">a.</span></span> <span data-ttu-id="b12dc-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="b12dc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="b12dc-159">b.</span><span class="sxs-lookup"><span data-stu-id="b12dc-159">b.</span></span> <span data-ttu-id="b12dc-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b12dc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="b12dc-161">Marque **Mostrar configurações avançadas de URL**, execute a seguinte etapa:</span><span class="sxs-lookup"><span data-stu-id="b12dc-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="b12dc-163">Na caixa de texto **Estado de Retransmissão**, digite uma URL usando os seguintes padrões: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="b12dc-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="b12dc-164">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="b12dc-164">Please note that these are not the real values.</span></span> <span data-ttu-id="b12dc-165">é necessário atualizar esses valores com a URL de Logon, o Estado de retransmissão e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="b12dc-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="b12dc-166">Entre em contato com a [equipe de suporte do cliente Lifesize Cloud](https://www.lifesize.com/support) para obter a URL de Logon e os valores de identificador e você pode obter o valor do Estado de Retransmissão da configuração de SSO que é explicada posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="b12dc-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="b12dc-167">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="b12dc-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="b12dc-169">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b12dc-169">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b12dc-171">Na seção **Configuração do Lifesize Cloud**, clique em **Configurar Lifesize Cloud** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b12dc-172">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="b12dc-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="b12dc-174">Para configurar o SSO para seu aplicativo, faça logon no aplicativo Lifesize Cloud com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="b12dc-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="b12dc-175">No canto superior direito, clique em seu nome e, em seguida, clique em **Configurações Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="b12dc-177">Nas configurações de adiantamento agora, clique em de **configuração de SSO** link.</span><span class="sxs-lookup"><span data-stu-id="b12dc-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="b12dc-178">Isso abrirá a página de configuração de SSO para sua instância.</span><span class="sxs-lookup"><span data-stu-id="b12dc-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="b12dc-180">Agora, configure os seguintes valores na interface do usuário de configuração de SSO.</span><span class="sxs-lookup"><span data-stu-id="b12dc-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="b12dc-182">a.</span><span class="sxs-lookup"><span data-stu-id="b12dc-182">a.</span></span> <span data-ttu-id="b12dc-183">Na caixa de texto **Emissor do Provedor de Identidade**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12dc-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b12dc-184">b.</span><span class="sxs-lookup"><span data-stu-id="b12dc-184">b.</span></span>  <span data-ttu-id="b12dc-185">Na caixa de texto **URL de Logon**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b12dc-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b12dc-186">c.</span><span class="sxs-lookup"><span data-stu-id="b12dc-186">c.</span></span> <span data-ttu-id="b12dc-187">Abra seu certificado codificado em base 64 no bloco de notas baixado do portal do Azure, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="b12dc-188">d.</span><span class="sxs-lookup"><span data-stu-id="b12dc-188">d.</span></span> <span data-ttu-id="b12dc-189">No mapeamento de atributo do SAML para a caixa de texto Nome, insira o valor como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="b12dc-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="b12dc-190">e.</span><span class="sxs-lookup"><span data-stu-id="b12dc-190">e.</span></span> <span data-ttu-id="b12dc-191">No mapeamento de atributo SAML para a caixa de texto **Sobrenome**, insira o valor como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="b12dc-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="b12dc-192">f.</span><span class="sxs-lookup"><span data-stu-id="b12dc-192">f.</span></span> <span data-ttu-id="b12dc-193">No mapeamento de atributo SAML para a caixa de texto **Email**, insira o valor como **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="b12dc-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="b12dc-194">Para verificar a configuração, você pode clicar no botão **Testar**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="b12dc-195">Para realizar um teste bem-sucedido, você precisa concluir o assistente de configuração no Azure AD e também fornecer acesso a usuários ou grupos que possam executar o teste.</span><span class="sxs-lookup"><span data-stu-id="b12dc-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="b12dc-196">Habilite o SSO ao marcar o botão **Habilitar SSO**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="b12dc-197">Agora, clique no botão **Atualizar** para que todas as configurações sejam salvas.</span><span class="sxs-lookup"><span data-stu-id="b12dc-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="b12dc-198">Isso irá gerar o valor de RelayState.</span><span class="sxs-lookup"><span data-stu-id="b12dc-198">This will generate the RelayState value.</span></span> <span data-ttu-id="b12dc-199">Copie o valor de RelayState, que é gerado na caixa de texto, cole-o na caixa de texto **Estado de Retransmissão** na seção **URLs e Domínio do Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="b12dc-200">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="b12dc-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b12dc-201">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b12dc-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b12dc-202">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b12dc-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b12dc-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="b12dc-204">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b12dc-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b12dc-206">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b12dc-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b12dc-207">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b12dc-209">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b12dc-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b12dc-211">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b12dc-213">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b12dc-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b12dc-215">a.</span><span class="sxs-lookup"><span data-stu-id="b12dc-215">a.</span></span> <span data-ttu-id="b12dc-216">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b12dc-217">b.</span><span class="sxs-lookup"><span data-stu-id="b12dc-217">b.</span></span> <span data-ttu-id="b12dc-218">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b12dc-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b12dc-219">c.</span><span class="sxs-lookup"><span data-stu-id="b12dc-219">c.</span></span> <span data-ttu-id="b12dc-220">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b12dc-221">d.</span><span class="sxs-lookup"><span data-stu-id="b12dc-221">d.</span></span> <span data-ttu-id="b12dc-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="b12dc-223">Criação de um usuário de teste do Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="b12dc-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="b12dc-224">Nesta seção, você criará um usuário chamado Brenda Fernandes no Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="b12dc-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="b12dc-225">O Lifesize Cloud oferece suporte ao provisionamento automático de usuário.</span><span class="sxs-lookup"><span data-stu-id="b12dc-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="b12dc-226">Após a autenticação bem-sucedida no Azure AD, o usuário será provisionado no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b12dc-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b12dc-227">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b12dc-228">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="b12dc-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b12dc-230">**Para atribuir Brenda Fernandes ao Lifesize Cloud, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b12dc-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b12dc-231">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b12dc-233">Na lista de aplicativos, selecione **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="b12dc-235">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b12dc-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b12dc-237">Click **Add** button.</span></span> <span data-ttu-id="b12dc-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b12dc-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b12dc-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b12dc-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b12dc-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b12dc-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b12dc-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b12dc-243">Testing single sign-on</span></span>

<span data-ttu-id="b12dc-244">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b12dc-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b12dc-245">Ao clicar no bloco Lifesize Cloud no Painel de Acesso, você deve entrar na página de logon no aplicativo Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="b12dc-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="b12dc-246">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b12dc-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b12dc-247">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b12dc-247">Additional resources</span></span>

* [<span data-ttu-id="b12dc-248">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b12dc-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b12dc-249">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b12dc-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

