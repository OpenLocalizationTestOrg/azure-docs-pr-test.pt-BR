---
title: "Tutorial: Integração do Azure Active Directory com o Cloud Management Portal for Microsoft Azure | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Cloud Management Portal for Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: bae5f05a161b2730bf662bcb47f20ab3e1799951
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="5db63-103">Tutorial: Integração do Azure Active Directory com o Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="5db63-104">O objetivo deste tutorial é mostrar como integrar o Cloud Management Portal do Microsoft Azure ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5db63-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5db63-105">A Integração do Cloud Management Portal for Microsoft Azure com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5db63-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5db63-106">No Azure AD, você pode controlar quem tem acesso ao Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="5db63-107">Você pode permitir que seus usuários façam logon automaticamente no Cloud Management Portal for Microsoft Azure (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5db63-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5db63-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5db63-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5db63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5db63-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5db63-110">Prerequisites</span></span>

<span data-ttu-id="5db63-111">Para configurar a integração do Azure AD com o Cloud Management Portal for Microsoft Azure, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5db63-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="5db63-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5db63-113">Uma assinatura habilitada para logon único do Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5db63-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5db63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5db63-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5db63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5db63-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5db63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5db63-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5db63-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5db63-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5db63-118">Scenario description</span></span>
<span data-ttu-id="5db63-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5db63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5db63-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5db63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5db63-121">Adição do Cloud Management Portal for Microsoft Azure a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="5db63-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
2. <span data-ttu-id="5db63-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="5db63-123">Adição do Cloud Management Portal for Microsoft Azure a partir da galeria</span><span class="sxs-lookup"><span data-stu-id="5db63-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="5db63-124">Para configurar a integração do Cloud Management Portal for Microsoft Azure ao Azure AD, você precisará adicionar o Cloud Management Portal for Microsoft Azure da galeria para sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5db63-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5db63-125">**Para adicionar o Cloud Management Portal for Microsoft Azure a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5db63-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5db63-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5db63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5db63-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5db63-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5db63-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5db63-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5db63-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5db63-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5db63-133">Na caixa de pesquisa, digite **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5db63-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="5db63-135">No painel de resultados, selecione **Cloud Management Portal for Microsoft Azure** e clique em **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5db63-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5db63-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5db63-138">O objetivo desta seção é mostrar como configurar e testar o logon único do Azure AD com o Cloud Management Portal for Microsoft Azure, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="5db63-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5db63-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Cloud Management Portal for Microsoft Azure é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5db63-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="5db63-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="5db63-141">No Cloud Management Portal for Microsoft Azure, atribua o valor de **nome de usuário** no Azure AD ao valor de **Nome de Usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5db63-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5db63-142">Para configurar e testar o logon único do Azure AD com o Cloud Management Portal for Microsoft Azure, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5db63-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5db63-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5db63-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5db63-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5db63-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5db63-145">**[Criação de um usuário de teste do Cloud Management Portal for Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** – para ter um equivalente de Brenda Fernandes no Cloud Management Portal for Microsoft Azure vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5db63-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5db63-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5db63-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5db63-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5db63-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5db63-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5db63-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="5db63-150">**Para configurar o logon único do Azure AD com o Cloud Management Portal for Microsoft Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5db63-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="5db63-151">No portal do Azure, na página de integração de aplicativos do **Cloud Management Portal for Microsoft Azure**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5db63-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5db63-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5db63-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="5db63-155">Na seção **URLs e Domínio do Cloud Management Portal for Microsoft Azure**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5db63-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="5db63-157">a.</span><span class="sxs-lookup"><span data-stu-id="5db63-157">a.</span></span> <span data-ttu-id="5db63-158">Na caixa de texto **URL de Logon**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="5db63-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="5db63-159">b.</span><span class="sxs-lookup"><span data-stu-id="5db63-159">b.</span></span> <span data-ttu-id="5db63-160">Na caixa de texto **Identificador**, digite uma URL usando os seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="5db63-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="5db63-161">c.</span><span class="sxs-lookup"><span data-stu-id="5db63-161">c.</span></span> <span data-ttu-id="5db63-162">Na caixa de texto **URL de Resposta** , digite uma URL nos seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="5db63-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="5db63-163">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5db63-163">These values are not real.</span></span> <span data-ttu-id="5db63-164">Você precisa atualizar esses valores com a URL de Logon, o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="5db63-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="5db63-165">Entre em contato com [a equipe de suporte do cliente do Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="5db63-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
4. <span data-ttu-id="5db63-166">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="5db63-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="5db63-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5db63-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5db63-170">Na seção **Configuração do Cloud Management Portal for Microsoft Azure**, clique em **Configurar o Cloud Management Portal for Microsoft Azure** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5db63-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5db63-171">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5db63-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="5db63-173">Para configurar o logon único no lado do **Cloud Management Portal for Microsoft Azure**, você precisa enviar o **Certificado** baixado, a **URL de Logout**, **a URL de Serviço de Logon Único do SAML** e a **ID da entidade do SAML** para a [equipe de suporte do Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="5db63-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="5db63-174">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="5db63-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5db63-175">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5db63-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5db63-176">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5db63-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5db63-177">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5db63-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5db63-178">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="5db63-179">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5db63-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5db63-181">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5db63-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5db63-182">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5db63-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5db63-184">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5db63-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5db63-186">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5db63-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5db63-188">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5db63-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5db63-190">a.</span><span class="sxs-lookup"><span data-stu-id="5db63-190">a.</span></span> <span data-ttu-id="5db63-191">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5db63-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5db63-192">b.</span><span class="sxs-lookup"><span data-stu-id="5db63-192">b.</span></span> <span data-ttu-id="5db63-193">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5db63-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5db63-194">c.</span><span class="sxs-lookup"><span data-stu-id="5db63-194">c.</span></span> <span data-ttu-id="5db63-195">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5db63-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5db63-196">d.</span><span class="sxs-lookup"><span data-stu-id="5db63-196">d.</span></span> <span data-ttu-id="5db63-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5db63-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="5db63-198">Criação de um usuário de teste do Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="5db63-199">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="5db63-200">Trabalhe com a [equipe de suporte do Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com) para adicionar os usuários à conta do Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5db63-201">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5db63-202">O objetivo desta seção é permitir que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5db63-204">**Para atribuir Brenda Fernandes ao Cloud Management Portal for Microsoft Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5db63-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="5db63-205">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5db63-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5db63-207">Na lista de aplicativos, selecione **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5db63-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="5db63-209">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5db63-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5db63-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5db63-211">Click **Add** button.</span></span> <span data-ttu-id="5db63-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5db63-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5db63-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5db63-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5db63-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5db63-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5db63-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5db63-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5db63-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5db63-217">Testing single sign-on</span></span>

<span data-ttu-id="5db63-218">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5db63-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="5db63-219">Quando você clicar no bloco Cloud Management Portal for Microsoft Azure no Painel de Acesso, deverá fazer logon automaticamente no aplicativo do Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5db63-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="5db63-220">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5db63-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5db63-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5db63-221">Additional resources</span></span>

* [<span data-ttu-id="5db63-222">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5db63-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5db63-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5db63-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

