---
title: "Tutorial: integração do Azure Active Directory ao Weekdone | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="8e3d6-103">Tutorial: integração do Azure Active Directory ao Weekdone</span><span class="sxs-lookup"><span data-stu-id="8e3d6-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="8e3d6-104">Neste tutorial, você aprenderá como integrar o Weekdone ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8e3d6-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e3d6-105">A integração do Weekdone ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e3d6-106">Você pode controlar no Azure AD quem tem acesso ao Weekdone</span><span class="sxs-lookup"><span data-stu-id="8e3d6-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="8e3d6-107">Você pode habilitar seus usuários a fazerem logon automaticamente no Weekdone (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e3d6-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e3d6-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e3d6-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e3d6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e3d6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8e3d6-110">Prerequisites</span></span>

<span data-ttu-id="8e3d6-111">Para configurar a integração do Azure AD ao Weekdone, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="8e3d6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e3d6-113">Uma assinatura do Weekdone habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="8e3d6-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e3d6-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e3d6-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e3d6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e3d6-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e3d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e3d6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8e3d6-118">Scenario description</span></span>
<span data-ttu-id="8e3d6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e3d6-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e3d6-121">Adicionando Weekdone da galeria</span><span class="sxs-lookup"><span data-stu-id="8e3d6-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="8e3d6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="8e3d6-123">Adicionando Weekdone da galeria</span><span class="sxs-lookup"><span data-stu-id="8e3d6-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="8e3d6-124">Para configurar a integração do Weekdone ao Azure AD, você precisa adicionar o Weekdone na galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e3d6-125">**Para adicionar o Weekdone da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e3d6-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e3d6-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e3d6-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e3d6-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8e3d6-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8e3d6-133">Na caixa de pesquisa, digite **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-133">In the search box, type **Weekdone**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="8e3d6-135">No painel de resultados, selecione **Weekdone** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e3d6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e3d6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Weekdone com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e3d6-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Weekdone é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="8e3d6-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Weekdone.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="8e3d6-141">No Weekdone, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e3d6-142">Para configurar e testar o logon único do Azure AD com o Weekdone, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e3d6-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e3d6-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e3d6-145">**[Criação de um usuário de teste do Weekdone](#creating-a-weekdone-test-user)** – para ter um equivalente de Brenda Fernandes no Weekdone que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e3d6-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e3d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e3d6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e3d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e3d6-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Weekdone.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="8e3d6-150">**Para configurar o logon único do Azure AD com o Weekdone, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e3d6-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="8e3d6-151">No Portal do Azure, na página de integração de aplicativos do **Weekdone**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8e3d6-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="8e3d6-155">Na seção **URLs e Domínio do Weekdone**, se você desejar configurar o aplicativo em modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="8e3d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-157">a.</span></span> <span data-ttu-id="8e3d6-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="8e3d6-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="8e3d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-159">b.</span></span> <span data-ttu-id="8e3d6-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="8e3d6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="8e3d6-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="8e3d6-162">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="8e3d6-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="8e3d6-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8e3d6-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-165">These values are not real.</span></span> <span data-ttu-id="8e3d6-166">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8e3d6-167">Contate a [equipe de suporte ao cliente do Weekdone](mailto:hello@weekdone.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="8e3d6-168">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="8e3d6-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8e3d6-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8e3d6-172">Na seção **Configuração do Weekdone**, clique em **Configurar o Weekdone** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e3d6-173">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="8e3d6-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="8e3d6-175">Para configurar o logon único no lado do **Weekdone**, é necessário enviar o **XML de metadados, a URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** baixados para a [equipe de suporte do Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="8e3d6-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="8e3d6-176">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8e3d6-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e3d6-177">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e3d6-178">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e3d6-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e3d6-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e3d6-180">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8e3d6-182">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e3d6-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e3d6-183">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e3d6-185">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e3d6-187">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e3d6-189">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8e3d6-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e3d6-191">a.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-191">a.</span></span> <span data-ttu-id="8e3d6-192">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e3d6-193">b.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-193">b.</span></span> <span data-ttu-id="8e3d6-194">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e3d6-195">c.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-195">c.</span></span> <span data-ttu-id="8e3d6-196">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e3d6-197">d.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-197">d.</span></span> <span data-ttu-id="8e3d6-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="8e3d6-199">Criando um usuário de teste Weekdone</span><span class="sxs-lookup"><span data-stu-id="8e3d6-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="8e3d6-200">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Weekdone.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="8e3d6-201">O Weekdone dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8e3d6-202">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-202">There is no action item for you in this section.</span></span> <span data-ttu-id="8e3d6-203">Um novo usuário será criado durante uma tentativa de acessar o Weekdone se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="8e3d6-204">Se for necessário criar um usuário manualmente, será preciso contatar a [equipe de suporte ao cliente do Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="8e3d6-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e3d6-205">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e3d6-206">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Weekdone.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8e3d6-208">**Para atribuir Brenda Fernandes ao Weekdone, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8e3d6-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="8e3d6-209">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8e3d6-211">Na lista de aplicativos, selecione **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-211">In the applications list, select **Weekdone**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="8e3d6-213">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8e3d6-215">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-215">Click **Add** button.</span></span> <span data-ttu-id="8e3d6-216">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8e3d6-218">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e3d6-219">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e3d6-220">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e3d6-221">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8e3d6-221">Testing single sign-on</span></span>

<span data-ttu-id="8e3d6-222">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8e3d6-223">Quando você clica no bloco Weekdone no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo Weekdone.</span><span class="sxs-lookup"><span data-stu-id="8e3d6-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e3d6-224">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8e3d6-224">Additional resources</span></span>

* [<span data-ttu-id="8e3d6-225">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8e3d6-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e3d6-226">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e3d6-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

