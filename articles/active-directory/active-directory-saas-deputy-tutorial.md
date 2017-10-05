---
title: "Tutorial: integração do Azure Active Directory ao Deputy | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="21b2e-103">Tutorial: integração do Azure Active Directory ao Deputy</span><span class="sxs-lookup"><span data-stu-id="21b2e-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="21b2e-104">Neste tutorial, você aprende a integrar o Github ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="21b2e-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21b2e-105">A integração do Deputy ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="21b2e-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21b2e-106">No Azure AD, é possível controlar quem tem acesso ao Deputy</span><span class="sxs-lookup"><span data-stu-id="21b2e-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="21b2e-107">Você pode permitir que seus usuários façam logon automaticamente no Deputy (Logon único) com as contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="21b2e-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21b2e-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="21b2e-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21b2e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21b2e-110">Prerequisites</span></span>

<span data-ttu-id="21b2e-111">Para configurar a integração do Azure AD ao Deputy, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="21b2e-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="21b2e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21b2e-113">Uma assinatura do Deputy habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="21b2e-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21b2e-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="21b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21b2e-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="21b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21b2e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="21b2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21b2e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21b2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21b2e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="21b2e-118">Scenario description</span></span>
<span data-ttu-id="21b2e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="21b2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21b2e-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="21b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21b2e-121">Adicionando o Deputy da galeria</span><span class="sxs-lookup"><span data-stu-id="21b2e-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="21b2e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="21b2e-123">Adicionando o Deputy da galeria</span><span class="sxs-lookup"><span data-stu-id="21b2e-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="21b2e-124">Para configurar a integração do Deputy ao Azure AD, você precisará adicionar o Deputy da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="21b2e-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21b2e-125">**Para adicionar o Deputy da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="21b2e-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21b2e-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21b2e-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21b2e-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="21b2e-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="21b2e-133">Na caixa de pesquisa, digite **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-133">In the search box, type **Deputy**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="21b2e-135">No painel de resultados, selecione **Deputy** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21b2e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21b2e-138">Nesta seção, você configura e testa o logon único do Azure AD com o Deputy com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="21b2e-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="21b2e-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Deputy é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21b2e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="21b2e-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Deputy.</span><span class="sxs-lookup"><span data-stu-id="21b2e-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="21b2e-141">No Deputy, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="21b2e-142">Para configurar e testar o logon único do Azure AD com o Deputy, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="21b2e-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21b2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="21b2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21b2e-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="21b2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21b2e-145">**[Como criar um usuário de teste do Deputy](#creating-a-deputy-test-user)** – para ter um equivalente de Brenda Fernandes no Deputy que esteja vinculado à representação do usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21b2e-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21b2e-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="21b2e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21b2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="21b2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21b2e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="21b2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21b2e-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo Deputy.</span><span class="sxs-lookup"><span data-stu-id="21b2e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="21b2e-150">**Para configurar o logon único do Azure AD com o Deputy, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="21b2e-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="21b2e-151">No portal do Azure, na página de integração de aplicativos do **Deputy**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="21b2e-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="21b2e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="21b2e-155">Na seção **URLs e Domínio do Deputy**, se você desejar configurar o aplicativo em modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="21b2e-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="21b2e-157">a.</span><span class="sxs-lookup"><span data-stu-id="21b2e-157">a.</span></span> <span data-ttu-id="21b2e-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="21b2e-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="21b2e-159">b.</span><span class="sxs-lookup"><span data-stu-id="21b2e-159">b.</span></span> <span data-ttu-id="21b2e-160">Na caixa de texto **URL de resposta** , digite uma URL no seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="21b2e-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="21b2e-161">Marque **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="21b2e-162">Se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="21b2e-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="21b2e-164">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="21b2e-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="21b2e-165">O sufixo de região do Deputy é opcional ou ele deve usar uma destas opções: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="21b2e-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21b2e-166">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="21b2e-166">These values are not real.</span></span> <span data-ttu-id="21b2e-167">Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada.</span><span class="sxs-lookup"><span data-stu-id="21b2e-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="21b2e-168">Entre em contato com a [equipe de suporte do Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="21b2e-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="21b2e-169">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="21b2e-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="21b2e-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="21b2e-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="21b2e-173">Na seção **Configuração do Deputy**, clique em **Configurar Deputy** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="21b2e-174">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="21b2e-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="21b2e-176">Navegue até a seguinte URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="21b2e-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="21b2e-177">Vá para as **Configurações de Segurança** e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="21b2e-179">Na página **Configurações de Segurança** , execute etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="21b2e-181">a.</span><span class="sxs-lookup"><span data-stu-id="21b2e-181">a.</span></span> <span data-ttu-id="21b2e-182">Habilite o **Logon Social**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="21b2e-183">b.</span><span class="sxs-lookup"><span data-stu-id="21b2e-183">b.</span></span> <span data-ttu-id="21b2e-184">Abra seu certificado codificado em base64 baixado do portal do Azure no bloco de notas, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="21b2e-185">c.</span><span class="sxs-lookup"><span data-stu-id="21b2e-185">c.</span></span> <span data-ttu-id="21b2e-186">Na caixa de texto URL de SSO do SAML, digite `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="21b2e-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="21b2e-187">d.</span><span class="sxs-lookup"><span data-stu-id="21b2e-187">d.</span></span> <span data-ttu-id="21b2e-188">Na caixa de texto URL de SSO do SAML, substitua `<your subdomain>` pelo seu subdomínio.</span><span class="sxs-lookup"><span data-stu-id="21b2e-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="21b2e-189">e.</span><span class="sxs-lookup"><span data-stu-id="21b2e-189">e.</span></span> <span data-ttu-id="21b2e-190">Na caixa de texto URL de SSO do SAML, substitua `<saml sso url>` pela **URL de Serviço de Logon Único do SAML** copiada do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="21b2e-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="21b2e-191">f.</span><span class="sxs-lookup"><span data-stu-id="21b2e-191">f.</span></span> <span data-ttu-id="21b2e-192">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="21b2e-193">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="21b2e-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21b2e-194">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="21b2e-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21b2e-195">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="21b2e-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21b2e-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="21b2e-197">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="21b2e-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="21b2e-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="21b2e-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21b2e-200">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21b2e-202">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="21b2e-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21b2e-204">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21b2e-206">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="21b2e-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21b2e-208">a.</span><span class="sxs-lookup"><span data-stu-id="21b2e-208">a.</span></span> <span data-ttu-id="21b2e-209">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21b2e-210">b.</span><span class="sxs-lookup"><span data-stu-id="21b2e-210">b.</span></span> <span data-ttu-id="21b2e-211">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="21b2e-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21b2e-212">c.</span><span class="sxs-lookup"><span data-stu-id="21b2e-212">c.</span></span> <span data-ttu-id="21b2e-213">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="21b2e-214">d.</span><span class="sxs-lookup"><span data-stu-id="21b2e-214">d.</span></span> <span data-ttu-id="21b2e-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="21b2e-216">Criando um usuário de teste do Deputy</span><span class="sxs-lookup"><span data-stu-id="21b2e-216">Creating a Deputy test user</span></span>

