---
title: "Tutorial: Integração do Azure Active Directory ao Samanage | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c54dbe407145a29a712acc3c0fb549a38ac26bed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="b8032-103">Tutorial: Integração do Azure Active Directory ao Samanage</span><span class="sxs-lookup"><span data-stu-id="b8032-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="b8032-104">Neste tutorial, você aprende a integrar o Samanage ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b8032-104">In this tutorial, you learn how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8032-105">A integração do Samanage ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="b8032-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8032-106">No Azure AD, é possível controlar quem tem acesso ao Samanage</span><span class="sxs-lookup"><span data-stu-id="b8032-106">You can control in Azure AD who has access to Samanage</span></span>
- <span data-ttu-id="b8032-107">Você pode permitir que seus usuários façam logon automaticamente no Samanage (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="b8032-107">You can enable your users to automatically get signed-on to Samanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8032-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8032-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8032-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8032-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8032-110">Prerequisites</span></span>

<span data-ttu-id="b8032-111">Para configurar a integração do Azure AD ao Samanage, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b8032-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

- <span data-ttu-id="b8032-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8032-113">Uma assinatura habilitada para logon único do Samanage</span><span class="sxs-lookup"><span data-stu-id="b8032-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8032-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b8032-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8032-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b8032-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8032-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b8032-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8032-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8032-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8032-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b8032-118">Scenario description</span></span>
<span data-ttu-id="b8032-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b8032-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8032-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="b8032-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8032-121">Adição do Samanage da galeria</span><span class="sxs-lookup"><span data-stu-id="b8032-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="b8032-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="b8032-123">Adição do Samanage da galeria</span><span class="sxs-lookup"><span data-stu-id="b8032-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="b8032-124">Para configurar a integração do Samanage ao Azure AD, você precisa adicionar o Samanage na galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b8032-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8032-125">**Para adicionar o Samanage da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b8032-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8032-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8032-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8032-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b8032-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8032-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b8032-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b8032-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8032-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b8032-133">Na caixa de pesquisa, digite **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="b8032-133">In the search box, type **Samanage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="b8032-135">No painel de resultados, selecione **Samanage** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8032-135">In the results panel, select **Samanage**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8032-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8032-138">Nesta seção, você configura e testa o logon único do Azure AD com o Samanage, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b8032-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b8032-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Samanage é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8032-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Samanage is to a user in Azure AD.</span></span> <span data-ttu-id="b8032-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Samanage.</span><span class="sxs-lookup"><span data-stu-id="b8032-140">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="b8032-141">No Samanage, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="b8032-141">In Samanage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8032-142">Para configurar e testar o logon único do Azure AD com o Samanage, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="b8032-142">To configure and test Azure AD single sign-on with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8032-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b8032-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8032-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b8032-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8032-145">**[Criando um usuário de teste do Samanage](#creating-a-samanage-test-user)** – para ter um equivalente de Brenda Fernandes no Samanage que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8032-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8032-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8032-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8032-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="b8032-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8032-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8032-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8032-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Samanage.</span><span class="sxs-lookup"><span data-stu-id="b8032-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="b8032-150">**Para configurar o logon único do Azure AD com o Samanage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b8032-150">**To configure Azure AD single sign-on with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="b8032-151">No portal do Azure, na página de integração do aplicativo **Samanage**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="b8032-151">In the Azure portal, on the **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b8032-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="b8032-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="b8032-155">Na seção **Domínio e URLs do Samanage**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b8032-155">On the **Samanage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="b8032-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8032-157">a.</span></span> <span data-ttu-id="b8032-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="b8032-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="b8032-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8032-159">b.</span></span> <span data-ttu-id="b8032-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="b8032-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8032-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b8032-161">These values are not real.</span></span> <span data-ttu-id="b8032-162">Atualize esses valores com a URL de Logon e o Identificador reais, que são explicados adiante no tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8032-162">Update these values with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> <span data-ttu-id="b8032-163">Para obter mais detalhes, contate a [equipe de suporte ao Cliente do Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="b8032-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="b8032-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="b8032-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="b8032-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b8032-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8032-168">Na seção **Configuração do Samanage**, clique em **Configurar o Samanage** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="b8032-168">On the **Samanage Configuration** section, click **Configure Samanage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b8032-169">Copie a **URL de Saída e a ID da Entidade SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="b8032-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="b8032-171">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="b8032-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="b8032-172">Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b8032-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="b8032-173">![Painel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Painel")</span><span class="sxs-lookup"><span data-stu-id="b8032-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="b8032-174">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="b8032-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="b8032-175">![Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="b8032-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="b8032-176">Navegue até a seção **Logon usando SAML** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b8032-176">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b8032-177">![Logon usando SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Logon usando SAML")</span><span class="sxs-lookup"><span data-stu-id="b8032-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="b8032-178">a.</span><span class="sxs-lookup"><span data-stu-id="b8032-178">a.</span></span> <span data-ttu-id="b8032-179">Clique em **Habilitar o Logon Único com SAML**.</span><span class="sxs-lookup"><span data-stu-id="b8032-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="b8032-180">b.</span><span class="sxs-lookup"><span data-stu-id="b8032-180">b.</span></span> <span data-ttu-id="b8032-181">Na caixa de texto **URL do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8032-181">In the **Identity Provider URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="b8032-182">c.</span><span class="sxs-lookup"><span data-stu-id="b8032-182">c.</span></span> <span data-ttu-id="b8032-183">Confirme se a **URL de Logon** corresponde à **URL de Logon** da seção **Domínio e URLs do Samanage** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8032-183">Confirm the **Login URL** matches the **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="b8032-184">d.</span><span class="sxs-lookup"><span data-stu-id="b8032-184">d.</span></span> <span data-ttu-id="b8032-185">Na caixa de texto **URL de Logoff**, insira o valor da **URL de Saída** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8032-185">In the **Logout URL** textbox, enter the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="b8032-186">e.</span><span class="sxs-lookup"><span data-stu-id="b8032-186">e.</span></span> <span data-ttu-id="b8032-187">Na caixa de texto **Emissor SAML**, digite o URI da ID do aplicativo definido no provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="b8032-187">In the **SAML Issuer** textbox, type the app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="b8032-188">f.</span><span class="sxs-lookup"><span data-stu-id="b8032-188">f.</span></span> <span data-ttu-id="b8032-189">Abra o certificado codificado em Base64 baixado no portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Cole o Certificado x.509 do Provedor de Identidade abaixo**.</span><span class="sxs-lookup"><span data-stu-id="b8032-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="b8032-190">g.</span><span class="sxs-lookup"><span data-stu-id="b8032-190">g.</span></span> <span data-ttu-id="b8032-191">Clique em **Criar usuários se eles não existirem no Samanage**.</span><span class="sxs-lookup"><span data-stu-id="b8032-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="b8032-192">h.</span><span class="sxs-lookup"><span data-stu-id="b8032-192">h.</span></span> <span data-ttu-id="b8032-193">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="b8032-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="b8032-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="b8032-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8032-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b8032-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8032-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8032-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8032-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8032-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b8032-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b8032-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b8032-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8032-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8032-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8032-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b8032-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8032-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8032-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8032-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b8032-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8032-209">a.</span><span class="sxs-lookup"><span data-stu-id="b8032-209">a.</span></span> <span data-ttu-id="b8032-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="b8032-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8032-211">b.</span><span class="sxs-lookup"><span data-stu-id="b8032-211">b.</span></span> <span data-ttu-id="b8032-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="b8032-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8032-213">c.</span><span class="sxs-lookup"><span data-stu-id="b8032-213">c.</span></span> <span data-ttu-id="b8032-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="b8032-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8032-215">d.</span><span class="sxs-lookup"><span data-stu-id="b8032-215">d.</span></span> <span data-ttu-id="b8032-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b8032-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="b8032-217">Criação de um usuário de teste de Samanage</span><span class="sxs-lookup"><span data-stu-id="b8032-217">Creating a Samanage test user</span></span>

<span data-ttu-id="b8032-218">Para permitir que os usuários do Azure AD façam logon no Samanage, eles devem ser provisionados no Samanage.</span><span class="sxs-lookup"><span data-stu-id="b8032-218">To enable Azure AD users to log in to Samanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="b8032-219">No caso do Samanage, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b8032-219">In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="b8032-220">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b8032-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b8032-221">Faça logon em seu site de empresa Samanage como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b8032-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="b8032-222">Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b8032-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="b8032-223">![Configuração](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="b8032-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="b8032-224">Clique na guia **Usuários**</span><span class="sxs-lookup"><span data-stu-id="b8032-224">Click the **Users** tab</span></span>
   
    <span data-ttu-id="b8032-225">![Usuários](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="b8032-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="b8032-226">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="b8032-226">Click **New User**.</span></span>
   
    <span data-ttu-id="b8032-227">![Novo Usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="b8032-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="b8032-228">Digite o **Nome** e o **Endereço de Email** de uma conta do Azure Active Directory que você deseja provisionar e clique em **Criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="b8032-228">Type the **Name** and the **Email Address** of an Azure Active Directory account you want to provision and click **Create user**.</span></span>
   
    <span data-ttu-id="b8032-229">![Criar usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="b8032-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="b8032-230">O titular da conta do Active Directory do Azure receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="b8032-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="b8032-231">Você pode usar qualquer outra ferramenta de criação de conta de usuário do Samanage ou as APIs fornecidas pelo Samanage para provisionar contas de usuário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8032-231">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8032-232">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8032-233">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Samanage.</span><span class="sxs-lookup"><span data-stu-id="b8032-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Samanage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b8032-235">**Para atribuir Brenda Fernandes ao Samanage, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="b8032-235">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="b8032-236">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b8032-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b8032-238">Na lista de aplicativos, selecione **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="b8032-238">In the applications list, select **Samanage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="b8032-240">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b8032-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b8032-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b8032-242">Click **Add** button.</span></span> <span data-ttu-id="b8032-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8032-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b8032-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="b8032-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8032-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8032-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8032-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8032-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8032-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b8032-248">Testing single sign-on</span></span>

<span data-ttu-id="b8032-249">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="b8032-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8032-250">Ao clicar no bloco do Samanage no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Samanage.</span><span class="sxs-lookup"><span data-stu-id="b8032-250">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>
<span data-ttu-id="b8032-251">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8032-251">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8032-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b8032-252">Additional resources</span></span>

* [<span data-ttu-id="b8032-253">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b8032-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8032-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8032-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

