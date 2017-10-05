---
title: "Tutorial: integração do Azure Active Directory com o BlueJeans | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="cb5c1-103">Tutorial: Integração do Azure Active Directory ao BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5c1-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="cb5c1-104">Neste tutorial, você aprende a integrar o BlueJeans ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cb5c1-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb5c1-105">A integração do BlueJeans ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cb5c1-106">No Azure AD, é possível controlar quem tem acesso ao BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5c1-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="cb5c1-107">É possível permitir que os usuários se conectem automaticamente ao BlueJeans (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5c1-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb5c1-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cb5c1-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb5c1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb5c1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb5c1-110">Prerequisites</span></span>

<span data-ttu-id="cb5c1-111">Para configurar a integração do Azure AD ao BlueJeans, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="cb5c1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb5c1-113">Uma assinatura habilitada para logon único do BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5c1-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb5c1-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb5c1-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb5c1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb5c1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb5c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb5c1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cb5c1-118">Scenario description</span></span>
<span data-ttu-id="cb5c1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb5c1-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb5c1-121">Adicionando o BlueJeans por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cb5c1-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="cb5c1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="cb5c1-123">Adicionando o BlueJeans por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cb5c1-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="cb5c1-124">Para configurar a integração do BlueJeans ao Azure AD, você precisa adicionar o BlueJeans à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cb5c1-125">**Para adicionar o BlueJeans por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cb5c1-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb5c1-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cb5c1-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cb5c1-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cb5c1-133">Na caixa de pesquisa, digite **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-133">In the search box, type **BlueJeans**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="cb5c1-135">No painel de resultados, selecione **BlueJeans** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb5c1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb5c1-138">Nesta seção, você configura e testa o logon único do Azure AD com o BlueJeans, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb5c1-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BlueJeans é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="cb5c1-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="cb5c1-141">No BlueJeans, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cb5c1-142">Para configurar e testar o logon único do Azure AD com o BlueJeans, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cb5c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cb5c1-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb5c1-145">**[Criando um usuário de teste do BlueJeans](#creating-a-bluejeans-test-user)** – para ter um equivalente de Brenda Fernandes no BlueJeans que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb5c1-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb5c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb5c1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb5c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb5c1-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="cb5c1-150">**Para configurar o logon único do Azure AD com o BlueJeans, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="cb5c1-151">No portal do Azure, na página de integração do aplicativo do **BlueJeans**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cb5c1-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="cb5c1-155">Na seção **Domínio e URLs do BlueJeans**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="cb5c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-157">a.</span></span> <span data-ttu-id="cb5c1-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="cb5c1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="cb5c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-159">b.</span></span> <span data-ttu-id="cb5c1-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="cb5c1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb5c1-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-161">These values are not real.</span></span> <span data-ttu-id="cb5c1-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cb5c1-163">Contate a [equipe de suporte ao Cliente do BlueJeans](https://support.bluejeans.com/contact) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="cb5c1-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="cb5c1-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cb5c1-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb5c1-168">Na seção **Configuração do BlueJeans**, clique em **Configurar o BlueJeans** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cb5c1-169">Copie a **URL de Saída, a URL de Alteração de Senha e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="cb5c1-171">Em outra janela do navegador da Web, faça logon em seu site de empresa do **BlueJeans** como administrador.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="cb5c1-172">Vá para **ADMINISTRADOR \> Configurações de Grupo \> Segurança**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="cb5c1-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="cb5c1-174">Na seção **Segurança** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="cb5c1-175">![Logon Único do SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="cb5c1-176">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-176">a.</span></span> <span data-ttu-id="cb5c1-177">Selecione **Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="cb5c1-178">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-178">b.</span></span> <span data-ttu-id="cb5c1-179">Selecione **Habilitar provisionamento automático**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="cb5c1-180">Siga em frente com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-180">Move on with the following steps:</span></span>

    <span data-ttu-id="cb5c1-181">![Caminho de Certificado](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Caminho de Certificado")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="cb5c1-182">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-182">a.</span></span> <span data-ttu-id="cb5c1-183">Clique em **Escolher Arquivo**e carregue o certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="cb5c1-184">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-184">b.</span></span> <span data-ttu-id="cb5c1-185">Cole a **URL do Serviço de Logon Único SAML** na caixa de texto **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="cb5c1-186">c.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-186">c.</span></span> <span data-ttu-id="cb5c1-187">Cole a **URL de Alteração de Senha** na caixa de texto **URL de Alteração de Senha**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="cb5c1-188">d.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-188">d.</span></span> <span data-ttu-id="cb5c1-189">Cole a **URL de Saída** na caixa de texto **URL de Logoff**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="cb5c1-190">Siga em frente com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="cb5c1-191">![Salvar Alterações](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Salvar Alterações")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="cb5c1-192">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-192">a.</span></span> <span data-ttu-id="cb5c1-193">Na caixa de texto **ID de usuário**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="cb5c1-194">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-194">b.</span></span> <span data-ttu-id="cb5c1-195">Na caixa de texto **Email**, digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="cb5c1-196">c.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-196">c.</span></span> <span data-ttu-id="cb5c1-197">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cb5c1-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="cb5c1-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cb5c1-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cb5c1-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb5c1-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb5c1-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb5c1-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cb5c1-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cb5c1-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb5c1-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb5c1-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb5c1-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb5c1-213">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-213">a.</span></span> <span data-ttu-id="cb5c1-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb5c1-215">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-215">b.</span></span> <span data-ttu-id="cb5c1-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb5c1-217">c.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-217">c.</span></span> <span data-ttu-id="cb5c1-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cb5c1-219">d.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-219">d.</span></span> <span data-ttu-id="cb5c1-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="cb5c1-221">Criando um usuário de teste do BlueJeans</span><span class="sxs-lookup"><span data-stu-id="cb5c1-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="cb5c1-222">Para permitir que os usuários do Azure AD façam logon no BlueJeans, eles devem ser provisionados no BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="cb5c1-223">No caso do BlueJeans, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="cb5c1-224">**Para provisionar contas de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="cb5c1-225">Faça logon em seu site de empresa do **BlueJeans** como administrador.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="cb5c1-226">Vá para **ADMINISTRADOR \> Gerenciar Usuários \> Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="cb5c1-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="cb5c1-228">A guia **Adicionar Usuário** só estará disponível se, na **guia Segurança**, a opção **Habilitar provisionamento automático** estiver desmarcada.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="cb5c1-229">Na seção **Adicionar Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cb5c1-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="cb5c1-230">![Adicionar Usuário](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="cb5c1-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="cb5c1-231">a.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-231">a.</span></span> <span data-ttu-id="cb5c1-232">Digite um **Nome de Usuário do BlueJeans**, **Endereço de email**, **ID de Reunião do BlueJeans**, **Senha de Moderador**, **Nome Completo** e a **Empresa** de uma conta válida do AAD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="cb5c1-233">b.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-233">b.</span></span> <span data-ttu-id="cb5c1-234">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="cb5c1-235">É possível usar qualquer outra ferramenta de criação da conta de usuário do BlueJeans ou as APIs fornecidas pelo BlueJeans para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cb5c1-236">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cb5c1-237">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cb5c1-239">**Para atribuir Brenda Fernandes ao BlueJeans, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cb5c1-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="cb5c1-240">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cb5c1-242">Na lista de aplicativos, selecione **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-242">In the applications list, select **BlueJeans**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="cb5c1-244">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cb5c1-246">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-246">Click **Add** button.</span></span> <span data-ttu-id="cb5c1-247">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cb5c1-249">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cb5c1-250">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb5c1-251">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb5c1-252">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cb5c1-252">Testing single sign-on</span></span>

<span data-ttu-id="cb5c1-253">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cb5c1-254">Quando você clicar no bloco BlueJeans no Painel de Acesso, deverá acessar a página de logon do aplicativo BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="cb5c1-255">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb5c1-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb5c1-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cb5c1-256">Additional resources</span></span>

* [<span data-ttu-id="cb5c1-257">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5c1-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb5c1-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb5c1-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

