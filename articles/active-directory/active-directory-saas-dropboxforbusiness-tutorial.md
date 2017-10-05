---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="1d9f4-103">Tutorial: integração do Active Directory do Azure ao Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="1d9f4-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="1d9f4-104">Neste tutorial, você aprende a integrar o Dropbox for Business ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1d9f4-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d9f4-105">A integração do Dropbox for Business ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d9f4-106">No Azure AD, é possível controlar quem tem acesso ao Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="1d9f4-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="1d9f4-107">É possível permitir que os usuários se conectem automaticamente ao Dropbox for Business (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d9f4-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d9f4-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1d9f4-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d9f4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d9f4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d9f4-110">Prerequisites</span></span>

<span data-ttu-id="1d9f4-111">Para configurar a integração do Azure AD ao Dropbox for Business, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="1d9f4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d9f4-113">Uma assinatura habilitada para logon único do Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="1d9f4-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d9f4-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d9f4-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d9f4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d9f4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d9f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d9f4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1d9f4-118">Scenario description</span></span>
<span data-ttu-id="1d9f4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d9f4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d9f4-121">Adicionando o Dropbox for Business por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="1d9f4-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="1d9f4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="1d9f4-123">Adicionando o Dropbox for Business por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="1d9f4-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="1d9f4-124">Para configurar a integração do Dropbox for Business ao Azure AD, é necessário adicionar o Dropbox for Business à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d9f4-125">**Para adicionar o Dropbox for Business por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d9f4-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d9f4-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d9f4-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d9f4-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1d9f4-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1d9f4-133">Na caixa de pesquisa, digite **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="1d9f4-135">No painel de resultados, selecione **Dropbox for Business** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d9f4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d9f4-138">Nesta seção, você configura e testa o logon único do Azure AD com o Dropbox for Business, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1d9f4-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Dropbox for Business é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="1d9f4-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="1d9f4-141">Essa relação de vínculo é estabelecida com a atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="1d9f4-142">Para configurar e testar o logon único do Azure AD com o Dropbox for Business, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d9f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d9f4-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d9f4-145">**[Criando um usuário de teste do Dropbox for Business](#creating-a-dropbox-for-business-test-user)** – para ter um equivalente de Brenda Fernandes no Dropbox for Business que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d9f4-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d9f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d9f4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d9f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d9f4-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="1d9f4-150">**Para configurar o logon único do Azure AD com o Dropbox for Business, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d9f4-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="1d9f4-151">No portal do Azure, na página de integração do aplicativo **Dropbox for Business**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1d9f4-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="1d9f4-155">Na seção **Domínio e URLs do Dropbox for Business**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="1d9f4-156">a.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-156">a.</span></span> <span data-ttu-id="1d9f4-157">Faça logon no locatário do Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="1d9f4-158">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1d9f4-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="1d9f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-159">b.</span></span> <span data-ttu-id="1d9f4-160">No painel de navegação à esquerda, clique em **Console do Administrador**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="1d9f4-161">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1d9f4-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="1d9f4-162">c.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-162">c.</span></span> <span data-ttu-id="1d9f4-163">No **Console do Administrador**, clique em **Autenticação** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="1d9f4-164">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1d9f4-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="1d9f4-165">d.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-165">d.</span></span> <span data-ttu-id="1d9f4-166">Na seção **Logon único**, selecione **Habilitar logon único** e clique em **Mais** para expandir essa seção.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="1d9f4-167">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1d9f4-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="1d9f4-168">e.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-168">e.</span></span> <span data-ttu-id="1d9f4-169">Copie a URL ao lado de **Os usuários podem entrar inserindo o endereço de email ou podem ir diretamente para**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurar o logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="1d9f4-171">f.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-171">f.</span></span> <span data-ttu-id="1d9f4-172">No portal do Azure, na caixa de texto **URL de Logon**, cole a URL.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="1d9f4-174">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="1d9f4-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d9f4-175">Esse valor não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-175">This value is not real value.</span></span> <span data-ttu-id="1d9f4-176">Atualize o valor com a URL de Logon real obtida na seção Logon único.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="1d9f4-177">Contate a [equipe de suporte ao Cliente do Dropbox for Business](https://www.dropbox.com/business/contact) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="1d9f4-178">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="1d9f4-180">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1d9f4-180">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d9f4-182">Na seção **Configuração do Dropbox for Business** do portal do Azure, clique em **Configurar o Dropbox for Business** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1d9f4-183">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="1d9f4-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="1d9f4-185">Para configurar o logon único no lado do **Dropbox for Business**, acesse o locatário do Dropbox for Business e, na seção **Logon único** da página **Autenticação**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="1d9f4-186">![Configurar logon único](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurar logon único")</span><span class="sxs-lookup"><span data-stu-id="1d9f4-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="1d9f4-187">a.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-187">a.</span></span> <span data-ttu-id="1d9f4-188">Clique em **Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-188">Click **Required**.</span></span>
   
    <span data-ttu-id="1d9f4-189">b.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-189">b.</span></span> <span data-ttu-id="1d9f4-190">No portal do Azure, na janela **Configurar logon**, copie o valor da **URL do Serviço de Logon Único SAML** e, em seguida, cole-o na caixa de texto **URL de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="1d9f4-191">c.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-191">c.</span></span> <span data-ttu-id="1d9f4-192">Clique em **Escolher certificado** e, depois, procure o **arquivo de certificado codificado em Base64**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="1d9f4-193">d.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-193">d.</span></span> <span data-ttu-id="1d9f4-194">Clique em **Salvar alterações** para concluir a configuração no seu locatário do DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="1d9f4-195">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="1d9f4-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d9f4-196">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d9f4-197">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d9f4-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d9f4-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d9f4-199">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1d9f4-201">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d9f4-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d9f4-202">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="1d9f4-204">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d9f4-206">Na parte superior da caixa de diálogo, clique em **Adicionar** para abrir a caixa de diálogo **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d9f4-208">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1d9f4-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d9f4-210">a.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-210">a.</span></span> <span data-ttu-id="1d9f4-211">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d9f4-212">b.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-212">b.</span></span> <span data-ttu-id="1d9f4-213">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d9f4-214">c.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-214">c.</span></span> <span data-ttu-id="1d9f4-215">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d9f4-216">d.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-216">d.</span></span> <span data-ttu-id="1d9f4-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="1d9f4-218">Criando um usuário de teste do Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="1d9f4-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="1d9f4-219">Nesta seção, um usuário chamado Brenda Fernandes é criado no Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="1d9f4-220">O Dropbox for Business dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="1d9f4-221">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-221">There is no action item for you in this section.</span></span> <span data-ttu-id="1d9f4-222">Se um usuário ainda não existir no Dropbox for Business, um novo será criado quando você tentar acessar o Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="1d9f4-223">Se você precisar criar um usuário manualmente, contate a [equipe de suporte ao Cliente do Dropbox for Business](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="1d9f4-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d9f4-224">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d9f4-225">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1d9f4-227">**Para atribuir Brenda Fernandes ao Dropbox for Business, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="1d9f4-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="1d9f4-228">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1d9f4-230">Na lista de aplicativos, selecione **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="1d9f4-232">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1d9f4-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-234">Click **Add** button.</span></span> <span data-ttu-id="1d9f4-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1d9f4-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d9f4-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d9f4-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d9f4-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1d9f4-240">Testing single sign-on</span></span>

<span data-ttu-id="1d9f4-241">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d9f4-242">Quando você clicar no bloco do Dropbox for Business no Painel de Acesso, deverá ver a página de logon do aplicativo Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="1d9f4-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d9f4-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1d9f4-243">Additional resources</span></span>

* [<span data-ttu-id="1d9f4-244">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1d9f4-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d9f4-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1d9f4-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1d9f4-246">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="1d9f4-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

