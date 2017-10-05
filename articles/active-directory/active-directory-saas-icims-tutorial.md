---
title: "Tutorial: integração do Azure Active Directory com ICIMS | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 26a6b41a0e59924d007855ca548f22ed00bd7e23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="58c83-103">Tutorial: integração do Azure Active Directory ao ICIMS</span><span class="sxs-lookup"><span data-stu-id="58c83-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="58c83-104">Neste tutorial, você aprenderá a integrar o ICIMS ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="58c83-104">In this tutorial, you learn how to integrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58c83-105">A integração do ICIMS ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="58c83-105">Integrating ICIMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58c83-106">Você pode controlar no Azure AD quem terá acesso ao ICIMS</span><span class="sxs-lookup"><span data-stu-id="58c83-106">You can control in Azure AD who has access to ICIMS</span></span>
- <span data-ttu-id="58c83-107">Você pode permitir que seus usuários entrem automaticamente no ICIMS (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="58c83-107">You can enable your users to automatically get signed-on to ICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="58c83-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="58c83-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="58c83-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="58c83-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58c83-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="58c83-110">Prerequisites</span></span>

<span data-ttu-id="58c83-111">Para configurar a integração do Azure AD ao ICIMS, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="58c83-111">To configure Azure AD integration with ICIMS, you need the following items:</span></span>

- <span data-ttu-id="58c83-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="58c83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58c83-113">Uma assinatura do ICIMS habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="58c83-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58c83-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="58c83-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58c83-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="58c83-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58c83-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="58c83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58c83-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58c83-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58c83-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="58c83-118">Scenario description</span></span>
<span data-ttu-id="58c83-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="58c83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58c83-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="58c83-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58c83-121">Como adicionar o ICIMS da galeria</span><span class="sxs-lookup"><span data-stu-id="58c83-121">Adding ICIMS from the gallery</span></span>
2. <span data-ttu-id="58c83-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="58c83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-the-gallery"></a><span data-ttu-id="58c83-123">Como adicionar o ICIMS da galeria</span><span class="sxs-lookup"><span data-stu-id="58c83-123">Adding ICIMS from the gallery</span></span>
<span data-ttu-id="58c83-124">Para configurar a integração do ICIMS ao Azure AD, você precisará adicionar o ICIMS da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="58c83-124">To configure the integration of ICIMS into Azure AD, you need to add ICIMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58c83-125">**Para adicionar o ICIMS da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="58c83-125">**To add ICIMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58c83-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58c83-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="58c83-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="58c83-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58c83-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="58c83-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="58c83-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58c83-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="58c83-133">Na caixa de pesquisa, digite **ICIMS**, selecione **ICIMS** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58c83-133">In the search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button to add the application.</span></span>

    ![ICIMS na lista de resultados](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="58c83-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="58c83-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="58c83-136">Nesta seção, você configurará e testará o logon único do Azure AD com o ICIMS, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="58c83-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58c83-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ICIMS é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58c83-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ICIMS is to a user in Azure AD.</span></span> <span data-ttu-id="58c83-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-138">In other words, a link relationship between an Azure AD user and the related user in ICIMS needs to be established.</span></span>

<span data-ttu-id="58c83-139">No ICIMS, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="58c83-139">In ICIMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="58c83-140">Para configurar e testar o logon único do Azure AD com o ICIMS, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="58c83-140">To configure and test Azure AD single sign-on with ICIMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58c83-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="58c83-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="58c83-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="58c83-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="58c83-143">**[Criar um usuário de teste do ICIMS](#create-an-icims-test-user)** – para ter um equivalente de Brenda Fernandes no ICIMS vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58c83-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - to have a counterpart of Britta Simon in ICIMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="58c83-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58c83-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="58c83-145">**[Testar o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="58c83-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="58c83-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="58c83-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="58c83-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="58c83-148">**Para configurar o logon único do Azure AD com o ICIMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="58c83-148">**To configure Azure AD single sign-on with ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="58c83-149">No Portal do Azure, na página de integração de aplicativos do **ICIMS**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="58c83-149">In the Azure portal, on the **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="58c83-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="58c83-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="58c83-153">Na seção **Domínio e URLs do ICIMS**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="58c83-153">On the **ICIMS Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="58c83-155">a.</span><span class="sxs-lookup"><span data-stu-id="58c83-155">a.</span></span> <span data-ttu-id="58c83-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="58c83-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="58c83-157">b.</span><span class="sxs-lookup"><span data-stu-id="58c83-157">b.</span></span> <span data-ttu-id="58c83-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="58c83-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="58c83-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="58c83-159">These values are not real.</span></span> <span data-ttu-id="58c83-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="58c83-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="58c83-161">Contate a [equipe de suporte ao cliente do ICIMS](https://www.icims.com/contact-us) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="58c83-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="58c83-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="58c83-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="58c83-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="58c83-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="58c83-166">Na seção **Configuração do ICIMS**, clique em **Configurar o ICIMS** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="58c83-166">On the **ICIMS Configuration** section, click **Configure ICIMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="58c83-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="58c83-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="58c83-169">Para configurar o logon único no lado do **ICIMS**, é necessário enviar o **XML de metadados**, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** baixados para a [equipe de suporte do ICIMS](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="58c83-169">To configure single sign-on on **ICIMS** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="58c83-170">Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="58c83-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="58c83-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="58c83-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="58c83-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="58c83-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58c83-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58c83-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="58c83-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="58c83-174">Create an Azure AD test user</span></span>
<span data-ttu-id="58c83-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="58c83-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="58c83-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="58c83-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58c83-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58c83-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="58c83-180">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="58c83-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="58c83-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="58c83-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![O botão Adicionar](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="58c83-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="58c83-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![A caixa de diálogo Usuário](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="58c83-186">a.</span><span class="sxs-lookup"><span data-stu-id="58c83-186">a.</span></span> <span data-ttu-id="58c83-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="58c83-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58c83-188">b.</span><span class="sxs-lookup"><span data-stu-id="58c83-188">b.</span></span> <span data-ttu-id="58c83-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="58c83-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="58c83-190">c.</span><span class="sxs-lookup"><span data-stu-id="58c83-190">c.</span></span> <span data-ttu-id="58c83-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="58c83-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="58c83-192">d.</span><span class="sxs-lookup"><span data-stu-id="58c83-192">d.</span></span> <span data-ttu-id="58c83-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="58c83-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="58c83-194">Criar um usuário de teste do ICIMS</span><span class="sxs-lookup"><span data-stu-id="58c83-194">Create an ICIMS test user</span></span>

<span data-ttu-id="58c83-195">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-195">The objective of this section is to create a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="58c83-196">Trabalhe com a [equipe de suporte do ICIMS](https://www.icims.com/contact-us) para adicionar os usuários à conta do ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-196">Work with [ICIMS support team](https://www.icims.com/contact-us) to add the users in the ICIMS account.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="58c83-197">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="58c83-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="58c83-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ICIMS.</span></span>

![Atribuir a função de usuário][200]

<span data-ttu-id="58c83-200">**Para atribuir Brenda Fernandes ao ICIMS, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="58c83-200">**To assign Britta Simon to ICIMS, perform the following steps:**</span></span>

1. <span data-ttu-id="58c83-201">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="58c83-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="58c83-203">Na lista de aplicativos, escolha **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="58c83-203">In the applications list, select **ICIMS**.</span></span>

    ![O link do ICIMS na lista de Aplicativos](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="58c83-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="58c83-205">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202] 

4. <span data-ttu-id="58c83-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="58c83-207">Click **Add** button.</span></span> <span data-ttu-id="58c83-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="58c83-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="58c83-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="58c83-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="58c83-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="58c83-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="58c83-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="58c83-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="58c83-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="58c83-213">Test single sign-on</span></span>

<span data-ttu-id="58c83-214">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="58c83-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="58c83-215">Ao clicar no bloco ICIMS no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo ICIMS.</span><span class="sxs-lookup"><span data-stu-id="58c83-215">When you click the ICIMS tile in the Access Panel, you should get automatically signed-on to your ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58c83-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="58c83-216">Additional resources</span></span>

* [<span data-ttu-id="58c83-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="58c83-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="58c83-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58c83-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

