---
title: "Tutorial: integração do Azure Active Directory com o Proofpoint on Demand | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e Proofpoint on Demand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="66381-103">Tutorial: integração do Azure Active Directory ao Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="66381-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="66381-104">Neste tutorial, você aprenderá a integrar o Proofpoint on Demand ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="66381-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66381-105">Integrar o Proofpoint on Demand ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="66381-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66381-106">Você pode controlar no Azure AD quem tem acesso ao Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="66381-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="66381-107">Você pode habilitar os usuários para serem conectados automaticamente no Proofpoint on Demand (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66381-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66381-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66381-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66381-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66381-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="66381-110">Prerequisites</span></span>

<span data-ttu-id="66381-111">Para configurar a integração do Azure AD ao Proofpoint on Demand, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="66381-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="66381-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66381-113">Uma assinatura de logon único do Proofpoint on Demand habilitada</span><span class="sxs-lookup"><span data-stu-id="66381-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66381-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="66381-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66381-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="66381-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66381-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="66381-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66381-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66381-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66381-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="66381-118">Scenario description</span></span>
<span data-ttu-id="66381-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="66381-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66381-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="66381-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66381-121">Adicionar Proofpoint on Demand da galeria</span><span class="sxs-lookup"><span data-stu-id="66381-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="66381-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="66381-123">Adicionar Proofpoint on Demand da galeria</span><span class="sxs-lookup"><span data-stu-id="66381-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="66381-124">Para configurar a integração do Proofpoint on Demand ao Azure AD, você precisa adicionar o Proofpoint on Demand da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="66381-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66381-125">**Para adicionar o Proofpoint on Demand da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66381-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66381-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66381-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66381-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="66381-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66381-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66381-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="66381-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66381-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="66381-133">Na caixa de pesquisa, digite **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="66381-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="66381-135">No painel de resultados, selecione **Proofpoint on Demand** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66381-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66381-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66381-138">Nesta seção, você configura e testa o logon único do Azure AD com o Proofpoint on Demand com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="66381-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66381-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Proofpoint on Demand é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66381-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="66381-140">Em outras palavras, você precisa estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="66381-141">Essa relação de vínculo é estabelecida atribuindo o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="66381-142">Para configurar e testar o logon único do Azure AD com o Proofpoint on Demand, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="66381-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66381-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="66381-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66381-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66381-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66381-145">**[Criar um usuário de teste do Proofpoint on Demand](#creating-a-proofpoint-on-demand-test-user)** – para ter um equivalente de Brenda Fernandes no Proofpoint on Demand que seja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66381-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="66381-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="66381-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66381-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="66381-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66381-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66381-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66381-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo do Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="66381-150">**Para configurar o logon único do Azure AD com o Proofpoint on Demand, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66381-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="66381-151">No portal do Azure, na página de integração de aplicativos do **Proofpoint on Demand**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="66381-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="66381-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="66381-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="66381-155">Na seção **URLs e Domínio do Proofpoint on Demand**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66381-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="66381-157">a.Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="66381-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="66381-158">b.</span><span class="sxs-lookup"><span data-stu-id="66381-158">b.</span></span> <span data-ttu-id="66381-159">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="66381-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="66381-160">c.</span><span class="sxs-lookup"><span data-stu-id="66381-160">c.</span></span>  <span data-ttu-id="66381-161">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="66381-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="66381-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="66381-162">These values are not the real.</span></span> <span data-ttu-id="66381-163">Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais.</span><span class="sxs-lookup"><span data-stu-id="66381-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="66381-164">Contate a [equipe de suporte do cliente Proofpoint on Demand](https://www.proofpoint.com/us/support-services) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="66381-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="66381-165">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="66381-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="66381-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="66381-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="66381-169">Na seção **Configuração do Proofpoint on Demand**, clique em **Configurar Proofpoint on Demand** para abrir a janela **Configurar Logon**.</span><span class="sxs-lookup"><span data-stu-id="66381-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="66381-170">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="66381-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="66381-172">Para configurar o logon único no lado do **Proofpoint on Demand**, é necessário enviar o **Certificado (Base64)** baixado, a **ID da Entidade do SAML** e a **URL do Serviço de Logon Único do SAML** para a [equipe de suporte do cliente Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="66381-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="66381-173">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="66381-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66381-174">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="66381-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66381-175">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66381-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66381-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="66381-177">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66381-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="66381-179">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66381-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66381-180">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66381-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66381-182">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="66381-182">These values are not the real.</span></span> <span data-ttu-id="66381-183">Atualize esses valores com os reais</span><span class="sxs-lookup"><span data-stu-id="66381-183">Update these values with the actual</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66381-185">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66381-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66381-187">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="66381-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66381-189">a.</span><span class="sxs-lookup"><span data-stu-id="66381-189">a.</span></span> <span data-ttu-id="66381-190">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="66381-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="66381-191">b.</span><span class="sxs-lookup"><span data-stu-id="66381-191">b.</span></span> <span data-ttu-id="66381-192">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="66381-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="66381-193">c.</span><span class="sxs-lookup"><span data-stu-id="66381-193">c.</span></span> <span data-ttu-id="66381-194">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="66381-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66381-195">d.</span><span class="sxs-lookup"><span data-stu-id="66381-195">d.</span></span> <span data-ttu-id="66381-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66381-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="66381-197">Criar um usuário de teste do Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="66381-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="66381-198">Nesta seção, você cria uma usuária chamada Brenda Fernandes no Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="66381-199">Trabalhe com a [equipe de suporte do cliente Proofpoint on Demand](https://www.proofpoint.com/us/support-services) para adicionar usuários na plataforma Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66381-200">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66381-201">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="66381-203">**Para atribuir Brenda Fernandes ao Proofpoint on Demand, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="66381-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="66381-204">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="66381-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="66381-206">Na lista de aplicativos, selecione **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="66381-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="66381-208">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="66381-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="66381-210">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="66381-210">Click **Add** button.</span></span> <span data-ttu-id="66381-211">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66381-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="66381-213">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="66381-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="66381-214">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66381-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66381-215">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66381-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66381-216">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="66381-216">Testing single sign-on</span></span>

<span data-ttu-id="66381-217">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="66381-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="66381-218">Ao clicar no bloco do **Proofpoint on Demand** no painel de acesso, você deve entrar automaticamente em seu aplicativo do Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="66381-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="66381-219">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66381-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="66381-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="66381-220">Additional resources</span></span>

* [<span data-ttu-id="66381-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="66381-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66381-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66381-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