<span data-ttu-id="21b2e-217">Para permitir que os usuários do Azure AD façam logon no Deputy, eles devem ser provisionados no Deputy.</span><span class="sxs-lookup"><span data-stu-id="21b2e-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="21b2e-218">No caso do Deputy, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="21b2e-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="21b2e-219">Para provisionar uma conta de usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="21b2e-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="21b2e-220">Faça logon no site da empresa do Deputy como administrador.</span><span class="sxs-lookup"><span data-stu-id="21b2e-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="21b2e-221">No painel de navegação superior, clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="21b2e-222">![Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="21b2e-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="21b2e-223">Clique no botão **Adicionar Pessoas** e em **Adicionar uma única pessoa**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="21b2e-224">![Adicionar Pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Adicionar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="21b2e-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="21b2e-225">Execute as etapas a seguir e clique em **Salvar e Convidar**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="21b2e-226">![Novo Usuário](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="21b2e-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="21b2e-227">a.</span><span class="sxs-lookup"><span data-stu-id="21b2e-227">a.</span></span> <span data-ttu-id="21b2e-228">Na caixa de texto **Nome**, digite o nome do usuário como **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="21b2e-229">b.</span><span class="sxs-lookup"><span data-stu-id="21b2e-229">b.</span></span> <span data-ttu-id="21b2e-230">Na caixa de texto **Email** , digite o endereço de email de uma conta do Azure AD que você deseja provisionar.</span><span class="sxs-lookup"><span data-stu-id="21b2e-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="21b2e-231">c.</span><span class="sxs-lookup"><span data-stu-id="21b2e-231">c.</span></span> <span data-ttu-id="21b2e-232">Na caixa de texto **Trabalha em**, digite o nome da empresa.</span><span class="sxs-lookup"><span data-stu-id="21b2e-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="21b2e-233">d.</span><span class="sxs-lookup"><span data-stu-id="21b2e-233">d.</span></span> <span data-ttu-id="21b2e-234">Clique no botão **Salvar e Convidar**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="21b2e-235">O titular da conta do AAD receberá um email e seguirá um link para confirmar sua conta antes de se tornar ativo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="21b2e-236">Você pode usar qualquer outra ferramenta de criação da conta de usuário do Deputy ou as APIs fornecidas pelo Deputy para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="21b2e-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="21b2e-237">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="21b2e-238">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Deputy.</span><span class="sxs-lookup"><span data-stu-id="21b2e-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="21b2e-240">**Para atribuir Brenda Fernandes ao Deputy, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="21b2e-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="21b2e-241">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="21b2e-243">Na lista de aplicativos, selecione **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-243">In the applications list, select **Deputy**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="21b2e-245">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="21b2e-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="21b2e-247">Click **Add** button.</span></span> <span data-ttu-id="21b2e-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="21b2e-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="21b2e-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21b2e-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21b2e-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21b2e-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21b2e-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="21b2e-253">Testing single sign-on</span></span>

<span data-ttu-id="21b2e-254">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="21b2e-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="21b2e-255">Quando você clicar no bloco Deputy no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Deputy.</span><span class="sxs-lookup"><span data-stu-id="21b2e-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21b2e-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="21b2e-256">Additional resources</span></span>

* [<span data-ttu-id="21b2e-257">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="21b2e-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21b2e-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="21b2e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

